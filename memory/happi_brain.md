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

## 2. ENVIRONNEMENT DE DÉVELOPPEMENT GLOBAL H'APPI

> Ces outils et versions sont la **référence pour TOUS les projets H'appi** (présents et futurs).
> Valable sur toute machine Ubuntu / WSL2 Ubuntu sur Windows.
> **Dernière mise en place complète : avril 2026**

---

### ÉTAPE 1 — Outils système à installer

| Outil | Version ref. | Commande d'installation |
|-------|-------------|------------------------|
| Node.js | v24.x (NVM) | `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh \| bash` puis `nvm install --lts` |
| npm | 11.x | `npm install -g npm@latest` |
| Python | 3.12.x | `sudo apt install python3.12 python3.12-venv python3-pip` |
| PostgreSQL | 16.x | `sudo apt install postgresql postgresql-contrib` |
| Docker | 28.x | Docker Desktop WSL2 ou `sudo apt install docker.io` |
| Git | 2.43+ | `sudo apt install git` |

---

### ÉTAPE 2 — CLIs globaux npm (obligatoires pour tous les projets)

```bash
npm install -g eas-cli        # Build + deploy apps Expo (Android/iOS)
npm install -g vercel         # Deploy tous les frontends Next.js
npm install -g railway        # Deploy tous les backends FastAPI + PostgreSQL
npm install -g @anthropic-ai/claude-code   # Claude Code CLI
```

**Versions de référence (avril 2026) :**
| CLI | Version |
|-----|---------|
| eas-cli | 18.5.0 |
| vercel | 50.39.0 |
| railway | 2.0.17 |
| @anthropic-ai/claude-code | 2.1.92 |

---

### ÉTAPE 3 — Outil Python global

```bash
# Ruff = linter + formatter Python ultra-rapide (remplace black + flake8)
pip3 install ruff --break-system-packages
# Vérifier : ruff --version  → ruff 0.15.x
# Binaire installé dans : /home/[user]/.local/bin/ruff
```

---

### ÉTAPE 4 — Git global config

```bash
# Identité
git config --global user.name "nbayonne76-ui"
git config --global user.email "nbayonne76@gmail.com"

# Gitignore global (s'applique à TOUS les projets sans les modifier)
cat > ~/.gitignore_global << 'EOF'
venv/
.venv/
__pycache__/
*.py[cod]
node_modules/
.next/
.expo/
.expo-shared/
dist/
build/
.env
.env.local
.env.*.local
.env.production
uploads/
media/
*.sqlite3
.DS_Store
Thumbs.db
*.swp
.ruff_cache/
.pytest_cache/
.mypy_cache/
docker-compose.override.yml
EOF

git config --global core.excludesfile ~/.gitignore_global
```

---

### ÉTAPE 5 — VS Code Extensions (installer dans cet ordre)

```bash
# Formatters & Linters
code --install-extension esbenp.prettier-vscode
code --install-extension dbaeumer.vscode-eslint
code --install-extension charliermarsh.ruff          # ← Python formatter/linter

# Python
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-python.debugpy
code --install-extension ms-python.vscode-python-envs

# React Native / Expo
code --install-extension msjsdiag.vscode-react-native
code --install-extension expo.vscode-expo-tools       # ← Expo SDK, EAS, app.json

# Frontend
code --install-extension bradlc.vscode-tailwindcss
code --install-extension dsznajder.es7-react-js-snippets
code --install-extension formulahendry.auto-rename-tag

# Base de données
code --install-extension mtxr.sqltools
code --install-extension mtxr.sqltools-driver-pg

# Productivité
code --install-extension dotenv.dotenv-vscode
code --install-extension christian-kohler.path-intellisense
code --install-extension christian-kohler.npm-intellisense
code --install-extension eamodio.gitlens
code --install-extension GitHub.vscode-pull-request-github

# Infrastructure
code --install-extension ms-azuretools.vscode-containers

# Claude
code --install-extension anthropic.claude-code
```

---

### ÉTAPE 6 — .vscode/ à créer dans chaque projet

Chaque projet doit avoir :
```
[projet]/
  .vscode/
    settings.json    → format on save, ESLint, ruff, Python venv, SQLTools, path aliases
    launch.json      → debug FastAPI port 8001 + debug frontend (Next.js ou Expo)
    extensions.json  → recommandations équipe
  [frontend]/
    .prettierrc      → single quotes, printWidth 100, trailingComma es5
    .eslintrc.json   → rules TypeScript + framework (expo / next)
```

**Template `settings.json` Python dans `.vscode/` :**
```json
"[python]": {
  "editor.defaultFormatter": "charliermarsh.ruff",
  "editor.formatOnSave": true,
  "editor.tabSize": 4,
  "editor.codeActionsOnSave": {
    "source.fixAll.ruff": "explicit",
    "source.organizeImports.ruff": "explicit"
  }
},
"ruff.path": ["/home/[user]/.local/bin/ruff"],
"python.defaultInterpreterPath": "${workspaceFolder}/backend/venv/bin/python",
"python.terminal.activateEnvironment": true
```

---

### ÉTAPE 7 — Règles universelles (valables sur toutes les machines)

- **Port FastAPI : toujours `8001`** — le 8000 est souvent bloqué par le système sur WSL2
- **Python venv** : toujours dans `backend/venv/`, créé avec `python3 -m venv venv`
- **Variables d'env** : toujours via `.env` + `python-dotenv` (jamais hardcodé)
- **DB locale** : `postgresql://postgres:postgres@localhost/[projet]_db`
- **Démarrage backend** : `uvicorn app.main:app --host 0.0.0.0 --port 8001 --reload`
- **URL mobile** : `EXPO_PUBLIC_API_URL=http://localhost:8001/api` dans `.env`

---

### ÉTAPE 8 — Packages Python backend par projet (versions minimales)

```bash
# Dans chaque backend/venv après création
pip install fastapi>=0.135 uvicorn>=0.43 pydantic>=2.12 \
  sqlalchemy>=2.0 alembic>=1.18 psycopg2-binary>=2.9 \
  python-dotenv>=1.2 python-multipart>=0.0.24 bcrypt>=5.0 \
  httpx>=0.28 python-jose>=3.3
```

---

### Commandes de vérification / maintenance

```bash
# Vérifier tous les CLIs globaux
eas --version && vercel --version && railway --version && ruff --version

# Santé projet mobile Expo
npx expo-doctor              # doit afficher 17/17 checks passed

# Vulnérabilités npm (à faire sur chaque projet)
npm audit                    # doit afficher 0 vulnerabilities
npm audit fix                # corriger (2 passes si nécessaire)

# Mise à jour packages Python backend
cd backend && source venv/bin/activate
pip install --upgrade fastapi pydantic uvicorn alembic \
  python-multipart bcrypt python-dotenv httpx starlette

# Mise à jour CLIs globaux
npm update -g @anthropic-ai/claude-code eas-cli vercel railway
```

---

## 4. STACK TECHNIQUE DE RÉFÉRENCE H'APPI

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

## 5. PROJETS CHATBOT — CATALOGUE COMPLET

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

## 6. PROJETS SHOWCASE CLIENTS (démos HTML statiques)

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

## 7. PLATEFORMES ET SAAS

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
- **Branch principale** : `workflow/admin`
- **Type** : App mobile de suivi qualité livraisons meubles (multi-rôle)
- **Stack complète** :
  ```
  Mobile   → React Native (Expo SDK 54) + TypeScript
  Backend  → FastAPI 0.135+ + PostgreSQL 16 + SQLAlchemy 2 + Alembic
  State    → Zustand + AsyncStorage (offline sync queue)
  Auth     → JWT (access + refresh token, auto-refresh, expo-secure-store)
  Photos   → expo-image-picker + expo-image-loader
  Notifs   → expo-notifications (+ stubs web)
  Sig      → react-native-signature-canvas + react-native-webview (peer dep obligatoire)
  Geo      → expo-location
  Storage  → expo-secure-store (natif) / localStorage (web)
  ```

#### Architecture mobile
```
mobile/
  src/
    navigation/
      AppNavigator.tsx      → React Navigation v6 (native-stack + bottom-tabs)
    screens/
      RoleSelectionScreen.tsx
      auth/
      supplier/             → Home, Deliveries, ProductPhotos, TruckLoading, Profile
      driver/               → Home, Deliveries, DeliveryDetail, Profile
      client/               → TrackingInput, DeliveryCard, Tracking, DeliveryDetail, Signature, OrderSummary
      admin/                → Dashboard, LiveTracking, Statistics, Profile + 3 placeholder mgmt
      showroom/             → Placeholder (coming soon)
    store/
      useStore.ts           → Zustand store (auth + deliveries + stats + offline + error)
    services/
      api.ts                → ApiService class (JWT, auto-refresh, getBaseUrl())
      notifications.ts      → expo-notifications wrapper
      offlineSync.ts        → sync queue avec AsyncStorage
      storage.ts            → expo-secure-store / localStorage abstraction
    types/
      index.ts              → types centralisés
    constants/
      delivery.ts           → STATUS_LABELS, STATUS_FLAT_COLORS (partagés entre rôles)
```

#### Architecture backend
```
backend/
  app/
    main.py                 → FastAPI + CORS + StaticFiles (/uploads) + /health
    core/
      config.py             → Settings (DB, JWT, CORS, uploads, FCM, Redis)
    api/
      routes.py             → router principal
      endpoints/            → endpoints par domaine
    models/
      models.py             → SQLAlchemy models
    schemas/                → Pydantic v2 schemas
    crud/                   → CRUD operations
    services/
      notifications.py      → FCM push notifications
    db/
      database.py           → engine + session
    middleware/
  alembic/                  → migrations DB
  venv/                     → Python 3.12 virtualenv
```

#### Config FastAPI clés
```python
# Ports : 8000 souvent bloqué sur WSL2 → toujours utiliser 8001
# CORS autorisés : localhost:5173, 3000, 8081, 19006, exp://
# Upload : 10MB max, formats jpg/png/webp/heic
# JWT : 24h expiry, HS256
# DB par défaut : postgresql://postgres:postgres@localhost/quality_tracking_db
```

#### Pattern ApiService (à réutiliser)
```typescript
// URL auto selon env : EXPO_PUBLIC_API_URL || localhost:8001/api (dev) || prod URL
const API_BASE_URL = process.env.EXPO_PUBLIC_API_URL
  || (__DEV__ ? 'http://localhost:8001/api' : 'https://api.example.com/api');

class ApiService {
  // getBaseUrl() → retire /api pour construire URL fichiers statiques
  // setTokens() / clearTokens() → gestion stockage sécurisé
  // request<T>() → helper avec auth header auto + refresh token
}
```

#### Pattern Zustand Store (à réutiliser)
```typescript
// État : user, isAuthenticated, isLoading, deliveries, stats, error, isOnline, pendingSyncItems
// Offline queue : addPendingSyncItem() + syncPendingItems() → AsyncStorage
// Auth : login(), logout(), loadUser()
// Données : fetchDeliveries(), fetchDelivery(), updateDeliveryStatus(), fetchStats()
```

#### Utilisateurs test (password: `Password123`)
| Rôle | Email |
|------|-------|
| Admin | admin@mobilierdefrance.com |
| Supplier | fournisseur@example.com |
| Driver | chauffeur@mobilierdefrance.com |
| Client | client@example.com |

#### Setup VS Code (`.vscode/` configuré)
- `settings.json` → format on save, ESLint, Python venv auto-detect, SQLTools connecté, path aliases `@/`
- `launch.json` → debug Expo Android/Web + FastAPI (port 8001) en F5
- `extensions.json` → recommandations équipe
- `mobile/.prettierrc` + `mobile/.eslintrc.json` → règles cohérentes

#### Commandes de démarrage
```bash
# Backend
cd backend && source venv/bin/activate
uvicorn app.main:app --host 0.0.0.0 --port 8001 --reload

# Mobile
cd mobile && npx expo start

# DB
psql -U postgres -d quality_tracking_db
```

#### Leçons apprises (projet Quality Tracking)
- `react-native-webview` est un peer dep **obligatoire** de `react-native-signature-canvas` — toujours l'installer ensemble
- `expo-barcode-scanner` non utilisé dans le code mais référencé dans `app.json` plugins → causa un crash expo-doctor, supprimer les deux (npm + app.json)
- Port 8000 bloqué sur WSL2 par un process système → **toujours démarrer FastAPI sur 8001**
- Les path aliases TypeScript (`@/`, `@screens/`, etc.) doivent être déclarés dans `tsconfig.json` ET dans `path-intellisense.mappings` VS Code pour que l'IntelliSense fonctionne
- `npm audit fix` peut nécessiter 2 passes pour tout résoudre (les fixes créent parfois de nouveaux conflits)
- Toujours créer un fichier `.env` avec `EXPO_PUBLIC_API_URL` pour éviter les URLs hardcodées
- Zustand avec AsyncStorage = pattern offline robuste pour apps de terrain (chauffeurs sans réseau)

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
- **Type** : Base de connaissance commerciale Microsoft — D365, Azure, M365
- **Stack** : Next.js 15 (App Router) + JavaScript + JSON statique
- **Deploy** : Vercel (auto-deploy sur push `main`)
- **Git remote** : `ssh://ssh.github.com:443/nbayonne76-ui/microsoft-sales-app.git` (port 443 WSL2 workaround)
- **Détails complets** : Section 20

---

## 8. SECTEURS CLIENTS COUVERTS

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

## 9. PATTERNS ARCHITECTURE (bonnes pratiques)

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

### Pattern 3 : App mobile multi-rôle (Expo + FastAPI)
```
mobile/src/
  navigation/AppNavigator.tsx  → React Navigation (native-stack + bottom-tabs par rôle)
  screens/[role]/              → dossier par rôle + index.ts barrel export
  store/useStore.ts            → Zustand (auth + data + offline queue)
  services/api.ts              → ApiService class (JWT auto-refresh, getBaseUrl())
  services/storage.ts          → expo-secure-store / localStorage abstraction
  services/offlineSync.ts      → AsyncStorage queue pour mode hors-ligne
  types/index.ts               → types centralisés
  constants/delivery.ts        → constantes partagées entre rôles

backend/app/
  main.py                      → FastAPI + CORS + /health + StaticFiles
  core/config.py               → Settings (env vars, JWT, CORS, uploads)
  api/endpoints/               → routes par domaine
  models/models.py             → SQLAlchemy 2
  schemas/                     → Pydantic v2
  crud/                        → opérations DB
  alembic/                     → migrations

# Règles critiques :
# → Port 8001 (WSL2) pas 8000
# → EXPO_PUBLIC_API_URL dans .env
# → expo-secure-store pour les tokens (jamais AsyncStorage pour auth)
# → react-native-webview obligatoire si signature canvas
# → index.ts barrel export dans chaque dossier screens/[role]/
```

### Pattern 4 : Secrétariat vocal
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

## 10. RÈGLES IA ET PROMPTS (ce qui fonctionne)

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

## 11. CHECKLISTS NOUVEAUX PROJETS

### 9.1 Checklist Chatbot

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

### 9.2 Checklist App Mobile Full-Stack (Expo + FastAPI)

Avant de commencer une app mobile multi-rôle :

**Setup projet**
- [ ] `npx create-expo-app mobile --template` (SDK 54+, TypeScript strict)
- [ ] Installer : `zustand`, `@react-navigation/native`, `@react-navigation/native-stack`, `@react-navigation/bottom-tabs`
- [ ] Installer : `expo-secure-store`, `@react-native-async-storage/async-storage`
- [ ] Installer : `expo-image-picker`, `expo-location`, `expo-notifications`
- [ ] Si signature : `react-native-signature-canvas` **+ `react-native-webview`** (obligatoire)
- [ ] Créer `.env` avec `EXPO_PUBLIC_API_URL=http://localhost:8001/api`
- [ ] Configurer `tsconfig.json` avec path aliases (`@/`, `@screens/`, `@store/`, etc.)

**Structure**
- [ ] `AppNavigator.tsx` avec navigation par rôle (native-stack racine + bottom-tabs par rôle)
- [ ] `useStore.ts` Zustand : auth + data + error + isOnline + pendingSyncItems
- [ ] `api.ts` ApiService avec JWT auto-refresh + `getBaseUrl()`
- [ ] `storage.ts` abstraction expo-secure-store / localStorage (compatibilité web)
- [ ] `constants/` pour les valeurs partagées entre rôles (statuts, couleurs, labels)
- [ ] `index.ts` barrel export dans chaque dossier `screens/[role]/`

**Backend FastAPI**
- [ ] Port **8001** (pas 8000 sur WSL2)
- [ ] `/health` endpoint obligatoire
- [ ] CORS : inclure `localhost:8081`, `localhost:19006`, `exp://`
- [ ] `Settings` class dans `core/config.py` avec tous les env vars
- [ ] JWT 24h + refresh token
- [ ] `StaticFiles` pour servir les uploads photos

**VS Code**
- [ ] Créer `.vscode/settings.json` (format on save, Python venv, SQLTools, path aliases)
- [ ] Créer `.vscode/launch.json` (debug Expo + FastAPI port 8001)
- [ ] Créer `mobile/.prettierrc` + `mobile/.eslintrc.json`

**Avant livraison**
- [ ] `npx expo-doctor` → 17/17 checks passés
- [ ] `npm audit` → 0 vulnerabilities
- [ ] Vérifier toutes les peer deps (notamment `react-native-webview`)
- [ ] Tester login/logout pour chaque rôle
- [ ] Vérifier mode hors-ligne (couper réseau, créer action, rétablir → sync)

---

## 12. DEPLOY & INFRA

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

## 13. ÉVOLUTION DU BRAIN

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

