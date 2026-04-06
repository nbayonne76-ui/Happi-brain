---
name: Happi Brain
description: Base de connaissance centrale de tous les projets H'appi — sert de cerveau évolutif pour la création de chatbots et solutions IA
type: project
---

# 🧠 HAPPI BRAIN — Base de connaissance centrale

> Ce fichier est le cerveau évolutif de Claude pour tous les projets H'appi.
> Il doit être consulté EN PRIORITÉ pour tout nouveau projet chatbot, IA ou développement client.
> Il doit être MIS À JOUR après chaque nouveau projet terminé.

---

## 1. IDENTITÉ H'APPI

**Startup franco-égyptienne** lancée début 2026.
- **Mission** : Créer des chatbots IA sur-mesure et solutions digitales pour les entreprises françaises
- **Positionnement** : CX (expérience client) + Supply Chain + Secrétariat IA
- **Philosophie** : "Qualité avant quantité" — personnalisation radicale, pas de solutions génériques
- **Site** : happi-bot.com
- **Tarification** :
  - Implémentation : devis personnalisé (50-70% sous le marché)
  - Maintenance Essential : inclus
  - Maintenance Pro : 100-500€/mois
  - Maintenance Enterprise : 500-2000€/mois avec SLA
- **Conformité** : RGPD, hébergement France/Europe (Scaleway, Hetzner), ISO 27001

---

## 2. STACK TECHNIQUE DE RÉFÉRENCE H'APPI

### Stack chatbot standard (à réutiliser)
```
Backend   → FastAPI (Python) + PostgreSQL + SQLAlchemy + Alembic
Frontend  → Next.js 14 (App Router) + TypeScript + Tailwind CSS
IA        → Claude (Anthropic SDK) — modèle préféré pour tous les chatbots
Voice     → Vapi.ai (téléphonie) + ElevenLabs (TTS) + Deepgram (STT)
Auth      → JWT
Deploy    → Docker + docker-compose + Railway / Vercel
Notifs    → Resend (email) + Twilio (SMS)
Calendar  → Cal.com API
CRM       → Webhooks HubSpot / Pipedrive / Zapier / Make
```

### Stack démo/showcase clients (rapide à livrer)
```
HTML + CSS + JS vanilla (léger, rapide à déployer)
Hébergement → Vercel (domaine : happi-[client].vercel.app)
```

### Stack SaaS / Plateformes
```
Frontend  → Next.js 16 (App Router, Turbopack) + TypeScript + Tailwind CSS v4
Backend   → FastAPI + PostgreSQL
State     → Zustand + persist middleware (web & mobile)
Mobile    → React Native (Expo SDK 54)
Animation → Framer Motion
DnD       → @dnd-kit/core + @dnd-kit/sortable
```

### Stack Web Builder (happi-webcreator)
```
Framework → Next.js 16.2.2 + TypeScript + Tailwind CSS v4
State     → Zustand + persist (projets en localStorage)
DnD       → @dnd-kit/core + @dnd-kit/sortable (sections réordonnables)
Animation → Framer Motion
Export    → HTML standalone via Blob + URL.createObjectURL (zéro dépendance)
Preview   → Route /preview/[id] (rendu propre sans chrome éditeur)
Blocs     → 13 types : navbar, hero, features, stats, cta, pricing, faq,
            testimonials, logowall, footer, text, image, divider
```

---

## 3. PROJETS CHATBOT — CATALOGUE COMPLET

### 3.1 SAV-BOT Mobilier de France ⭐ (projet phare)
- **Repo** : `SAV-BOT-Meuble-de-france`
- **Client** : Mobilier de France (enseigne meuble)
- **Type** : Chatbot SAV après-vente + ticketing
- **Stack** : FastAPI + React + PostgreSQL + Redis + Docker
- **IA** : OpenAI (GPT)
- **Features clés** :
  - Dialogue naturel multilingue (FR, EN, AR, IT, DE)
  - Recommandations produits intelligentes
  - Upload photo + analyse défauts visuels
  - Ticketing automatique avec priorité P0-P3
  - Support vocal (speech recognition + synthesis)
  - 351+ tests, CI/CD pipeline complet
  - Monitoring santé + métriques
- **Deploy** : Docker + Railway
- **Couverture tests** : Backend 62%, Frontend 53%
- **Leçons** : Toujours intégrer un système de priorité de tickets. Les clients SAV ont besoin de photos. Le multilingue est critique pour la France.

