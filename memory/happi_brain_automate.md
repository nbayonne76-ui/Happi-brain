---
name: happi-brain-automate
description: "H'appi Automate — orchestrateur workflows visuels (comparable Azure Logic Apps) : roadmap MVP 4 sprints, architecture complète, stack, modèle données, canvas React Flow, workers Celery, nodes catalogue, positionnement marché"
metadata: 
  node_type: memory
  type: project
  originSessionId: a870a091-4581-44f5-b83c-93a16696bac9
---

# HAPPI BRAIN — H'APPI AUTOMATE

> Nouveau produit SaaS H'appi — Orchestrateur de workflows visuels pour PME françaises.
> Comparable à Azure Logic Apps / Make / n8n — avec Claude natif + RGPD France.
> **Statut : Conception validée — MVP à construire (roadmap 4 sprints)**
> **Conçu le : 2026-07-17**

---

## POSITIONNEMENT PRODUIT

### Problème adressé
Azure Logic Apps coûte €150–500+/mois et nécessite une expertise Azure. Make/Zapier sont en USD, hébergés US (problème RGPD). n8n en self-hosted demande de la maintenance infra. Les PME françaises n'ont pas de solution simple, française, avec IA native.

### Solution H'appi Automate
Orchestrateur de workflows visuels pour PME françaises :
- **Drag-and-drop** sur canvas (React Flow)
- **Claude IA natif** dans les actions (génération, classification, extraction)
- **RGPD-compliant** — hébergement France/Europe (Railway/Scaleway)
- **Connecteurs H'appi natifs** — Happi CRM, chatbots, ERP Scraper
- **Pricing PME** — €29–99/mois (vs €150–500/mois Azure)

### Positionnement concurrentiel
| Critère | Azure Logic Apps | Make | n8n self-hosted | **H'appi Automate** |
|---|---|---|---|---|
| Hébergement | Azure (US) | US | Ton serveur | France/Europe |
| RGPD | Partiel | ❌ | ✅ | ✅ |
| Claude IA natif | ❌ | ❌ | ❌ | ✅ |
| Connecteurs H'appi | ❌ | ❌ | ❌ | ✅ |
| Pricing PME FR | ❌ | Partiel | Infra seule | ✅ |
| Setup | Complexe | Moyen | Complexe | Simple |

### Cibles clients
- PME françaises 10–200 salariés
- Clients Happi CRM (upsell naturel)
- Clients chatbots H'appi (automatisation post-conversation)
- DSI / Ops managers sans expertise Azure

---

## STACK TECHNIQUE

```
Frontend  → Next.js 14 (App Router) + TypeScript + Tailwind CSS
Canvas    → React Flow (MIT license) — drag-and-drop workflow builder
Backend   → FastAPI 0.135+ + PostgreSQL 16 + SQLAlchemy 2 + Alembic
Queue     → Redis 7 + Celery (workers Python asynchrones)
IA        → Claude Sonnet 4.6 (Anthropic SDK Python) — défaut
Auth      → JWT (access + refresh token, jti UUID)
Email     → Resend
Deploy    → Docker + docker-compose · Railway (backend+workers) · Vercel (frontend)
Port dev  → Backend : 8001 (jamais 8000 — bloqué WSL2)
Repo      → github.com/nbayonne76-ui/happi-automate (à créer)
```

### Dépendances Python backend
```bash
pip install fastapi>=0.135 uvicorn>=0.43 pydantic>=2.12 \
  sqlalchemy>=2.0 alembic>=1.18 psycopg2-binary>=2.9 \
  python-dotenv>=1.2 anthropic>=0.40 httpx>=0.28 \
  celery>=5.4 redis>=5.0 python-jose>=3.3 bcrypt>=5.0 \
  python-multipart>=0.0.24
```

### Dépendances npm frontend
```bash
npm install reactflow @xyflow/react zustand \
  @anthropic-ai/sdk next-auth \
  @radix-ui/react-dialog @radix-ui/react-select \
  lucide-react class-variance-authority clsx
```

---

## ARCHITECTURE FONCTIONNELLE

