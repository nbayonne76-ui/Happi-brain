---
name: Microsoft Sales App
type: saas-pattern
status: production
client: Nicolas (interne) — multi-utilisateur depuis 07/2026
sector: Sales intelligence / Sales enablement (Microsoft Partner)
repo: microsoft-sales-app
deploy: microsoft-sales-app.vercel.app (Vercel Hobby)
---

# Microsoft Sales App — Sales Intelligence + Agents autonomes

## Contexte
Outil de vente pour Partner Account Managers Microsoft, construit par Nicolas. Démarré comme
outil perso, passé multi-utilisateur en juillet 2026. Ce qui rend ce projet intéressant pour
Happi Brain : **l'architecture agents + KB + multi-tenant est un pattern réutilisable pour un
futur produit SaaS de sales/marketing intelligence**, pas juste un outil interne Microsoft.

## Stack
- **Frontend/Backend** : Next.js 15 (App Router) + React 19
- **DB** : Neon Postgres (serverless) + Prisma ORM 6.19
- **Auth** : NextAuth v4 (credentials + JWT), `User` model avec `role` (user/manager/admin)
- **IA** : OpenAI GPT-4o-mini (génération), Tavily (recherche/signaux), Anthropic (agent de veille tech)
- **Déploiement** : Vercel Hobby — contrainte clé : **2 crons max, 60s maxDuration par fonction**,
  filesystem read-only sauf `/tmp` (éphémère, non partagé entre instances)
- **CI génération de contenu** : GitHub Actions (accès écriture réel au repo, pas de limite 60s)

## Inventaire complet des agents (18 juillet 2026)