## 14. HAPPI CRM — RÉFÉRENCE COMPLÈTE (Sprints 1-15 + Phases 2-4)

> CRM full-stack interne H'appi. Référence technique maximale — 120+ endpoints, 15 modules, tous patterns validés en production Docker.

### Infos projet
- **Repo** : `github.com/nbayonne76-ui/Happi-CRM` (branch `main`)
- **Login** : `admin@happi-crm.com` / `Admin123!`
- **Backend** : `http://localhost:8001` — **Frontend** : `http://localhost:3000`
- **Dernière mise à jour** : mai 2026 (Phases 2-4 + Docker + Email tracking + HTML preview)

### Stack
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

### Architecture backend
```
backend/
  app/
    main.py              → FastAPI + CORS + lifespan (Redis cache + APScheduler)
    core/
      config.py          → Settings (DB, JWT, Redis, Anthropic, Resend, Google OAuth)
      security.py        → hash_password, create_access_token, create_refresh_token (+ jti)
      logging.py         → JSON en prod, human-readable en dev
    api/
      router.py          → api_router (tous modules sauf WebSocket)
      endpoints/         → auth, contacts, deals, companies, tickets, activities,
                           analytics, ai, forecast, products, quotes, emails,
                           notifications, integrations, webhooks, leads_import, ws
      deps.py            → get_current_user, require_admin
    models/models.py     → SQLAlchemy : User, Contact, Deal, Company, Ticket, Activity,
                           Pipeline, PipelineStage, Notification, RefreshToken,
                           AiChatSession, AiChatMessage, Tag, EmailTemplate...
    schemas/             → Pydantic v2 schemas par domaine
    services/
      email.py           → send_welcome_email(), send_sla_alert_email() via Resend
      scoring.py         → score_contact() IA + heuristique (0-100)
    tasks/
      scheduler.py       → APScheduler : sla_alerts (1h), stalled_deals (daily 9h), weekly_digest (lundi 8h)
      sla_alerts.py      → tickets P0-P3 expirés → Notification + email
      stalled_deals.py   → deals ouverts non bougés 14j → notif owner
      weekly_digest.py   → stats hebdo + résumé Claude → email admins/sales
    db/database.py       → engine, SessionLocal, Base
  alembic/               → migrations (dont phase3_chat_history, phase4_composite_indexes)
  seed.py                → crée admin + pipeline 7 stages + tags (à run une fois)
  requirements.txt       → uvicorn[standard] obligatoire (WebSocket)
  pytest.ini             → testpaths=tests, asyncio_mode=auto
  tests/
    conftest.py          → setup_db, admin_user, client, auth_headers, default_pipeline
    test_auth.py         → 13 tests
    test_contacts.py     → 14 tests
    test_deals.py        → 14 tests
```

### Modules et endpoints clés
| Module | Préfixe | Points clés |
|--------|---------|-------------|
| Auth | `/api/auth` | login, refresh (jti), logout, invite, register, /me |
| Contacts | `/api/contacts` | CRUD, bulk, export CSV, leads board, qualify→deal, lead-score |
| Deals | `/api/deals` | CRUD, move stage, mark won/lost, bulk, export CSV, stage history |
| Pipelines | `/api/pipelines` | CRUD pipelines + stages, reorder stages |
| Companies | `/api/companies` | CRUD + enrichissement |
| Tickets | `/api/tickets` | CRUD, assign, SLA P0-P3 |
| Activities | `/api/activities` | CRUD, timeline |
| Analytics | `/api/analytics` | overview, pipeline, revops, sources (Redis cache 5min, date range) |
| Forecast | `/api/forecast` | /summary, /reps, /quotas |
| AI | `/api/ai` | streaming chat SSE, sessions historique, scoring contact |
| Notifications | `/api/notifications` | LIST, /count, mark-read, read-all |
| **WebSocket** | `/ws/notifications` | Monté via `app.add_api_websocket_route()` (PAS via api_router) |
| Emails | `/api/emails` | templates (+ HTML preview côté frontend), sequences, send, enroll, dispatch, logs, **webhook Resend** (`/webhook/resend`) |
| Integrations | `/api/integrations` | Slack, Gmail, Cal.com, Zapier |
| Webhooks | `/api/webhooks` | outbound webhooks (fire_outbound) |
| Products | `/api/products` | CRUD catalogue |
| Quotes | `/api/deals/{id}/line-items` + `/quote/pdf` | devis PDF (fpdf2) |
| Leads Import | `/api/leads/import` | POST fichier .xlsx |

### Patterns critiques découverts (à réutiliser)

#### 1. Route ordering FastAPI (piège fréquent)
```python
# TOUJOURS enregistrer les routes statiques AVANT les routes paramétrées
# ✅ Correct :
@router.get("/deals/export")   # statique en premier
@router.get("/deals/bulk")     # statique en premier
@router.get("/deals/{deal_id}") # paramétré après

# ❌ Bug silencieux : "export" et "bulk" sont traités comme des deal_id
```

#### 2. WebSocket dans FastAPI
```python
# ❌ Ne PAS inclure le WS router dans api_router (ne fonctionne pas avec prefix /api)
# ✅ Monter directement sur l'app :
from app.api.endpoints.ws import notifications_ws
app.add_api_websocket_route("/ws/notifications", notifications_ws)

# ✅ uvicorn[standard] OBLIGATOIRE dans requirements.txt (websockets côté serveur)
# Sans ça : "No supported WebSocket library detected" → 404 sur tout WS

# ✅ Access token n'a PAS de champ "type" (seul refresh a type="refresh")
# Check correct :
if not payload or payload.get("type") == "refresh":
    await websocket.close(code=4001)
```

#### 3. JWT refresh token unicité
```python
# ❌ Problème : même user connecté 2x dans la même seconde → même token → UniqueViolation
# ✅ Fix : ajouter jti (JWT ID) unique dans chaque refresh token
def create_refresh_token(subject):
    return jwt.encode({
        "sub": str(subject), "exp": expire,
        "type": "refresh",
        "jti": str(uuid.uuid4())  # ← unicité garantie
    }, SECRET_KEY)
```

#### 4. Pytest avec slowapi rate limiter
```python
# Désactiver le limiter dans les tests (session-scoped) :
@pytest.fixture(scope="session", autouse=True)
def disable_rate_limit():
    from app.api.endpoints.auth import limiter as auth_limiter
    from app.api.endpoints.ai import limiter as ai_limiter
    auth_limiter._enabled = False
    ai_limiter._enabled = False
# ✅ NE PAS monkeypatcher _check_request_limit → cause AttributeError sur request.state.view_rate_limit
```

#### 5. Teardown fixtures pytest avec FK
```python
# Quand une fixture session-scoped crée des objets avec FK chaînées,
# toujours supprimer dans l'ordre inverse des FK :
# Activities → DealStageHistory → Deals → Stages → Pipeline
deal_ids = [row[0] for row in db.query(Deal.id).filter(...).all()]
db.query(Activity).filter(Activity.deal_id.in_(deal_ids)).delete(synchronize_session=False)
db.query(DealStageHistory).filter(DealStageHistory.deal_id.in_(deal_ids)).delete(synchronize_session=False)
db.query(Deal).filter(Deal.pipeline_id == pipeline.id).delete(synchronize_session=False)
```

#### 6. Email tracking via webhooks Resend (Svix)
```python
# POST /emails/webhook/resend — PUBLIC, pas d'auth, signature Svix optionnelle
# Resend utilise Svix pour la livraison de webhooks → headers: svix-id, svix-timestamp, svix-signature
# Vérification HMAC-SHA256 : f"{svix_id}.{svix_timestamp}.{body}"
# Events : email.delivered, email.opened, email.clicked, email.bounced, email.complained
# Matcher via EmailLog.resend_id (stocké au moment du send Resend)

# Règle de priorité des statuts (ne jamais dégrader) :
_PRECEDENCE = {"scheduled":0, "sent":1, "delivered":2, "opened":3, "clicked":4, "bounced":5, "failed":6}
# clicked > opened > delivered > sent (sauf bounced/failed qui s'appliquent toujours)

# EmailLog colonnes tracking : delivered_at, opened_at, clicked_at, bounced_at
# enum étendu avec : delivered, opened, clicked, bounced
# Enum PostgreSQL → ALTER TYPE ... ADD VALUE IF NOT EXISTS (pas de recréation)

# Config : RESEND_WEBHOOK_SECRET (optionnel — si absent, pas de vérification signature)
# À configurer dans Resend Dashboard : Webhooks → URL → cocher les 4 events
```

#### 7. HTML preview iframe dans modal Next.js
```tsx
// Substituer les variables avec valeurs exemples CÔTÉ CLIENT (pas d'appel API)
const SAMPLE_VARS = { first_name: "Marie", last_name: "Dupont", company: "Acme Corp", ... };
function renderPreview(html: string) {
  return html.replace(/\{\{(\w+)\}\}/g, (_, key) => SAMPLE_VARS[key] ?? `{{${key}}}`);
}
// Render dans iframe sandboxé (sandbox="allow-same-origin") via srcDoc
const previewHtml = `<!DOCTYPE html><html>...<body>${renderPreview(body_html)}</body></html>`;
<iframe srcDoc={previewHtml} sandbox="allow-same-origin" />
// ✅ Aucun appel backend — 100% client-side, instantané
// ✅ sandbox interdit JS dans l'iframe (sécurité XSS)
```

#### 8. Streaming SSE (AI chat)
```python
# Backend : StreamingResponse + async generator
async def stream_gen():
    async with client.messages.stream(...) as stream:
        async for text in stream.text_stream:
            yield f"data: {text}\n\n"
return StreamingResponse(stream_gen(), media_type="text/event-stream")

# Frontend : fetch + ReadableStream (pas axios — ne supporte pas le streaming)
const res = await fetch("/api/ai/chat", { method: "POST", body: ... })
const reader = res.body.getReader()
while (true) {
    const { done, value } = await reader.read()
    if (done) break
    // parse SSE token
}
```

### Docker setup validé
```bash
# Structure
docker-compose.yml      → postgres 16, redis 7, backend :8001, frontend :3000
backend/Dockerfile      → python:3.12-slim + alembic upgrade head au démarrage
frontend/Dockerfile     → node:20-alpine multi-stage + output: standalone
.env.example            → template variables
frontend/next.config.ts → output: "standalone" obligatoire pour Docker

# Démarrage complet
cp .env.example .env && nano .env  # remplir SECRET_KEY + API keys
docker compose up -d
docker compose exec backend python seed.py  # créer admin + pipeline + tags

# Credentials Docker
Email    : admin@happi-crm.com
Password : Admin123!
```

### Requirements.txt essentiels CRM
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
python-json-logger>=2.0
fpdf2>=2.7              ← pour les devis PDF
```

### Leçons apprises Happi CRM
- **WebSocket** : `uvicorn[standard]` manquant = 404 silencieux. Toujours l'inclure.
- **Route ordering** : FastAPI match dans l'ordre d'enregistrement. Static avant paramétré = règle absolue.
- **Soft delete** : `is_deleted=False` dans tous les WHERE. Ne jamais DELETE physiquement les entités métier.
- **Composite indexes** : `(is_deleted, status)`, `(is_deleted, owner_id)` sur toutes les tables avec beaucoup de filtres.
- **Redis cache** : toujours prévoir un fallback gracieux (`try/except` au démarrage si Redis absent).
- **APScheduler** : démarrer dans `lifespan()` de FastAPI, pas dans un event handler global.
- **fpdf2** vs `fpdf` : la lib s'appelle `fpdf2` sur PyPI mais s'importe `from fpdf import FPDF`.
- **fpdf2 + unicode** : Helvetica = Latin-1 uniquement. Les em-dashes `—` (U+2014) crashent avec `FPDFUnicodeEncodingException`. Utiliser `-` ou une police Unicode.
- **Alembic enum PostgreSQL** : pour ajouter des valeurs à un Enum existant → `op.execute("ALTER TYPE myenum ADD VALUE IF NOT EXISTS 'newval'")` dans la migration. Ne pas recréer l'enum.
- **Webhook public FastAPI** : endpoint sans `Depends(get_current_user)` pour les callbacks externes (Resend, Stripe, etc.). Toujours vérifier la signature côté serveur si possible.
- **Email tracking** : stocker le `resend_id` retourné par `resend.Emails.send()` pour matcher les webhooks entrants. Ne jamais dégrader un statut (clicked > opened > delivered).

---

## 15. RÈGLES QUALITÉ UNIVERSELLES H'APPI (audit guidelines)

> Ces règles s'appliquent à TOUS les projets H'appi backend FastAPI.

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
1. **Session-scoped** fixtures pour DB setup/teardown (pas function-scoped = trop lent).
2. **Désactiver rate limiter** : `limiter._enabled = False` sur chaque instance (pas de monkeypatch).
3. **FK teardown order** : supprimer dans l'ordre inverse des contraintes FK.
4. **Test DB isolée** : `postgresql://postgres:postgres@localhost/test_[projet]`

### Frontend Next.js
1. **Streaming AI** : utiliser `fetch` natif avec `ReadableStream`, pas axios.
2. **API URL** : toujours via variable d'env (`NEXT_PUBLIC_API_URL`), jamais hardcodé.
3. **Docker** : `output: "standalone"` dans `next.config.ts` pour le build Docker.
4. **Auth** : stocker les tokens en `httpOnly cookie` ou `localStorage` selon le contexte.

---

---

## 16. HAPPI CRM — GUIDE D'INTÉGRATION CLIENT

> Ce guide est la référence pour livrer Happi CRM à un nouveau client.
> Il couvre : l'offre commerciale, le déploiement technique, les intégrations MCP, et le plan d'onboarding.

---

### 16.1 CE QU'ON LIVRE AU CLIENT

Happi CRM est un CRM full-stack prêt à l'emploi, livré clé en main avec :

| Module | Ce que le client obtient |
|--------|--------------------------|
| Contacts | Gestion complète, import CSV/Excel, scoring IA, export |
| Deals | Pipeline Kanban visuel, historique de stages, prévision revenus |
| Companies | Fiche entreprise enrichie, lien contacts + deals |
| Tickets | Système P0-P3 avec alertes SLA automatiques |
| Activités | Timeline complète par contact/deal |
| AI Chat | Assistant IA Claude intégré dans le CRM |
| Analytics | Dashboard revenus, pipeline, performance équipe |
| Emails | Templates HTML, séquences automatisées, tracking ouverture/clic |
| Intégrations | Slack, Gmail, Cal.com, Zapier, Stripe, Amplitude, Jotform, Notion |
| Notifications | Temps réel via WebSocket |

**Ce qu'on ne livre PAS** : formation générique, slides, consultants. On livre le logiciel + l'onboarding technique. Le client gagne 50-70% vs Salesforce/HubSpot.

---

### 16.2 OFFRE COMMERCIALE

| Formule | Prix | Contenu |
|---------|------|---------|
| **Starter** | Devis personnalisé | Déploiement Docker + 1 mois support |
| **Pro** | 300-800€/mois | Starter + intégrations MCP + mises à jour |
| **Enterprise** | 800-2000€/mois | Pro + SLA + personnalisations + formation |

**Arguments de vente clés :**
- HubSpot Pro : 90€/user/mois + 15k€ d'implémentation → Happi CRM : fraction du coût
- 5 intégrations MCP incluses (Stripe, Amplitude, Jotform, Coupler.io, Notion)
- AI Chat Claude intégré — aucun CRM concurrent ne l'a nativement
- RGPD natif, hébergement France/Europe

---

### 16.3 PRÉREQUIS TECHNIQUES CLIENT

Avant de commencer le déploiement, vérifier avec le client :

**Minimum requis :**
- Serveur Linux (Ubuntu 22.04+) ou VPS (Hetzner, Scaleway, OVH)
- Docker + Docker Compose installés
- Nom de domaine (ex: crm.client.fr)
- Accès DNS pour pointer le domaine