```
┌─────────────────────────────────────────────────────────────────┐
│                       H'APPI AUTOMATE                           │
├─────────────────┬───────────────────────┬───────────────────────┤
│    TRIGGERS     │    WORKFLOW ENGINE     │       ACTIONS         │
│   (1 par wf)   │                       │    (N nodes)          │
│                 │  Canvas React Flow     │                       │
│ • Webhook       │  ┌─────────────────┐  │ ── IA ──             │
│ • Cron/planif  │  │ [Trigger Node]  │  │ • claude_generate     │
│ • Form submit   │  │      ↓         │  │ • claude_classify     │
│ • Chatbot event │  │ [Action Node]  │  │ • claude_extract      │
│ • CRM event     │  │      ↓         │  │                       │
│ • Email reçu    │  │ [Cond. Node]  │  │ ── Communication ──   │
│ • Webhook ext.  │  │   ↙    ↘      │  │ • send_email (Resend) │
│                 │  │[Node] [Node]  │  │ • send_sms (Twilio)   │
│                 │  └─────────────────┘  │ • send_slack          │
│                 │                       │                       │
│                 │  Stockage JSON (PG)   │ ── H'appi natif ──   │
│                 │  + Redis Queue        │ • crm_create_contact  │
│                 │  + Celery Workers     │ • crm_update_deal     │
│                 │  + Retry + DLQ        │ • crm_create_ticket   │
│                 │                       │ • chatbot_send_msg    │
│                 │                       │                       │
│                 │                       │ ── HTTP/Data ──      │
│                 │                       │ • http_request        │
│                 │                       │ • condition (if/else) │
│                 │                       │ • loop (iterate list) │
│                 │                       │ • wait (délai/event)  │
│                 │                       │ • transform (JSON map)│
└─────────────────┴───────────────────────┴───────────────────────┘
         ↓                                          ↓
  PostgreSQL                               PostgreSQL
  (workflow defs)                          (run logs + step logs)
```

---

## MODÈLE DE DONNÉES COMPLET

### Table `workspaces` (multi-tenant)
```sql
CREATE TABLE workspaces (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name        VARCHAR(255) NOT NULL,
  slug        VARCHAR(100) UNIQUE NOT NULL,
  plan        VARCHAR(50) DEFAULT 'starter',  -- starter | pro | enterprise
  created_at  TIMESTAMPTZ DEFAULT NOW()
);
```

### Table `users`
```sql
CREATE TABLE users (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  workspace_id  UUID REFERENCES workspaces(id),
  email         VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role          VARCHAR(50) DEFAULT 'member',  -- admin | member | viewer
  created_at    TIMESTAMPTZ DEFAULT NOW()
);
```

### Table `workflows` (définition du template)
```sql
CREATE TABLE workflows (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  workspace_id   UUID REFERENCES workspaces(id),
  name           VARCHAR(255) NOT NULL,
  description    TEXT,
  trigger_type   VARCHAR(100) NOT NULL,  -- webhook | schedule | crm_event | ...
  trigger_config JSONB NOT NULL DEFAULT '{}',
  -- trigger_config exemple webhook : {"path": "/wh/abc123", "method": "POST"}
  -- trigger_config exemple schedule : {"cron": "0 9 * * 1", "timezone": "Europe/Paris"}
  definition     JSONB NOT NULL DEFAULT '{"nodes": [], "edges": []}',
  -- definition : graph React Flow sérialisé (nodes + edges + viewport)
  is_active      BOOLEAN DEFAULT false,
  version        INTEGER DEFAULT 1,
  last_run_at    TIMESTAMPTZ,
  run_count      INTEGER DEFAULT 0,
  is_deleted     BOOLEAN DEFAULT false,  -- soft delete (règle H'appi)
  created_by     UUID REFERENCES users(id),
  created_at     TIMESTAMPTZ DEFAULT NOW(),
  updated_at     TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_workflows_workspace ON workflows(workspace_id) WHERE NOT is_deleted;
CREATE INDEX idx_workflows_active ON workflows(is_active, workspace_id) WHERE NOT is_deleted;
```

### Table `workflow_runs` (instance d'exécution)
```sql
CREATE TABLE workflow_runs (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  workflow_id     UUID REFERENCES workflows(id),
  workspace_id    UUID REFERENCES workspaces(id),
  trigger_data    JSONB DEFAULT '{}',  -- payload reçu au déclenchement
  status          VARCHAR(50) DEFAULT 'pending',
  -- statuts : pending | running | success | failed | cancelled | timeout
  error_message   TEXT,
  started_at      TIMESTAMPTZ,
  finished_at     TIMESTAMPTZ,
  duration_ms     INTEGER,
  celery_task_id  VARCHAR(255),  -- pour cancel/status via Celery
  created_at      TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_runs_workflow ON workflow_runs(workflow_id, created_at DESC);
CREATE INDEX idx_runs_status ON workflow_runs(status, workspace_id);
```

