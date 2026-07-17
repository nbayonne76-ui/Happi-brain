---
name: happi-brain-core
description: Identité H'appi, stack technique de référence, environnement dev WSL2, deploy infra, règles qualité universelles FastAPI/Next.js
metadata:
  type: project
---

# HAPPI BRAIN — CORE (Identité · Stack · Dev · Deploy · Qualité)

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

## 2. ENVIRONNEMENT DE DÉVELOPPEMENT GLOBAL H'APPI

> Valable sur toute machine Ubuntu / WSL2 Ubuntu sur Windows. **Dernière mise en place complète : avril 2026**

### ÉTAPE 1 — Outils système

| Outil | Version ref. | Commande |
|-------|-------------|----------|
| Node.js | v24.x (NVM) | `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh \| bash` puis `nvm install --lts` |
| npm | 11.x | `npm install -g npm@latest` |
| Python | 3.12.x | `sudo apt install python3.12 python3.12-venv python3-pip` |
| PostgreSQL | 16.x | `sudo apt install postgresql postgresql-contrib` |
| Docker | 28.x | Docker Desktop WSL2 ou `sudo apt install docker.io` |
| Git | 2.43+ | `sudo apt install git` |

### ÉTAPE 2 — CLIs globaux npm

```bash
npm install -g eas-cli vercel railway @anthropic-ai/claude-code
```

**Versions de référence (avril 2026) :**
| CLI | Version |
|-----|---------|
| eas-cli | 18.5.0 |
| vercel | 50.39.0 |
| railway | 2.0.17 |
| @anthropic-ai/claude-code | 2.1.92 |

### ÉTAPE 3 — Python global

```bash
pip3 install ruff --break-system-packages
# ruff --version → ruff 0.15.x
# Binaire : /home/[user]/.local/bin/ruff
```

### ÉTAPE 4 — Git global config

```bash
git config --global user.name "nbayonne76-ui"
git config --global user.email "nbayonne76@gmail.com"
git config --global core.excludesfile ~/.gitignore_global
# Gitignore global inclut : venv/, .venv/, node_modules/, .next/, .env, uploads/, .DS_Store...
```

### ÉTAPE 5 — VS Code Extensions essentielles

```bash
code --install-extension charliermarsh.ruff          # Python formatter
code --install-extension ms-python.python
code --install-extension bradlc.vscode-tailwindcss
code --install-extension mtxr.sqltools-driver-pg
code --install-extension dotenv.dotenv-vscode
code --install-extension anthropic.claude-code
```

### ÉTAPE 6 — .vscode/ à créer dans chaque projet

```
[projet]/
  .vscode/
    settings.json    → format on save, ESLint, ruff, Python venv, SQLTools, path aliases
    launch.json      → debug FastAPI port 8001 + debug frontend (Next.js ou Expo)
    extensions.json  → recommandations équipe
```

**Template settings.json Python :**
```json
"[python]": {
  "editor.defaultFormatter": "charliermarsh.ruff",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.ruff": "explicit",
    "source.organizeImports.ruff": "explicit"
  }
},
"ruff.path": ["/home/[user]/.local/bin/ruff"],
"python.defaultInterpreterPath": "${workspaceFolder}/backend/venv/bin/python"
```

### ÉTAPE 7 — Règles universelles WSL2

- **Port FastAPI : toujours `8001`** — le 8000 est souvent bloqué sur WSL2
- **Python venv** : toujours dans `backend/venv/`, créé avec `python3 -m venv venv`
- **Variables d'env** : toujours via `.env` + `python-dotenv` (jamais hardcodé)
- **DB locale** : `postgresql://postgres:postgres@localhost/[projet]_db`
- **Démarrage backend** : `uvicorn app.main:app --host 0.0.0.0 --port 8001 --reload`

### ÉTAPE 8 — Packages Python backend (versions minimales)

```bash
pip install fastapi>=0.135 uvicorn>=0.43 pydantic>=2.12 \
  sqlalchemy>=2.0 alembic>=1.18 psycopg2-binary>=2.9 \
  python-dotenv>=1.2 python-multipart>=0.0.24 bcrypt>=5.0 \
  httpx>=0.28 python-jose>=3.3
```

---

## 3. STACK TECHNIQUE DE RÉFÉRENCE H'APPI

### Stack chatbot standard
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

### Stack démo/showcase clients
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

## 4. DEPLOY & INFRA

### Railway (backend + DB)
- Idéal pour FastAPI + PostgreSQL
- Fichiers : `railway.json`, `nixpacks.toml`, `Procfile`
- Variables d'environnement via Railway Dashboard

### Vercel (frontend + démos)
- Next.js et HTML statiques → déploiement automatique depuis GitHub
- Domaine : `happi-[client].vercel.app` pour les démos

### Docker (dev local + prod)
- `docker-compose.yml` avec services : backend, frontend, postgres, redis
- Port 8000 souvent bloqué sur WSL2 → utiliser **8001** par défaut
- Commande standard : `docker-compose up -d`

### Git remote WSL2 (workaround port 22 bloqué)
- SSH via port 443 : `ssh://ssh.github.com:443/nbayonne76-ui/[repo].git`
- Config `~/.ssh/config` : `Host ssh.github.com → Port 443 → IdentityFile ~/.ssh/id_ed25519`

---

## 5. RÈGLES QUALITÉ UNIVERSELLES H'APPI

> S'appliquent à TOUS les projets H'appi backend FastAPI.

### Backend FastAPI
1. **Soft delete** : jamais `DELETE` SQL sur entités métier. Toujours `is_deleted = True`.
2. **Route ordering** : toutes routes statiques (`/export`, `/bulk`, `/board`) AVANT `/{id}` paramétré.
3. **WebSocket** : `uvicorn[standard]` + `app.add_api_websocket_route()` directement sur `app`.
4. **JWT refresh** : toujours inclure `jti: uuid4()` pour garantir l'unicité en DB.
5. **CORS** : inclure `localhost:3000`, `localhost:8081`, `exp://`, `localhost:19006` selon le projet.
6. **Indexes DB** : FK columns (`owner_id`, `contact_id`, etc.) + `(is_deleted, status)` composite.
7. **Errors** : try/except autour de tout appel externe (Slack, webhooks, email, Redis).
8. **Port** : **8001** toujours (pas 8000, bloqué sur WSL2).
9. **Structured logging** : JSON en production, human-readable en dev (`python-json-logger`).
10. **Health endpoint** : `GET /health` → `{"status": "ok"}` obligatoire sur tout service.

### Tests pytest
1. **Session-scoped** fixtures pour DB setup/teardown.
2. **Désactiver rate limiter** : `limiter._enabled = False` sur chaque instance.
3. **FK teardown order** : supprimer dans l'ordre inverse des contraintes FK.
4. **Test DB isolée** : `postgresql://postgres:postgres@localhost/test_[projet]`

### Frontend Next.js
1. **Streaming AI** : utiliser `fetch` natif avec `ReadableStream`, pas axios.
2. **API URL** : toujours via variable d'env (`NEXT_PUBLIC_API_URL`), jamais hardcodé.
3. **Docker** : `output: "standalone"` dans `next.config.ts` pour le build Docker.
4. **Suspense** : toute page utilisant `useSearchParams()` doit être enveloppée dans `<Suspense>`.

---

*Mis à jour : 2026-05-31 — extrait de happi_brain.md v22*