### 3.2 INnatural Stores Chatbot
- **Repo** : `Innaturalstores-Chatbot`
- **Client** : INnatural (cosmétiques naturels)
- **Type** : Chatbot e-commerce produits + support
- **Stack** : Node.js (Express) + widget JS embeddable
- **IA** : Claude (Anthropic)
- **Features clés** :
  - Bilingue Arabe/Anglais
  - Recommandations par type de cheveux
  - Collecte de leads
  - Widget embeddable (1 script tag)
  - Catalogue produits + FAQ configurables (JSON)
  - Système de qualification en 3 phases
  - Redis session manager
- **Architecture** : widget/ + backend/ + config/ (products.json, faqs.json, bot-personality.json)
- **Leçons** : La qualification en 3 phases convertit mieux. Le JSON de config permet aux clients de modifier sans dev. Toujours prévoir un widget embeddable.

### 3.3 Happi Secretary (Secrétariat IA vocal)
- **Repo** : `Happi-Secretary`
- **Type** : Secrétariat IA vocal 24h/24 pour entreprises
- **Stack** : FastAPI + PostgreSQL + Next.js 14 + Docker
- **IA** : Claude (Anthropic) — conversation + analyse post-appel
- **Téléphonie** : Vapi.ai (latence <500ms)
- **Voice** : ElevenLabs TTS + Deepgram STT
- **Calendar** : Cal.com API
- **Notifs** : Resend + Twilio
- **Features clés** :
  - Réponse appels entrants 24h/7j
  - Prise de RDV en direct pendant l'appel
  - FAQ depuis base de connaissance (PDF, URL, texte)
  - Routage intelligent + résumé humain
  - Transcription + envoi email/SMS immédiat
  - Support L1 avec auto-escalation
  - Détection sentiment (positif/négatif/urgent)
  - Reconnaissance appelants VIP
  - Analyse IA post-appel (résumé, intention, résultat)
  - Dashboard analytique
  - Webhook CRM (HubSpot, Pipedrive, Zapier, Make)
  - Multilangue auto (FR/EN/ES)
  - Enregistrement RGPD-compliant
- **Flow d'appel** :
  ```
  Caller → Vapi.ai → /api/vapi/webhook → Claude → ElevenLabs
  → [book_appointment] → Cal.com
  → [transfer_call] → Vapi transfer
  → [take_message] → Email + SMS
  End → Claude analyse → Email transcript + SMS summary + CRM webhook
  ```
- **Leçons** : Vapi.ai est le meilleur pour la téléphonie IA (<500ms). Claude est supérieur à GPT pour les analyses post-appel. Toujours intégrer webhook CRM dès le départ.

---

## 4. PROJETS SHOWCASE CLIENTS (démos HTML statiques)

Ces projets sont des démos/présentations pour convaincre les clients. Stack : HTML/CSS/JS → Vercel.

| Repo | Client | Secteur | URL |
|------|--------|---------|-----|
| Happi-Audit-Expert | Cabinet audit | Finance | happi-audit-expert.vercel.app |
| Happi-Benta | Benta | Commerce | happi-benta.vercel.app |
| Happi-Cabinet-Arc | Cabinet Arc | Juridique | happi-cabinet-arc.vercel.app |
| Happi-Charier | Charier | BTP/Construction | happi-charier.vercel.app |
| Happi-Groupe-Bellion | Groupe Bellion | Industrie | happi-groupe-bellion.vercel.app |
| Happi-Groupe-Monassier | Groupe Monassier | Notariat | happi-groupe-monassier.vercel.app |
| Happi-Groupe-Trouillet | Groupe Trouillet | Transport | happi-groupe-trouillet.vercel.app |
| Happi-Icelec | Icelec | Électronique | happi-icelec.vercel.app |
| Happi-KingKong | King Kong | E-commerce | happi-king-kong.vercel.app |
| Happi-labeyrie-fine-foods | Labeyrie | Agroalimentaire | happi-labeyrie-fine-foods.vercel.app |
| happi-lavorel-hotels | Lavorel Hotels | Hôtellerie | happi-lavorel-hotels.vercel.app |
| Happi-Mademoiselledesserts | Mademoiselle Desserts | Agroalimentaire | happi-mademoiselledesserts.vercel.app |
| happi-monsieur-meuble | Monsieur Meuble | Meuble | happi-monsieur-meuble.vercel.app |
| Happi-Plastivaloire | Plastivaloire | Plasturgie/Industrie | happi-plastivaloire.vercel.app |
| Happi-Saint-Jean | Saint-Jean | Agroalimentaire | happi-saint-jean.vercel.app |
| Uqudo-Presentation | Uqudo | Identité digitale/KYC | uqudo-presentation.vercel.app |
| L-OL-presentation- | L'OL | Sport/Football | l-ol-presentation.vercel.app |
| MDF.com | Mobilier de France | Meuble | mdf-com.vercel.app |

