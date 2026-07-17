---
name: happi-brain-crm
description: Happi CRM complet — 28+ sprints livrés, 130+ endpoints, architecture automatisation MCP (Phases 1-7), AI Intelligence Suite (9 outils IA), intégrations Vapi/SAP/Generix, guide déploiement client, Docker Railway Vercel
metadata:
  type: project
---

# HAPPI BRAIN — HAPPI CRM

## INFOS PROJET
- **Repo** : `github.com/nbayonne76-ui/Happi-CRM` (branch `main`)
- **Login** : `admin@happi-crm.com` / `Admin123!`
- **Backend** : `http://localhost:8001` — **Frontend** : `http://localhost:3000`
- **État** : 28+ sprints livrés · 130+ endpoints · 16+ pages frontend
- **Dernière mise à jour** : juin 2026 (audit jq — nouveaux sprints post-28 découverts)

## STACK
```
Backend   → FastAPI 0.135+ + PostgreSQL 16 + SQLAlchemy 2 + Alembic
Frontend  → Next.js 16 + TypeScript + Tailwind CSS + shadcn/ui
IA        → Claude Sonnet 4.6 (Anthropic) + OpenAI GPT-4o (fallback)
Cache     → Redis 7 + fastapi-cache2 (TTL 5 min)
Scheduler → APScheduler (AsyncIOScheduler)
Email     → Resend
Auth      → JWT (access + refresh avec jti UUID pour unicité)
WebSocket → uvicorn[standard] obligatoire + add_api_websocket_route()
Tests     → pytest + TestClient (37 tests, session-scoped fixtures)
Docker    → docker-compose (postgres 16, redis 7, backend :8001, frontend :3000)
```

## MODULES ET ENDPOINTS CLÉS
| Module | Préfixe | Points clés |
|--------|---------|-------------|
| Auth + User Mgmt | `/api/auth` | login, refresh (jti), logout, invite, register, /me, api-keys |
| Contacts | `/api/contacts` | CRUD, bulk, export CSV, leads board, qualify→deal, lead-score, sms |
| Deals | `/api/deals` | CRUD, move stage, mark won/lost, bulk, export CSV |
| Pipelines | `/api/pipelines` | CRUD pipelines + stages, reorder, kanban |
| Companies | `/api/companies` | CRUD + enrichissement |
| Tickets | `/api/tickets` | CRUD, assign, SLA P0-P3, comments, status |
| Analytics | `/api/analytics` | overview, pipeline, revops, sources, team, scoring, tickets-metrics, products, sequences (Redis cache 5min) |
| Forecast | `/api/forecast` | /summary, /reps, /quotas |
| **AI Intelligence Suite** | `/api/ai` | voir section dédiée ci-dessous |
| Notifications | `/api/notifications` + `/ws` | LIST, /count, mark-read, /team + WebSocket |
| Emails | `/api/emails` | templates HTML preview, séquences, send, send-direct, tracking, webhook Resend |
| Workflows | `/api/workflows` | 4 triggers, 6 actions, logs |
| Custom Fields | `/api/custom-fields` | 6 types, 4 entités, JSONB |
| Portal | `/api/portal` | lien sécurisé B2B, signature devis, tickets client, PDF |
| Invoices | `/api/invoices` | FAC-{year}-{n:04d}, cycle vie, PDF, status |
| Enrichments | `/api/contacts/{id}/enrich` | Stripe + Amplitude + Notion JSONB |
| Intégrations | `/api/integrations` | Slack, Gmail, Cal.com, Vapi, SAP, Generix + webhooks |
| Webhooks | `/api/webhooks` | outbound, chatbot, secretary, keys, logs |

---

## AI INTELLIGENCE SUITE (post-Sprint 28)

> 9 outils IA découverts via audit jq (juin 2026). Endpoints non documentés dans les sprints 1-28.

