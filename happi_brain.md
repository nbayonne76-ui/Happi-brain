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
Frontend  → Next.js 14 + TypeScript + Tailwind
Backend   → FastAPI + PostgreSQL
State     → Zustand (React Native) / Redux ou Context (web)
Mobile    → React Native (Expo SDK 54)
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

---
## 📰 Veille Tech — 2026-04-04
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic accidentally releases source code for Claude AI agent](https://www.bloomberg.com/news/articles/2026-04-01/anthropic-accidentally-releases-source-code-for-claude-ai-agent) | Bloomberg | #Anthropic #Claude |
| [Claude Mythos : nouveau modèle Anthropic avec raisonnement avancé en préparation](https://siliconangle.com/2026/03/27/anthropic-launch-new-claude-mythos-model-advanced-reasoning-features/) | SiliconAngle | #Anthropic #LLM |
| [Claude API : max_tokens 300k, résidence des données EU, fine-grained tool streaming GA](https://releasebot.io/updates/anthropic) | Releasebot / Anthropic | #Anthropic #API #RGPD |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV Community | #FastAPI #Next.js #SaaS #Docker |
| [Vercel vs Hetzner in 2026: Which Is Actually Worth It for Solo Developers?](https://devtoolpicks.com/blog/vercel-vs-hetzner-2026-solo-developers) | DevToolPicks | #Vercel #SaaS |
| [onyx — Open Source AI Chat Platform (23k★, +1212 today)](https://github.com/onyx-dot-app/onyx) | GitHub Trending Python | #chatbot #LLM |
| [LightRAG — Simple and Fast Retrieval-Augmented Generation (32k★)](https://github.com/HKUDS/LightRAG) | GitHub Trending Python | #LLM #chatbot #RAG |
| [microsoft/agent-framework — Build & orchestrate AI agents Python/.NET (8.6k★)](https://github.com/microsoft/agent-framework) | GitHub Trending Python | #LLM #SaaS |
| [Mastra — TypeScript-first agent framework, 1M+ npm/mois, Y Combinator $13M](https://www.firecrawl.dev/blog/best-open-source-agent-frameworks) | Firecrawl Blog | #LLM #Next.js #SaaS |
| [oh-my-openagent — Meilleur harness d'agents IA (48k★, +468 today)](https://github.com/code-yeongyu/oh-my-openagent) | GitHub Trending TS | #LLM #chatbot |
| [Vapi.ai — Build Advanced Voice AI Agents](https://vapi.ai/) | Vapi | #VoiceAI #chatbot |
| [React Native Speech Recognition in 2026: The Complete Guide](https://picovoice.ai/blog/react-native-speech-recognition/) | Picovoice | #ReactNative #VoiceAI #RGPD |
| [The State of AI in 2026: From Chatbots to the Chorus](https://dev.to/maximus_prime_1/the-state-of-ai-in-2026-from-chatbots-to-the-chorus-a25) | DEV Community | #chatbot #LLM |
| [Rapid Development with Next.js + FastAPI + Vercel + Neon Postgres](https://www.wolk.work/blog/posts/rapid-development-with-next-js-fastapi-vercel-neon-postgres) | Wolk | #FastAPI #Next.js #PostgreSQL #Vercel |
| [just-bash — Bash for Agents by Vercel Labs (2.5k★)](https://github.com/vercel-labs/just-bash) | GitHub Trending TS | #Vercel #LLM |

### 💡 Insights clés
- **Claude Mythos arrive** : Anthropic finalise un nouveau modèle plus puissant qu'Opus — à surveiller pour migrer les projets H'appi dès la sortie GA.
- **Claude API → 300k tokens + résidence EU** : La limite max_tokens passe à 300 000 tokens sur les Batches API, et la résidence des données en Europe est disponible via `inference_geo` — critique pour la conformité RGPD des clients H'appi.
- **Dokploy = alternative low-cost à Railway** : Stack Next.js + FastAPI + Dokploy sur Hetzner VPS devient un choix populaire pour réduire les coûts infra par rapport à Railway/Vercel.
- **onyx (23k★) explose** : Plateforme open source de chat IA complète avec LLM, RAG, connecteurs — architecture de référence à étudier pour les projets H'appi.
- **LightRAG s'impose pour le RAG** : Approche plus rapide et simple que LangChain pour les bases de connaissance — à intégrer dans les chatbots clients à fort volume documentaire.
- **Marché Voice AI = 27 Mds$ en 2026** : Excellent timing pour Happi Secretary — Vapi.ai reste la référence, et Mistral Voxtral TTS (<100ms, 3GB RAM) est à surveiller comme alternative à ElevenLabs.
- **Mastra (TypeScript)** : Framework agent TypeScript-first avec 1.77M npm/mois — pertinent pour les projets Next.js H'appi intégrant de l'agentic AI.

---

---
## 📰 Veille Tech — 2026-04-05
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Build GenAI Applications Locally With Docker Model Runner](https://thenewstack.io/build-genai-applications-locally-with-docker-model-runner/) | TheNewStack | #Docker #LLM |
| [A Practical Guide To Building a RAG-Powered Chatbot](https://thenewstack.io/a-practical-guide-to-building-a-rag-powered-chatbot/) | TheNewStack | #RAG #chatbot |
| [Frontend AI: Vercel Abstracts Model Chaos in One Interface](https://thenewstack.io/frontend-ai-vercel-abstracts-model-chaos-in-one-interface/) | TheNewStack | #Vercel #LLM |
| [Choosing Your AI Orchestration Stack for 2026](https://thenewstack.io/choosing-your-ai-orchestration-stack-for-2026/) | TheNewStack | #LLM #SaaS |
| [LLMs and AI Agents Evolving Like Programming Languages](https://thenewstack.io/llms-and-ai-agents-evolving-like-programming-languages/) | TheNewStack | #LLM #AI-agents |
| [Building a Full-Stack AI Chatbot with FastAPI (Backend) and React (Frontend)](https://dev.to/vipascal99/building-a-full-stack-ai-chatbot-with-fastapi-backend-and-react-frontend-51ph) | DEV Community | #chatbot #FastAPI |
| [RAG using LLMSmith and FastAPI](https://dev.to/dheerajgopi/rag-using-llmsmith-and-fastapi-1e6i) | DEV Community | #RAG #FastAPI |
| [Building a RAG chatbot with TypeScript and Next.js](https://dev.to/emertechie/building-a-rag-chatbot-with-typescript-and-nextjs-53c6) | DEV Community | #RAG #chatbot #Next.js |
| [From LangChain Demos to a Production-Ready FastAPI Backend](https://dev.to/hamluk/from-langchain-demos-to-a-production-ready-fastapi-backend-1c0a) | DEV Community | #FastAPI #LLM |
| [Why we no longer use LangChain for building our AI agents](https://news.ycombinator.com/item?id=40739982) | HackerNews | #AI-agents #LLM |
| [Show HN: AI Timeline – 171 LLMs from Transformer (2017) to GPT-5.3 (2026)](https://news.ycombinator.com/item?id=47119871) | HackerNews | #LLM |
| [LightRAG — Simple and Fast Retrieval-Augmented Generation](https://github.com/HKUDS/LightRAG) | GitHub Trending Python | #RAG #LLM #chatbot |
| [onyx — Open Source AI Chat Platform](https://github.com/onyx-dot-app/onyx) | GitHub Trending Python | #chatbot #LLM #SaaS |
| [microsoft/agent-framework — Build & orchestrate AI agents](https://github.com/microsoft/agent-framework) | GitHub Trending Python | #AI-agents #LLM |
| [vercel-labs/just-bash — Bash for Agents](https://github.com/vercel-labs/just-bash) | GitHub Trending TypeScript | #AI-agents #Vercel |

### 💡 Insights clés
- **RAG s'impose comme standard de production** : LightRAG, onyx, et plusieurs guides DEV.to confirment que le RAG (Retrieval-Augmented Generation) est l'architecture incontournable pour les chatbots clients à fort volume documentaire — à intégrer en priorité dans les prochains projets H'appi.
- **FastAPI + Next.js reste la stack de référence** : Confirmé par de multiples sources DEV.to et TheNewStack pour les backends IA en production — stack H'appi parfaitement alignée.
- **Vercel AI Gateway** : Vercel abstrait désormais plus de 100 modèles LLM via une seule interface — pertinent pour les projets Next.js H'appi qui intègrent de l'IA générative côté frontend.
- **Docker Model Runner** : Permet de tester des LLMs localement avant déploiement sur Railway/Vercel, réduisant les cycles de dev et les coûts de test — à adopter dans le workflow H'appi.
- **Abandon de LangChain en production** : Tendance confirmée sur HackerNews — les équipes préfèrent des frameworks plus légers (LightRAG, FastAPI direct) pour les agents de production. À surveiller pour les nouveaux projets.
- **microsoft/agent-framework (Python/.NET)** : Nouveau framework multi-agents Microsoft en trending — alternative sérieuse à explorer pour les architectures multi-agents complexes.
- **Orchestration IA 2026** : TheNewStack recommande de choisir son stack d'orchestration maintenant (LangGraph, AutoGen, CrewAI) avant que le marché se consolide — décision architecturale critique pour H'appi.

*Dernière mise à jour : 2026-04-05*
*Projets analysés : 27 repos GitHub (nbayonne76-ui)*

---
## 📰 Veille Tech — 2026-04-06
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [I built a demo of what AI chat will look like when it's "free" and ad-supported](https://news.ycombinator.com/item?id=47205890) | HackerNews | #chatbot |
| [The current hype around autonomous agents, and what actually works in production](https://news.ycombinator.com/item?id=44623207) | HackerNews | #LLM #chatbot |
| [AI Chatbots vs AI Agents: What Developers Should Build in 2026](https://dev.to/the_bookmaster/ai-chatbots-vs-ai-agents-what-developers-should-build-in-2026-40jf) | DEV Community | #chatbot #LLM |
| [10 AI Agents Powering Million-Dollar Businesses in 2026](https://dev.to/joinwithken/10-ai-agents-powering-million-dollar-businesses-in-2026-25mn) | DEV Community | #SaaS #LLM |
| [Best Visual AI Agents in 2026: Real-Time & Multimodal Tools](https://dev.to/getstreamhq/best-visual-ai-agents-in-2026-real-time-multimodal-tools-44g6) | DEV Community | #chatbot #LLM #VoiceAI |
| [onyx — Open Source AI Chat Platform](https://github.com/onyx-dot-app/onyx) | GitHub Trending Python | #chatbot #LLM |
| [RAG-Anything: All-in-One RAG Framework](https://github.com/HKUDS/RAG-Anything) | GitHub Trending Python | #LLM #chatbot #RAG |
| [NousResearch/hermes-agent — The agent that grows with you](https://github.com/NousResearch/hermes-agent) | GitHub Trending Python | #LLM #chatbot |
| [microsoft/agent-framework — Build & orchestrate AI agents](https://github.com/microsoft/agent-framework) | GitHub Trending Python | #LLM |
| [badlogic/pi-mono — AI agent toolkit: CLI + unified LLM API + Slack bot](https://github.com/badlogic/pi-mono) | GitHub Trending TypeScript | #LLM #chatbot |
| [simstudioai/sim — Build, deploy and orchestrate AI agents](https://github.com/simstudioai/sim) | GitHub Trending TypeScript | #SaaS #LLM |
| [Anthropic's rough week: leaked models, exposed source code, botched GitHub takedown](https://thenewstack.io/anthropic-claude-code-leak/) | TheNewStack | #Anthropic #Claude |
| [5 Key Trends Shaping Agentic Development in 2026](https://thenewstack.io/5-key-trends-shaping-agentic-development-in-2026/) | TheNewStack | #LLM |
| [6 agentic knowledge base patterns emerging in the wild](https://thenewstack.io/agentic-knowledge-base-patterns/) | TheNewStack | #LLM #chatbot |
| [The hidden technical debt of agentic engineering](https://thenewstack.io/hidden-agentic-technical-debt/) | TheNewStack | #LLM |

### 💡 Insights clés
- **RAG-Anything (HKUDS)** : nouveau framework RAG all-in-one en trending Python — plus complet que LightRAG, supporte texte, image, audio, vidéo — à évaluer pour les chatbots H'appi à fort volume documentaire.
- **Hermes Agent (NousResearch)** : agent "qui grandit avec l'utilisateur" via mémoire persistante — concept clé à intégrer dans les prochains chatbots H'appi pour améliorer la personnalisation.
- **simstudioai/sim** : plateforme SaaS open source pour orchestrer des agents (deploy + monitor) — architecture de référence pour une future offre multi-agents H'appi.
- **Anthropic / Claude** : semaine difficile (leak code source Claude Code) — aucun impact immédiat sur les SDK clients, mais à surveiller pour les prochaines updates Anthropic.
- **Dette technique agentic** : TheNewStack alerte sur le coût caché des systèmes agents en prod (observabilité, tests, rollback) — anticiper dès la conception dans les projets H'appi.
- **AI chat ad-supported** : modèle freemium publicitaire exploré sur HN — opportunité de pricing alternatif à explorer pour des offres H'appi grand public.
- **pi-mono (TypeScript)** : toolkit agent unifié (CLI + API LLM + TUI + Slack bot) — candidat sérieux pour remplacer plusieurs outils internes H'appi en un seul framework.

*Dernière mise à jour : 2026-04-06*