### A. Agents autonomes de fond (6, persistés en Postgres via `AgentRun`)
| Agent | Rôle | Déclenchement |
|---|---|---|
| **KB Drift Detector** | Scanne la KB Markdown contre un registre de prix connus ; détecte les prix obsolètes + une catégorie "non vérifié" (prix rencontrés mais absents du registre) | Auto (orchestrateur, 5h UTC) |
| **Health Monitor** | Ping de 7 routes critiques de l'app, alerte Slack temps réel si DOWN | Auto (orchestrateur) |
| **Article Quality Agent** | Score structurel des articles de blog générés par IA (bilingue, sections, CTA...) | Auto (orchestrateur) |
| **Buying Signal Monitor** | Watchlist de comptes cibles → recherche Tavily + API gouv.fr → détection de signaux (recrutement IT, appel d'offres, nouveau dirigeant...) → score → synthèse GPT d'un angle de vente | Manuel (bouton dashboard), personnel par utilisateur |
| **Weekly Sales Brief** | Assemble signaux + articles récents + actu Microsoft + extrait KB prix → brief hebdo GPT-4o-mini | Manuel, personnel par utilisateur |
| **MS Announcement Watcher** | Suit 5 flux RSS Microsoft officiels, détecte l'impact sur la KB (changement de prix, nouveau plan, GA, sécurité...), génère des TODOs de mise à jour priorisés | Manuel (bouton KB) |

### B. Agents de génération de contenu blog (16, GitHub Actions — accès écriture réel, pas de limite 60s)
Pipeline commun : RSS + Exa → Jina → Tavily fallback → scorer mots-clés → GPT-4o-mini générateur → `data/blog-articles.json` + KB.
Un agent par verticale : **Azure, Dynamics, Modern Work, Copilot, Sécurité, Retail, Healthcare,
Energy, Government, Manufacturing, Tech, Finance, Telecom, Media** (inclus dans le cron
quotidien 6h UTC) + **Hospitality, Restauration** (test, déclenchement manuel uniquement).

Plus **Article Fix Agent** (nouveau, 18/07) : corrige réellement les articles sous le seuil
qualité — fix structurel → commit direct ; fix contenu/prix → PR de relecture humaine (jamais
mergée automatiquement). Voir section dédiée plus bas.

### C. Agent interactif (chat, à la demande)
**Microsoft AI Agent** (`/ai-agent`) — commandes `/brief`, `/pitch`, `/swot`, `/prix`, répond
exclusivement depuis la Knowledge Base (anti-hallucination).

## Le pattern central : agents autonomes + KB-grounding + multi-tenant

### 1. Orchestrateur unique (contrainte Vercel Hobby)
Un seul cron (`/api/cron/orchestrator`, 5h UTC) appelle 3 agents rapides **en import direct**
(pas de fetch HTTP interne, pour éviter les pièges d'appels internes Vercel et rester sous 60s) :
- **KB Drift Detector** : scanne la knowledge base (fichiers Markdown) contre un registre de
  prix connus, détecte les écarts (prix obsolètes) + une catégorie "non vérifié" (prix rencontrés
  mais absents du registre — évite la fausse confiance d'un rapport "tout va bien")
- **Health Monitor** : ping de 7 routes critiques, alerte Slack en temps réel si DOWN
- **Article Quality Agent** : score structurel des articles de blog générés par IA

Les agents plus lents (Buying Signal Monitor, Weekly Brief, MS Watcher) sont **manuels only**
(boutons dashboard), jamais dans le cron automatique.

### 2. Persistance : DB partagée au lieu de /tmp + localStorage
Erreur initiale corrigée : les agents écrivaient dans `/tmp` (perdu à chaque cold start Vercel)
et le frontend cachait en `localStorage` (propre à un navigateur). Migré vers 2 modèles Prisma :
- `AgentRun` (log générique : agent, status, summary, details JSON, `userId` nullable)
- `WatchedAccount` (comptes suivis par Buying Signals, `userId` obligatoire)

### 3. Multi-tenant (ajouté 07/2026)
Découverte en auditant le projet : l'infra d'auth existait déjà (User model, NextAuth JWT,
pages signin/signup, un helper `requireAuth()`) **mais n'était jamais branchée** — aucune
route API ne vérifiait de session, aucun `SessionProvider` monté côté client. Correction :
- `WatchedAccount` et `AgentRun` scopés par `userId` — **seulement pour les agents personnels**
  (Buying Signals, Weekly Brief). Les agents partagés (KB Drift, Health, Article Quality,
  MS Watcher) restent globaux — ils portent sur l'état de l'app elle-même, pas sur des données
  utilisateur.
- Chaque utilisateur a sa propre watchlist de comptes cibles et son propre brief hebdomadaire
  personnalisé (le nom dans le prompt GPT n'est plus codé en dur).
- Bannière d'onboarding dismissible au premier login (clé localStorage par `userId`).

### 4. Buying Signal Monitor — le cœur "sales intelligence"
Pour chaque compte de la watchlist : recherche Tavily (actualités, recrutement IT, transfo
digitale) + API gouv.fr (effectif/SIREN) → détection de signaux par regex pondérés (recrutement
IT, appel d'offres, nouveau dirigeant, difficultés financières...) → score total → si score ≥ 3,
synthèse GPT-4o-mini d'un angle de vente concret. Résultat : un rapport hebdo avec top comptes
"chauds" et argumentaire prêt à l'emploi.

### 5. Weekly Brief — assemblage KB-grounded
Combine les signaux (ci-dessus), les articles de blog récents, l'actu Microsoft, et un extrait
de la KB de prix — GPT génère un brief structuré (comptes à contacter, actu Microsoft, article à
partager, relance suggérée, tip commercial). Tout est ancré dans la KB pour éviter les
hallucinations de prix/produits.

### 6. Article Quality Fix Agent — auto-fix avec garde-fou
Le détecteur (Vercel) ne peut que logger un score (filesystem read-only). Le vrai fix tourne
en CI (GitHub Actions, accès écriture réel) : `scripts/agents/article-fix-agent.js`.
**Règle de sécurité** : fixes purement structurels (CTA manquant, slug invalide...) → commit
direct ; fixes touchant contenu ou prix (risque d'hallucination IA) → **PR ouverte pour
relecture humaine, jamais mergée automatiquement**. Ce garde-fou (classifier le risque avant
d'autoriser un commit automatique) est un pattern réutilisable pour tout agent de correction
de contenu.

## Ce qui rend l'architecture réutilisable pour un futur SaaS

Le pattern **watchlist → recherche externe (Tavily/DDG) → scoring par règles → synthèse GPT →
KB-grounding → persistance par tenant → digest périodique** ne dépend pas de Microsoft
spécifiquement. Pour un futur client, il suffirait de :
1. Remplacer la KB Markdown (prix/produits Microsoft) par la KB du client (son propre catalogue/pricing)
2. Adapter les `SIGNAL_PATTERNS` (regex) au secteur du client
3. Réutiliser tel quel : multi-tenant (User + scoping), orchestrateur cron, agents CI de
   génération/correction de contenu, garde-fou structurel/PR pour l'auto-fix

**⚠️ Ce n'est PAS équivalent à Dynamics 365 Customer Insights.** D365 CI est une vraie CDP
(Customer Data Platform) : elle unifie des données de PREMIÈRE PARTIE (transactions, CRM, web
analytics) sur les CLIENTS EXISTANTS du client, à l'échelle (millions de profils), avec
résolution d'identité et orchestration de parcours temps réel (Power Platform).

Ce qu'on a construit ici est plus proche d'un **outil de sales intelligence account-based**
(catégorie ZoomInfo / Cognism / Klue / Crayon / LinkedIn Sales Navigator alerts) : il surveille
des PROSPECTS via des signaux PUBLICS tiers (actualités, recrutement, appels d'offres), pas des
clients existants via leurs données internes. Pas de profils clients unifiés, pas de scale CDP,
pas de moteur de résolution d'identité. La comparaison honnête : un ABM (Account-Based
Marketing) sales-intelligence tool + un générateur de contenu IA ancré KB — pas un CDP
entreprise. Le potentiel SaaS est réel (le pattern est généralisable), mais positionné comme
"sales intelligence pour équipes commerciales B2B", pas comme concurrent de Customer Insights.

## Contraintes Vercel Hobby à retenir pour tout futur projet similaire
- 2 crons max, 60s maxDuration par fonction serverless
- Filesystem read-only sauf `/tmp`, et `/tmp` n'est PAS partagé entre instances/cold starts
  → toute persistance doit passer par une vraie DB, jamais par le filesystem
- Pour du contenu qui doit être committé dans le repo (pas juste loggé), il faut un environnement
  avec accès écriture réel : GitHub Actions, pas les fonctions serverless Vercel