| Endpoint | Méthode | Input | Rôle |
|----------|---------|-------|------|
| `/api/ai/chat` | POST | streaming SSE | Chat IA principal avec tool_use |
| `/api/ai/pipeline-analysis` | GET | — | Analyse IA du pipeline complet |
| `/api/ai/summarize-meeting` | POST | `{notes, contact_id?, deal_id?}` | Résumé de réunion → action items |
| `/api/ai/search` | POST | `{query, entity}` | Recherche en langage naturel dans le CRM |
| `/api/ai/extract-contact` | POST | `{text}` | Extrait les infos d'un contact depuis du texte libre (email, carte de visite…) |
| `/api/ai/stalled-deals` | GET | — | Détecte les deals non bougés + recommandations |
| `/api/ai/next-action` | POST | `{deal_id?, contact_id?}` | Next Best Action pour un deal ou contact |
| `/api/ai/research` | POST | `{company_name, context?, deal_id?}` | Recherche d'opportunité sur une entreprise |
| `/api/ai/predict-win` | POST | `{deal_id}` | Probabilité de gain d'un deal (scoring IA) |
| `/api/ai/score-lead` | POST | contact_id | Score d'un lead 0-100 |
| `/api/ai/draft-email` | POST | `{contact_id, deal_id?, goal, language}` | Rédaction email commercial |

**Usages clés :**
```
"Extraire contact depuis ce texte"  → POST /api/ai/extract-contact {text: "..."}
"Quel est le prochain pas sur ce deal ?"  → POST /api/ai/next-action {deal_id: "..."}
"Analyse notre pipeline"            → GET /api/ai/pipeline-analysis
"Recherche info sur Acme Corp"     → POST /api/ai/research {company_name: "Acme Corp"}
"Probabilité de gagner ce deal ?"  → POST /api/ai/predict-win {deal_id: "..."}
"Résume cette réunion"             → POST /api/ai/summarize-meeting {notes: "..."}
```

---

## NOUVELLES INTÉGRATIONS (post-Sprint 28)

### Vapi (téléphonie IA)
```
PUT    /api/integrations/vapi         → Configure Vapi (webhook URL, API key)
DELETE /api/integrations/vapi         → Supprime la config Vapi
POST   /api/integrations/vapi/webhook → Reçoit les événements Vapi (appels entrants)
POST   /api/webhooks/secretary        → Webhook dédié secrétariat IA (Happi Secretary)
```
**Usage** : connecter Happi Secretary au CRM → chaque appel traité crée une activité + log.

### SAP (ERP enterprise)
```
PUT  /api/integrations/sap      → Configure la connexion SAP
DELETE /api/integrations/sap    → Supprime la config
POST /api/integrations/sap/sync → Synchronise les données SAP → CRM
```

### Generix (ERP/WMS français — Supply Chain)
```
PUT    /api/integrations/generix         → Configure Generix
DELETE /api/integrations/generix         → Supprime la config
POST   /api/integrations/generix/webhook → Reçoit les événements Generix (commandes, stocks)
```
**Contexte** : Generix est un ERP/WMS très utilisé en logistique et supply chain France. Pertinent pour les clients H'appi dans la distribution et l'agroalimentaire.

### Chatbot webhook
```
POST /api/webhooks/chatbot → Reçoit les événements des chatbots H'appi (SAV-Bot, INnatural…)
```
**Usage** : les chatbots peuvent créer des tickets, contacts, ou activités directement dans le CRM via ce webhook.

---

## PATTERNS CRITIQUES (à réutiliser)

### 1. Route ordering FastAPI
```python
# TOUJOURS statiques AVANT paramétrées
@router.get("/deals/export")    # statique en premier
@router.get("/deals/bulk")
@router.get("/deals/{deal_id}") # paramétré après
```

### 2. WebSocket dans FastAPI
```python
# ❌ Ne PAS inclure dans api_router
# ✅ Monter directement :
app.add_api_websocket_route("/ws/notifications", notifications_ws)
# uvicorn[standard] OBLIGATOIRE dans requirements.txt
```

### 3. JWT refresh token unicité
```python
def create_refresh_token(subject):
    return jwt.encode({
        "sub": str(subject), "exp": expire,
        "type": "refresh",
        "jti": str(uuid.uuid4())  # ← unicité garantie
    }, SECRET_KEY)
```

### 4. Streaming SSE (AI chat)
```python
# Backend : StreamingResponse + async generator
async def stream_gen():
    async with client.messages.stream(...) as stream:
        async for text in stream.text_stream:
            yield f"data: {text}\n\n"
return StreamingResponse(stream_gen(), media_type="text/event-stream")

# Frontend : fetch + ReadableStream (pas axios)
const res = await fetch("/api/ai/chat", { method: "POST", body: ... })
const reader = res.body.getReader()
while (true) {
    const { done, value } = await reader.read()
    if (done) break
}
```