### Table `step_logs` (audit trail de chaque node)
```sql
CREATE TABLE step_logs (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  run_id       UUID REFERENCES workflow_runs(id) ON DELETE CASCADE,
  step_id      VARCHAR(255) NOT NULL,  -- id du node React Flow
  step_type    VARCHAR(100) NOT NULL,  -- claude_generate | send_email | ...
  step_name    VARCHAR(255),
  input_data   JSONB DEFAULT '{}',
  output_data  JSONB DEFAULT '{}',
  status       VARCHAR(50) NOT NULL,  -- running | success | failed | skipped
  error_message TEXT,
  retry_count  INTEGER DEFAULT 0,
  duration_ms  INTEGER,
  executed_at  TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_step_logs_run ON step_logs(run_id, executed_at);
```

### Table `connectors` (credentials chiffrés par workspace)
```sql
CREATE TABLE connectors (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  workspace_id  UUID REFERENCES workspaces(id),
  type          VARCHAR(100) NOT NULL,
  -- types : claude | slack | resend | twilio | happi_crm | hubspot | pipedrive | sap | http_generic
  name          VARCHAR(255) NOT NULL,  -- libellé UI ex: "Slack Marketing"
  credentials   JSONB NOT NULL DEFAULT '{}',
  -- credentials chiffrés AES-256 côté app avant stockage
  -- exemple slack : {"webhook_url": "enc:...", "channel": "#alerts"}
  -- exemple claude : {"api_key": "enc:sk-ant-..."}
  is_active     BOOLEAN DEFAULT true,
  created_at    TIMESTAMPTZ DEFAULT NOW()
);
```

### Table `webhook_endpoints` (URLs publiques générées)
```sql
CREATE TABLE webhook_endpoints (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  workflow_id  UUID REFERENCES workflows(id),
  secret_token VARCHAR(255) UNIQUE NOT NULL,  -- dans l'URL : /api/wh/{secret_token}
  is_active    BOOLEAN DEFAULT true,
  created_at   TIMESTAMPTZ DEFAULT NOW()
);
```

---

## STRUCTURE DU PROJET

```
happi-automate/
├── backend/
│   ├── app/
│   │   ├── main.py                    # FastAPI app + CORS + routers
│   │   ├── database.py                # SQLAlchemy engine + Session
│   │   ├── models/
│   │   │   ├── workspace.py
│   │   │   ├── user.py
│   │   │   ├── workflow.py
│   │   │   ├── workflow_run.py
│   │   │   ├── step_log.py
│   │   │   └── connector.py
│   │   ├── schemas/
│   │   │   ├── workflow.py            # Pydantic schemas in/out
│   │   │   └── workflow_run.py
│   │   ├── routers/
│   │   │   ├── auth.py                # /api/auth — login, refresh, me
│   │   │   ├── workflows.py           # /api/workflows — CRUD + activate
│   │   │   ├── runs.py                # /api/runs — list, detail, cancel
│   │   │   ├── connectors.py          # /api/connectors — CRUD
│   │   │   └── webhooks.py            # /api/wh/{token} — endpoint public trigger
│   │   ├── workers/
│   │   │   ├── celery_app.py          # Celery config + Redis broker
│   │   │   ├── workflow_runner.py     # Task principale run_workflow()
│   │   │   └── nodes/
│   │   │       ├── base.py            # Classe abstraite BaseNode.execute()
│   │   │       ├── claude_generate.py
│   │   │       ├── claude_classify.py
│   │   │       ├── claude_extract.py
│   │   │       ├── send_email.py      # Resend
│   │   │       ├── send_sms.py        # Twilio
│   │   │       ├── send_slack.py
│   │   │       ├── http_request.py
│   │   │       ├── crm_action.py      # Happi CRM API
│   │   │       ├── condition.py       # if/else + JSONPath eval
│   │   │       ├── loop_node.py
│   │   │       └── wait_node.py
│   │   └── utils/
│   │       ├── auth.py                # JWT create/verify
│   │       ├── crypto.py              # AES-256 encrypt/decrypt credentials
│   │       ├── jsonpath.py            # evaluate JSONPath expressions
│   │       └── graph.py               # topological sort des nodes
│   ├── alembic/                        # migrations DB
│   ├── venv/
│   ├── .env
│   └── requirements.txt
│
├── frontend/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx                   # Dashboard liste workflows
│   │   ├── workflows/
│   │   │   ├── page.tsx               # Liste avec stats
│   │   │   ├── new/page.tsx           # Création
│   │   │   └── [id]/
│   │   │       ├── page.tsx           # Canvas éditeur
│   │   │       └── runs/page.tsx      # Historique exécutions
│   │   ├── connectors/page.tsx        # Gestion connecteurs
│   │   └── api/                       # API routes Next.js (proxy vers backend)
│   ├── components/
│   │   ├── canvas/
│   │   │   ├── WorkflowCanvas.tsx     # React Flow principal
│   │   │   ├── nodes/
│   │   │   │   ├── TriggerNode.tsx
│   │   │   │   ├── ActionNode.tsx
│   │   │   │   └── ConditionNode.tsx
│   │   │   ├── NodePanel.tsx          # Sidebar liste des nodes à drag
│   │   │   └── NodeConfig.tsx         # Panel config du node sélectionné
│   │   ├── runs/
│   │   │   ├── RunsList.tsx
│   │   │   └── RunDetail.tsx          # Timeline steps + logs
│   │   └── ui/                        # shadcn/ui components
│   ├── lib/
│   │   ├── api.ts                     # fetch wrapper vers backend
│   │   └── store.ts                   # Zustand (canvas state)
│   └── package.json
│
├── docker-compose.yml
└── .env.example
```

