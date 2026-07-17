---
name: happi-brain-platforms
description: "Plateformes H'appi — DropOS (SaaS dropshipping), Quality Tracking App (Expo+FastAPI multi-rôle), TopTier (e-commerce), Microsoft Sales App (67 solutions D365/Azure bilingues, KB enrichissement en cours juillet 2026, 6 solutions 100%, Foundry+Blueprints nouveaux)"
metadata: 
  node_type: memory
  type: project
  originSessionId: a4910c74-de49-44dc-8288-af394838a719
---

# HAPPI BRAIN — PLATEFORMES & SAAS

## 1. DropOS (SaaS dropshipping)
- **Repo** : `DropOS-DropShipping`
- **Type** : Plateforme SaaS all-in-one pour dropshippers
- **Stack** : Next.js + FastAPI + PostgreSQL + JWT
- **Target** : Dropshippers $10K-$200K/mois
- **Pricing** : $99-149/mois (remplace $400-1000/mois d'outils)
- **Roadmap** : Phase 1 Analytics → Phase 2 Fulfillment → Phase 3 Sourcing → Phase 4 Marketing
- **Intégrations** : Shopify Partner API, tarifs douaniers US HTS / EU TARIC

---

## 2. Quality Tracking App (Mobilier de France)
- **Repo** : `Quality-tracking-app`
- **Branch principale** : `workflow/admin`
- **Type** : App mobile de suivi qualité livraisons meubles (multi-rôle)

### Stack complète
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

### Architecture mobile
```
mobile/src/
  navigation/AppNavigator.tsx      → React Navigation v6
  screens/
    supplier/             → Home, Deliveries, ProductPhotos, TruckLoading, Profile
    driver/               → Home, Deliveries, DeliveryDetail, Profile
    client/               → TrackingInput, DeliveryCard, Tracking, DeliveryDetail, Signature
    admin/                → Dashboard, LiveTracking, Statistics, Profile
  store/useStore.ts           → Zustand (auth + deliveries + stats + offline + error)
  services/api.ts             → ApiService class (JWT, auto-refresh, getBaseUrl())
  services/offlineSync.ts     → sync queue avec AsyncStorage
  services/storage.ts         → expo-secure-store / localStorage abstraction
  types/index.ts              → types centralisés
  constants/delivery.ts       → STATUS_LABELS, STATUS_FLAT_COLORS
```

### Pattern ApiService (à réutiliser)
```typescript
const API_BASE_URL = process.env.EXPO_PUBLIC_API_URL
  || (__DEV__ ? 'http://localhost:8001/api' : 'https://api.example.com/api');

class ApiService {
  // getBaseUrl() → retire /api pour construire URL fichiers statiques
  // setTokens() / clearTokens() → gestion stockage sécurisé
  // request<T>() → helper avec auth header auto + refresh token
}
```

### Pattern Zustand Store (à réutiliser)
```typescript
// État : user, isAuthenticated, isLoading, deliveries, stats, error, isOnline, pendingSyncItems
// Offline queue : addPendingSyncItem() + syncPendingItems() → AsyncStorage
// Auth : login(), logout(), loadUser()
// Données : fetchDeliveries(), fetchDelivery(), updateDeliveryStatus(), fetchStats()
```

### Utilisateurs test (password: `Password123`)
| Rôle | Email |
|------|-------|
| Admin | admin@mobilierdefrance.com |
| Supplier | fournisseur@example.com |
| Driver | chauffeur@mobilierdefrance.com |
| Client | client@example.com |

### Leçons apprises
- `react-native-webview` est un peer dep **obligatoire** de `react-native-signature-canvas`
- Port 8000 bloqué sur WSL2 → **toujours démarrer FastAPI sur 8001**
- Path aliases TypeScript (`@/`) doivent être déclarés dans `tsconfig.json` ET dans `path-intellisense.mappings`
- `npm audit fix` peut nécessiter 2 passes
- Zustand avec AsyncStorage = pattern offline robuste pour apps de terrain (chauffeurs sans réseau)

---

## 3. Top Tier Collection (e-commerce)
- **Repo** : `toptiercollection.shop`
- **Type** : Site e-commerce
- **Stack** : Next.js + Sanity CMS + TypeScript + Tailwind

---

## 4. MICROSOFT SALES APP — BASE DE CONNAISSANCE COMMERCIALE

- **Repo** : `github.com/nbayonne76-ui/microsoft-sales-app` (branch `main`)
- **Stack** : Next.js 15 App Router + JavaScript + Tailwind CSS
- **Data** : JSON statique `data/azure-solutions.json` — **58 solutions** au total
- **Deploy** : Vercel auto-deploy sur push `main`
- **Git remote** : `ssh://ssh.github.com:443/nbayonne76-ui/microsoft-sales-app.git` (port 443 WSL2)

### Architecture des données — 58 solutions par catégorie
| Catégorie | Nb | Tab UI |
|-----------|-----|--------|
| `business` | 16 | Dynamics |
| `modern-work` | 3 | Azure |
| `ai` | 4 | Azure |
| `analytics` | 4 | Azure |
| `compute` | 7 | Azure |
| `security` | 4 | Azure |
| `storage` | 3 | Azure |
| `management` | 10 | Azure |
| `networking` | 2 | Azure |
| `integration` | 3 | Azure |
| `iot` | 1 | Azure |
| `development` | 2 | Azure |

**Règle catégorie / tab UI** :
- `category === 'business'` → onglet **Dynamics**
- tout le reste (y compris `modern-work`) → onglet **Azure**

### Système bilingue EN/FR

```javascript
// API route : app/api/azure-solutions/route.js
const LANG_FIELDS = [
  'shortDescription','fullDescription','keyFeatures','benefits','useCases',
  'estimatedCost','implementationTime','idealCustomerSize'
];

function applyLang(solutions, lang) {
  return solutions.map(s => {
    const out = { ...s };
    for (const field of LANG_FIELDS) {
      const variant = s[field + (lang === 'fr' ? 'Fr' : 'En')];
      if (variant !== undefined) out[field] = variant;
    }
    return out;
  });
}
// Usage : GET /api/azure-solutions?lang=en|fr
```

**Règle critique** : Si le champ base (`shortDescription`) est en FR, ajouter OBLIGATOIREMENT `shortDescriptionEn`. Sinon le switch de langue ne fonctionne pas.

### Pattern cache API Route Next.js
```javascript
let _cache = null;
function loadSolutions() {
  if (_cache) return _cache;
  const raw = readFileSync(join(process.cwd(), 'data', 'solutions.json'), 'utf-8');
  _cache = JSON.parse(raw).map(s => { /* parse JSON_FIELDS */ return s; });
  return _cache;
}
// Invalider via POST { action: 'invalidate-cache' }
// Headers : 'Cache-Control': 'public, s-maxage=3600, stale-while-revalidate=7200'
```

### Pattern switch de langue (remount forcé React)
```jsx
<DynamicsSolutionDetail
  key={lang + selectedSol.id}     // ← force remount complet
  solution={selectedSol}
  lang={lang}
/>
useEffect(() => {
  if (selectedSol) {
    const updated = solutions.find(s => s.id === selectedSol.id);
    if (updated) setSelectedSol(updated);
  }
}, [solutions]);
```

### Script Python mise à jour JSON en masse
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
# ✅ Toujours matcher par officialName (pas par id tronqué)
# ✅ ensure_ascii=False pour conserver les accents
```

### D365 2026 Release Wave 1 — Features clés (Avr–Sep 2026)

| Solution | Feature | Disponibilité |
|----------|---------|---------------|
| D365 Sales | Sales Research Agent (préparation réunions auto) | GA Avr 2026 |
| D365 Sales | Sales Close Agent | GA Jun 2026 |
| D365 Customer Service | Case Management Agent (shadow mode) | GA Mai 2026 |
| D365 Finance | French e-invoicing (obligatoire Sep 2026) | GA Août 2026 |
| D365 Finance | MCP for ERP Analytics (langage naturel) | GA Sep 2026 |
| D365 SCM | Supplier Communications Agent | GA Jun 2026 |
| D365 Business Central | Custom AI agent design in-product | GA Mai 2026 |
| D365 Business Central | French e-invoicing | GA Jul 2026 |

### Pricing D365 (référence vendeurs)
| Solution | Prix de départ |
|----------|---------------|
| D365 Sales | $65/user/mois (Pro) |
| D365 Customer Service | $50/user/mois (Pro) |
| D365 Finance | $180/user/mois |
| D365 Business Central | $70/user/mois (Essential) |
| Microsoft 365 Copilot | $30/user/mois |

### Audit sécurité résolu (mai 2026)
- Auth ajoutée sur 6 routes API (`getServerSession`) : `/api/ai-agent`, `/api/account-intel`, `/api/generate-kb-email`, `/api/dashboard/brief`, `/api/sequences/generate`, `/api/knowledge-base`
- 3 fichiers morts supprimés (-1522 lignes)
- `lib/api-error.js` helper partagé créé (voir [[happi-brain-prompts]])

---

## MICROSOFT SALES APP — Mise à jour majeure Juin 2026

### État de l'app (juin 2026)
- **URL prod** : `https://microsoft-sales-app.vercel.app`
- **Toutes les features IA opérationnelles** sur Vercel
- **AI provider** : OpenAI GPT-4o (`OPENAI_API_KEY` dans Vercel)
- **`ANTHROPIC_API_KEY` NON configuré sur Vercel** — utiliser OpenAI pour toutes les routes

### Variables d'environnement Vercel (état réel)
```
DATABASE_URL     = file:/tmp/dev.db       (fallback build — SQLite vide en /tmp)
NEXTAUTH_URL     = https://microsoft-sales-app.vercel.app
NEXTAUTH_SECRET  = b8ee543d...            (dans vercel.json — sessions persistantes)
OPENAI_API_KEY   = sk-proj-...            (GPT-4o — toutes les features IA)
TAVILY_API_KEY   = ...                    (Account Intel + blog news)
```

### Problèmes Vercel résolus — règles critiques à retenir

1. **`prisma generate` dans `postinstall` échoue sur Vercel** si `DATABASE_URL` absent ET si `node_modules` est caché (postinstall skippé). **Fix** : mettre dans `build` script : `"build": "node scripts/prisma-generate.js && next build"`. Le script injecte `DATABASE_URL=file:/tmp/dev.db` si absent.

2. **`NEXTAUTH_SECRET` fixe obligatoire** sur Vercel — chaque déploiement sans secret fixe génère un random → toutes les sessions invalidées → 401 sur toutes les routes protégées. Configurer dans `vercel.json` ou dashboard Vercel.

3. **`revalidate = 3600` sur une route API** force Next.js à exécuter le handler au build → timeout possible. Utiliser `export const dynamic = 'force-dynamic'` à la place.

4. **`maxDuration = 60`** sur les routes avec scraping (Account Intel) — Vercel coupe à 10s par défaut sur Hobby.

5. **`getServerSession` retourne null** si `NEXTAUTH_SECRET` n'est pas défini ou a changé. Les routes IA de cette app sont publiques (pas de données sensibles) → auth supprimée.

### Architecture Account Intel — Happi Brain Phase 7 (tool_use OpenAI)

**Pattern** : 6 recherches fixes en parallèle → 1 appel GPT-4o → JSON dossier

```javascript
// pipeline (app/api/account-intel/route.js)
const [govData, news, itSignals, jobs, website, tavily] = await Promise.allSettled([
  fetchGovData(company),    // API gouv.fr — effectif EXACT, SIREN, NAF (GRATUIT)
  ddgSearch(`"${company}" actualités 2025`),
  ddgSearch(`"${company}" cloud Microsoft transformation`),
  ddgSearch(`"${company}" recrutement DSI cloud`),
  ddgSearch(`"${company}" site officiel`).then(fetchWebsite),
  tavilySearch(`${company} stratégie IT`),
]);
// → 1 appel GPT-4o (temperature 0.2, max_tokens 4096) → JSON SWOT+PESTEL
```

**Sources gratuites validées** :
- `recherche-entreprises.api.gouv.fr` → effectif exact, SIREN, NAF, date création — GOLD pour entreprises FR
- `r.jina.ai/{URL}` → fetch URL libre (sites web, pages publiques)
- `html.duckduckgo.com/html/?q=...` via `r.jina.ai` → résultats web sans clé

**Sources qui NE marchent PAS gratuitement** :
- `s.jina.ai` (search) → requiert clé payante maintenant
- `pappers.fr` → Cloudflare protection
- `builtwith.com`, `linkedin.com` → bot protection / login requis

**Bug OpenAI tool_use critique** : ne jamais reconstruire `{ role, content, tool_calls }` manuellement. Toujours pousser `choice.message` directement :
```javascript
messages.push(choice.message); // ✅ — content est null quand tool_calls présent
// messages.push({ role, content, tool_calls }); // ❌ — content: null casse l'appel suivant
```

### Architecture Blog News — Pipeline 3 sources

```javascript
// app/api/blog/news/route.js
const [rssResults, tavilyItems, ddgItems] = await Promise.allSettled([
  Promise.all(RSS_FEEDS.map(fetchRSS)),  // 8 feeds RSS Microsoft officiels
  fetchTavily(),                          // 5 requêtes Tavily "Microsoft X 2026"
  fetchDDG(),                             // DuckDuckGo via Jina — temps réel
]);
// Cache 30min (s-maxage=1800), 40 articles max, dédup par URL, triés par date
```

**8 RSS feeds** : `blogs.microsoft.com`, `azure.microsoft.com/blog`, `microsoft.com/m365/blog`, `cloudblogs.microsoft.com/dynamics365`, TechCommunity (microsoft365blog, AzureInfrastructureblog, MicrosoftSecurityandCompliance), `cloudblogs.microsoft.com/microsoftsecure`

### KB Service — Architecture 2 couches

```javascript
// lib/kb-service.js
// PRIORITÉ 1 : Blog articles (lib/blog-articles.js) — informations les plus récentes
// PRIORITÉ 2 : Fichiers MD (templates/knowledge-base/) — référence détaillée

const BLOG_TO_KB = {
  m365: ['m365'], copilot: ['m365'], azure: ['azure'],
  dynamics: ['dynamics'], securite: ['security'],
};
// getFullKb(), getKbByTopic(), getKbByTopics() → injectent le blog content AVANT les MD
```

**Impact** : ajouter un article de blog → Account Intel, Email Generator, Séquences, Agent IA utilisent automatiquement les nouvelles infos.

### Blog bilingue — Structure article obligatoire

```javascript
// lib/blog-articles.js — TOUJOURS avoir sections EN et FR
{
  slug: 'article-slug',
  category: 'm365', // m365 | copilot | azure | dynamics | securite
  fr: { title, excerpt, sections: [...] },
  en: { title, excerpt, sections: [...] },  // ← OBLIGATOIRE sinon fallback FR même en EN
}
// Section types : intro | h2 | p | list | pricing | cta
// Merge page : { ...article.fr, ...article.en } — en.sections écrase fr.sections
```

### Commits clés session juin 2026
```
3104a29  feat: kb-service — blog articles feed knowledge base automatically
dfe8e62  fix: blog article — pass isFr to renderSection for pricing table headers
fe18086  fix: add English sections to all 5 blog articles
8da146a  feat: blog news — 3-source pipeline RSS+Tavily+DDG real-time
b586bfc  feat: account-intel Phase 1 — 6 fixed parallel searches, no AI randomness
177a35e  feat: account-intel — Phase 1 roadmap — gov API + DDG search
1bcd671  fix: account-intel tool_use loop — use choice.message directly
30ad983  feat: account-intel — Happi Brain Phase 7 tool_use architecture
f41b8c8  fix: add NEXTAUTH_SECRET + NEXTAUTH_URL to vercel.json
a63076a  (revert) migrated to Claude then back to OpenAI (ANTHROPIC_API_KEY absent Vercel)
b6dd679  fix: remove getServerSession from all AI routes — fixes Unauthorized error
ddffa3f  fix: unblock Vercel build — prisma generate fallback + KB auth removed
```

---

## MICROSOFT SALES APP — Mise à jour majeure Juillet 2026

### État de l'app (13 juillet 2026)
- **URL prod** : `https://microsoft-sales-app.vercel.app`
- **Base Neon Postgres** (migration depuis SQLite /tmp — commit `6b419fe`)
- **Auth routes IA** : `lib/ai-guard.js` → `requireAiAccess()` utilise IP rate-limit si pas de session (plus de 401)
- **6 agents continus** déployés (voir section Agents)
- **Prix M365 mis à jour** au 1er juillet 2026 dans 8 fichiers KB
- **Nouveau fichier KB** : `templates/knowledge-base/m365-roadmap-fy27.md`

### Variables d'environnement Vercel (état juillet 2026)
```
DATABASE_URL          = neon postgres pooled URL    (dashboard Vercel)
DATABASE_URL_UNPOOLED = neon postgres direct URL    (dashboard Vercel)
NEXTAUTH_URL          = https://microsoft-sales-app.vercel.app  (vercel.json)
NEXTAUTH_SECRET       = [retiré de vercel.json pour sécurité]  (dashboard Vercel)
OPENAI_API_KEY        = sk-proj-...                 (dashboard Vercel)
TAVILY_API_KEY        = ...                         (dashboard Vercel)
```

### Règles critiques Vercel Hobby — Juillet 2026

6. **Vercel Hobby = 2 crons max** — au-delà, le build échoue silencieusement et Vercel sert
   l'ancienne build. Fix : un orchestrateur unique (`/api/cron/orchestrator`) + `refresh-news`.

7. **`/tmp` NON partagé entre instances serverless** — écrire dans `/tmp` depuis une function
   et lire depuis une autre GET route → fichier introuvable. Fix : `localStorage` côté client
   pour persister les rapports d'agents entre rechargements (single-user app).

8. **Appels HTTP internes Vercel (fetch vers même deployment) → échouent avec 500** sans raison
   documentée. Fix : exporter les fonctions core des agents et les appeler directement depuis
   l'orchestrateur (pas de fetch HTTP interne).

9. **`writeFileSync` vers `data/` échoue sur Vercel** (EROFS — read-only). Écrire dans `/tmp/`
   pour les fichiers runtime. Les fichiers bundlés au build (`data/blog-articles.json`, etc.)
   sont lisibles mais pas modifiables. Utiliser DB ou localStorage pour persistance runtime.

10. **`lib/ai-guard.js` pattern** — guard IA qui accepte les utilisateurs sans session :
    ```javascript
    // requireAiAccess() : session → rate-limit par user.id, sinon → rate-limit par IP
    // getServerSession() enveloppé dans try/catch (DB failure → fallback IP)
    ```

### Architecture Agents — 6 agents continus (juillet 2026)

**2 crons Vercel** :
- `0 6 * * *` → `/api/cron/refresh-news` (blog news cache)
- `0 5 * * *` → `/api/cron/orchestrator` (lance Health + KBDrift + ArticleQuality)

**Orchestrateur** (`app/api/cron/orchestrator/route.js`) :
- Import direct : `runHealthCheck()`, `runKbDrift()`, `runArticleQuality()`
- Pas de fetch HTTP interne (évite le bug Vercel)
- Retourne tout en une réponse → frontend sauvegarde en localStorage

**Agents manuels** (boutons UI → localStorage) :
| Agent | Bouton | Stockage |
|-------|--------|---------|
| Buying Signal Monitor | Dashboard "Scanner" | `localStorage['agent_signals']` |
| Weekly Brief | Dashboard "Générer" | `localStorage['agent_brief']` |
| MS Watcher | KB "Rescanner" | `localStorage['agent_watcher']` |

**Agents auto** (via orchestrateur → localStorage depuis DashboardHome) :
| Agent | Stockage |
|-------|---------|
| Health Monitor | `localStorage['agent_health']` |
| KB Drift | `localStorage['agent_drift']` |
| Article Quality | quality log `/tmp/` |

### Prix M365 — Juillet 2026 (effectifs 1er juillet 2026)
| Plan | Ancien | Nouveau |
|------|--------|---------|
| Business Basic | $6 | **$7** |
| Apps for Business | $8.25 | **$10** |
| Business Standard | $12.50 | **$14** |
| M365 E3 | $36 | **$39** |
| M365 E5 | $57 | **$60** |
| Office 365 E3 | $23 | **$26** |
| Office 365 E5 | $38 | **$41** |
| M365 F1 | $2.25 | **$3** |
| M365 F3 | $8 | **$10** |

### Commits clés session juillet 2026
```
af9fecc  fix: ai-guard — wrap getServerSession in try/catch for DB resilience
285b70d  fix: ai-guard — allow public access with IP-based rate limiting
d69cf08  feat(agent-1): KB Drift Detector — scan prix obsolètes lundi 7h
ecac765  feat(agent-2): Blog Article Quality Agent — score + auto-fix
4d7453c  feat(agent-3): API Health Monitor — surveillance 7 routes toutes les 4h
3a0d762  feat(agent-P0): Buying Signal Monitor — surveillance comptes cibles
1932e41  feat(agent-P1): Weekly Sales Brief — synthèse commerciale lundi 8h30
43697cc  feat(agent-P2): MS Announcement Watcher — TODOs KB automatiques
b70a8fa  fix: orchestrateur unique — Vercel Hobby = 2 crons max
f030e70  fix: orchestrateur — import direct au lieu d'appels HTTP internes
900670f  fix: localStorage persistence — contourne /tmp non-partagé
098c501  feat: update M365 pricing — nouveaux tarifs juillet 2026
d6a63e5  feat: KB — M365 Roadmap FY27 + Copilot updates
```

---

*Mis à jour : 2026-07-13 — Session agents continus + fix Vercel + prix M365 juillet 2026*

---

## MICROSOFT SALES APP — Mise à jour majeure 17 Juillet 2026

### État de l'app (17 juillet 2026)
- **67 solutions** dans `data/azure-solutions.json` (était 65 → +2 nouvelles)
- **Enrichissement KB en cours** : alimentation systématique des champs FR + salesContext
- **Nouvelles solutions** : Azure Blueprints (migration), Microsoft Foundry (Azure AI Foundry)
- **Recatégorisation** : catégorie `development` créée et peuplée

### Protocole d'enrichissement KB (session juillet 2026)

**Méthode établie** : l'utilisateur envoie 2 URLs (page produit + docs principale), Claude :
1. Fetche la page docs hub → identifie les sous-pages clés automatiquement
2. Fetche 3-5 sous-pages en parallèle (overview, whats-new, prerequisites, pricing, concepts)
3. Crée/enrichit l'entrée JSON avec 7 champs obligatoires : `keyFeaturesEn/Fr`, `benefitsEn/Fr`, `useCasesEn/Fr`, `salesContext`
4. Commit + push GitHub → Vercel auto-deploy
5. **L'utilisateur N'A PAS besoin d'envoyer les sous-liens manuellement**

**Structure des champs enrichis** :
- `keyFeaturesEn/Fr` : 12-14 items (features détaillées avec contexte 2026)
- `benefitsEn/Fr` : 7-9 items (ROI, différenciateurs, stats chiffrées)
- `useCasesEn/Fr` : 4-6 cas d'usage avec `title`, `description`, `industries`, `businessImpact`
- `salesContext` : `targetPersonas`, `keyStats`, `painPoints`, `keyDifferentiators`, `competitiveEdge`, `whyNow`, `nextSteps`

### Recatégorisation — 17 juillet 2026

Catégorie `development` créée dans `app/knowledge-base/page.jsx` (ligne 27) mais était vide en JSON.
4 solutions déplacées depuis management/compute :

| Solution | Avant | Après |
|----------|-------|-------|
| Azure DevOps | management | **development** |
| Azure Repos | management | **development** |
| Azure DevTest Labs | compute | **development** |
| Azure Application Insights | management | **development** |

### Statut enrichissement — 17 juillet 2026

**6 solutions à 100%** (keyFeaturesFr + benefitsFr + useCasesFr + salesContext) :
- ✅ `Azure Machine Learning` — keyFeaturesFr(17) benefitsFr(9) useCasesFr(6). Nouveautés : Workload Identity Federation, Azure Event Grid ML lifecycle, Power BI dataflows integration
- ✅ `Microsoft 365 Copilot` — keyFeaturesFr(14) benefitsFr(9) useCasesFr(6). Nouveautés : Work IQ, Cowork GA juin 2026 (fastest Frontier adoption), Scout Public Preview, multi-model GPT-5.5+Claude Sonnet 5+Claude Opus 4.8, Legal Agent, Agent Mode Word/Excel/PPT, Agentic Email Outlook, Finance Workflows Excel, E7 $99/user
- ✅ `Azure Virtual Desktop (AVD)` — keyFeaturesFr(13) benefitsFr(9) useCasesFr(6). Nouveautés : Automated Host Pools + Dynamic Autoscaling GA juin 2026, RDP Multipath GA juillet 2026, AVD sur Azure Local (Arc-Enabled) Public Preview mai 2026, External Identity GA nov 2025, App Attach WS2025/2022 GA, RDP Shortpath UDP Private Link GA, Windows App FIDO/passkeys
- ✅ `Azure Policy` (renommé depuis "Azure Policy & Blueprints") — 13/9/6 items. Nouveautés : 8 effets policy (dont DenyAction), 30+ frameworks réglementaires intégrés (ISO 27001, NIST Rev4/5, CIS 2.0, FedRAMP High/Moderate, PCI DSS 4.0, SOC 2, CMMC Level 3, SWIFT, Spain ENS, NL BIO, Australian ISM...), identity-based policies (requestContext().identity MFA + blocage suppression), Azure Policy for Kubernetes (AKS + Arc via Gatekeeper/OPA), Machine Configuration OS, Arc multi-cloud, Policy-as-Code GitHub/ADO
- ✅ `Azure Blueprints (Migration → Deployment Stacks)` — **NOUVELLE ENTRÉE** (isActive: false, salesPriority: 4)
- ✅ `Microsoft Foundry (Azure AI Foundry)` — **NOUVELLE ENTRÉE** (salesPriority: 10)

**61 solutions encore à enrichir** (57-85%) — toutes ont keyFeaturesEn/benefitsEn/useCasesEn mais manquent les champs FR + salesContext

### Azure Blueprints — Retrait (CRITIQUE)

| Date | Action |
|------|--------|
| **31 juil 2026** (PASSÉ) | Plus de création de définitions/versions |
| **31 oct 2026** | Gel modifications définitions + assignations |
| **31 déc 2026** | Gel modifications assignations |
| **31 jan 2027** | Retrait complet — données non exportées **SUPPRIMÉES DÉFINITIVEMENT** |

**Remplacement Microsoft recommandé** :
- **Azure Deployment Stacks** (GA) = remplacement des assignments (lifecycle + deny settings DenyDelete/DenyWriteAndDelete, actionOnUnmanage)
- **Template Specs** (GA) = remplacement des définitions (stockage/versioning)
- **Pattern** : Template Specs (stockage) + Deployment Stacks (lifecycle) = 100% parité Blueprints
- Azure Advisor identifie automatiquement les clients utilisant Blueprints → opportunité de migration conseil

### Microsoft Foundry — Nouveau produit clé (ex Azure AI Foundry)

**Renommage** : Azure AI Studio → Azure AI Foundry → **Microsoft Foundry** (2026)
**Portal** : https://ai.azure.com
**Ancien portal classic** : https://ai.azure.com (toggle "New Foundry" activé)

**Architecture nouvelle** :
- Avant : Hub + Azure OpenAI + Azure AI Services (3 ressources)
- Maintenant : **Foundry resource** (1 ressource, avec projects)
- SDK unifié : `azure-ai-projects` 2.x (remplace `azure-ai-inference`, `azure-ai-generative`, `azure-ai-ml`, `AzureOpenAI()`)
- Endpoint unifié : compatible OpenAI (code existant OpenAI SDK fonctionne avec modifications minimales)
- API : Responses API (remplace Assistants API), routes stables `/openai/v1/`

**Catalogue modèles — 1 900+** :
| Famille | Meilleur pour |
|---------|--------------|
| GPT-5 | Plus puissant — raisonnement complexe, multimodal |
| GPT-4.1 | Équilibre qualité/coût production |
| GPT-4.1 mini | Rapidité, faible latence, haute volumétrie |
| Claude Sonnet 5 / Opus 4.8 | Raisonnement avancé, code, multimodal (Anthropic) |
| Grok (xAI) | Raisonnement, code, extraction données |
| Mistral | Code, multilingue |
| DeepSeek-R1 | Open-weight raisonnement à grande échelle |
| Phi-4 | On-device, edge, ressources contraintes |
| Meta Llama | Open, fine-tunable |

**Features clés 2026** :
- **Foundry IQ** : RAG enterprise intégré (documents SharePoint/OneDrive/web) avec réponses citées
- **Work IQ** (preview) : agents connectés au contenu M365 (Teams, Outlook, SharePoint)
- **Fabric IQ** (preview) : agents connectés aux données Microsoft Fabric
- **A2A Agent-to-Agent endpoints** (preview) : agents exposés comme endpoints découvrables par d'autres agents
- **Voice agents** (preview) : speech-to-speech, infrastructure hébergée
- **Routines** (preview) : workflows multi-étapes réutilisables pour agents
- **Model routing** (Responses API) : sélection automatique du modèle optimal par tâche
- **Instant access** (preview) : appel direct d'un modèle par nom sans créer un déploiement
- **Foundry Local** : LLMs on-device GRATUIT (HuggingFace), sans abonnement Azure
- **Foundry Labs** : hub preview (ai.azure.com/labs) des dernières recherches IA Microsoft
- **AI Red Teaming Agent** (preview) : tests adversariaux automatisés
- **Foundry Control Plane** : gestion agents à grande échelle, limites tokens, Azure Policy

**Pricing Foundry** :
- Plateforme : GRATUIT (exploration, portail, Foundry Local)
- GPT-4.1 mini : ~$0.15/1M tokens input
- GPT-4.1 : ~$2/1M tokens input
- GPT-5 : ~$2.50/1M tokens input
- Claude Sonnet 5 : ~$3/1M tokens input
- ROI calculator : aka.ms/Foundry-ROI-Calculator

### Connaissances produits nouvelles — 17 juillet 2026

**Azure Policy** :
- 8 effets : Deny, Audit, Modify, DeployIfNotExists, AuditIfNotExists, Append, Disabled, DenyAction
- `requestContext().identity` : enforce MFA à la création de ressources, bloquer suppression manuelle
- Kubernetes : Azure Policy + Gatekeeper (OPA) sur AKS et clusters Arc-enabled
- Machine Configuration : audit/enforcement paramètres OS VMs (pas seulement propriétés ARM)
- Azure Blueprints DÉPRÉCIÉ → Azure Deployment Stacks + Template Specs
- Limite : 500 définitions/périmètre, 200 initiatives/périmètre, 50 000 ressources/tâche remediation

**Azure Virtual Desktop** :
- Multi-session Windows 11/10 = EXCLUSIF Azure (Citrix/VMware ne peuvent pas offrir ça sur Azure)
- Aucun gateway/broker à gérer — Microsoft opère le plan de contrôle
- Dynamic Autoscaling GA juin 2026 : coût VMs inactives = 0
- RDP Multipath GA juillet 2026 : redondance TCP automatique
- HEVC/H.265 GPU acceleration GA juin 2025
- QuickStart : host pool Windows 11 multi-session en ~20 minutes (GA mars 2025)
- Compétiteur VMware Horizon : Broadcom acquisition → vague migration massive vers AVD
- Per-user access pricing pour utilisateurs externes (pas de licence M365 requise)

**M365 Copilot** :
- E7 $99/user/mois = E5 + Copilot + Agent 365 + Entra Suite (économie $18/user/mois vs séparé)
- Copilot Cowork GA juin 2026 : fastest Frontier adoption ever
- Claude Sonnet 5 dans Copilot : juillet 2026
- Claude Opus 4.8 dans Copilot : mai 2026
- GPT-5.5 Instant : mai 2026 (faible latence)
- Legal Agent (Word) : révision contrats avec modifications suivies
- Agent 365 (GA mai 2026) : plan de contrôle universel pour agents IA (shadow AI résolu)
- Work Trend Index 2026 : "Frontier Professionals" — 30-70% gains productivité

### Commits clés session 17 juillet 2026

```
885f977  feat: Microsoft Foundry (Azure AI Foundry) — nouvelle entrée complète
0461c41  feat: Azure Blueprints — fiche migration/transition (retrait jan 2027)
346dbd0  feat: Azure Policy — enrichissement complet + renommage (était 55%)
968ef42  feat: Azure Virtual Desktop — enrichissement complet (était 55%)
d4167fa  feat: Microsoft 365 Copilot — enrichissement complet (était 55%)
b2fc1ed  feat: Azure Machine Learning — keyFeaturesFr + benefitsFr + useCasesFr
b01cfe6  fix: recatégorisation — 4 solutions déplacées vers development
```

---

*Mis à jour : 2026-07-17 — Session KB enrichissement + nouvelles solutions Foundry+Blueprints + recatégorisation*
