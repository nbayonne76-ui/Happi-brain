---
name: happi-brain-inspiration
description: Veille GitHub — patterns et insights extraits des meilleurs repos publics (Twenty CRM, Dify, Chatwoot, Basjoo, Vapi) applicables aux projets H'appi
metadata:
  type: project
---

# HAPPI BRAIN — VEILLE GITHUB & INSPIRATION

> Analyse réalisée juin 2026 via GitHub API publique + jq.
> Ces insights sont extraits de repos à haute valeur (49k à 145k stars) et filtrés pour leur applicabilité directe à H'appi.

---

## 1. TWENTY CRM — 49 815 ⭐ (l'alternatif open source Salesforce)

**Repo** : `twentyhq/twenty` | Stack : NestJS + GraphQL + TypeScript + PostgreSQL + TypeORM + Redis

### Ce qu'ils font différemment de Happi CRM

| Feature | Twenty CRM | Happi CRM actuel |
|---------|-----------|-----------------|
| API | GraphQL (yoga + nestjs) | REST (FastAPI) |
| Jobs asynchrones | **BullMQ** (Redis-based) | APScheduler |
| Email rendering | **@react-email/render** | HTML strings |
| Multi-provider IA | **Vercel AI SDK** (Anthropic, OpenAI, Google, Mistral…) | Anthropic seul |
| Storage | AWS S3 + Cloudflare R2 | Local uploads |
| Observabilité | OpenTelemetry + **Sentry** | Logs structurés |
| Architecture | Monorepo 20+ packages | Mono-repo backend/frontend |
| Extensibilité | **twenty-sdk** (apps as code) | Non (custom dev) |

### Insight critique : `twenty-claude-skills`
Twenty a un package dédié **`twenty-claude-skills`** — ils ont intégré Claude Code directement dans le CRM comme skill native. Ils ont aussi `twenty-codex-plugin`. Ça confirme leur vision : le CRM est une plateforme d'agents IA, exactement la même vision qu'Happi CRM.

**→ Action H'appi** : explorer une intégration/plugin Happi CRM pour Twenty (marché de l'open source).

### Pattern `defineObject` à retenir
```typescript
// Twenty SDK : définir des objets CRM as code → déployable comme une app
import { defineObject, FieldType } from 'twenty-sdk/define';
export default defineObject({
  nameSingular: 'deal',
  fields: [
    { name: 'amount', type: FieldType.CURRENCY },
    { name: 'closeDate', type: FieldType.DATE_TIME },
  ],
});
// npx twenty app:publish --private
```
**→ Pattern à adopter** : permettre aux clients H'appi CRM de définir leurs objets métier as code.

### BullMQ > APScheduler pour les jobs critiques
```typescript
// Twenty utilise BullMQ pour tous les jobs asynchrones (emails, enrichissement, sync)
// BullMQ = Redis-based, persist les jobs, retry automatique, dashboard visuel
// APScheduler (actuel Happi CRM) = in-memory, pas de persistence, pas de retry
```
**→ Migration à prévoir** : remplacer APScheduler par **BullMQ** (ou `celery` côté Python) pour la prod.

### Vercel AI SDK — multi-provider sans changement de code
```typescript
// Permet de switcher entre Anthropic, OpenAI, Google, Mistral avec le même code
import { generateText } from 'ai';
import { anthropic } from '@ai-sdk/anthropic';
import { openai } from '@ai-sdk/openai';
const model = useAnthropic ? anthropic('claude-sonnet-4-6') : openai('gpt-4o');
await generateText({ model, prompt: '...' });
```
**→ À adopter dans Happi CRM** pour le chat IA : permet de basculer de provider sans refactorer.

---

## 2. DIFY — 145 053 ⭐ (plateforme agentic workflows)

**Repo** : `langgenius/dify` | Stack : Python backend + TypeScript frontend + Docker

### Ce que Dify apporte que H'appi n'a pas encore

**1. RAG Pipeline complet**
- Ingestion documents (PDF, URL, texte, Notion, GitHub…)
- Chunking intelligent + embedding → pgvector / Weaviate / Pinecone
- Retrieval avec reranking
- **→ Applicable à Happi Secretary** : la base de connaissance est aujourd'hui statique (JSON/texte hardcodé). Passer à un vrai RAG permettrait aux clients de l'alimenter eux-mêmes (upload PDF, URL de leur site…).