**Recommandé :**
- 2 CPU / 4 GB RAM minimum (8 GB pour prod confortable)
- PostgreSQL 16 (inclus dans Docker)
- Certificat SSL (Let's Encrypt via Nginx/Traefik)

**Comptes API à créer par le client (selon les intégrations souhaitées) :**
- Stripe → `STRIPE_SECRET_KEY`
- Amplitude → `AMPLITUDE_API_KEY` + `AMPLITUDE_SECRET_KEY`
- Jotform → `JOTFORM_API_KEY`
- Notion → `NOTION_API_TOKEN` (via notion.so/my-integrations)
- Resend → `RESEND_API_KEY` (emails transactionnels)
- Coupler.io → OAuth via `claude mcp add coupler-io --transport http https://mcp.coupler.io/mcp`

---

### 16.4 DÉPLOIEMENT ÉTAPE PAR ÉTAPE

#### Étape 1 — Cloner et configurer

```bash
git clone https://github.com/nbayonne76-ui/Happi-CRM.git crm-client
cd crm-client
cp .env.example .env
nano .env
```

**Variables .env à remplir obligatoirement :**
```env
SECRET_KEY=<générer avec: openssl rand -hex 32>
POSTGRES_PASSWORD=<mot de passe fort>
FRONTEND_URL=https://crm.client.fr
BACKEND_URL=https://api.crm.client.fr
ANTHROPIC_API_KEY=<clé Anthropic du client ou H'appi>
RESEND_API_KEY=<clé Resend>
EMAIL_FROM=crm@client.fr
```

#### Étape 2 — Lancer Docker

```bash
docker compose up -d
# Vérifier que tout est vert :
docker compose ps
# Initialiser la base de données :
docker compose exec backend python seed.py
```

#### Étape 3 — Vérifier le déploiement

```bash
# Backend health
curl https://api.crm.client.fr/health
# → {"status": "ok"}

# Frontend
open https://crm.client.fr
# → Login page visible
```

#### Étape 4 — Créer le premier admin client

```bash
docker compose exec backend python -c "
from app.db.database import SessionLocal
from app.models.models import User
from app.core.security import hash_password
db = SessionLocal()
u = User(email='admin@client.fr', first_name='Admin', last_name='Client',
         hashed_password=hash_password('MotDePasseForce123!'), role='admin', is_active=True)
db.add(u); db.commit()
print('Admin créé')
"
```

---

### 16.5 CONFIGURATION DES INTÉGRATIONS MCP

Les MCP servers permettent à Claude de lire/écrire dans les outils tiers du client directement depuis le CRM AI Chat.

#### Setup sur la machine de développement H'appi

Fichier à configurer : `~/.claude/mcp.json`

```json
{
  "mcpServers": {
    "happi-stripe": {
      "command": "/path/to/venv/bin/python",
      "args": ["/home/v-nbayonne/happi-crm/mcp/stripe_server.py"],
      "env": { "STRIPE_SECRET_KEY": "sk_live_..." }
    },
    "happi-amplitude": {
      "command": "/path/to/venv/bin/python",
      "args": ["/home/v-nbayonne/happi-crm/mcp/amplitude_server.py"],
      "env": {
        "AMPLITUDE_API_KEY": "...",
        "AMPLITUDE_SECRET_KEY": "..."
      }
    },
    "happi-jotform": {
      "command": "/path/to/venv/bin/python",
      "args": ["/home/v-nbayonne/happi-crm/mcp/jotform_server.py"],
      "env": {
        "JOTFORM_API_KEY": "...",
        "CRM_API_URL": "https://api.crm.client.fr/api/v1",
        "CRM_API_TOKEN": "<JWT admin>"
      }
    },
    "happi-notion": {
      "command": "/path/to/venv/bin/python",
      "args": ["/home/v-nbayonne/happi-crm/mcp/notion_server.py"],
      "env": { "NOTION_API_TOKEN": "secret_..." }
    }
  }
}
```

**Coupler.io** (intégration officielle, pas de clé API) :
```bash
claude mcp add coupler-io --transport http https://mcp.coupler.io/mcp
```

**Installer les dépendances MCP :**
```bash
cd /home/v-nbayonne/happi-crm/backend
source venv/bin/activate
pip install fastmcp httpx
```

**Obtenir le CRM_API_TOKEN :**
```bash
curl -s -X POST https://api.crm.client.fr/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@client.fr","password":"MotDePasseForce123!"}' \
  | python3 -c "import sys,json; print(json.load(sys.stdin)['access_token'])"
```

---

### 16.6 PLAN D'ONBOARDING CLIENT — 6 PHASES

#### Phase 1 — Capture de leads automatique (Jotform) — Semaine 1
**Objectif** : Zéro saisie manuelle pour les leads entrants

1. Client fournit son form_id Jotform (visible dans l'URL de son formulaire)
2. Configurer `JOTFORM_API_KEY` dans mcp.json
3. Tester : *"Synchronise les soumissions Jotform du formulaire [form_id] des dernières 24h"*
4. Mettre en place une routine quotidienne via `/schedule` Claude Code

**Impact mesurable** : 0 lead perdu, temps de réponse < 1h vs parfois jamais

---

#### Phase 2 — Visibilité revenus Stripe — Semaine 1-2
**Objectif** : Voir le statut de paiement d'un client en 2 secondes

1. Client fournit sa `STRIPE_SECRET_KEY` (test d'abord, live ensuite)
2. Configurer dans mcp.json
3. Commandes clés à apprendre au client :
   - *"Revenus ce mois sur Stripe"* → `stripe_get_revenue_summary`
   - *"Factures impayées"* → `stripe_list_invoices(status="open")`
   - *"Statut client [email]"* → `stripe_list_customers(email=X)`

**Impact mesurable** : Fin des allers-retours Stripe / CRM

---

#### Phase 3 — Attribution marketing Coupler.io — Semaine 2-3
**Objectif** : Savoir quelles campagnes génèrent des deals fermés

1. Connecter Coupler.io avec `claude mcp add coupler-io --transport http https://mcp.coupler.io/mcp`
2. Client configure ses importers (Google Ads, Facebook Ads, HubSpot) dans Coupler.io
3. Commandes clés :
   - *"Performance Google Ads ce mois"* → `coupler_get_google_ads_summary`
   - *"Quelles pubs Facebook génèrent le plus de leads"* → `coupler_get_facebook_ads_summary`

**Impact mesurable** : Budget pub optimisé, ROI mesurable par campagne

---

#### Phase 4 — Détection churn Amplitude — Semaine 3-4
**Objectif** : Identifier les clients à risque avant qu'ils partent

1. Client fournit `AMPLITUDE_API_KEY` + `AMPLITUDE_SECRET_KEY`
2. Setup dans mcp.json
3. Routine hebdomadaire : *"Montre-moi les utilisateurs actifs cette semaine vs la semaine dernière"*
4. Créer une activité CRM de suivi pour chaque compte avec baisse > 30%

**Impact mesurable** : Taux de churn réduit, interventions proactives

---

#### Phase 5 — Base de connaissance Notion — En continu
**Objectif** : Chaque contact CRM a des notes et docs liés dans Notion

1. Client crée une intégration Notion sur notion.so/my-integrations
2. Fournit le `NOTION_API_TOKEN`
3. Workflow standard à adopter :
   - Après chaque appel client → *"Crée une page Notion 'Appel [Client] [Date]' avec : [notes]"*
   - Avant une relance → *"Recherche Notion pour [nom client]"*

**Impact mesurable** : Fin de la perte d'information, contexte complet à chaque interaction

---

#### Phase 6 — CRM AI Chat connecté aux outils — Semaine 4-5
**Objectif** : Toute l'équipe peut interroger les 5 outils depuis le CRM, sans Claude Code

Cette phase nécessite une mise à jour du backend :
- Modifier `/api/v1/ai/chat` pour accepter des `tools` (Anthropic tool_use)
- Mapper chaque outil MCP vers une fonction Python callable
- Retourner les résultats dans le flux SSE existant

**Commandes qui deviennent disponibles dans le CRM pour toute l'équipe :**
```
"Quel est notre MRR ce mois ?"
"Qui n'a pas payé depuis 30 jours ?"
"Quels leads Jotform attendent d'être contactés ?"
"Crée une page Notion pour le deal qu'on vient de signer"
```

**Impact mesurable** : Toute l'équipe a accès à l'intelligence, pas seulement le fondateur

---

### 16.7 CHECKLIST LIVRAISON CLIENT

**Avant de livrer :**
- [ ] Docker compose up -d → tous les services verts
- [ ] `GET /health` → `{"status": "ok"}`
- [ ] Login admin fonctionne
- [ ] Pipeline par défaut créé (seed.py exécuté)
- [ ] Premier contact de test créé + deal créé
- [ ] AI Chat répond (vérifier `ANTHROPIC_API_KEY`)
- [ ] Au moins 1 intégration MCP testée (Stripe ou Jotform)
- [ ] Email Resend fonctionne (test send depuis le CRM)
- [ ] SSL valide sur le domaine (pas d'avertissement navigateur)

**Livrables au client :**
- [ ] URL du CRM + credentials admin
- [ ] Guide des commandes Claude pour chaque intégration MCP activée
- [ ] Accès au repo GitHub (fork ou accès en lecture)
- [ ] Contact support H'appi (email + délai de réponse selon formule)

---

### 16.8 COMMANDES MCP RÉFÉRENCE (à remettre au client)

```
# Jotform
"Synchronise les nouvelles soumissions du formulaire [form_id]"
"Crée un contact CRM depuis la soumission Jotform [submission_id]"

# Stripe
"Revenus Stripe ce mois / cette semaine / cette année"
"Factures impayées ou en retard"
"Statut abonnement de [email client]"
"Crée un lien de paiement pour [price_id]"

# Amplitude
"Combien d'utilisateurs actifs cette semaine ?"
"Activité de l'utilisateur [amplitude_user_id]"
"Top événements des 7 derniers jours"

# Coupler.io
"Performance Google Ads ce mois"
"Quelles pubs Facebook génèrent des leads ?"
"Contacts HubSpot non encore dans le CRM"

# Notion
"Recherche Notion : [nom client ou sujet]"
"Crée une page Notion '[titre]' avec le contenu : [texte]"
"Ajoute une note à la page Notion [page_id]"
"Liste toutes les bases de données Notion disponibles"
```

---

## 17. HAPPI CRM — ARCHITECTURE D'AUTOMATISATION (Phases 1-7)

> **Vision fondamentale (2026-05-14)** : Les 7 phases ne sont pas des "intégrations" isolées.
> Elles constituent ensemble **l'architecture d'automatisation du CRM** — la fondation qui transforme
> un simple outil de gestion en une plateforme qui travaille seule.

### Architecture globale

```
ENTRÉES AUTOMATIQUES                    COUCHE INTELLIGENCE              SORTIE NATURELLE
─────────────────────                   ───────────────────              ────────────────
Jotform      → leads CRM (Phase 1)  ┐
Stripe       → paiements    (P2)    │
Coupler.io   → attribution  (P3)    ├──▶  contact_enrichments  ──▶  AI Chat tool_use
Amplitude    → comportement (P4)    │     (Phase 6 : backbone)       (Phase 7)
Notion       → connaissance (P5)    ┘
                                         Toutes les sources            "Qui n'a pas payé ?"
APScheduler → sync 1h/auto               unifiées par contact          "Quel est notre MRR ?"
                                         dans 1 table JSONB            "Cherche l'onboarding"
```

### Ce que ça change concrètement

**Avant** : le commercial ouvre 5 onglets (Stripe, Jotform, Notion, Amplitude, CRM) pour préparer un appel client.

**Après** : il tape dans le CRM AI Chat — *"Donne-moi le profil complet de client@example.com"* — et il obtient en 3 secondes : statut de paiement Stripe, dernière activité Amplitude, pages Notion liées, et l'historique CRM.

### Les 3 couches de l'architecture

| Couche | Rôle | Phases |
|--------|------|--------|
| **Collecte** | Faire entrer les données automatiquement | 1 (Jotform), 3 (Coupler), 4 (Amplitude tracker) |
| **Unification** | Centraliser par contact, synchroniser en continu | 6 (Enrichment backbone) |
| **Action** | Permettre à l'équipe d'interroger et d'agir en langage naturel | 7 (AI Chat tool_use) |

> Les phases 2 (Stripe) et 5 (Notion) alimentent à la fois la couche Collecte ET la couche Action directement.

### Pourquoi cette architecture est réplicable

Chaque nouveau client H'appi qui prend la formule **Pro ou Enterprise** reçoit cette architecture complète.
Il suffit de :
1. Copier `mcp/` + migration Alembic dans son instance
2. Brancher ses propres clés API (Stripe, Amplitude, Jotform, Notion)
3. Lancer `alembic upgrade head` + redémarrer le scheduler
4. Toute l'automatisation est active — sans code supplémentaire

**C'est l'argument commercial différenciant de Happi CRM vs Salesforce/HubSpot** :
les concurrents vendent des intégrations. Happi vend une architecture d'automatisation connectée à l'IA.

---

### Implémentation technique par phase

> Implémentées 2026-05-13/14. Chaque phase est indépendante et déployable séparément.

---

### Phase 1 — Jotform (capture de leads)

**Fichier** : `mcp/jotform_server.py` (FastMCP stdio)

**Outils exposés** :
- `jotform_list_submissions(form_id, limit)` → liste les soumissions d'un formulaire
- `jotform_get_submission(submission_id)` → détail d'une soumission
- `jotform_sync_to_crm(submission_id)` → parse les champs → POST `/api/contacts` (CRM REST)

**Env vars requises** : `JOTFORM_API_KEY`, `CRM_API_URL=http://localhost:8001/api`, `CRM_API_TOKEN`

**Enregistrement** : `~/.claude/mcp.json` → clé `happi-jotform`

**Détail champs Jotform** : les réponses sont dans `submission.answers`, clé = nom du champ Jotform. Extraction par recherche de patterns dans les clés (`email`, `first`, `phone`, `company`).

**Limite connue** : `CRM_API_TOKEN` JWT expire en 24h → doit être rafraîchi manuellement ou remplacé par un API key permanent.

---

### Phase 2 — Stripe (revenus)

**Fichier** : `mcp/stripe_server.py` (FastMCP stdio)

**Outils exposés** :
- `stripe_list_customers(email, limit)` → liste les clients Stripe
- `stripe_list_charges(days, limit)` → paiements sur N jours
- `stripe_list_subscriptions(status)` → abonnements (active, past_due, canceled)
- `stripe_list_invoices(status, limit)` → factures filtrées par statut
- `stripe_get_mrr()` → calcule le MRR depuis les abonnements actifs

**Env vars** : `STRIPE_SECRET_KEY` (sk_test_... ou sk_live_...)

**Auth Stripe** : Basic auth avec `(STRIPE_SECRET_KEY, "")` ou header `Authorization: Bearer KEY`

**sk_test vs sk_live** : `sk_test_` → mode sandbox (aucune transaction réelle). `sk_live_` → production (vrais paiements). On commence toujours par sk_test_ pour valider l'intégration, puis on bascule en sk_live_ en prod.

---

### Phase 3 — Coupler.io (attribution marketing)

**Différence des autres phases** : Coupler.io a un MCP natif HTTP/OAuth — pas de fichier Python custom.

**Installation** :
```bash
claude mcp add coupler-io --transport http https://mcp.coupler.io/mcp
# → enregistré dans ~/.claude.json (HTTP), PAS dans ~/.claude/mcp.json
```

**Authentification** : OAuth dans le navigateur au premier `claude mcp list` ou `claude`

**Usage** : Configurer un dataflow dans Coupler.io :
1. Source : Google Ads / Meta Ads / HubSpot (choisir le template)
2. Destination : Google Sheets (ou tout autre connecteur)
3. Planification : Import automatique toutes les X heures
4. Après import → interroger depuis Claude Code : *"Quelles pubs génèrent des leads ?"*

**Données disponibles** : performance pub (clics, impressions, CPC, conversions), pipeline HubSpot, contacts importés

---

### Phase 4 — Amplitude (comportement utilisateurs)

**Fichier MCP** : `mcp/amplitude_server.py` (FastMCP stdio)

**Outils exposés** :
- `amplitude_get_event_counts(event_type, days)` → nombre d'occurrences d'un événement
- `amplitude_search_user(user_id)` → propriétés d'un utilisateur Amplitude
- `amplitude_list_events(days)` → top événements sur N jours

**Auth Amplitude** : Basic auth `base64(API_KEY:SECRET_KEY)` → header `Authorization: Basic <encoded>`

**Env vars** : `AMPLITUDE_API_KEY`, `AMPLITUDE_SECRET_KEY`

**Instrumentation frontend** (`frontend/src/lib/amplitude.ts`) :
```typescript
initAmplitude()                           // appelé dans AuthGuard au chargement
identifyUser(userId, {email, role, name}) // après login réussi
track("contact_created", {source, status})
track("deal_created", {value, stage})
track("deal_won", {value, contact_email})
track("deal_lost", {value, stage})
resetUser()                               // à la déconnexion
```

**Env frontend** : `NEXT_PUBLIC_AMPLITUDE_API_KEY` dans `frontend/.env.local`

**Délai de données** : les événements Amplitude apparaissent après 5-10 min dans le dashboard et l'API. Les requêtes de segmentation échouent si aucun événement n'a encore été envoyé.

---

### Phase 5 — Notion (base de connaissances)

**Fichier** : `mcp/notion_server.py` (FastMCP stdio)

**Outils exposés** :
- `notion_search(query, page_size)` → recherche full-text dans les pages accessibles
- `notion_create_page(parent_id, title, content)` → crée une page markdown-like
- `notion_get_page(page_id)` → contenu d'une page (blocs récursifs)
- `notion_list_databases(page_size)` → liste les databases Notion accessibles

**Auth Notion** : Bearer token, header `Notion-Version: 2022-06-28`

**Env vars** : `NOTION_API_TOKEN` (format `ntn_...` depuis notion.so/my-integrations)

**Étape critique** : après avoir créé l'intégration sur notion.so/my-integrations, il faut **partager manuellement** chaque page Notion avec l'intégration via le menu "Connections" de la page. Sans ça, l'API retourne 0 résultats.

**Structure recommandée pour les clients** :
```
📁 Happi CRM Knowledge Base
  📄 Procédures internes
  📄 Fiches clients
  📄 Templates de relance
  📄 Documentation produit
```

---

### Phase 6 — Contact Enrichment Layer (backbone dataverse)

**Concept** : Table PostgreSQL JSONB qui centralise les données de toutes les sources externes par contact. Évite de rappeler les APIs à chaque question.

**Modèle** (`backend/app/models/models.py`) :
```python
class ContactEnrichment(Base):
    __tablename__ = "contact_enrichments"
    id         = Column(String, primary_key=True)
    contact_id = Column(String, ForeignKey("contacts.id", ondelete="CASCADE"), index=True)
    source     = Column(Enum("stripe","amplitude","notion","jotform","coupler"))
    data       = Column(JSON, default=dict)
    synced_at  = Column(DateTime(timezone=True))
```

**Migration** : `backend/alembic/versions/c8bc59113082_add_contact_enrichments.py`

**Service** (`backend/app/services/enrichment.py`) :
- `enrich_stripe(db, contact)` → cherche client Stripe par email, sauve charges + subscriptions
- `enrich_amplitude(db, contact)` → cherche user Amplitude par email
- `enrich_notion(db, contact)` → cherche pages Notion par nom de contact
- `enrich_contact(db, contact)` → lance les 3, retourne dict unifié
- `enrich_all_contacts(db)` → job schedulé, tourne sur tous les contacts non-supprimés avec email

**API endpoints** (`backend/app/api/endpoints/enrichments.py`) :
- `POST /api/contacts/{id}/enrich` → enrichissement on-demand
- `GET /api/contacts/{id}/enrichments` → lecture des données stockées

**Scheduler** (`backend/app/tasks/scheduler.py`) :
```python
scheduler.add_job(run_enrichment, IntervalTrigger(hours=1), id="contact_enrichment")
```

**Clé d'upsert** : `(contact_id, source)` — on ne crée pas de doublons, on met à jour.

---

## 18. HAPPI CRM — PHASE 7 : AI CHAT AVEC TOOL_USE (Anthropic)

> Implémenté le 2026-05-14 dans `/happi-crm/backend/app/api/endpoints/ai.py`
> Permet à toute l'équipe d'interroger Stripe, Amplitude, Notion et le CRM en langage naturel depuis l'onglet AI Chat.

### 18.1 Architecture tool_use

**Principe** : Au lieu de streamer directement, le chat fait d'abord un appel non-streaming avec des `tools`. Si Claude décide d'appeler un outil, le backend l'exécute et renvoie le résultat. Puis Claude génère la réponse finale, pseudo-streamée en SSE.

```
User message
    ↓
client.messages.create(tools=[...])   ← 1er appel (non-streaming)
    ↓
stop_reason == "tool_use" ?
    ├── OUI → exécuter l'outil Python → envoyer tool_result → 2ème appel
    └── NON → pseudo-stream la réponse finale (chunks 25 chars)
```

**Boucle max 3 itérations** pour éviter les chaînes infinies.

### 18.2 Les 6 outils définis

| Outil | API appelée | Question exemple |
|-------|-------------|------------------|
| `get_stripe_revenue` | Stripe `/charges` + `/subscriptions` | "Quel est notre MRR ce mois ?" |
| `list_stripe_unpaid_invoices` | Stripe `/invoices?status=open` | "Qui n'a pas payé ?" |
| `get_amplitude_events` | Amplitude `/api/2/events/segmentation` | "Combien de deals créés ce mois ?" |
| `search_notion_pages` | Notion `/v1/search` | "Cherche la procédure onboarding" |
| `get_contact_enrichment` | DB locale (`contact_enrichments`) | "Profil complet de client@example.com" |
| `get_crm_stats` | DB locale (contacts, deals, tickets) | "Rapport général du CRM" |

### 18.3 Fonctions clés à connaître

```python
# backend/app/api/endpoints/ai.py
_build_crm_tools()     → list[dict]  # schemas Anthropic des 6 outils
_block_to_dict(block)  → dict        # convertit SDK blocks → dicts pour messages
_execute_tool(name, input, db) → dict  # dispatch → Stripe/Amplitude/Notion/DB
```

### 18.4 Contact Enrichment Layer (Phase 6 = Backbone)

Table `contact_enrichments` (PostgreSQL JSONB) :
```
(contact_id, source) → data JSONB, synced_at
```
- Sources : `stripe`, `amplitude`, `notion`, `jotform`, `coupler`
- Job APScheduler toutes les 1h → `enrich_all_contacts(db)`
- Endpoint on-demand : `POST /api/contacts/{id}/enrich`
- Lecture : `GET /api/contacts/{id}/enrichments`

### 18.5 Instrumentation Amplitude (frontend)

```
frontend/src/lib/amplitude.ts
  initAmplitude()         → init au chargement (AuthGuard)
  identifyUser(id, props) → lie userId + email/role
  track(event, props)     → envoie un événement
  resetUser()             → à la déconnexion
```

**Événements trackés** : `contact_created`, `deal_created`, `deal_won`, `deal_lost`

### 18.6 MCP Servers (Claude Code uniquement)

Fichiers dans `/happi-crm/mcp/` — 5 serveurs FastMCP stdio :
- `stripe_server.py`, `amplitude_server.py`, `jotform_server.py`, `notion_server.py`, `coupler_server.py`
- Enregistrés dans `~/.claude/mcp.json` (global Claude Code)
- Coupler.io via HTTP OAuth natif (`claude mcp add --transport http`)
- **Note** : `CRM_API_TOKEN` dans mcp.json expire en 24h → prévoir un système d'API key permanent

### 18.7 Pattern de réplication pour nouveaux clients

1. Copier les 5 fichiers `mcp/*.py` + `requirements.txt`
2. Adapter les env vars dans `~/.claude/mcp.json` avec les clés du client
3. Exécuter la migration Alembic : `alembic upgrade head` (ajoute `contact_enrichments`)
4. Ajouter `NEXT_PUBLIC_AMPLITUDE_API_KEY` dans `frontend/.env.local`
5. Les 6 outils AI Chat sont automatiquement actifs (pas de config supplémentaire)

---

---

## 19. HAPPI CRM — SPRINTS 22-28 (mai 2026)

> Sprints livrés après la phase d'automatisation MCP. Tous déployés en Docker local.
> Repo pushé sur `main` le 2026-05-18. Prêt pour Railway + Vercel.

### État du projet après Sprint 28
- **28 sprints livrés** · 120+ endpoints · 16+ pages frontend
- **Login** : `admin@happi-crm.com` / `Admin123!`
- **Backend** : port 8001 (Docker) · **Frontend** : port 3000 (Docker)
- **Migrations Alembic** : chaîne complète jusqu'à `a1b2c3d4e5f6` (invoices)

---

### Sprint 22 — Workflow Automation Engine

**But** : Automatiser des actions CRM en réponse à des événements métier, sans code.

**Backend** : `backend/app/api/endpoints/workflows.py` (réécriture complète)

**4 triggers** :
- `deal_won` · `deal_stage_changed` · `contact_created` · `ticket_created`

**6 types d'actions** :
- `create_activity` · `slack_notif` · `send_email` · `send_sms` · `webhook_fire` · `update_field`

**Conditions** : `stage_id`, `min_deal_value`, `contact_source`

**Modèle** `WorkflowRunLog` (migration `d4f8a2c91e05`) :
```python
class WorkflowRunLog(Base):
    rule_id, trigger, context (JSON), actions_executed (JSON), status, ran_at
```

**Endpoints** :
- `GET/POST /workflows` · `PATCH /workflows/{id}` · `DELETE /workflows/{id}`
- `GET /workflows/{id}/logs` → 50 dernières exécutions

**Frontend** : `settings/page.tsx` → `WorkflowsSection` + `ActionEditor` + `WorkflowLogsModal`

---

### Sprint 23 — Custom Fields

**But** : Permettre à chaque client d'adapter le CRM à son métier.

**6 types de champs** : `text`, `number`, `boolean`, `date`, `select`, `multiselect`
**4 entités** : `contact`, `deal`, `company`, `ticket`

**Modèle** `CustomFieldDef` (migration `e3b1c7a82f40`) :
```python
class CustomFieldDef(Base):
    entity_type, name, label, field_type, options (JSON), is_required, is_active
```

**Colonne JSONB** ajoutée à 4 tables :
```python
custom_fields = Column(JSON, default=dict)  # sur Contact, Deal, Company, Ticket
```

**Endpoints** (`custom_fields.py`) :
- `GET /custom-fields/defs?entity_type=x` · `POST /custom-fields/defs` (admin)
- `PATCH /custom-fields/defs/{id}` · `DELETE /custom-fields/defs/{id}`
- `PATCH /custom-fields/{entity_type}/{entity_id}` → valide les clés + sauve en JSONB

**Frontend** : `CustomFieldsSection` dans settings · inputs contextuels dans ContactDrawer et DealDrawer

---

### Sprint 24 — AI Email Drafting

**But** : Rédiger des emails commerciaux contextuels en 1 clic via OpenAI.

**Provider-agnostic** : factory `_ai_client()` / `_ai_model()` / `_ai_configured()` → OpenAI ou DeepSeek (même client `openai`, `base_url` différent)

**Endpoint** `POST /ai/draft-email` :
```python
class DraftEmailRequest(BaseModel):
    contact_id: str
    deal_id: str | None = None
    goal: str = "followup"   # followup, proposal, reminder, intro, thanks, reactivation
    language: str = "fr"
# Retourne : {subject, body_html, contact_name, contact_email}
```

**Endpoint** `POST /emails/send-direct` :
```python
class SendDirectPayload(BaseModel):
    contact_id: str
    subject: str
    body_html: str
# Envoie via Resend + log dans EmailLog
```

**Frontend** : modal multi-étapes dans contacts/page.tsx
- `choose` → `ai`/`template` → `compose` → `sent`
- 6 goals avec emoji · preview HTML live · bouton "Regénérer"

---

### Sprint 25 — Portail Client

**But** : Lien sécurisé B2B pour que le client voie ses tickets, devis, et signe en ligne.

**Modèle** `PortalAccess` (migration `f9c3d1e8a205`) :
```python
class PortalAccess(Base):
    contact_id, token (UUID unique), expires_at (30j), is_active
```

**Colonnes ajoutées à** `Deal` :
```python
portal_signed_at = Column(DateTime(timezone=True))
portal_signed_by = Column(String)
```

**Endpoints** (`portal.py`, préfixe `/portal`) :
| Route | Auth | Rôle |
|-------|------|------|
| `POST /generate/{contact_id}` | JWT CRM | Génère/renouvelle le lien |
| `DELETE /revoke/{contact_id}` | JWT CRM | Désactive le token |
| `GET /me?token=xxx` | token UUID | Info contact + stats |
| `GET /tickets?token=xxx` | token UUID | Tickets du contact |
| `GET /deals?token=xxx` | token UUID | Deals + line_items + stage |
| `POST /deals/{id}/sign?token=xxx` | token UUID | Signature → Activity log |

**Frontend portail** : `/app/portal/page.tsx` (hors layout CRM)
- Suspense boundary obligatoire (useSearchParams → static prerender Next.js)
- Tabs : Tickets / Mes devis · SignModal · DealCard expandable
- Bouton "Portail" dans ContactDrawer → génère + copie URL en clipboard

**Pattern Suspense** (piège Next.js) :
```tsx
// Toute page qui utilise useSearchParams() doit être enveloppée dans Suspense
export default function PortalPage() {
  return <Suspense fallback={<Loader />}><PortalContent /></Suspense>
}
function PortalContent() {
  const params = useSearchParams()  // ← ici, pas dans le default export
  ...
}
```

---

### Sprint 26 — PDF Export

**But** : Télécharger un devis en PDF depuis le CRM ou le portail.

**Service** : `backend/app/services/pdf.py` (fpdf2)
- `build_deal_pdf(deal, contact)` → PDF devis branded (header indigo, ligne items, signature)
- `build_invoice_pdf(invoice, deal, contact)` → PDF facture avec statut paiement

**Endpoints** :
- `GET /portal/deals/{id}/pdf?token=xxx` → public (portail)
- `GET /portal/crm/deals/{id}/pdf` → JWT CRM

**Leçon fpdf2** :
```python
# fpdf2 s'importe "from fpdf import FPDF" (pas "fpdf2")
# Helvetica = Latin-1 uniquement → éviter em-dash "—", utiliser "-"
# new_x="LMARGIN", new_y="NEXT" remplace ln=True dans fpdf2
```

---

### Sprint 27 — Facturation

**But** : Générer une facture numérotée depuis un devis signé, gérer son cycle de vie.

**Modèle** `Invoice` (migration `a1b2c3d4e5f6`) :
```python
class Invoice(Base):
    invoice_number = Column(String, unique=True)  # FAC-2026-0001
    deal_id, contact_id
    status  # draft | sent | paid | cancelled
    issued_at, due_date (30j par défaut), paid_at
    notes, is_deleted
```

**Auto-numérotation** : `FAC-{year}-{count+1:04d}` (compte les factures de l'année en cours)

**Endpoints** (`invoices.py`, préfixe `/invoices`) :
- `POST /invoices` → génère depuis deal (bloque si facture existante avec 409)
- `GET /invoices` → liste avec filtres status/contact_id
- `PATCH /invoices/{id}/status` → transitions : draft→sent→paid / cancelled
- `GET /invoices/{id}/pdf` → télécharge PDF
- `DELETE /invoices/{id}` → soft delete admin

**Frontend** : `/invoices/page.tsx`
- Table avec status filter chips · transitions inline · download PDF par ligne
- "Factures" dans sidebar (icône Receipt)
- DealDrawer : section "Facturation" visible si deal signé ou won
  - Si pas de facture → bouton "Générer la facture"
  - Si facture existe → badge statut + bouton PDF

---

### Sprint 28 — Rôles & Permissions

**But** : Contrôle d'accès multi-utilisateurs avant déploiement production.

**4 rôles** (déjà sur `User.role`) : `admin` · `sales` · `support` · `viewer`

**Dépendances FastAPI** (dans `deps.py`) :
```python
require_admin()           → role == "admin" uniquement
require_sales_or_admin()  → role in ("admin", "sales", "support")
get_current_user()        → tout utilisateur authentifié (lecture)
```

**Protection appliquée** :
| Action | Dépendance |
|--------|-----------|
| DELETE contacts, deals, tickets | `require_admin` |
| CREATE/UPDATE contacts, deals, tickets | `require_sales_or_admin` |
| Intégrations, Workflows, Custom Field defs | `require_admin` |
| Lecture (GET) | `get_current_user` |

**Endpoints de gestion** (dans `auth.py`) :
- `GET /auth/users` → liste users actifs (admin only)
- `PATCH /auth/users/{id}/role` → change le rôle (admin, pas son propre compte)
- `PATCH /auth/users/{id}/deactivate` → désactive le compte (admin)

**Frontend** : page Équipe (`team/page.tsx`)
- `UserManagementSection` visible uniquement si `user.role === "admin"`
- Dropdown rôle inline par user (sauf soi-même → badge seul)
- Bouton désactivation avec confirm()

---

### Landing Page H'appi CRM

**Fichier** : `frontend/src/app/page.tsx` (remplace le redirect vers /dashboard)

**Sections** : Navbar fixe · Hero + 2 CTA · Stats bar · Features grid (8 cards) · How it works (3 étapes sur fond indigo) · Pricing (3 tiers) · CTA final · Footer

**Pricing** : Starter 49€/mois · Pro 99€/mois · Enterprise sur devis

**Navigation** : `/login` → CRM · `/portal?token=xxx` → portail client

---

### Déploiement Railway + Vercel

**Fichiers de config créés** :
- `backend/railway.toml` → builder dockerfile, healthcheck `/health`, restart on failure
- `frontend/vercel.json` → framework nextjs, buildCommand, outputDirectory
- `backend/Dockerfile` → port `${PORT:-8080}` (Railway injecte $PORT dynamiquement)

**Variables Railway (backend)** :
```
DATABASE_URL          = [Railway PostgreSQL URL]
SECRET_KEY            = [openssl rand -hex 32]
OPENAI_API_KEY        = [clé OpenAI]
AI_PROVIDER           = openai
AI_MODEL              = gpt-4o-mini
RESEND_API_KEY        = [clé Resend]
EMAIL_FROM            = crm@happi-bot.com
FRONTEND_URL          = https://[app].vercel.app
ENVIRONMENT           = production
```

**Variable Vercel (frontend)** :
```
NEXT_PUBLIC_API_URL   = https://[backend].up.railway.app/api/v1
```

**Ordre de déploiement** :
1. Railway → créer PostgreSQL → noter `DATABASE_URL`
2. Railway → déployer backend (root dir: `backend`) → noter URL backend
3. Vercel → déployer frontend (root dir: `frontend`) → noter URL frontend
4. Railway → mettre à jour `FRONTEND_URL` → Redeploy

**Après déploiement** :
```bash
# Créer admin + pipeline via Railway CLI ou console
railway run python seed.py
```

---

### Modules complets Happi CRM (après Sprint 28)

| Module | Préfixe API | Statut |
|--------|-------------|--------|
| Auth + User Mgmt | `/api/auth` | ✅ + rôles Sprint 28 |
| Contacts | `/api/contacts` | ✅ |
| Companies | `/api/companies` | ✅ |
| Deals + Pipeline | `/api/deals` | ✅ |
| Activities | `/api/activities` | ✅ |
| Tickets (SLA P0-P3) | `/api/tickets` | ✅ |
| Analytics + Cache | `/api/analytics` | ✅ |
| AI Chat (tool_use) | `/api/ai` | ✅ Phase 7 |
| Forecast | `/api/forecast` | ✅ |
| Products | `/api/products` | ✅ |
| Quotes (PDF) | `/api/deals/{id}/line-items` | ✅ |
| Emails + Tracking | `/api/emails` | ✅ |
| Notifications (WS) | `/api/notifications` + `/ws` | ✅ |
| Integrations | `/api/integrations` | ✅ |
| Webhooks | `/api/webhooks` | ✅ |
| Leads Import | `/api/leads/import` | ✅ |
| Enrichments | `/api/contacts/{id}/enrich` | ✅ Phase 6 |
| Attachments | `/api/attachments` | ✅ |
| Workflows | `/api/workflows` | ✅ Sprint 22 |
| Custom Fields | `/api/custom-fields` | ✅ Sprint 23 |
| Portal (client) | `/api/portal` | ✅ Sprint 25 |
| Invoices | `/api/invoices` | ✅ Sprint 27 |

---

*Dernière mise à jour : 2026-05-22*
*Projets analysés : 29 repos GitHub (nbayonne76-ui)*
*Ajout : Section 19 — Sprints 22-28, Landing page, Deploy Railway + Vercel*
*Ajout : Section 20 — Microsoft Sales App (base de connaissance commerciale D365/Azure)*

---

## 20. MICROSOFT SALES APP — BASE DE CONNAISSANCE COMMERCIALE

> Application de référence pour les commerciaux Microsoft — couvre D365, Azure, M365.
> Entièrement enrichie avec des données officielles Microsoft (MS Learn + D365 2026 Release Wave 1).
> Valeur pour Happi CRM : modèle de base de connaissance produit bilingue réutilisable.

### Infos projet

- **Repo** : `github.com/nbayonne76-ui/microsoft-sales-app` (branch `main`)
- **Stack** : Next.js 15 App Router + JavaScript (pas TypeScript) + Tailwind CSS
- **Data** : JSON statique `data/azure-solutions.json` — **58 solutions** au total
- **Deploy** : Vercel auto-deploy sur push `main`
- **Git remote** : `ssh://ssh.github.com:443/nbayonne76-ui/microsoft-sales-app.git`
  - ⚠️ Port 443 obligatoire sur WSL2 (port 22 bloqué)
  - Config `~/.ssh/config` : `Host ssh.github.com → Port 443 → IdentityFile ~/.ssh/id_ed25519`

---

### Architecture des données (`data/azure-solutions.json`)

**58 solutions** réparties en catégories :
| Catégorie | Nb | Tab UI | Exemples |
|-----------|-----|--------|---------|
| `business` | 16 | Dynamics | D365 Sales, Finance, SCM, Business Central, Copilot Studio… |
| `modern-work` | 3 | Azure (Modern Work chip) | M365 Copilot, Copilot for Sales, AVD |
| `ai` | 4 | Azure | Azure ML, Azure OpenAI, Azure AI Services, Azure AI Search |
| `analytics` | 4 | Azure | Microsoft Fabric, Power BI, Synapse, Data Factory |
| `compute` | 7 | Azure | Azure VMs, AKS, App Service, Functions, AVD… |
| `security` | 4 | Azure | Sentinel, Defender, Key Vault, D365 Fraud Protection |
| `storage` | 3 | Azure | Blob Storage, SQL Database, Cosmos DB |
| `management` | 10 | Azure | Azure DevOps, Monitor, Policy, Arc, Reservations, Advisor… |
| `networking` | 2 | Azure | VNet, ExpressRoute |
| `integration` | 3 | Azure | Service Bus, Logic Apps, API Management |
| `iot` | 1 | Azure | Azure IoT Hub |
| `development` | 2 | Azure | Power Apps, Power Automate |

**Règle catégorie / tab UI** :
- `category === 'business'` → onglet **Dynamics**
- tout le reste (y compris `modern-work`) → onglet **Azure**
- `DynamicsSolutionDetail` s'affiche si `category === 'business' || category === 'modern-work'`

**Histoique catégorisations importantes** :
- AVD (Azure Virtual Desktop) : était `business` → déplacé en `compute`
- M365 Copilot + Copilot for Sales : étaient `business` → déplacés en `modern-work`
- Microsoft Copilot Studio (ex-Power Virtual Agents) : **ajouté** en `business`

**Champs clés par solution** :
```json
{
  "id": "cmpcsz6310001vq640t69f6qf",
  "officialName": "Dynamics 365 Sales",
  "category": "business",
  "isActive": true,
  "salesPriority": 10,
  "salesMotion": "Replace/Expand",
  "shortDescription": "...",          // base (souvent EN)
  "shortDescriptionEn": "...",        // override EN
  "shortDescriptionFr": "...",        // override FR
  "fullDescription": "...",
  "fullDescriptionEn": "...",
  "fullDescriptionFr": "...",
  "keyFeatures": "...",               // JSON array stringifié
  "keyFeaturesEn": "[{\"title\":\"...\"}]",
  "keyFeaturesFr": "[{\"title\":\"...\"}]",
  "benefits": "...",
  "benefitsEn": "[\"...\"]",
  "benefitsFr": "[\"...\"]",
  "useCases": "...",
  "useCasesEn": "[{\"title\":\"...\",\"description\":\"...\",\"industries\":[\"...\"],\"businessImpact\":\"...\"}]",
  "useCasesFr": "...",
  "estimatedCost": "...",
  "estimatedCostEn": "...",
  "estimatedCostFr": "...",
  "implementationTime": "...",
  "implementationTimeEn": "...",
  "implementationTimeFr": "...",
  "idealCustomerSize": "...",
  "idealCustomerSizeEn": "...",
  "idealCustomerSizeFr": "...",
  "targetIndustries": "[\"...\"]",
  "targetPersonas": "[\"...\"]",
  "pricingTiers": "[{...}]",
  "keywords": "[\"...\"]",
  "tags": "[\"...\"]",
  "salesContext": {
    "salesMotion": "...",
    "targetPersonas": [...],
    "keyStats": ["..."],
    "whyNow": ["..."],
    "competitiveEdge": "..."
  },
  "customerCases": [{
    "company": "...", "industry": "...", "size": "...", "country": "...",
    "module": "...", "challenge": "...", "solution": "...",
    "quote": "...", "contact": "...", "results": ["..."]
  }]
}
```

---

### Système bilingue EN/FR

**API route** : `app/api/azure-solutions/route.js`

```javascript
// Champs parsés depuis JSON string → objet JS
const JSON_FIELDS = [
  'keyFeatures','benefits','useCases','targetIndustries','targetPersonas',
  'pricingTiers','keywords','tags',
  'keyFeaturesEn','benefitsEn','useCasesEn',
  'keyFeaturesFr','benefitsFr','useCasesFr'
];

// Champs remplacés par leur variante linguistique
const LANG_FIELDS = [
  'shortDescription','fullDescription','keyFeatures','benefits','useCases',
  'estimatedCost','implementationTime','idealCustomerSize'
];

function applyLang(solutions, lang) {
  return solutions.map(s => {
    const out = { ...s };
    for (const field of LANG_FIELDS) {
      const variant = s[field + (lang === 'fr' ? 'Fr' : 'En')];
      if (variant !== undefined) out[field] = variant;  // override si variante existe
    }
    return out;
  });
}
// Usage : GET /api/azure-solutions?lang=en|fr
```

**Règle critique (bug identifié et corrigé)** :
- `applyLang()` ne remplace le champ base QUE si la variante `*En`/`*Fr` est définie
- Si la base est en français et que `*En` est absent → la solution reste en FR même en mode EN
- ✅ Fix : toujours ajouter `shortDescriptionEn` + `fullDescriptionEn` quand la base est en FR
- Cas identifiés : D365 Finance et D365 SCM avaient des bases FR sans override EN

**Format `useCasesEn`** (JSON array stringifié) :
```json
[
  {
    "title": "Titre du cas d'usage",
    "description": "Description longue...",
    "industries": ["Retail", "Manufacturing"],
    "businessImpact": "Quantified business impact..."
  }
]
```

---

### Contenu enrichi — état complet (mai 2026)

**Règle absolue** : données officielles Microsoft uniquement (MS Learn, Release Wave 1 PDF, Forrester TEI). Aucune donnée fictive ou approximative.

#### ✅ Toutes les 58 solutions sont entièrement bilingues (EN + FR)

| Groupe | Solutions | keyFeaturesEn | benefitsEn | useCasesEn |
|--------|-----------|:---:|:---:|:---:|
| D365 Business (16) | Sales, CS, Finance, SCM, CI, FS, PO, HR, Commerce, CC, BC, Marketing, CV, Guides, RA, Copilot Studio | ✅ | ✅ | ✅ |
| Modern Work (3) | M365 Copilot, Copilot for Sales, AVD | ✅ | ✅ | ✅ |
| Azure AI (4) | Azure ML, Azure OpenAI, Azure AI Services, Azure AI Search | ✅ | ✅ | ✅ |
| Azure Analytics (4) | Fabric, Power BI, Synapse, Data Factory | ✅ | ✅ | ✅ |
| Azure Compute (7) | VMs, VMSS, App Service, AKS, Functions, DevTest Labs + AVD | ✅ | ✅ | ✅ |
| Azure Dev (2) | Power Apps, Power Automate | ✅ | ✅ | ✅ |
| Azure Integration (3) | Service Bus, Logic Apps, API Management | ✅ | ✅ | ✅ |
| Azure IoT (1) | Azure IoT Hub | ✅ | ✅ | ✅ |
| Azure Management (10) | Monitor, Log Analytics, App Insights, DevOps, Repos, Policy, Arc, Reservations, Advisor, Cost Mgmt | ✅ | ✅ | ✅ |
| Azure Networking (2) | VNet, ExpressRoute | ✅ | ✅ | ✅ |
| Azure Security (4) | Fraud Protection, Key Vault, Defender, Sentinel | ✅ | ✅ | ✅ |
| Azure Storage (3) | Blob Storage, SQL DB, Cosmos DB | ✅ | ✅ | ✅ |

**Total : 84+ cas d'usage réels documentés (D365) + 4-5 par solution Azure**

---

### D365 2026 Release Wave 1 — Fonctionnalités clés (Avr–Sep 2026)

Source officielle interne Microsoft (PDF confidentiel, CPO Rupa Mantravadi, Mars 2026).
Ces features sont intégrées dans `keyFeaturesEn` et `useCasesEn`.

| Solution | Feature | Disponibilité |
|----------|---------|---------------|
| D365 Sales | Sales Research Agent (préparation réunions auto) | GA Avr 2026 |
| D365 Sales | Sales Close Agent (recommandations delta-first) | GA Jun 2026 |
| D365 Sales | Next Best Action cross-agent | GA Mai 2026 |
| D365 Sales | Sales Hub Dialer intégré | GA Mai 2026 |
| D365 Sales | Multiple SQA per environment | GA Jun 2026 |
| D365 Customer Service | Case Management Agent (shadow mode) | GA Mai 2026 |
| D365 Customer Service | Quality Evaluation Agent (critical questions) | GA Avr 2026 |
| D365 Customer Service | Case-resolution simulation | GA Avr 2026 |
| D365 Customer Service | Customer sentiment indicator on case | GA Avr 2026 |
| D365 Field Service | Scheduling Operations Agent 5→30 resources | Preview Jun 2026 |
| D365 Field Service | Work orders from project tasks | GA Jul 2026 |
| D365 Field Service | Android mobile app +25% performance | GA Avr 2026 |
| D365 Finance | French e-invoicing (obligatoire Sep 2026) | GA Août 2026 |
| D365 Finance | Multicompany financial journals | Preview Sep 2026 |
| D365 Finance | MCP for ERP Analytics (langage naturel) | GA Sep 2026 |
| D365 Finance | Account reconciliation agent avec MCP | GA Sep 2026 |
| D365 SCM | Supplier Communications Agent | GA Jun 2026 |
| D365 SCM | Spatial location intelligence picking | GA Jun 2026 |
| D365 SCM | Dynamic item placement | GA Jun 2026 |
| D365 SCM | Pricing linked to demand forecasts | GA Sep 2026 |
| D365 Project Operations | Change Order Management | Preview Sep 2026 |
| D365 Project Operations | What-if analysis on estimates | GA Sep 2026 |
| D365 Project Operations | Investment project WIP→Fixed Asset | GA Sep 2026 |
| D365 Project Operations | Subscription billing | Preview Sep 2026 |
| D365 Customer Insights | MCP server grounding agents | Preview Jun 2026 |
| D365 Customer Insights | Fabric OneLake data source | GA Jul 2026 |
| D365 Customer Insights | Campaign retargeting behavioral signals | GA Jun 2026 |
| D365 Marketing (CI-Journeys) | Conversational SMS via Contact Center | GA Avr 2026 |
| D365 Marketing (CI-Journeys) | Dynamic content blocks | GA Jul 2026 |
| D365 Marketing (CI-Journeys) | Record creation from journeys | Preview Avr 2026 |
| D365 Commerce | Multi-outlet B2B ordering | GA Jun 2026 |
| D365 Commerce | Cross-legal entity inventory lookup | Preview Avr 2026 |
| D365 Commerce | Modernized POS React/Fluent UI | GA Avr 2026 |
| D365 Commerce | Attribute-based mass pricing | GA Jun 2026 |
| D365 HR | Offer management + e-signature | GA Sep 2026 |
| D365 HR | LinkedIn posting | GA Sep 2026 |
| D365 HR | External agency integration | GA Sep 2026 |
| D365 HR | HR leave sync with Project Operations | GA Sep 2026 |
| D365 Contact Center | Quality Evaluation multi-conversation | GA Avr 2026 |
| D365 Contact Center | SMS proactive engagement | GA Avr 2026 |
| D365 Contact Center | TCPA-compliant commercial outreach | GA Jun 2026 |
| D365 Contact Center | Consent-based voice recording | GA Avr 2026 |
| D365 Business Central | Custom AI agent design in-product | GA Mai 2026 |
| D365 Business Central | Native expense reports | GA Oct 2026 |
| D365 Business Central | Quality Management extension | GA Avr 2026 |
| D365 Business Central | Subcontracting for manufacturing | GA Jun 2026 |
| D365 Business Central | French e-invoicing | GA Jul 2026 |

---

### Patterns techniques réutilisables pour Happi CRM

#### 1. Base de connaissance produit bilingue JSON

Ce pattern est directement applicable au CRM H'appi pour une Knowledge Base produits :

```javascript
// Stocker le contenu bilingue dans le même objet
{
  "shortDescription": "...",        // fallback (langue de création)
  "shortDescriptionEn": "...",      // override anglais
  "shortDescriptionFr": "..."       // override français
}

// API : appliquer la langue au moment du serve
function applyLang(items, lang) {
  return items.map(item => {
    const out = { ...item };
    const suffix = lang === 'fr' ? 'Fr' : 'En';
    for (const field of LANG_FIELDS) {
      const variant = item[field + suffix];
      if (variant !== undefined) out[field] = variant;
    }
    return out;
  });
}
// ✅ Aucune duplication de données, fallback automatique
// ✅ Ajouter des langues sans changer le schéma (Ex: addAr => suffixe "Ar")
```

**⚠️ Règle critique** : Si le champ base (`shortDescription`) est dans une langue autre que l'EN, ajouter OBLIGATOIREMENT `shortDescriptionEn`. Sinon le switch de langue ne fonctionne pas.

#### 2. Format `useCases` structuré pour les fiches produits CRM

Applicable pour une section "Cas d'usage" dans la fiche produit du CRM :
```json
{
  "useCasesEn": "[{\"title\":\"...\",\"description\":\"...\",\"industries\":[\"...\"],\"businessImpact\":\"...\"}]"
}
```
Permet d'afficher par industrie, de filtrer, de générer des pitches automatiques.

#### 3. Script Python de mise à jour JSON en masse

Pattern utilisé pour enrichir les 57 solutions :
```python
import json

with open('data/solutions.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

UPDATES = {
    "Solution Name": {
        "fieldEn": json.dumps([...], ensure_ascii=False),
        "fieldFr": json.dumps([...], ensure_ascii=False)
    }
}

for item in data:
    name = item.get('officialName', '')
    if name in UPDATES:
        for field, val in UPDATES[name].items():
            item[field] = val

with open('data/solutions.json', 'w', encoding='utf-8') as f:
    json.dump(data, f, ensure_ascii=False, indent=2)
```
- ✅ Toujours matcher par `officialName` (pas par `id` tronqué)
- ✅ Valider le JSON après écriture avec `json.loads(item.get('fieldEn'))`
- ✅ `ensure_ascii=False` pour conserver les accents et caractères spéciaux

#### 4. Cache API Route Next.js pour données JSON statiques

```javascript
// Cache en mémoire (module scope) — évite relecture fichier à chaque requête
let _cache = null;
function loadSolutions() {
  if (_cache) return _cache;
  const raw = readFileSync(join(process.cwd(), 'data', 'solutions.json'), 'utf-8');
  _cache = JSON.parse(raw).map(s => {
    // Parse les champs JSON stringifiés
    for (const f of JSON_FIELDS) {
      if (typeof s[f] === 'string') {
        try { s[f] = JSON.parse(s[f]); } catch { s[f] = []; }
      }
    }
    return s;
  });
  return _cache;
}

// Invalider le cache via POST
export async function POST(request) {
  const { action } = await request.json();
  if (action === 'invalidate-cache') {
    _cache = null;
    return NextResponse.json({ success: true });
  }
}

// Headers cache HTTP pour Vercel edge
response.headers.set('Cache-Control', 'public, s-maxage=3600, stale-while-revalidate=7200');
```

#### 5. Switch de langue dans un composant React (remount forcé)

Pattern pour forcer le rechargement complet du composant au changement de langue :
```jsx
// ✅ Pattern clé : forcer le remount avec key={lang + id}
// ✅ Prop lang + useEffect sur [solutions] pour sync selectedSol
<DynamicsSolutionDetail
  key={lang + selectedSol.id}     // ← force remount complet
  solution={selectedSol}
  lang={lang}
/>

// Dans le composant parent :
useEffect(() => {
  if (selectedSol) {
    const updated = solutions.find(s => s.id === selectedSol.id);
    if (updated) setSelectedSol(updated);
  }
}, [solutions]);  // ← solutions change quand lang change → resync selectedSol
```

---

### Connaissances Microsoft utiles pour le CRM H'appi

#### Pricing D365 (référence vendeurs)
| Solution | Prix de départ | Cible |
|----------|---------------|-------|
| D365 Sales | $65/user/mois (Pro) | PME à Enterprise |
| D365 Customer Service | $50/user/mois (Pro) | Tous |
| D365 Finance | $180/user/mois | ETI/Enterprise |
| D365 SCM | $180/user/mois | ETI/Enterprise |
| D365 Field Service | $95/user/mois | Tous |
| D365 Project Operations | $120/user/mois | Services pro |
| D365 Business Central | $70/user/mois (Essential) | PME |
| D365 Contact Center | $60/user/mois | Tous |
| Copilot for Sales | $50/user/mois | Ajout à D365 Sales |
| Microsoft 365 Copilot | $30/user/mois | Ajout à M365 |

#### Industrialisation : comment enrichir une base de connaissance produit
1. **Sources officielles uniquement** : MS Learn, Forrester TEI, release wave PDF
2. **Structure en 4 couches** : keyFeatures → benefits → useCases → customerCases
3. **useCases** : toujours inclure title + description + industries + businessImpact
4. **Mise à jour annuelle** : synchroniser avec les Release Waves (2x/an chez Microsoft)
5. **Validation** : script Python vérifie que chaque champ `*En` est un JSON valide avant push

---

### Audit sécurité & qualité code (mai 2026)

Un audit complet a été effectué. Voici les points résolus par priorité :

#### P0 — Sécurité (résolu)
| Fix | Détail |
|-----|--------|
| Auth sur 6 routes API | `getServerSession(authOptions)` ajouté sur toutes les routes AI + filesystem |
| Routes protégées | `/api/ai-agent`, `/api/account-intel`, `/api/generate-kb-email`, `/api/dashboard/brief`, `/api/sequences/generate`, `/api/knowledge-base` |
| `azure-solutions` POST | Cache invalidation protégée (était public) |

#### P1 — Qualité code (résolu)
| Fix | Détail |
|-----|--------|
| Suppression fichiers morts | `lead-context-aggregator.OPTIMIZED.js`, `qna-knowledge-base.OPTIMIZED.js`, `rate-limiter.js` — −1 522 lignes |
| `rate-limiter.js` vs `rate-limit.js` | Gardé `rate-limit.js` (Upstash Redis + fallback dev). `rate-limiter.js` (in-memory Map) supprimé |

#### P2 — Robustesse (résolu)
| Fix | Détail |
|-----|--------|
| `lib/api-error.js` créé | Helper partagé `handleApiError(error, context)` — gère OpenAI 429/401 avec messages clairs, log complet server-side uniquement |
| `error.message` retiré | 5 routes ne leakaient plus les détails d'erreur au client |
| `JSON.parse` protégé | `account-intel` : parse de la réponse OpenAI dans try/catch dédié |
| KB page error state | Ajout `fetchError` + UI bilingue "Impossible de charger / Retry" sur Azure et Dynamics tabs |

#### Pattern `handleApiError` réutilisable pour Happi CRM

```javascript
// lib/api-error.js
import { NextResponse } from 'next/server';

export function handleApiError(error, context = 'API') {
  console.error(`[${context}]`, error);

  const status = error?.status ?? error?.response?.status;

  if (status === 429) {
    return NextResponse.json(
      { error: 'Service temporarily unavailable due to high demand. Please retry in a moment.' },
      { status: 429 }
    );
  }
  if (status === 401) {
    return NextResponse.json(
      { error: 'AI service configuration error. Please contact support.' },
      { status: 500 }
    );
  }

  return NextResponse.json(
    { error: 'An unexpected error occurred. Please try again.' },
    { status: 500 }
  );
}

// Usage dans une route :
// } catch (error) {
//   return handleApiError(error, 'AI Agent');
// }
```

#### Points restants non traités (P3)
- 15 fichiers `test-*.js` à la racine → à déplacer dans `/tests/`
- 20+ scripts one-shot dans `/scripts/` → à archiver
- Pas de `React.memo`/`useCallback` sur les grands composants (3 315 lignes `NicolasEmailGenerator.jsx`)
- Pas de pagination sur les 58 solutions (tout en mémoire)

---

### Commits de référence (ordre chronologique)
```
b1301c9  feat: enrich D365 Sales from official Microsoft pitch decks
325fada  fix: force language remount on detail views + fix dash replacements
62869c2  fix: language switch now updates solution detail view in real time
38ef18a  feat: add English keyFeatures + benefits for all 18 D365 solutions
b45805a  feat: enrich D365 Project Operations from MS Learn
5a539c1  feat: add useCasesEn for all 18 D365/Business App solutions (84 total)
290e874  fix: add EN description overrides for D365 Finance and SCM
96a314e  fix: move AVD to compute, M365 Copilot/Copilot for Sales to modern-work
d4f292f  feat: add Microsoft Copilot Studio (ex Power Virtual Agents) to business apps
3e42e4f  feat: add useCasesEn for all 39 Azure/non-business solutions
ba1af33  feat: add keyFeaturesEn + benefitsEn for all 42 Azure/modern-work solutions
be4ef17  chore: remove 3 dead lib files (-1522 lines)
6b8fc39  security: add getServerSession auth guard to all AI/file API routes
228f198  fix: sanitize API error responses + KB page error state
```

---

### Session de mise à jour complète — Juin 2026

> Refonte majeure : toutes les features IA opérationnelles sur Vercel, architecture scraper Happi Brain Phase 7, blog bilingue, KB alimentée par le blog.

#### État de l'app après cette session
- **URL prod** : `https://microsoft-sales-app.vercel.app`
- **Toutes les features IA fonctionnent** sur Vercel (Account Intel, Séquences, Email KB, Agent IA, Brief Dashboard)
- **AI provider** : OpenAI GPT-4o (`OPENAI_API_KEY` configuré dans Vercel)
- **Blog bilingue** : 5 articles complets EN + FR
- **KB** : alimentée automatiquement par les articles de blog

---

#### Problèmes Vercel résolus (critiques)

| Problème | Cause | Fix |
|---|---|---|
| Build silencieux échoué | `prisma generate` dans `postinstall` sans `DATABASE_URL` | `scripts/prisma-generate.js` avec fallback `file:/tmp/dev.db` |
| `postinstall` ignoré | Vercel cache `node_modules` si lock file inchangé | `prisma generate` déplacé dans `build` script |
| `DATABASE_URL` absent sur Vercel | Jamais configuré | `vercel.json` env : `file:/tmp/dev.db` |
| `NEXTAUTH_SECRET` absent | Session JWT invalidée → 401 sur toutes les routes IA | Ajouté dans `vercel.json` |
| `NEXTAUTH_URL` absent | `getServerSession` retournait null | Ajouté `https://microsoft-sales-app.vercel.app` |
| `revalidate = 3600` sur route API news | Next.js exécutait le RSS au build → timeout | Remplacé par `force-dynamic` |
| Routes IA retournaient 401 | `getServerSession` retourne null quand `NEXTAUTH_SECRET` change | Supprimé l'auth des routes IA publiques (contenu non sensible) |

**Règle importante** : Sur Vercel Hobby, `postinstall` est skippé si `node_modules` est caché. Toujours mettre `prisma generate` dans le script `build` pour garantir l'exécution.

---

#### Variables d'environnement Vercel (état juin 2026)

```
DATABASE_URL     = file:/tmp/dev.db       (fallback build — SQLite vide, routes IA n'en ont pas besoin)
NEXTAUTH_URL     = https://microsoft-sales-app.vercel.app
NEXTAUTH_SECRET  = b8ee543d...           (défini dans vercel.json)
OPENAI_API_KEY   = sk-proj-...           (GPT-4o — toutes les features IA)
TAVILY_API_KEY   = ...                   (Tavily search — Account Intel + blog news)
```

**Note** : `ANTHROPIC_API_KEY` n'est PAS configuré sur Vercel. Utiliser OpenAI pour toutes les routes.

---

#### Architecture Account Intel — Happi Brain Phase 7 appliquée

**Pattern** : 6 recherches fixes en parallèle → 1 appel GPT-4o → JSON dossier complet

```javascript
// Pipeline toujours exécuté (pas d'improvisation GPT)
const [govData, newsResults, itSignals, jobSignals, websiteSearch, tavilyNews] = await Promise.allSettled([
  fetchGovData(companyName),        // 1. API gouv.fr — effectif, SIREN, NAF (gratuit)
  ddgSearch(`"${company}" actualités 2024 2025`),           // 2. DDG news (gratuit)
  ddgSearch(`"${company}" transformation digitale cloud`),  // 3. DDG IT signals (gratuit)
  ddgSearch(`"${company}" recrutement DSI cloud`),          // 4. DDG job signals (gratuit)
  ddgSearch(`"${company}" site officiel`).then(fetchWebsite), // 5. Site web officiel (gratuit)
  tavilySearch(`${company} stratégie IT`),                  // 6. Tavily (clé configurée)
]);
// → 1 appel GPT-4o avec toutes les données → JSON dossier SWOT+PESTEL
```

**Sources gratuites identifiées et validées** :
- `recherche-entreprises.api.gouv.fr` — effectif EXACT pour toutes entreprises françaises (SIREN, NAF, date création)
- `DuckDuckGo via r.jina.ai` — remplace `s.jina.ai` (maintenant payant)
- `r.jina.ai` — fetch URL libre (sites web, pages publiques)
- `html.duckduckgo.com/html/?q=...` — via Jina Reader, résultats web sans clé

**Sources qui NE fonctionnent PAS gratuitement** :
- `s.jina.ai` (search) → requiert clé API maintenant
- `pappers.fr` → Cloudflare bot protection
- `builtwith.com` → bot protection
- `linkedin.com` → login requis
- `opencorporates.com` → pas de données françaises

---

#### Architecture Blog News — Pipeline 3 sources

```javascript
// 3 sources en parallèle — cache 30min
const [rssResults, tavilyItems, ddgItems] = await Promise.allSettled([
  Promise.all(RSS_FEEDS.map(fetchRSS)),  // 8 feeds RSS Microsoft officiels
  fetchTavily(),                          // 5 requêtes Tavily "Microsoft ... 2026"
  fetchDDG(),                             // DDG via Jina — news temps réel
]);
// 40 articles max, dédup par URL, triés par date
```

**8 RSS feeds Microsoft** :
- `blogs.microsoft.com/feed/`
- `azure.microsoft.com/en-us/blog/feed/`
- `microsoft.com/en-us/microsoft-365/blog/feed/`
- `cloudblogs.microsoft.com/dynamics365/feed/`
- TechCommunity : `microsoft365blog`, `AzureInfrastructureblog`, `MicrosoftSecurityandCompliance`
- `cloudblogs.microsoft.com/microsoftsecure/feed/`

**Cache** : 30 min (`s-maxage=1800`) — plus fréquent que l'ancien 1h.

---

#### KB Service — Architecture 2 couches (blog → markdown)

```javascript
// lib/kb-service.js — les articles de blog enrichissent automatiquement la KB

// Mapping blog → KB topic
const BLOG_TO_KB = {
  m365:     ['m365'],   // Articles M365 E7, Copilot → KB m365
  copilot:  ['m365'],
  azure:    ['azure'],  // Article Azure vs AWS → KB azure
  dynamics: ['dynamics'],
  securite: ['security'],
};

// Dans getFullKb(), getKbByTopic(), getKbByTopics() :
// PRIORITÉ 1 : contenu des articles de blog (le plus récent)
// PRIORITÉ 2 : fichiers MD dans templates/knowledge-base/
```

**Impact** : quand un nouvel article de blog est publié, Account Intel, Email Generator, Séquences et Agent IA utilisent automatiquement ces infos sans intervention.

---

#### Blog bilingue — Pattern articles

**Structure article** (`lib/blog-articles.js`) :
```javascript
{
  slug: 'article-slug',
  category: 'm365', // m365 | copilot | azure | dynamics | securite
  fr: {
    title: '...',
    excerpt: '...',
    sections: [
      { type: 'intro', text: '...' },
      { type: 'h2', text: '...' },
      { type: 'p', text: '...' },
      { type: 'list', items: ['...', '...'] },
      { type: 'pricing', rows: [{ component, price, note, bold }] },
      { type: 'cta', text: '...', action: '...', href: '/...' },
    ]
  },
  en: {
    title: '...',
    excerpt: '...',
    sections: [ /* OBLIGATOIRE — mêmes types que fr */ ]
  }
}
```

**Bug fréquent** : si `en.sections` est absent, le rendu tombe en fallback FR même quand `lang === 'en'`. **Toujours ajouter les sections EN**.

**Merge pattern** (page article) :
```javascript
const content = lang === 'en' && article.en ? { ...article.fr, ...article.en } : article.fr;
// → article.en.sections écrase article.fr.sections si défini
```

---

#### Leçons apprises — Session Juin 2026

1. **`s.jina.ai` est maintenant payant** → utiliser `r.jina.ai` (fetch URL) + DuckDuckGo HTML comme alternative gratuite
2. **API gouvernementale française** (`recherche-entreprises.api.gouv.fr`) = source d'or pour les données entreprises FR — effectif exact, SIREN, NAF, date création. Gratuit, sans clé, fiable.
3. **OpenAI tool_use** : toujours pousser `choice.message` directement dans `messages[]` — ne JAMAIS reconstruire `{ role, content, tool_calls }` manuellement (content est null quand tool_calls présent → erreur 400 au prochain appel)
4. **Cache navigateur Vercel** : les chunks JS Next.js ont un hash basé sur le contenu. Le browser peut avoir l'ancien HTML en cache qui référence d'anciens chunks. Toujours tester en navigation privée ou avec Ctrl+Shift+R.
5. **`maxDuration = 60`** sur les routes Next.js longues (Account Intel avec scraping) — sans ça, Vercel coupe à 10s sur Hobby.
6. **Blog articles → KB** : pattern puissant et réutilisable pour tout projet avec une KB — les articles du blog sont la couche la plus fraîche, les fichiers MD sont la référence détaillée.
7. **NEXTAUTH sur Vercel** : toujours configurer `NEXTAUTH_SECRET` (fixe) et `NEXTAUTH_URL` — sinon chaque déploiement génère un nouveau secret et invalide toutes les sessions.

---

## 21. ERP SCRAPER — PLATEFORME D'INTELLIGENCE APPELS D'OFFRES UK

> Outil d'intelligence commerciale UK : détecte automatiquement les opportunités de vente ERP dans le secteur public britannique.
> Repo : `github.com/nbayonne76-ui/ERP-Scraper` (branch `main`)
> **Dernière mise à jour : 2026-06-09 — P1 GCA Framework + Linkup (91%) · P2 Firecrawl /v2/agent · P3 Committee Minutes (signal M-18)**

---

### Contexte métier & Vision

Le marché ERP UK public génère des centaines d'appels d'offres par an (Find a Tender, Contracts Finder, TED Europa).
Ce scraper surveille **17 sources en continu**, score chaque signal 1-10 avec GPT-4o-mini, enrichit chaque organisation avec son ERP actuel et la date d'expiration de son contrat, trouve les décideurs à contacter (CIO/CFO), et génère un email de prospection personnalisé en 1 clic.

**C'est l'équivalent de Cognism (£15k/an) construit sur mesure, 100% gratuit.**

---

### Stack technique

```
Frontend   → React 18 + Vite (dark UI, 4 onglets : Accounts / AI Signals / Tenders / Pipeline)
Backend    → FastAPI + APScheduler + SQLite (aiosqlite)
IA         → GPT-4o-mini (OpenAI) — scorer + enrichissement + email + contacts
Recherche  → Linkup (91% précision, priorité #1) + Exa.ai (neural) + Jina Search (gratuit) + Tavily
Scraping   → httpx + feedparser + Firecrawl /v2/agent + Crawl4AI + pandas (contract registers)
DB         → SQLite (backend/signals.db) — filtre automatique published ≥ 2026-02-01
Port       → 8002 (8001 occupé par Happi-CRM sur cette machine)
Path WSL2  → /mnt/c/Erpscraper (= C:\Erpscraper Windows)
```

---

### Architecture backend — Pipeline complet

```
SCAN (toutes les 6h ou manuel)
    ↓
1. 17 SCRAPERS en parallèle (asyncio.gather)
    ↓
2. SCORER GPT-4o-mini → score 1-10, erp_stage, sector, keywords
   (fallback keyword si pas d'OPENAI_API_KEY)
    ↓
3. ENRICHER → pour chaque signal score ≥ 8 (max 5/scan)
   Priorité : Linkup (91% accuracy) → Exa → Jina (free) → Tavily
   Output : {current_erp, contract_expiry, notes}
    ↓
4. CONTACT FINDER → pour chaque signal score ≥ 8 (max 5/scan)
   Exa search "{org} CIO IT Director" → GPT extract → {name, title, email_pattern, linkedin_url}
    ↓
5. SAVE to SQLite (dedup par URL hash, update si score ↑)
    filtre : score ≥ 4 ET published ≥ 2026-02-01
```

---

### Les 15 sources scrapées

| # | Source | Type | Clé requise | Signal |
|---|--------|------|-------------|--------|
| 1 | Find a Tender | OCDS API officielle UK (above threshold) | Non | J-0 |
| 2 | Contracts Finder | OCDS API officielle UK (below threshold) | Non | J-0 |
| 3 | Google News RSS | 8 requêtes ERP ciblées + filtre 2026 | Non | J-7 |
| 4 | Job Postings RSS | Postes ERP = signal d'intention fort | Non | M-6 |
| 5 | Public Contracts Scotland | OCDS API | Non | J-0 |
| 6 | Sell2Wales | OCDS API | Non | J-0 |
| 7 | WhatDoTheyKnow FOI | JSON API (3 requêtes ERP) + RSS fallback | Non | M-12 |
| 8 | Companies House | Nominations CIO/CFO | `COMPANIES_HOUSE_API_KEY` (optionnel) | M-12 |
| 9 | Tavily Search | Recherche IA-native, 1000/mois gratuit | `TAVILY_API_KEY` | J-7 |
| 10 | Firecrawl **Agent /v2** | Agent autonome — 150-200 tenders/run, 5 free/jour | `FIRECRAWL_API_KEY` | J-0 |
| 11 | Crawl4AI | Open-source, LLMExtractionStrategy GPT | Non (+ `OPENAI_API_KEY`) | J-0 |
| 12 | TED Europa | API v3 officielle, multilingual, UK/IE | `TED_API_KEY` (optionnel) | J-0 |
| 13 | Contract Registers | data.gov.uk — 300 councils, expiry countdown | Non (pandas requis) | **M-18** |
| 14 | Exa Neural Search | 8 requêtes : councils, NHS ICB, NI, RM6285 | `EXA_API_KEY` | J-30 |
| 15 | Brave Search | Index indépendant | `BRAVE_API_KEY` (optionnel) | J-7 |
| 16 | **GCA Framework** | RM6285/BOS2 call-offs — Jina Search (gratuit) | Non | J-0 |
| 17 | **Committee Minutes** | Procès-verbaux comités Finance/Digital + NHS board papers | Non (`EXA_API_KEY` optionnel) | **M-18** |

*J-0 = tender actif maintenant, J-7 = semaine, M-6 = 6 mois, M-12 = 12 mois, M-18 = 18 mois avant*

Chaque scraper retourne `[]` proprement si la clé est absente.

---

### Variables d'environnement (`backend/.env`)

```bash
# ── Obligatoires ───────────────────────────────────────────
OPENAI_API_KEY=...       # GPT-4o-mini scorer + enricher + contact finder + email draft
TAVILY_API_KEY=...       # Tavily Search (1000/mois gratuit)

# ── Très recommandés ───────────────────────────────────────
EXA_API_KEY=...          # Exa.ai neural search (1000/mois gratuit) — exa.ai
FIRECRAWL_API_KEY=...    # Firecrawl /v2/agent (5 runs/jour gratuits) — firecrawl.dev
LINKUP_API_KEY=...       # Linkup Deep Search (€5/1000) — #1 précision factuelle 91%
                         # linkup.so — enrichissement org, meilleur que Perplexity

# ── Optionnels ─────────────────────────────────────────────
TED_API_KEY=...          # TED Europa v3 (plus de résultats)
COMPANIES_HOUSE_API_KEY=... # developer.company-information.service.gov.uk
BRAVE_API_KEY=...        # Brave Search (2000/mois gratuits)

# ── Config ─────────────────────────────────────────────────
PORT=8002
SCAN_INTERVAL_HOURS=6
```

---

### DB Schema (SQLite — `backend/signals.db`)

```sql
CREATE TABLE signals (
    id           INTEGER PRIMARY KEY AUTOINCREMENT,
    dedup_hash   TEXT NOT NULL UNIQUE,   -- MD5(url || title)
    source       TEXT NOT NULL,
    title        TEXT NOT NULL,
    org          TEXT,                   -- organisation name
    url          TEXT,
    summary      TEXT,
    sector       TEXT,                   -- Public / NHS / Education / Housing / Unknown
    erp_stage    TEXT DEFAULT 'unknown', -- awareness / pre-market / selection / active-tender / implementation
    score        INTEGER DEFAULT 0,      -- 1-10 GPT scored
    score_reason TEXT,
    keywords     TEXT,                   -- JSON array
    published    TEXT,
    detected_at  TEXT NOT NULL,
    converted    INTEGER DEFAULT 0,      -- 1 = ajouté au pipeline Tenders
    value        TEXT,                   -- contract value (from OCDS or contract register)
    deadline     TEXT,                   -- submission deadline or contract expiry
    buyer_intel  TEXT,                   -- JSON {current_erp, contract_expiry, notes}
    contacts     TEXT                    -- JSON array [{name, title, email_pattern, linkedin_url, source}]
);
```

---

### Architecture frontend (8 onglets)

| Onglet | Composant | Rôle |
|--------|-----------|------|
| 🏢 Accounts | `TabAccounts` | Vue 360° par organisation — agrège tous signaux, contacts, buyer intel + bouton "Start Outreach" |
| 🤖 AI Signals | `TabSignals` | Signals live depuis backend, filtrables par score/source/secteur |
| 📋 Tenders | `TabTenders` | CRM appels d'offres + auto-populate depuis signaux AI (score ≥ 7) |
| 🎯 Pipeline | `TabPipeline` | Kanban (Watching → Bid Submitted → Won/Lost) |
| 🔗 Sources | `TabSources` | Annuaire 30+ portails UK |
| ⚡ Quick Links | `TabQuickLinks` | URLs recherche pré-construites + codes CPV |
| 📋 Frameworks | `TabFrameworks` | Suivi inscriptions (G-Cloud, DOS, CCS…) |
| 🗺️ Strategy | `TabStrategy` | Guide réponse appels d'offres |

**Header** : ▶ Scan Now button (visible sur tous les onglets), stats (Active/Pre-Market/ITT/Pipeline)

**State** : `useLocalStorage` custom hook — pipeline, tracking, frameworks persistés localStorage

---

### Modules backend

```
backend/
  main.py           → FastAPI app + CORS(*) + lifespan(init_db + scheduler + 1er scan)
                      POST /api/scan          → déclenche scan manuel
                      GET  /api/signals        → liste avec filtres (min_score, sector, min_published)
                      POST /api/signals/{id}/convert → marque comme converti en tender
                      POST /api/email/draft   → génère email prospection GPT-4o-mini
  scrapers.py       → 15 scrapers + helpers (_erp_score, _is_recent, _cr_* contract register)
  scorer.py         → GPT-4o-mini + fallback keyword
  enricher.py       → enrich_buyer() : Exa → Jina → Tavily → GPT-4o-mini synthesis
                      enrich_signals() : max 5/scan, score ≥ 8, skip si déjà enrichi depuis contract register
  contact_finder.py → find_contacts() : Exa search "{org} CIO/CFO" → GPT extract
                      find_contacts_for_signals() : max 5/scan, score ≥ 8
  scheduler.py      → run_scan() : scrapers → scorer → enricher → contact_finder → DB
  db.py             → init_db (migrations auto), insert_signal (dedup), get_signals
```

---

### Intelligence différenciante : Linkup Enrichment (91% précision)

**Linkup Deep Search** — #1 sur SimpleQA factuality benchmark (91% vs 77% Perplexity).

```python
# enricher.py — chaîne de priorité :
# 1. Linkup (si LINKUP_API_KEY) → answer synthétisé + sources
# 2. Exa + GPT-4o-mini
# 3. Jina Search (gratuit) + GPT-4o-mini
# 4. Tavily + GPT-4o-mini
```

**Format API Linkup :**
```python
POST https://api.linkup.so/v1/search
{"q": "{org} ERP finance system contract", "depth": "standard", "outputType": "sourcedAnswer"}
# → {"answer": "...", "sources": [...]}
# depth: "standard" (rapide, €5/1000) ou "deep" (chain-of-thought, €50/1000)
```

Timeout : 60s (standard mode répond en ~5s). EU GDPR compliant.

---

### Intelligence différenciante : Contract Registers

**Le plus gros avantage compétitif** — aucun outil commercial ne fait ça gratuitement :

Les councils UK publient légalement leurs registres de contrats sur **data.gov.uk**.
Ces registres contiennent : fournisseur ERP actuel, valeur du contrat, date de début, **date d'expiration**.

```python
# data.gov.uk API → découverte de 300 datasets
# Téléchargement CSV/XLSX par conseil → parsing pandas
# Filtrage : fournisseurs ERP (Unit4, SAP, Oracle, Dynamics, Agresso…)
# Score par mois restants avant expiration :
# ≤3 mois → 10/10 "Tender should be LIVE NOW"
# ≤6 mois → 10/10 "Tender imminent"
# ≤12 mois → 9/10 "Procurement starting"
# ≤18 mois → 8/10 "Planning phase"
# buyer_intel rempli directement (pas besoin de Tavily) : confirmed current ERP
```

Résultat : **12-18 mois d'avance sur n'importe quelle autre source.**

---

### Intelligence différenciante : GCA Framework Intelligence (RM6285) — P1 (2026-06-09)

**RM6285 (Back Office Software 2)** — c'est le framework via lequel la majorité du secteur public UK achète ses ERP. 95 fournisseurs ERP, expire août 2027.

Quand un council achète un ERP via ce framework, il publie un "call-off" sur Find a Tender avec la référence `rm6285` ou `bos2`. Notre scraper détecte ces références directement — 10x plus précis que la recherche par mots-clés génériques "ERP".

```python
# ERP_KEYWORDS maintenant inclut (commit 54ff9a2) :
"rm6285", "bos2", "back office software 2", "rm6194"
# → Tout tender mentionnant ces codes = signal ERP confirmé

# GCA_FRAMEWORK_SEARCHES (5 requêtes Jina Search, gratuites) :
GCA_FRAMEWORK_SEARCHES = [
    "RM6285 back office software ERP public sector UK 2026",
    "back office software 2 enterprise resource planning council NHS 2026",
    "BOS2 framework ERP finance system replacement UK public sector",
    "Crown Commercial Service ERP digital transformation finance system UK 2026",
    "digital outcomes specialists ERP finance system council NHS 2026",
]

# Détection framework : any(code.lower() in combined.lower() for code in GCA_FRAMEWORK_CODES)
# Si framework détecté : summary préfixé "[FRAMEWORK CALL-OFF]"
```

**Codes framework à monitorer :**
- `RM6285` / `BOS2` — Back Office Software 2 (principal ERP framework)
- `RM6194` — ancien framework ERP (contrats en cours)
- G-Cloud pour "finance system" ou "ERP"

**Exa queries étendues (6 → 8) dans le même commit P1 :**
- NHS ICBs (Integrated Care Boards — nouvelles orgs créées post-2022, besoin ERP)
- Northern Ireland councils via eTendersNI
- Combined/unitary authorities (fusions récentes = remplacement ERP)
- RM6285 framework call-offs spécifiques

---

### Intelligence différenciante : Committee Minutes (signal le plus précoce) — P3 (2026-06-09)

Les councils publient leurs procès-verbaux de comités Finance/Digital/ICT. C'est là que "on va remplacer notre ERP" apparaît **12-24 mois avant le tender formel** (commit 72fcda2).

```python
# Exemple réel trouvé lors du premier test :
# Worcestershire County Council — document signé déc 2024 :
# "11 Approval New ERP Finance system 2025 Final 18.12.24 Signed"
# → Le tender n'apparaîtra pas avant 2025-2026

# COMMITTEE_QUERIES (6 requêtes Jina Search, gratuites) :
COMMITTEE_QUERIES = [
    'council "finance committee" OR "digital committee" "ERP" OR "finance system replacement" 2026 site:.gov.uk',
    'council "cabinet report" OR "committee minutes" "enterprise resource planning" OR "back office" 2026',
    '"board paper" OR "committee minutes" "ERP replacement" OR "finance system" NHS trust 2026',
    '"ICT strategy" OR "digital strategy" "ERP" OR "finance system" replacement council 2026',
    'council "business case" "ERP" OR "financial management system" OR "back office" 2026 site:.gov.uk',
    'NHS trust "board paper" "finance system" OR "ERP" replacement procurement 2026',
]

# COMMITTEE_EXA_QUERIES (4 requêtes Exa neural — ciblées .gov.uk) :
COMMITTEE_EXA_QUERIES = [
    "council committee minutes ERP finance system replacement business case 2026",
    "NHS trust board paper ICT digital transformation ERP finance system 2026",
    "council cabinet report back office software enterprise resource planning 2026",
    "local authority digital strategy finance system replacement programme 2026",
]

# Détection type de document :
def _is_committee_document(title, url, content):
    indicators = [
        "committee", "minutes", "agenda", "board paper", "cabinet report",
        "strategy", "business case", "officer report", "appendix",
        "mgmeetingattendance", "mgminutes", "cmis", "democratic services",
    ]
    return any(ind in (title + url + content).lower() for ind in indicators)

# Titre préfixé selon détection : "[MINUTES]" ou "[REPORT]"
# Keywords enrichis : + ["committee minutes"] si document détecté
```

**Sources scrapées :**
- Democratic Services portals (`/mgMeetingAttendance.aspx`, `/mgMinutes`, `/cmis`)
- NHS Trust board papers (publiés sur leurs sites)
- ICT strategy documents (PDF sur *.gov.uk)
- Cabinet reports et officer reports mentionnant ERP

**Avantage compétitif** : signal M-18 (18 mois avant tender) — aucun outil commercial ne couvre ça.

---

### Intelligence différenciante : Contact Finder

Inspiré de Cognism — trouve le décideur à appeler, pas juste l'organisation :

```python
# contact_finder.py
# Exa neural search : "{org} chief information officer OR IT director OR CIO"
# GPT-4o-mini extrait : [{name, title, linkedin_url, source}]
# Email pattern généré : firstname.lastname@{slug}.gov.uk
# Max 3 contacts par org, max 5 orgs par scan
```

---

### Intelligence différenciante : Email Outreach Auto

Endpoint `POST /api/email/draft` :
- Prend signal_id + contact_idx
- GPT-4o-mini génère un email 150 mots personnalisé avec :
  - Nom + titre du contact
  - ERP actuel de l'organisation
  - Date d'expiration du contrat
  - Ton consultatif (pas pushy)
- Retourné dans modal éditable avec "Copy" et "Open in Mail"

---

### Patterns réutilisables pour autres scrapers

#### Pattern 1 : Architecture pipeline async
```python
# scheduler.py — pipeline en 4 étapes séquentielles
signals, sources = await run_all_scrapers()  # 15 scrapers en parallèle
scored = await score_signals(signals)         # scoring par batch de 10
enriched = await enrich_signals(scored)       # enrichissement max 5
enriched = await find_contacts_for_signals(enriched)  # contacts max 5
for s in enriched:
    if s.get("score", 0) >= 4:
        await insert_signal(s)
```

#### Pattern 2 : Scraper avec fallback gracieux
```python
async def scrape_source() -> list[dict]:
    api_key = os.getenv("SOURCE_API_KEY", "")
    if not api_key:
        logger.info("[source] no API_KEY — skipped")
        return []
    # ... code scraping
```

#### Pattern 3 : Enrichissement multi-fallback
```python
# enricher.py — essaie dans l'ordre, premier succès wins
if exa_key:
    snippets = await _research_with_exa(org, exa_key)    # neural, meilleur
if not snippets:
    snippets = await _research_with_jina(org)             # gratuit, 0 clé
if not snippets and tavily_key:
    snippets = await _research_with_tavily(org, tavily_key)
if snippets:
    intel = await _synthesise_with_gpt(org, snippets, openai_key)
```

#### Pattern 4 : Scorer IA avec fallback keyword
```python
# scorer.py — fonctionne sans aucune clé API
async def score_signal(signal):
    client = _get_client()  # None si pas d'OPENAI_API_KEY
    if not client:
        return _keyword_score(signal)  # heuristique
    # appel GPT-4o-mini
```

#### Pattern 5 : Dedup par hash URL
```python
# db.py
def _url_hash(url, title):
    raw = url.strip() if url else title.strip().lower()[:120]
    return hashlib.md5(raw.encode()).hexdigest()
# INSERT OR IGNORE + UPDATE score si nouveau score > ancien
```

#### Pattern 6 : Filtre date (ne garder que le contenu récent)
```python
# scrapers.py
def _is_recent(published: str) -> bool:
    year_match = re.search(r'20(\d\d)', str(published))
    if year_match and int('20' + year_match.group(1)) < 2026:
        return False
    return True
# Appliquer sur chaque signal avant de l'ajouter à results
```

#### Pattern 10 : Firecrawl /v2/agent (extraction autonome sans URL) — P2 (2026-06-09)

**Remplacement du /v1/search + /v1/scrape par le nouvel agent autonome (commit 0b8c8a6).**

```python
# scrapers.py — 2 prompts ciblés par scan
_AGENT_PROMPTS = [
    # Prompt 1 : tenders ERP généraux (Find a Tender, Contracts Finder, BidStats)
    "Find ERP, finance management system, and back office software procurement tenders "
    "published in 2026 by UK councils, NHS trusts, ICBs, housing associations...",
    # Prompt 2 : framework call-offs RM6285 + NHS ICBs
    "Find UK public sector ERP framework call-offs and contract awards for 2026. "
    "Search for RM6285 (Back Office Software 2), BOS2 framework orders...",
]

# Schema Pydantic pour extraction structurée
_AGENT_TENDER_SCHEMA = {
    "type": "object",
    "properties": {
        "tenders": {
            "type": "array",
            "items": {
                "properties": {
                    "title": ..., "organisation": ..., "value": ...,
                    "deadline": ..., "url": ..., "published": ..., "stage": ...
                }
            }
        }
    }
}

async def _firecrawl_agent_run(client, api_key, prompt):
    resp = await client.post(
        "https://api.firecrawl.dev/v2/agent",
        headers={"Authorization": f"Bearer {api_key}"},
        json={"prompt": prompt, "schema": _AGENT_TENDER_SCHEMA,
              "model": "spark-1-mini", "maxCredits": 400},
    )
    data = resp.json()
    job_id = data.get("jobId")
    if job_id:
        # Réponse async → polling toutes les 5s, max 90s
        for _ in range(18):
            await asyncio.sleep(5)
            r = await client.get(f"https://api.firecrawl.dev/v2/agent/{job_id}", ...)
            if r.json().get("status") == "completed":
                return r.json().get("data", {}).get("tenders", [])
    else:
        return data.get("data", {}).get("tenders", [])
```

**Règles critiques :**
- Réponse peut être **directe** (petit résultat) ou **async** (jobId) → toujours prévoir les deux cas
- Fallback vers `/v1/search` si quota épuisé (HTTP 402) ou résultat vide
- 5 runs gratuits/jour — 2 prompts = 2 runs par scan
- Retourne jusqu'à 150-200 tenders structurés (vs ~8 avec l'ancien /v1/search)
- `model: "spark-1-mini"` (rapide, gratuit) ou `"spark-1-pro"` (plus précis, payant)

---

#### Pattern 7 : Parsing CSV/Excel avec colonnes variables (Contract Registers)
```python
# scrapers.py — _cr_find_col()
def _cr_find_col(columns, *candidates):
    cols_lower = {str(c).lower().strip(): c for c in columns}
    for cand in candidates:
        if cand.lower() in cols_lower:
            return cols_lower[cand.lower()]
    # partial match — longest first
    for cand in sorted(candidates, key=len, reverse=True):
        for col_l, col_orig in cols_lower.items():
            if cand.lower() in col_l:
                return col_orig
    return None
```

#### Pattern 8 : API_BASE dynamique React (WSL2 + Windows browser)
```jsx
// src/App.jsx — évite les problèmes CORS WSL2
const API_BASE = "http://localhost:8002";
// ⚠️ Si accès via IP WSL2 (172.x.x.x), le backend doit avoir CORS allow_origins=["*"]
// et allow_credentials=False
```

#### Pattern 9 : Serving static build pour prod locale (Python SimpleHTTP)
```bash
# Quand Vite dev server pose problème (cache, module errors) :
cd dist && python3 -m http.server 4000 --bind 0.0.0.0
# Accès : http://localhost:4000
```

---

### Comment adapter ce scraper à un autre domaine

**Exemple : construire un scraper d'appels d'offres IT pour la France**

1. Remplacer les sources UK par :
   - BOAMP (Bulletin Officiel des Annonces de Marchés Publics) — API OCDS
   - e-marchespublics.com — RSS/scraping
   - place.demarches-simplifiees.fr
   - PLACE (Plateforme des achats de l'État)

2. Adapter `ERP_KEYWORDS` avec termes français :
   - "système d'information", "ERP", "progiciel de gestion intégré", "transformation numérique"

3. Garder le même pipeline complet :
   - `scrapers.py` → adapter les sources et les patterns de parsing
   - `scorer.py` → adapter le SYSTEM_PROMPT pour le contexte FR
   - `enricher.py` → identique (Exa/Jina cherchent en FR aussi)
   - `contact_finder.py` → adapter pour DSI/DAF au lieu de CIO/CFO
   - `db.py` → identique
   - `scheduler.py` → identique

4. Frontend : changer les labels UK → FR, garder toute l'architecture

**Effort estimé : 2-3 jours** pour adapter à un nouveau domaine/pays.

**Architecture finale (17 scrapers) :**
- Scrapers officiels OCDS (3-6) : Find a Tender, Contracts Finder, PCS, Sell2Wales, TED
- Scrapers web génériques (3-4) : Google News, Tavily, Exa, Brave
- Scrapers intelligents (3) : Firecrawl Agent, Crawl4AI, Jina
- Scrapers spécialisés (5) : WhatDoTheyKnow, Jobs, Companies House, Contract Registers, GCA Frameworks
- Signal précoce (1) : Committee Minutes (12-24 mois avant tender)

---

### Démarrage local (WSL2)

```bash
# Backend
cd /mnt/c/Erpscraper/backend
pip3 install -r requirements.txt --break-system-packages
# pip install pandas openpyxl --break-system-packages  # pour contract registers
cp .env.example .env && nano .env  # remplir les clés
python3 main.py
# → http://localhost:8002/health doit répondre {"status":"ok"}

# Frontend (dev)
cd /mnt/c/Erpscraper
npm install    # OBLIGATOIRE depuis WSL (node_modules Windows ≠ Linux)
npm run dev -- --host
# → http://localhost:5173

# Frontend (prod locale — plus stable)
npm run build
cd dist && python3 -m http.server 4000 --bind 0.0.0.0
# → http://localhost:4000
```

---

### Leçons apprises (mai 2026)

- **`export default` dans le mauvais composant** → page blanche. Toujours vérifier que `export default function App()` est sur le bon composant.
- **`import` après `const`** → crash ES module silencieux. Toutes les `import` doivent précéder les `const` au niveau module.
- **CORS `allow_origins=["*"]` + `allow_credentials=True`** → invalide en navigateur. Choisir l'un ou l'autre.
- **SQLite vs PostgreSQL** : SQLite suffisant pour scraper mono-utilisateur. Ne pas surarchitecturer.
- **pandas sur WSL2 system Python** : `pip install pandas openpyxl --break-system-packages` (pas de venv sur cette machine).
- **Crawl4AI sur Ubuntu 24.04** : `libatk1.0-0` → `libatk1.0-0t64`, `libcups2` → `libcups2t64`, `libasound2` → `libasound2t64`.
- **node_modules WSL2** : toujours `npm install` depuis WSL, jamais depuis PowerShell Windows.
- **APScheduler dans FastAPI** : démarrer dans `lifespan()`. `asyncio.create_task(run_scan())` pour le 1er scan immédiat.
- **LLMExtractionStrategy Crawl4AI** : `Setting 'provider' is deprecated → utiliser `llm_config=LLMConfig(provider=...)`.
- **data.gov.uk OCDS API** : retourne HTTP 301 → utiliser `follow_redirects=True` avec httpx.
- **Exa.ai** est le meilleur outil de recherche neurale gratuite (1000/mois). Excellent pour trouver des board papers, IT strategies, documents non indexés par Google.
- **Jina Search** (`s.jina.ai/{query}`) = recherche web gratuite 100%, sans clé, retourne contenu complet. Idéal comme fallback.
- **WhatDoTheyKnow FOI** : la JSON API retourne souvent 403. Toujours prévoir le fallback RSS.
- **TED Europa v3 API** : filtre `CY: ["GB", "IE"]` pour les notices UK/Ireland post-Brexit.
- **Contract registers data.gov.uk** : les colonnes ont des noms très variables entre councils → toujours utiliser une détection fuzzy (`_cr_find_col`) plutôt que des noms hardcodés.
- **Port 8002** : 8001 occupé par Happi-CRM sur cette machine. Adapter le port selon la machine.

---

*Ajouté : 2026-05-26 — Section 21 — ERP Scraper UK Intelligence Platform*
*Mis à jour : 2026-05-29 — 15 scrapers, Contact Intelligence, Account Profile, Email Outreach, Contract Registers, Exa Neural Search*
*Mis à jour : 2026-05-31 — 17 scrapers (plan) : GCA Framework, Linkup, Firecrawl /v2/agent, Committee Minutes*
*Mis à jour : 2026-06-09 — P1 : GCA Framework scraper + Exa 8 queries + Linkup priority #1 · P2 : Firecrawl /v2/agent (2 prompts, fallback /v1) · P3 : Committee Minutes (Jina 6q + Exa 4q, signal M-18)*

---

## 22. H'APPI WEBSITE — ARCHITECTURE BLOG

> Site vitrine corporate H'appi avec blog bilingue FR/EN + agrégateur de news live.
> Repo : `github.com/nbayonne76-ui/h-appi-website` (branch `main`)
> Deploy : h-appi-website.vercel.app
> **Référence pour tout nouveau blog Next.js multilingue avec articles statiques + news live.**

---

### Stack

```
Next.js 15 App Router + TypeScript
Tailwind CSS + @tailwindcss/typography  ← prose classes pour article body
Framer Motion 11                        ← animations (hover, stagger, transitions)
next-intl 4                             ← i18n (fr + en, défaut fr)
Resend 6                                ← formulaire newsletter + contact
Lucide React                            ← icônes
```

---

### Architecture blog — Vue d'ensemble

```
lib/blog-data.ts               → types + helpers (getArticles, getArticleBySlug…)
messages/fr.json               → métadonnées articles en français (blogData.articles)
messages/en.json               → métadonnées articles en anglais
app/[locale]/blog/page.tsx     → listing blog (client component)
app/[locale]/blog/[slug]/page.tsx → détail article (server component, SSG)
components/blog/
  ArticleCard.tsx              → carte article (variant featured + standard)
  ArticleLayout.tsx            → layout article (header + prose + sidebar)
  BlogCategoryNav.tsx          → navigation catégories
  BlogNewsletter.tsx           → bloc newsletter bas de page
  NewsSection.tsx              → agrégateur news live (client component)
  NewsCard.tsx                 → carte news individuelle
app/api/news/route.ts          → API route news (RSS aggregator, ISR 1h)
```

---

### Modèle de données (`lib/blog-data.ts`)

```typescript
export type Article = {
  slug: string;
  title: string;
  excerpt: string;
  category: string;         // 'Produit' | 'Guide' | 'Tendances' | 'Conformité' (FR)
  categoryColor: string;    // classe Tailwind pour le badge
  accentHex: string;        // couleur hex pour gradients + icônes
  date: string;
  readTime: string;
  author: string;
  authorRole: string;
  featured?: boolean;       // true sur l'article index 0
};
```

**Pattern clé — données séparées du contenu** :
- Métadonnées (title, excerpt, date…) → `messages/fr.json` et `messages/en.json` sous `blogData.articles`
- Slugs → tableau hardcodé dans `blog-data.ts` (contrôle manuel des URLs)
- Corps de l'article → composants React inline dans `[slug]/page.tsx` (pas de CMS ni MDX)

```typescript
// blog-data.ts
const slugs = ['mon-slug-1', 'mon-slug-2', ...];  // 1:1 avec blogData.articles

export function getArticles(locale: string): Article[] {
  const data = (messages[locale] || messages.fr).blogData.articles;
  return data.map((item, index) => ({
    slug: slugs[index],
    ...item,
    categoryColor: categoryColors[item.category] || 'bg-gray-100 text-gray-700',
    accentHex: categoryAccent[item.category] || '#3B82F6',
    featured: index === 0,   // ← toujours le premier article
  }));
}
```

**Mapping catégories → couleurs** :
| Catégorie (FR) | Catégorie (EN) | Couleur | Hex |
|---|---|---|---|
| Produit | Product | happi-blue | `#3B82F6` |
| Guide | Guide | happi-green | `#10B981` |
| Tendances | Trends | purple-400 | `#c084fc` |
| Conformité | Compliance | red-400 | `#f87171` |

---

### Page listing blog (`app/[locale]/blog/page.tsx`)

`'use client'` — requis pour l'état des filtres et les animations.

**Sections** :
1. Hero avec stats (nb articles, catégories, sources live, fréquence)
2. Navigation catégories avec compteurs
3. Article "À la une" (index 0, variant `featured`)
4. Tab bar : toutes les catégories + onglet "Actualités/News" spécial
5. Grille articles (2 cols sm / 3 cols lg) avec stagger Framer Motion
6. Section newsletter bas de page

**Onglet News** : affiche `<NewsSection />` au lieu de la grille d'articles — données live via `/api/news`.

```tsx
// Catégories dynamiques — construction de la tab bar
const allCategories = [allLabel, newsLabel, ...categories.slice(1)];
// newsLabel = 'Actualités' (fr) | 'News' (en)
// allLabel = categories[0] = 'Tous' / 'All'
```

---

### Page détail article (`app/[locale]/blog/[slug]/page.tsx`)

Server component (pas de `'use client'`).

```typescript
// SSG : génère toutes les combinaisons locale × slug
export async function generateStaticParams() {
  const locales = ['fr', 'en'];
  return locales.flatMap(locale => slugs.map(slug => ({ locale, slug })));
}

// SEO auto depuis les métadonnées de l'article
export async function generateMetadata({ params }) {
  const article = getArticleBySlug(locale, slug);
  return { title: `${article.title} — H'appi Blog`, description: article.excerpt };
}
```

**Corps d'article** : composants React inline (`function Article1_FR()`, `function Article1_EN()`).
Pas de MDX, pas de CMS — contenu hardcodé dans le fichier.

**Rendu** :
```typescript
<ArticleLayout
  article={article}
  sources={[{ name: 'Gartner', url: '...', detail: '...' }]}
  toc={[{ id: 'probleme', label: 'Le problème' }, ...]}
  relatedArticles={getRelatedArticles(locale, slug)}
>
  <Article1_FR />   {/* ou Article1_EN selon locale */}
</ArticleLayout>
```

---

### ArticleLayout (`components/blog/ArticleLayout.tsx`)

Layout 2 colonnes : `prose` (article) + sidebar sticky.

```tsx
// Classes prose (via @tailwindcss/typography)
<article className="prose prose-lg max-w-none
  prose-headings:text-white prose-headings:font-bold
  prose-a:text-happi-blue prose-a:no-underline hover:prose-a:underline
  prose-strong:text-white">
  {children}
</article>

// Sidebar sticky
<aside className="space-y-8 lg:sticky lg:top-24 lg:self-start">
  {/* TOC : liens href="#id" */}
  {/* Sources : liens externes */}
  {/* CTA : bouton contact modal */}
</aside>
```

---

### ArticleCard (`components/blog/ArticleCard.tsx`)

Deux variants contrôlés par la prop `featured`.

**Featured** (grande carte) :
- Header visuel coloré (`accentHex` en gradient)
- Barre top `h-1.5` en dégradé `accentHex → accentHex60`
- Titre en `text-2xl md:text-3xl`
- Hover `y: -3` (Framer Motion spring)

**Standard** (petite carte) :
- Header catégorie compact
- `line-clamp-3` sur l'excerpt
- Hover `y: -2`
- Flex column avec `flex-1` pour hauteur uniforme en grille

```tsx
// Pattern commun aux 2 variants
<div className="h-1.5 w-full"
  style={{ background: `linear-gradient(90deg, ${article.accentHex}, ${article.accentHex}60)` }}
/>
// "Lire l'article" + ArrowRight apparaissent uniquement au hover (opacity-0 → group-hover:opacity-100)
```

---

### Agrégateur news live

**API Route** (`app/api/news/route.ts`) :
```typescript
export const revalidate = 3600;  // ISR : rebuild toutes les heures

// 15 sources RSS/API
const FEEDS: FeedDef[] = [
  { name: 'Hacker News', url: 'https://news.ycombinator.com/rss', ... },
  { name: 'Dev.to', url: 'https://dev.to/feed/tag/ai', tagged: true, ... },
  // Dev.to (chatbot, webdev), InfoQ, The New Stack, CSS-Tricks, Smashing Mag,
  // Medium (chatbot, AI), Reddit (ML, webdev, programming), TechCrunch, Product Hunt
];

// Filtres appliqués :
// 1. Langue : EN/FR seulement (bloque Cyrillic, Arabic, CJK, Turkish, Polish)
// 2. Spam : regex casino/betting/seo/crypto...
// 3. Pertinence : keywords IA/chatbot/tech pour feeds non-tagués
// 4. Dedup : Set<url>
// 5. Sort newest first, cap 80 items

// Cache HTTP Vercel edge
'Cache-Control': 'public, s-maxage=3600, stale-while-revalidate=7200'
```

**Important** : pas de bibliothèque rss-parser — parser XML custom (support CDATA, Atom, RSS2).

**Client Component** (`NewsSection.tsx`) :
- Fetch `/api/news` au mount
- Tabs sources avec compteurs (HN, Dev.to, TechCrunch, Medium, Reddit, etc.)
- Pagination : 12 items/page, bouton "Load more"
- Skeleton loading (9 cards pulsantes)
- Bouton Refresh (cache-buster `?t=Date.now()`)
- `AnimatePresence` sur la grille au changement de source

---

### i18n avec next-intl v4

```typescript
// i18n/config.ts
export const locales = ['fr', 'en'] as const;
export const defaultLocale: Locale = 'fr';

// Structure URLs : /fr/blog, /en/blog
// Dynamic segment : app/[locale]/...
```

**Données article dans les JSON de traduction** :
```json
// messages/fr.json
{
  "blogData": {
    "articles": [
      {
        "title": "Mon article",
        "excerpt": "...",
        "category": "Produit",
        "date": "15 mai 2026",
        "readTime": "5 min",
        "author": "Nada Bayonne",
        "authorRole": "Fondatrice H'appi"
      }
    ]
  },
  "blog": {
    "categories": ["Tous", "Produit", "Guide", "Tendances", "Conformité"],
    "badge": "...", "title": "...", "subtitle": "...", ...
  }
}
```

---

### Comment ajouter un nouvel article

1. Ajouter le slug dans le tableau `slugs` de `lib/blog-data.ts`
2. Ajouter les métadonnées dans `messages/fr.json` et `messages/en.json` → `blogData.articles` (même index)
3. Créer les composants `ArticleN_FR()` et `ArticleN_EN()` dans `app/[locale]/blog/[slug]/page.tsx`
4. Ajouter le cas dans le switch de rendu du même fichier

**Règle** : les tableaux `slugs` et `blogData.articles` doivent toujours avoir la même longueur et le même ordre.

---

### Leçons apprises

- **Corps d'article en React components** (pas MDX) = moins de dépendances, meilleure performance, possibilité de JSX avancé dans l'article. Convient quand le contenu est écrit une seule fois par développeur.
- **`@tailwindcss/typography`** : nécessite `prose-invert` ou des overrides custom sur fond sombre (ex: `prose-headings:text-white`).
- **`'use client'` sur la page listing** : obligatoire pour l'état des filtres et les animations Framer Motion — mais le détail reste server component (SEO optimal).
- **ISR vs SSG pour les news** : `revalidate = 3600` sur la route API = données fraîches toutes les heures sans rebuild full.
- **Parser XML custom** : plus léger qu'`rss-parser`, supporte CDATA + Atom + RSS2. Indispensable pour agréger des sources hétérogènes.
- **Filtres langue sur les feeds RSS** : sans filtre, ~30% des items sont en cyrillique, arabe ou turc. Le regex multi-script couvre tous les cas sans librairie de détection.

---

*Ajouté : 2026-05-30 — Section 22 — H'appi Website Blog (blog statique + news live, next-intl v4, ISR)*