**Leçon** : Les démos HTML statiques Vercel se livrent en <1 jour. C'est la meilleure façon d'obtenir un accord client avant de développer le vrai bot.

---

## 5. PLATEFORMES ET SAAS

### Happi Web Creator (web builder SaaS)
- **Repo** : `happi-webcreator`
- **Type** : Éditeur de sites web no-code (inspiré Webflow/Framer)
- **Stack** : Next.js 16 + Zustand + @dnd-kit + Framer Motion
- **URL** : github.com/nbayonne76-ui/happi-webcreator
- **Features clés** :
  - 13 blocs configurables (navbar, hero, features, stats, pricing, faq, testimonials, etc.)
  - Éditeur visuel : drag-and-drop sections, propriétés par panneau latéral
  - Couleurs de fond par section (16 presets : dark/light/gradient) + textes adaptatifs auto
  - Espacement vertical (5 niveaux) + largeur contenu (4 niveaux) par section
  - Preview plein écran `/preview/[id]` avec switcher desktop/tablet/mobile
  - Export HTML standalone (zéro dépendance, déployable Vercel en 1 clic)
  - Undo/redo (20 étapes), gestion multi-pages, SEO par page
  - Galerie de templates (6 catégories), générateur IA par prompt
- **Leçons** :
  - Pour DnD + Framer Motion sur le même canvas : utiliser @dnd-kit uniquement dans les Layers, éviter les conflits avec AnimatePresence
  - Export HTML avec styles inline = plus robuste que Tailwind CDN pour déploiement client
  - Le panneau SEO avec prévisualisation Google SERP est très apprécié

### Happi Foundry (playground IA interne)
- **Repo** : `Happi-Foundry`
- **Type** : Claude AI playground + gestion de prompts (inspiré Azure AI Foundry)
- **Stack** : Next.js 14 + FastAPI + PostgreSQL + Anthropic SDK
- **Features** :
  - Playground interactif (streaming, model selector, temperature, max-tokens)
  - Bibliothèque de prompts (tags, recherche)
  - Catalogue de modèles Claude avec pricing
  - Dashboard usage (tokens, coûts, historique)
- **Usage interne** : Tester et affiner les prompts avant déploiement client