---

## ROADMAP MVP — 4 SPRINTS DÉTAILLÉS

---

### SPRINT 1 — Fondations + Canvas basique
**Durée estimée : 5–7 jours**
**Objectif : CRUD workflows + canvas React Flow fonctionnel avec trigger et 2 actions**

#### Backend S1
- [ ] Init projet FastAPI + structure dossiers
- [ ] PostgreSQL + SQLAlchemy models (workspace, user, workflow)
- [ ] Alembic — migration initiale
- [ ] Auth JWT : POST /api/auth/login, POST /api/auth/refresh, GET /api/auth/me
- [ ] CRUD workflows :
  - GET /api/workflows (liste avec pagination)
  - POST /api/workflows (création)
  - GET /api/workflows/{id} (détail)
  - PUT /api/workflows/{id} (mise à jour definition + trigger_config)
  - DELETE /api/workflows/{id} (soft delete)
  - POST /api/workflows/{id}/activate (is_active = true, génère webhook_endpoint)
- [ ] Health endpoint : GET /health → {"status": "ok"}
- [ ] CORS : localhost:3000

#### Frontend S1
- [ ] Init Next.js 14 + TypeScript + Tailwind
- [ ] Layout principal (sidebar nav + header)
- [ ] Page /workflows — liste cards avec name, status, last_run_at
- [ ] Page /workflows/new — formulaire nom + type de trigger
- [ ] Page /workflows/[id] — Canvas React Flow :
  - Zone canvas centrale (React Flow provider)
  - Sidebar gauche — palette de nodes à drag
  - Node TriggerNode (unique, vert, non-supprimable)
  - Node ActionNode (gris-bleu, configurable)
  - Connexions (edges) entre nodes
  - Bouton "Sauvegarder" → PUT /api/workflows/{id}
  - Bouton "Activer / Désactiver" → POST /api/workflows/{id}/activate
- [ ] NodeConfig panel (sidebar droite) :
  - Apparaît au clic sur un node
  - Formulaire dynamique selon le type de node
  - Champ "Nom du step" (label affiché sur le canvas)

#### Définition JSON d'un workflow (format React Flow étendu)
```json
{
  "nodes": [
    {
      "id": "trigger-1",
      "type": "trigger",
      "position": {"x": 100, "y": 100},
      "data": {
        "type": "webhook",
        "label": "Webhook entrant",
        "config": {"method": "POST"}
      }
    },
    {
      "id": "action-1",
      "type": "action",
      "position": {"x": 100, "y": 250},
      "data": {
        "type": "http_request",
        "label": "Appel API externe",
        "config": {
          "url": "https://api.example.com/endpoint",
          "method": "POST",
          "headers": {"Content-Type": "application/json"},
          "body": "{{trigger.body}}"
        }
      }
    }
  ],
  "edges": [
    {"id": "e1", "source": "trigger-1", "target": "action-1"}
  ],
  "viewport": {"x": 0, "y": 0, "zoom": 1}
}
```

#### Livrables S1
- Canvas fonctionnel — drag nodes, créer connexions, sauvegarder
- Workflow persiste en PostgreSQL (definition JSONB)
- Auth JWT opérationnelle
- Environnement Docker (postgres + redis + backend + frontend)

---

### SPRINT 2 — Moteur d'exécution + Logs
**Durée estimée : 5–7 jours**
**Objectif : Les workflows s'exécutent réellement via Celery + logs d'exécution consultables**