### 5. Email tracking via webhooks Resend (Svix)
```python
# POST /emails/webhook/resend — PUBLIC, pas d'auth
# Events : email.delivered, email.opened, email.clicked, email.bounced
# Matcher via EmailLog.resend_id
# Règle : ne jamais dégrader un statut (clicked > opened > delivered > sent)
_PRECEDENCE = {"scheduled":0,"sent":1,"delivered":2,"opened":3,"clicked":4,"bounced":5,"failed":6}
```

### 6. Alembic enum PostgreSQL
```python
# Ajouter valeur à un enum existant :
op.execute("ALTER TYPE myenum ADD VALUE IF NOT EXISTS 'newval'")
# NE PAS recréer l'enum
```

### 7. HTML preview iframe (sandboxé)
```tsx
<iframe srcDoc={previewHtml} sandbox="allow-same-origin" />
// ✅ Aucun appel backend — 100% client-side
// ✅ sandbox interdit JS dans l'iframe (sécurité XSS)
```

---

## LEÇONS APPRISES CRM
- **WebSocket** : `uvicorn[standard]` manquant = 404 silencieux.
- **Soft delete** : `is_deleted=False` dans tous les WHERE. Ne jamais DELETE physiquement.
- **Composite indexes** : `(is_deleted, status)`, `(is_deleted, owner_id)` sur toutes les tables filtrées.
- **Redis cache** : toujours prévoir un fallback gracieux (`try/except` au démarrage si Redis absent).
- **fpdf2** : lib s'appelle `fpdf2` sur PyPI mais s'importe `from fpdf import FPDF`. Helvetica = Latin-1 uniquement, éviter les em-dashes `—`.
- **Webhook public FastAPI** : endpoint sans `Depends(get_current_user)`. Toujours vérifier la signature.
- **Pytest avec slowapi** : `limiter._enabled = False` sur chaque instance (pas de monkeypatch).

---

## OFFRE COMMERCIALE CRM

| Formule | Prix | Contenu |
|---------|------|---------|
| **Starter** | Devis personnalisé | Déploiement Docker + 1 mois support |
| **Pro** | 300-800€/mois | Starter + intégrations MCP + mises à jour |
| **Enterprise** | 800-2000€/mois | Pro + SLA + personnalisations + formation |

**Arguments** : HubSpot Pro = 90€/user/mois + 15k€ implémentation. AI Chat Claude natif. RGPD.

---

## DÉPLOIEMENT RAILWAY + VERCEL

### Docker setup (local)
```bash
cp .env.example .env && nano .env
docker compose up -d
docker compose exec backend python seed.py  # admin + pipeline + tags
```

### Variables Railway (backend)
```
DATABASE_URL, SECRET_KEY, OPENAI_API_KEY, AI_PROVIDER=openai,
RESEND_API_KEY, EMAIL_FROM=crm@happi-bot.com, FRONTEND_URL, ENVIRONMENT=production
```

### Variable Vercel (frontend)
```
NEXT_PUBLIC_API_URL = https://[backend].up.railway.app/api/v1
```

### Ordre de déploiement
1. Railway → créer PostgreSQL → noter `DATABASE_URL`
2. Railway → déployer backend (root dir: `backend`)
3. Vercel → déployer frontend (root dir: `frontend`)
4. Railway → mettre à jour `FRONTEND_URL` → Redeploy
5. `railway run python seed.py`

---

## ARCHITECTURE D'AUTOMATISATION MCP (Phases 1-7)

```
ENTRÉES AUTOMATIQUES                    COUCHE INTELLIGENCE              SORTIE
─────────────────────────               ───────────────────              ──────
Jotform      → leads CRM (Phase 1)  ┐
Stripe       → paiements    (P2)    │
Coupler.io   → attribution  (P3)    ├──▶  contact_enrichments  ──▶  AI Chat tool_use
Amplitude    → comportement (P4)    │     (Phase 6 : backbone)       (Phase 7)
Notion       → connaissance (P5)    ┘
APScheduler → sync 1h/auto
```