**2. Observabilité LLM avec Langfuse**
```yaml
# Intégration Dify → Langfuse → traces de chaque appel LLM
# Permet de voir : coût par conversation, tokens utilisés, temps de réponse, prompts qui échouent
```
**→ À intégrer dans Happi CRM** pour optimiser les coûts Claude et débugger les prompts en production.

**3. Architecture Workflow visuel**
Dify permet de créer des workflows IA en "no-code" via un canvas. C'est la direction vers laquelle H'appi pourrait évoluer pour le module Workflows du CRM.

**4. Plugins system**
Dify a un système de plugins qui ressemble exactement aux MCP servers H'appi. La différence : les plugins Dify sont distribuables via marketplace.

---

## 3. CHATWOOT — 30 671 ⭐ (support omnicanal)

**Repo** : `chatwoot/chatwoot` | Stack : Ruby on Rails + Vue.js (non réutilisable pour H'appi)

### Features à copier pour les chatbots H'appi

| Feature Chatwoot | Description | Priorité H'appi |
|-----------------|-------------|-----------------|
| **Canned Responses** | Réponses pré-définies accessibles en `/` dans l'interface | P1 — à ajouter aux chatbots |
| **CSAT Reports** | Survey satisfaction automatique post-conversation | P1 — KPI manquant dans H'appi |
| **Pre-Chat Forms** | Formulaire avant le chat (nom, email, sujet) → qualification automatique | P0 — booste la qualification 3 phases |
| **Help Center Portal** | KB publique self-service pour réduire les tickets | P2 — applicable à Happi Secretary |
| **AI Agent "Captain"** | Agent IA qui répond automatiquement aux queries communes | ✅ déjà dans H'appi |
| **Labels + Auto-Assignment** | Routage intelligent des conversations | ✅ déjà dans H'appi CRM |
| **Agent Capacity Management** | Limite le nombre de conversations par agent | P2 — multi-tenant |
| **Live View** | Vue temps réel des conversations en cours | P2 — utile pour les admins |

### Pattern Pre-Chat Form → qualification automatique
```javascript
// Pattern Chatwoot adapté pour H'appi
const preChatFields = [
  { name: 'name', label: 'Votre nom', required: true },
  { name: 'email', label: 'Email', required: true },
  { name: 'subject', label: 'Sujet', type: 'select',
    options: ['SAV', 'Information produit', 'Commande', 'Autre'] }
];
// → Les données pré-renseignées alimentent directement la Phase 1 de qualification
// → Gain de 30-40% sur le temps de qualification (le bot ne redemande pas)
```

### Pattern CSAT (Customer Satisfaction)
```python
# À envoyer automatiquement 24h après la clôture d'un ticket
# Score 1-5 + commentaire libre
# Stocké dans DB → analytics tableau de bord
# Cible H'appi : 4.5/5+ (déjà dans les métriques du brain)
```

---

## 4. BASJOO — 134 ⭐ (RAG chatbot FastAPI + pgvector)

**Repo** : `haoyiyin/basjoo` | Stack : **FastAPI + Next.js + pgvector** — EXACTEMENT la stack H'appi

### Le pattern RAG qu'H'appi devrait adopter pour Secretary

```
SANS RAG (actuel H'appi) :
  Prompt système = texte statique hardcodé ou JSON fixe

AVEC RAG (Basjoo pattern) :
  1. Client upload PDF/URL/texte → chunking → embedding → pgvector
  2. À chaque message user → similarity search → top-k chunks
  3. Chunks injectés dans le contexte Claude → réponse précise et à jour
```

**Stack RAG minimale pour H'appi (ajout sur FastAPI existant) :**
```bash
pip install pgvector sqlalchemy-pgvector sentence-transformers
# OU via Anthropic embeddings (même API) :
# client.embeddings.create(model="voyage-3", input=text)
```

```python
# Migration Alembic pour pgvector :
op.execute("CREATE EXTENSION IF NOT EXISTS vector")
# Colonne embedding :
from pgvector.sqlalchemy import Vector
embedding = Column(Vector(1536))  # dimension selon le modèle

# Recherche similitude :
results = db.query(KnowledgeChunk).order_by(
    KnowledgeChunk.embedding.cosine_distance(query_embedding)
).limit(5).all()
```

**→ Application immédiate** : Happi Secretary + SAV-Bot → la base de connaissance devient dynamique, alimentée par les clients eux-mêmes.

---

## 5. VAPI FASTAPI VOICE AGENT — Pattern de référence

**Repo** : `extrawest/vapi_personal_assistant_voice_agent`

### Architecture Vapi + FastAPI (validée par la communauté)

```
Voice Call → Vapi AI → webhook POST /vapi/webhook → FastAPI router
                                                    → parse function_call
                                                    → execute tool (todo, calendar, reminder)
                                                    → return tool_result JSON
                                                    → Vapi synthétise la réponse vocale
```

Ce pattern est exactement celui de Happi Secretary. La différence : leur projet utilise des **tools Vapi natifs** (function calling côté Vapi) plutôt que des tools Claude. Les deux approches sont valides.

**Pattern tools Vapi (à comparer avec l'approche Claude tools actuelle) :**
```python
# Vapi envoie un "function_call" dans le webhook body
@router.post("/vapi/webhook")
async def vapi_webhook(body: dict):
    message = body.get("message", {})
    if message.get("type") == "function-call":
        fn_name = message["functionCall"]["name"]
        params = message["functionCall"]["parameters"]
        result = await dispatch_function(fn_name, params)
        return {"result": result}
```

---

## SYNTHÈSE — ROADMAP D'ENRICHISSEMENT H'APPI

### P0 — Court terme (impact immédiat)

| Action | Source | Projet H'appi concerné |
|--------|--------|------------------------|
| Ajouter **Pre-Chat Forms** aux widgets chatbot | Chatwoot | SAV-Bot, INnatural |
| Ajouter **CSAT survey** post-conversation | Chatwoot | Tous les chatbots |
| Intégrer **Langfuse** pour observer les appels LLM | Dify | Happi CRM + Secretary |
| Migrer base de connaissance Secretary vers **pgvector RAG** | Basjoo | Happi Secretary |

### P1 — Moyen terme

| Action | Source | Projet H'appi concerné |
|--------|--------|------------------------|
| Adopter **Vercel AI SDK** pour le multi-provider | Twenty | Happi CRM AI Chat |
| Remplacer **APScheduler** par **BullMQ** | Twenty | Happi CRM (jobs critiques) |
| Ajouter **@react-email/render** pour les templates | Twenty | Happi CRM emails |
| **Canned Responses** dans les interfaces chatbot | Chatwoot | Dashboard chatbots |

### P2 — Long terme

| Action | Source | Idée |
|--------|--------|------|
| **Plugin Happi pour Twenty CRM** | Twenty | Marché open source |
| **Workflow canvas** no-code pour clients | Dify | Happi CRM Workflows |
| **Help Center Portal** public | Chatwoot | Happi Secretary |
| **Marketplace de skills** pour Happi CRM | Twenty SDK | Extensibilité |

---

## OUTILS DE VEILLE À UTILISER RÉGULIÈREMENT

```bash
# Chercher les repos trending par topic
curl -s "https://api.github.com/search/repositories?q=topic:chatbot+topic:fastapi&sort=stars&order=desc&per_page=10" | jq '.items[] | {name: .full_name, stars: .stargazers_count, description: .description}'

# Suivre les releases d'un repo
curl -s "https://api.github.com/repos/twentyhq/twenty/releases/latest" | jq '{version: .tag_name, date: .published_at, notes: .body[:300]}'

# Analyser le package.json d'un repo
curl -s "https://raw.githubusercontent.com/[owner]/[repo]/main/package.json" | jq '.dependencies | keys'

# Analyser les requirements Python
curl -s "https://raw.githubusercontent.com/[owner]/[repo]/main/requirements.txt"
```

---

*Créé : 2026-06-13 — Analyse GitHub publique (5 repos, 270k+ stars cumulés)*
*Prochaine veille recommandée : septembre 2026 (tous les 3 mois)*