### DropOS (SaaS dropshipping)
- **Repo** : `DropOS-DropShipping`
- **Type** : Plateforme SaaS all-in-one pour dropshippers
- **Stack** : Next.js + FastAPI + PostgreSQL + JWT
- **Target** : Dropshippers $10K-$200K/mois
- **Pricing** : $99-149/mois (remplace $400-1000/mois d'outils)
- **Roadmap** : Phase 1 Analytics → Phase 2 Fulfillment → Phase 3 Sourcing → Phase 4 Marketing
- **Intégrations** : Shopify Partner API, tarifs douaniers US HTS / EU TARIC

### Quality Tracking App (Mobilier de France)
- **Repo** : `Quality-tracking-app`
- **Type** : App mobile de suivi qualité livraisons meubles
- **Stack** : React Native (Expo SDK 54) + FastAPI + PostgreSQL
- **Rôles** : Supplier, Driver, Client, Admin, Showroom
- **State** : Zustand + AsyncStorage (offline sync)
- **Auth** : JWT avec auto-refresh

### Top Tier Collection (e-commerce)
- **Repo** : `toptiercollection.shop`
- **Type** : Site e-commerce
- **Stack** : Next.js + Sanity CMS + TypeScript + Tailwind

### H'appi Website (site vitrine)
- **Repo** : `h-appi-website`
- **Type** : Site corporate H'appi
- **Stack** : Next.js + TypeScript
- **Deploy** : h-appi-website.vercel.app

### Microsoft Sales App
- **Repo** : `microsoft-sales-app`
- **Type** : Application commerciale (ancienne)
- **Stack** : JavaScript

---

## 6. SECTEURS CLIENTS COUVERTS

Basé sur les démos et projets réels :

| Secteur | Clients | Use cases chatbot |
|---------|---------|-------------------|
| Meuble/Déco | Mobilier de France, Monsieur Meuble | SAV, recommandations produits, suivi livraison |
| Hôtellerie | Lavorel Hotels | Réservation, concierge, FAQ |
| Agroalimentaire | Labeyrie, Saint-Jean, Mademoiselle Desserts | Support produits, recettes, SAV |
| BTP/Construction | Charier | Devis, planning, support technique |
| Industrie | Plastivaloire, Icelec | Support technique, commandes |
| Transport/Logistique | Groupe Trouillet | Suivi, dispatch, SAV |
| Notariat/Juridique | Groupe Monassier, Cabinet Arc | FAQ, RDV, information juridique |
| Finance/Audit | Audit Expert | FAQ, onboarding client |
| Sport | L'OL (Olympique Lyonnais) | Fan engagement, billetterie, infos |
| E-commerce | KingKong, INnatural, TopTier | Recommandations, suivi commande, support |
| KYC/Identité | Uqudo | Onboarding, vérification, support |

---

## 7. PATTERNS ARCHITECTURE CHATBOT (bonnes pratiques)

### Pattern 1 : Widget embeddable (pour site existant client)
```
widget/
  chatbot.js      → logique principale
  chatbot.css     → styles
  embed.js        → 1 script tag pour intégrer
backend/
  server.js       → Express ou FastAPI
  claudeService.js → intégration Claude
  productKnowledge.js → base de connaissance
config/
  products.json   → catalogue (éditable par client)
  faqs.json       → FAQ (éditable par client)
  bot-personality.json → personnalité (ton, langue)
```

### Pattern 2 : Chatbot full-stack (projet complet)
```
frontend/       → React / Next.js
backend/
  app/
    main.py
    routers/    → chat, auth, tickets, webhooks
    models/     → DB models
    services/   → claude_service, email_service...
  alembic/      → migrations DB
  requirements.txt
docker-compose.yml
```

### Pattern 4 : Web Builder no-code
```
src/
  app/
    dashboard/    → galerie projets + création
    editor/[id]/  → éditeur visuel (Topbar + Sidebar + Canvas + PropertiesPanel)
    preview/[id]/ → rendu propre sans chrome (utilisé aussi pour export)
    templates/    → galerie templates
    generate/     → générateur IA par prompt
  components/
    blocks/       → 1 fichier par type de bloc (HeroBlock, FeaturesBlock...)
    editor/       → Topbar, Sidebar, Canvas, PropertiesPanel
  lib/
    blockStyles.ts → helpers bg/padding/width + couleurs adaptatives dark/light
    defaults.ts    → props par défaut de chaque bloc + templates
    exportHtml.ts  → génère HTML standalone avec styles inline
  store/
    useEditorStore.ts → Zustand (projets, blocs, pages, undo/redo, SEO)
  types/index.ts  → Block, Page (+ seo), Project, Template...
```

### Pattern 3 : Secrétariat vocal
```
Vapi.ai webhook → FastAPI → Claude → ElevenLabs
                         → Cal.com (booking)
                         → Resend + Twilio (notifs)
                         → DB (logs + analytics)
dashboard/      → Next.js (analytics, historique)
```

### Système de qualification en 3 phases (conversion optimale)
```
Phase 1 : Identification → qui est l'utilisateur ? quel besoin ?
Phase 2 : Qualification → quel produit/service correspond ?
Phase 3 : Conversion → proposition + collecte lead / action
```

### Système de tickets priorité (SAV)
```
P0 → Urgence (sécurité, défaut grave)    → notification immédiate
P1 → Haute priorité (produit inutilisable) → <4h
P2 → Normale (problème fonctionnel)       → <24h
P3 → Basse (cosmétique, info)             → <72h
```

---

## 8. RÈGLES IA ET PROMPTS (ce qui fonctionne)

### Modèle préféré : Claude (Anthropic)
- **Pourquoi Claude** : Meilleur pour l'analyse post-appel, la compréhension du contexte long, le français naturel
- **SDK** : `anthropic` (Python) ou `@anthropic-ai/sdk` (Node.js)
- **Modèles recommandés** (avril 2026) :
  - Opus 4.6 (`claude-opus-4-6`) → tâches complexes, analyse
  - Sonnet 4.6 (`claude-sonnet-4-6`) → chatbot standard ← **défaut recommandé**
  - Haiku 4.5 (`claude-haiku-4-5-20251001`) → réponses rapides, faible coût

### Structure prompt système pour chatbot client
```
Tu es [NOM_BOT], l'assistant IA de [NOM_ENTREPRISE].
Tu aides les clients avec [USE_CASE].

PERSONNALITÉ : [ton, langue, formules de politesse]
LIMITES : Tu ne réponds qu'aux questions relatives à [DOMAINE]. Pour tout autre sujet, redirige vers [CONTACT].
BASE DE CONNAISSANCE : [produits, FAQ, procédures]
ACTIONS DISPONIBLES : [book_appointment, create_ticket, collect_lead, transfer_to_human]
LANGUE : Réponds toujours dans la langue de l'utilisateur.
```

### Gestion multilingue
- Détecter automatiquement la langue de l'utilisateur
- Priorité : FR > EN > AR pour les clients H'appi France
- Toujours prévoir FR/EN minimum

---

## 9. CHECKLIST NOUVEAU PROJET CHATBOT

Avant de commencer tout nouveau chatbot :

- [ ] Définir le secteur et le use case principal
- [ ] Choisir le pattern (widget / full-stack / vocal)
- [ ] Configurer `bot-personality.json` ou équivalent
- [ ] Construire la base de connaissance (produits, FAQ, procédures)
- [ ] Définir les actions disponibles (tickets, booking, lead, transfert)
- [ ] Choisir le modèle Claude adapté (coût vs performance)
- [ ] Prévoir multilingue dès le départ
- [ ] Intégrer un système de logs/analytics
- [ ] Prévoir webhook CRM si le client en a un
- [ ] Créer une démo HTML statique Vercel avant le dev complet
- [ ] Tester la qualification en 3 phases
- [ ] Documenter l'API et créer un guide d'installation client

---

## 10. DEPLOY & INFRA

### Railway (backend + DB)
- Idéal pour FastAPI + PostgreSQL
- Fichiers nécessaires : `railway.json`, `nixpacks.toml`, `Procfile`
- Variables d'environnement via Railway Dashboard

### Vercel (frontend + démos)
- Next.js et HTML statiques → déploiement automatique depuis GitHub
- Domaine : `happi-[client].vercel.app` pour les démos
- `EXPO_PUBLIC_API_URL` pour les apps Expo

### Docker (dev local + prod)
- `docker-compose.yml` avec services : backend, frontend, postgres, redis
- Port 8000 souvent bloqué sur WSL2 → utiliser **8001** par défaut
- Commande standard : `docker-compose up -d`

---

## 11. ÉVOLUTION DU BRAIN

### Comment mettre à jour ce fichier
Après chaque nouveau projet terminé, ajouter :
1. Une entrée dans la section 3 (chatbots) ou 5 (plateformes)
2. Le secteur client dans la section 6
3. Tout nouveau pattern découvert dans la section 7
4. Tout nouveau prompt qui fonctionne dans la section 8

### Métriques de succès à tracker par projet
- Taux de résolution autonome (cible : 80%+)
- Temps de réponse moyen (cible : <2s)
- Taux de satisfaction client (cible : 4.5/5+)
- Coût par conversation (optimiser avec Haiku pour les cas simples)

---

## ⚠️ SEUIL DE MIGRATION — HAPPI BRAIN V2

**Projets actifs actuellement : 3 chatbots + 5 plateformes = 8 projets**

> Quand ce chiffre dépasse **12 projets actifs**, migrer vers **Happi Brain V2 (Clean Room)**.

### Pourquoi V2 à 12 projets ?
Au-delà de 12 projets, ce fichier markdown devient trop volumineux pour être lu linéairement de façon efficace. La recherche sémantique devient indispensable.

### Architecture V2 (Clean Room)
```
happi-brain-v2/
  api/           → FastAPI — CRUD entités + endpoint RAG
  db/            → PostgreSQL + pgvector (recherche vectorielle)
    projects/    → table structurée (stack, features, leçons)
    patterns/    → patterns réutilisables indexés
    tech_news/   → veille quotidienne vectorisée
    clients/     → fiches clients avec secteur + use cases
  agent/         → agent de veille (écrit en DB, pas en markdown)
  mcp/           → serveur MCP → Claude l'interroge comme un outil
```

### Ce que V2 apporte
- Recherche sémantique : `search_brain("chatbot hôtellerie")` → résultats pertinents
- Mise à jour par entité (upsert) plutôt qu'append
- MCP server : Claude interroge le Brain comme un outil natif
- Peut devenir un produit vendable aux clients H'appi ("mémoire IA de votre entreprise")

### Comment migrer
1. Créer le repo `happi-brain-v2` avec FastAPI + pgvector
2. Importer tous les fichiers `projects/*.md` actuels via script d'ingestion
3. Configurer le MCP server dans `~/.claude/settings.json`
4. Mettre à jour l'agent de veille pour écrire en DB plutôt qu'en markdown

---

*Dernière mise à jour : 2026-04-06*
*Projets analysés : 28 repos GitHub (nbayonne76-ui)*