#### Backend S2
- [ ] Redis + Celery config (celery_app.py)
- [ ] Models workflow_runs + step_logs + migrations Alembic
- [ ] Webhook trigger endpoint :
  - POST /api/wh/{secret_token} — endpoint public (pas d'auth JWT)
  - Récupère le workflow via webhook_endpoints
  - Crée une workflow_run (status: pending)
  - Lance celery task run_workflow.delay(run_id)
  - Répond 202 Accepted immédiatement
- [ ] Task Celery run_workflow() :
  - Charge le workflow depuis DB
  - Tri topologique des nodes (graph.py)
  - Boucle sur les nodes en ordre
  - Pour chaque node : instancie le bon handler, execute(), log le résultat
  - Gestion erreurs : retry x3 (délai 60s), puis status failed
  - Met à jour workflow_run.status à la fin
- [ ] Nodes S2 implémentés :
  - http_request.py — GET/POST/PUT/DELETE vers URL externe (httpx async)
  - condition.py — évalue expression JSONPath sur contexte, branche sur true/false edge
- [ ] Runs API :
  - GET /api/workflows/{id}/runs — historique (pagination 20/page)
  - GET /api/runs/{run_id} — détail run + step_logs
  - POST /api/runs/{run_id}/cancel — révocation Celery task
- [ ] Système de contexte inter-nodes :
  ```python
  context = {
    "trigger": {...},   # payload du trigger
    "steps": {
      "action-1": {"output": {...}},  # sortie de chaque step précédent
    }
  }
  # Template rendering : "{{steps.action-1.output.id}}" → valeur réelle
  ```
- [ ] Template renderer (utils/template.py) :
  - Syntaxe `{{trigger.body.email}}` → JSONPath résolu depuis context
  - Utilisé dans tous les champs "dynamiques" des configs de nodes

#### Frontend S2
- [ ] Page /workflows/[id]/runs :
  - Liste des exécutions (status badge coloré, durée, date)
  - Filtres : statut, date
- [ ] Composant RunDetail :
  - Timeline verticale des steps exécutés
  - Pour chaque step : nom, statut, durée, input JSON, output JSON (accordéon)
  - Affichage erreur si failed
- [ ] Indicateur "En cours" (polling GET /runs/{id} toutes les 2s si status running)
- [ ] Bouton "Tester maintenant" → POST /api/workflows/{id}/test-run (modal avec payload JSON)
- [ ] Copier l'URL webhook dans le clipboard (bouton)

#### Livrables S2
- Webhook reçu → workflow s'exécute → logs consultables
- Condition node (branchement if/else)
- HTTP request node (appel API externe)
- Historique d'exécutions avec détail step par step

---

### SPRINT 3 — Nodes IA + Communication + Connecteurs
**Durée estimée : 5–7 jours**
**Objectif : Nodes Claude, Email, Slack, SMS + gestion des connecteurs (credentials)**

#### Backend S3

##### Nodes Claude (IA)
- [ ] claude_generate.py :
  ```python
  async def execute(self, input_data, context, config, connector):
    client = anthropic.Anthropic(api_key=connector.credentials["api_key"])
    prompt = render_template(config["prompt"], context)
    message = await client.messages.create(
      model=config.get("model", "claude-sonnet-4-6"),
      max_tokens=config.get("max_tokens", 1024),
      messages=[{"role": "user", "content": prompt}]
    )
    return {"text": message.content[0].text, "tokens_used": message.usage.input_tokens}
  ```
- [ ] claude_classify.py :
  - Input : texte + liste de catégories
  - Prompt structuré → JSON {"category": "...", "confidence": 0.95}
  - Output utilisé par Condition node (branchement automatique)
- [ ] claude_extract.py :
  - Input : texte brut + schéma JSON des champs à extraire
  - Output : JSON structuré avec les valeurs extraites
  - Utile pour parser des emails, formulaires, webhooks non structurés

##### Nodes Communication
- [ ] send_email.py (Resend) :
  - Config : to, subject, html_body (template avec {{variables}})
  - Credentials connector : api_key Resend + from_email
- [ ] send_slack.py :
  - Config : message (template), channel (override optionnel)
  - Credentials connector : webhook_url Slack
- [ ] send_sms.py (Twilio) :
  - Config : to (numéro), body (template)
  - Credentials connector : account_sid, auth_token, from_number

##### Nodes H'appi natifs
- [ ] crm_action.py (Happi CRM) :
  - Sous-types : create_contact | update_contact | create_deal | create_ticket
  - Credentials connector : url Happi CRM + api_key
  - Construit le payload depuis context + config
- [ ] chatbot_send_msg.py :
  - Envoie un message dans une conversation chatbot existante
  - Credentials : url backend chatbot + token

##### API Connecteurs
- [ ] GET /api/connectors — liste par workspace
- [ ] POST /api/connectors — créer connecteur (encrypt credentials AES-256)
- [ ] PUT /api/connectors/{id} — modifier
- [ ] DELETE /api/connectors/{id} — supprimer
- [ ] POST /api/connectors/{id}/test — tester la connexion (ping)
- [ ] utils/crypto.py :
  ```python
  from cryptography.fernet import Fernet
  KEY = os.getenv("ENCRYPTION_KEY")  # Fernet.generate_key() en prod
  
  def encrypt(value: str) -> str:
      return Fernet(KEY).encrypt(value.encode()).decode()
  
  def decrypt(value: str) -> str:
      return Fernet(KEY).decrypt(value.encode()).decode()
  ```

#### Frontend S3
- [ ] Page /connectors :
  - Liste des connecteurs configurés (type + nom + statut)
  - Bouton "Ajouter un connecteur" → modal par type
  - Formulaire par type (Claude : API key, Slack : webhook URL, etc.)
  - Bouton "Tester" sur chaque connecteur
- [ ] NodeConfig étendu :
  - Pour les nodes Claude : sélecteur de connecteur (dropdown des connectors type=claude)
  - Pour send_email : sélecteur connecteur Resend + champs to/subject/body
  - Éditeur de template avec auto-complétion `{{trigger.` / `{{steps.`
- [ ] Node icons dans la palette (lucide-react) :
  - Trigger webhook : Zap ⚡
  - Claude : Brain 🧠
  - Email : Mail ✉️
  - Slack : MessageSquare 💬
  - HTTP : Globe 🌐
  - Condition : GitBranch 🌿
  - CRM : Users 👥

#### Livrables S3
- Claude génère/classifie/extrait dans les workflows
- Email, SMS, Slack envoyés depuis les workflows
- Connecteurs sécurisés (credentials chiffrés)
- Nodes Happi CRM natifs

---

### SPRINT 4 — Cron trigger + Monitoring + Dashboard
**Durée estimée : 5–7 jours**
**Objectif : Workflows planifiés (cron) + dashboard opérationnel + mise en prod**

#### Backend S4

##### Cron trigger
- [ ] APScheduler (AsyncIOScheduler) dans main.py :
  ```python
  from apscheduler.schedulers.asyncio import AsyncIOScheduler
  scheduler = AsyncIOScheduler(timezone="Europe/Paris")
  
  # Au démarrage : charger tous les workflows actifs avec trigger_type=schedule
  # Créer un job APScheduler par workflow
  # À l'activation/désactivation d'un workflow → add_job / remove_job
  ```
- [ ] Endpoint POST /api/workflows/{id}/activate met à jour le scheduler
- [ ] Endpoint POST /api/workflows/{id}/deactivate remove le job du scheduler
- [ ] Config cron UI → validation expression (ex: "0 9 * * 1" = lundi 9h)
- [ ] Support timezone (Europe/Paris par défaut)

##### Trigger manuel
- [ ] POST /api/workflows/{id}/trigger (avec payload JSON optionnel)
- [ ] Utile pour tests et intégrations custom

##### Nodes S4
- [ ] wait_node.py :
  - Mode "délai fixe" : attendre X secondes/minutes avant de passer au node suivant
  - Mode "attente externe" : pause l'exécution, reprend sur webhook entrant spécifique
- [ ] loop_node.py :
  - Input : array dans le contexte (ex: `{{trigger.items}}`)
  - Exécute les nodes fils pour chaque item
  - Injecte `{{loop.current}}` dans le sous-contexte
- [ ] transform_node.py :
  - Map/filter/reduce sur un array du contexte
  - Expressions Python-safe (eval limité via ast.literal_eval ou jinja2 sandbox)

##### Analytics + Monitoring
- [ ] GET /api/analytics/overview :
  ```json
  {
    "total_workflows": 12,
    "active_workflows": 8,
    "runs_today": 47,
    "runs_this_week": 312,
    "success_rate": 0.94,
    "avg_duration_ms": 1240
  }
  ```
- [ ] GET /api/analytics/workflows/{id}/stats :
  - runs par jour (7 derniers jours)
  - taux de succès
  - durée moyenne par step
- [ ] Alertes : si un workflow fail 3 fois → email notif au owner (Resend)

#### Frontend S4
- [ ] Dashboard (page principale) :
  - Métriques globales (cards : workflows actifs, runs aujourd'hui, taux succès)
  - Graphique runs/jour (7 jours) — Recharts ou Chart.js
  - Liste "Dernières exécutions" avec statut coloré
  - Alerte visuelle si workflow avec taux d'erreur > 20%
- [ ] Cron trigger config :
  - Sélecteur expression cron avec helper visuel ("chaque lundi à 9h")
  - Sélecteur timezone
  - Aperçu "Prochaines 5 exécutions"
- [ ] Page /workflows/[id] améliorée :
  - Tabs : Canvas | Runs | Stats
  - Minimap React Flow (aperçu du workflow)
  - Undo/Redo (Ctrl+Z / Ctrl+Y) via zustand history
  - Keyboard shortcuts : Suppr = supprimer node sélectionné
- [ ] Responsive minimal (tablet) — l'éditeur canvas reste desktop-first

#### Deploy S4
- [ ] docker-compose.yml production :
  ```yaml
  services:
    backend:
      build: ./backend
      environment:
        - DATABASE_URL
        - REDIS_URL
        - ENCRYPTION_KEY
        - JWT_SECRET
      ports:
        - "8001:8001"
    
    worker:
      build: ./backend
      command: celery -A app.workers.celery_app worker --loglevel=info -c 4
      depends_on: [backend, redis]
    
    frontend:
      build: ./frontend
      ports:
        - "3000:3000"
    
    redis:
      image: redis:7-alpine
    
    postgres:
      image: postgres:16-alpine
  ```
- [ ] Railway : deploy backend + worker (même image, command différente)
- [ ] Vercel : deploy frontend
- [ ] Variables d'environnement à configurer :
  ```
  DATABASE_URL          = postgresql://...
  REDIS_URL             = redis://...
  JWT_SECRET            = [random 64 chars]
  ENCRYPTION_KEY        = [Fernet.generate_key()]
  ANTHROPIC_API_KEY     = sk-ant-...
  RESEND_API_KEY        = re_...
  NEXT_PUBLIC_API_URL   = https://api.happi-automate.railway.app
  ```

#### Livrables S4
- Workflows planifiés (cron) opérationnels
- Loop et Wait nodes
- Dashboard monitoring
- Application déployée Railway + Vercel
- **MVP complet livrable à un premier client**

---

## CATALOGUE COMPLET DES NODES (v1.0)

### Triggers
| Type | Description | Config requise |
|---|---|---|
| `webhook` | Endpoint HTTP public déclenche le workflow | method (POST par défaut) |
| `schedule` | Expression cron planifie l'exécution | cron, timezone |
| `manual` | Déclenchement via API ou bouton UI | — |
| `crm_event` | Événement Happi CRM (contact créé, deal won...) | event_type, workspace_id CRM |
| `chatbot_event` | Événement chatbot (lead qualifié, ticket...) | event_type, chatbot_id |

### Actions IA
| Type | Description | Config |
|---|---|---|
| `claude_generate` | Génère texte via Claude | connector_id, model, prompt, max_tokens |
| `claude_classify` | Classifie input dans catégories | connector_id, input_template, categories[] |
| `claude_extract` | Extrait champs structurés depuis texte | connector_id, input_template, schema JSON |

### Actions Communication
| Type | Description | Config |
|---|---|---|
| `send_email` | Envoie email via Resend | connector_id, to, subject, html_body |
| `send_sms` | Envoie SMS via Twilio | connector_id, to, body |
| `send_slack` | Message Slack via webhook | connector_id, message, channel? |

### Actions H'appi natif
| Type | Description | Config |
|---|---|---|
| `crm_create_contact` | Crée contact Happi CRM | connector_id, first_name, last_name, email, phone |
| `crm_update_deal` | Met à jour un deal CRM | connector_id, deal_id, fields à mettre à jour |
| `crm_create_ticket` | Crée ticket SAV CRM | connector_id, title, description, priority |
| `chatbot_send_msg` | Envoie message dans conversation | connector_id, conversation_id, message |

### Actions HTTP/Data
| Type | Description | Config |
|---|---|---|
| `http_request` | Appel HTTP vers n'importe quelle API | url, method, headers, body, auth? |
| `condition` | Branchement if/else | expression JSONPath, valeur attendue, opérateur |
| `loop` | Itère sur un tableau | array_path (JSONPath), variable_name |
| `wait` | Délai ou attente événement | mode (delay\|event), duration_seconds ou event_token |
| `transform` | Transforme/filtre données JSON | operations (map\|filter\|pick\|merge) |

---

## SYSTÈME DE TEMPLATES (VARIABLES DYNAMIQUES)

Syntaxe : `{{source.path.to.value}}`

### Sources disponibles
```
{{trigger.body.email}}           → body du webhook entrant
{{trigger.body.items[0].name}}   → accès tableau
{{steps.action-1.output.text}}   → sortie d'un step précédent par id de node
{{steps.action-1.output.tokens}} → métadonnée de sortie
{{loop.current.id}}              → item courant dans un loop node
{{loop.index}}                   → index 0-based de l'itération
{{workflow.id}}                  → id du workflow
{{run.id}}                       → id de l'exécution courante
{{now}}                          → timestamp ISO actuel
```

### Implémentation
```python
# utils/template.py
import re
import json
from datetime import datetime, timezone

def render_template(template: str, context: dict) -> str:
    """Résout {{variable.path}} dans une chaîne de template."""
    def resolve(match):
        path = match.group(1).strip()
        parts = path.split(".")
        value = context
        for part in parts:
            if isinstance(value, dict):
                value = value.get(part)
            elif part.isdigit() and isinstance(value, list):
                value = value[int(part)]
            else:
                return match.group(0)  # non résolu → garde le template
        if value is None:
            return ""
        if isinstance(value, (dict, list)):
            return json.dumps(value, ensure_ascii=False)
        return str(value)
    
    return re.sub(r'\{\{([^}]+)\}\}', resolve, template)
```

---

## SÉCURITÉ

- **Credentials** : chiffrés AES-256 (Fernet) avant stockage PostgreSQL
- **Webhook endpoints** : token secret dans l'URL (UUID v4 aléatoire, non devinable)
- **JWT** : access token 15min + refresh token 7j avec jti UUID
- **Rate limiting** : 100 req/min par IP sur les webhooks publics (fastapi-limiter + Redis)
- **Isolation multi-tenant** : toutes les requêtes filtrées par workspace_id
- **Credentials non retournés** : l'API ne renvoie jamais les credentials déchiffrés
- **CORS** : uniquement l'URL frontend en production
- **Soft delete** : jamais de suppression physique des workflows/runs (audit trail)

---

## PRICING CIBLE

| Plan | Prix | Workflows actifs | Runs/mois | Nodes IA |
|---|---|---|---|---|
| **Starter** | €29/mois | 5 | 1 000 | 100 appels Claude |
| **Pro** | €79/mois | 25 | 10 000 | 1 000 appels Claude |
| **Enterprise** | €199/mois | Illimité | 100 000 | Illimité |

---

## LIENS AVEC L'ÉCOSYSTÈME H'APPI

```
Happi CRM ────────→ H'appi Automate ────────→ Happi Chatbot
   ↑                      ↑                        ↑
   └──── Trigger sur deal won / contact créé        │
                          │                         │
                     Claude IA native               │
                     Email / SMS / Slack            │
                          └─────────────────────────┘
                              Action : envoyer message
                                 dans conversation
```

**Upsell naturel** :
- Client Happi CRM → ajoute Automate pour automatiser ses relances, onboarding, alertes
- Client chatbot → ajoute Automate pour orchestrer les actions post-conversation (ticket, CRM, email)
- Client H'appi Automate seul → découvre et achète CRM + chatbot

---

## RÉFÉRENCES TECHNIQUES

### React Flow — docs
- Site : reactflow.dev
- npm : `@xyflow/react` (nouveau nom v12+) ou `reactflow` (v11)
- Exemples pertinents : Custom Nodes, Subflows, Layouting (dagre), Undo/Redo

### Celery — docs
- Docs : docs.celeryq.dev
- Pattern retry : `@celery_app.task(bind=True, max_retries=3, default_retry_delay=60)`
- Dead Letter Queue : broker_transport_options avec `dead_letter_exchange`

### Temporal.io — alternative à Celery (si workflows longs > 5 min)
- Si besoin de workflows durables (jours/semaines), remplacer Celery par Temporal.io
- SDK Python : `temporalio`
- Temporalio gère automatiquement : retry, timeout, reprise après crash serveur

---

*Créé : 2026-07-17 — Conception initiale H'appi Automate (comparable Azure Logic Apps)*
*Statut : Roadmap validée — MVP à construire sur autre machine*