### Les 6 outils AI Chat (tool_use Anthropic)
| Outil | API | Question exemple |
|-------|-----|------------------|
| `get_stripe_revenue` | Stripe | "Quel est notre MRR ce mois ?" |
| `list_stripe_unpaid_invoices` | Stripe | "Qui n'a pas payé ?" |
| `get_amplitude_events` | Amplitude | "Combien de deals créés ce mois ?" |
| `search_notion_pages` | Notion | "Cherche la procédure onboarding" |
| `get_contact_enrichment` | DB locale | "Profil complet de client@example.com" |
| `get_crm_stats` | DB locale | "Rapport général du CRM" |

### MCP Servers (Claude Code — `~/.claude/mcp.json`)
```json
{
  "mcpServers": {
    "happi-stripe": { "command": "python", "args": [".../mcp/stripe_server.py"], "env": { "STRIPE_SECRET_KEY": "sk_live_..." } },
    "happi-amplitude": { "command": "python", "args": [".../mcp/amplitude_server.py"], "env": { "AMPLITUDE_API_KEY": "...", "AMPLITUDE_SECRET_KEY": "..." } },
    "happi-jotform": { "command": "python", "args": [".../mcp/jotform_server.py"], "env": { "JOTFORM_API_KEY": "...", "CRM_API_URL": "http://localhost:8001/api", "CRM_API_TOKEN": "<JWT>" } },
    "happi-notion": { "command": "python", "args": [".../mcp/notion_server.py"], "env": { "NOTION_API_TOKEN": "ntn_..." } }
  }
}
```
Coupler.io : `claude mcp add coupler-io --transport http https://mcp.coupler.io/mcp`

**Note** : `CRM_API_TOKEN` expire en 24h → prévoir un système d'API key permanent.

### Contact Enrichment Layer (backbone — Phase 6)
```python
class ContactEnrichment(Base):
    __tablename__ = "contact_enrichments"
    contact_id = Column(String, ForeignKey("contacts.id", ondelete="CASCADE"), index=True)
    source     = Column(Enum("stripe","amplitude","notion","jotform","coupler"))
    data       = Column(JSON, default=dict)
    synced_at  = Column(DateTime(timezone=True))
# Upsert par (contact_id, source) — job APScheduler toutes les 1h
```

---

## SPRINTS 22-28 (MAI 2026)

### Sprint 22 — Workflow Automation Engine
4 triggers : `deal_won`, `deal_stage_changed`, `contact_created`, `ticket_created`
6 actions : `create_activity`, `slack_notif`, `send_email`, `send_sms`, `webhook_fire`, `update_field`
Frontend : `WorkflowsSection` + `ActionEditor` + `WorkflowLogsModal` dans settings

### Sprint 23 — Custom Fields
6 types : `text`, `number`, `boolean`, `date`, `select`, `multiselect`
4 entités : `contact`, `deal`, `company`, `ticket`
Colonne JSONB `custom_fields` ajoutée à chaque table

### Sprint 24 — AI Email Drafting
Provider-agnostic : OpenAI ou DeepSeek (même client, `base_url` différent)
6 goals : followup, proposal, reminder, intro, thanks, reactivation
Modal multi-étapes + preview HTML live + bouton "Regénérer"

### Sprint 25 — Portail Client
Lien sécurisé B2B (token UUID, 30j) → tickets + devis + signature
Pattern Suspense obligatoire pour `useSearchParams()` dans Next.js

### Sprint 26 — PDF Export
`fpdf2` : `build_deal_pdf()` + `build_invoice_pdf()`
`new_x="LMARGIN", new_y="NEXT"` remplace `ln=True`

### Sprint 27 — Facturation
Auto-numérotation `FAC-{year}-{count+1:04d}`
États : draft → sent → paid / cancelled

### Sprint 28 — Rôles & Permissions
4 rôles : `admin`, `sales`, `support`, `viewer`
Dépendances : `require_admin()`, `require_sales_or_admin()`, `get_current_user()`

---

## REQUIREMENTS.TXT ESSENTIELS CRM
```
fastapi>=0.135
uvicorn[standard]>=0.43    ← [standard] OBLIGATOIRE pour WebSocket
sqlalchemy>=2.0
alembic>=1.18
psycopg2-binary>=2.9
python-jose[cryptography]>=3.3
anthropic>=0.97
openai>=1.0
resend>=2.0
slowapi>=0.1
apscheduler>=3.10
redis[hiredis]>=5.0
fastapi-cache2>=0.2
fpdf2>=2.7
```

---

*Mis à jour : 2026-05-31 — extrait de happi_brain.md v22*
