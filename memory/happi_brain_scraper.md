---
name: happi-brain-scraper
description: "ERP Scraper UK — plateforme intelligence appels d'offres public britannique, 15 scrapers async, GPT-4o-mini scorer, Contract Registers, Contact Intelligence, patterns réutilisables pour autres domaines"
metadata: 
  node_type: memory
  type: project
  originSessionId: 0ef60168-214b-4283-b9dd-5bbd8b6a2536
---

# HAPPI BRAIN — ERP SCRAPER UK

## CONTEXTE & VISION

Outil d'intelligence commerciale UK : détecte automatiquement les opportunités de vente ERP dans le secteur public britannique.
- **Repo** : `github.com/nbayonne76-ui/ERP-Scraper` (branch `main`)
- **Path WSL2** : `/mnt/c/Erpscraper` (= `C:\Erpscraper` Windows)
- **Équivalent** : Cognism (£15k/an) construit sur mesure, 100% gratuit

## STACK
```
Frontend   → React 18 + Vite (dark UI, 8 onglets)
Backend    → FastAPI + APScheduler + PostgreSQL (asyncpg)
IA         → Claude Haiku 4.5 (scorer + healer extraction)
             Claude Sonnet 4.6 (enricher/synthesis)
Recherche  → Exa.ai (neural) + Jina (gratuit) + Tavily + Linkup + Scrapfly
Scraping   → curl_cffi (9 fingerprints rotatifs JA3/JA4)
             feedparser + Firecrawl /v2/agent + Crawl4AI + Scrapfly ASP
DB         → PostgreSQL (asyncpg) + pgvector optionnel (FLOAT[] fallback)
             Tables: signals, scan_runs, org_intelligence, scraper_metrics
Port       → 8002 (8001 occupé par Happi-CRM sur cette machine)
```

## PIPELINE COMPLET (v2 — juin 2026)
```
SCAN (toutes les 6h ou manuel)
    ↓
1. 21 SCRAPERS en parallèle (asyncio.gather)
    ↓
2. SCORER Claude Haiku 4.5 → score 1-10, erp_stage, sector, keywords
   DOM pruning AXE (97.9% token reduction) — fallback keyword si pas de clé
    ↓
3. SEMANTIC DEDUP → pgvector cosine similarity ≥ 0.92
   (fallback : URL hash dedup sans OPENAI_API_KEY — embeddings via text-embedding-3-small)
    ↓
4. ENRICHER Claude Sonnet 4.6 → tous signals score ≥ 7 avec org connue (pas de cap)
   Chaîne de recherche : Linkup (91% accuracy) → Exa → Jina → Tavily
   → {current_erp, contract_expiry, notes}
    ↓
5. CONTACT FINDER → org-level intel, CIO/CFO/IT Director
    ↓
6. SAVE to PostgreSQL (score ≥ 4, published ≥ 2026-01-01)
   + upsert org_intelligence table
    ↓
7. STORE EMBEDDINGS → pour dedup sémantique futur
```

## LES 21 SOURCES SCRAPÉES (v2 — juin 2026)

### Sources P0 (base)
| # | Source | Clé requise |
|---|--------|-------------|
| 1 | Find a Tender (OCDS API UK above threshold) | Non |
| 2 | Contracts Finder (OCDS API UK below threshold) | Non |
| 3 | Google News RSS (5 requêtes ERP) | Non |
| 4 | Job Postings RSS (postes ERP = signal intention) | Non |
| 5 | Public Contracts Scotland (OCDS) | Non |
| 6 | Sell2Wales (OCDS) | Non |
| 7 | WhatDoTheyKnow FOI + RSS fallback | Non |
| 8 | Companies House (nominations CIO/CFO) | `COMPANIES_HOUSE_API_KEY` optionnel |
| 9 | Tavily Search (1000/mois gratuit) | `TAVILY_API_KEY` |
| 10 | Firecrawl **/v2/agent** (extraction autonome, 5 runs/jour gratuit) | `FIRECRAWL_API_KEY` |
| 11 | Crawl4AI (open-source, LLMExtractionStrategy) | Non |
| 12 | TED Europa (API v3, UK/IE) | `TED_API_KEY` optionnel |
| 13 | Contract Registers (data.gov.uk, 300 councils) | Non (pandas requis) |
| 14 | Exa Neural Search (board papers, IT strategies) | `EXA_API_KEY` |
| 15 | Brave Search | `BRAVE_API_KEY` optionnel |

### Sources P1 (ajoutées — GCA Framework)
| # | Source | Clé requise |
|---|--------|-------------|
| 16 | GCA Frameworks (RM6285/BOS2 via Jina Search — gratuit) | Non |

### Sources P2 (ajoutées — couverture étendue)
| # | Source | Clé requise |
|---|--------|-------------|
| 17 | Committee Minutes (gov.uk board papers — 12-24m d'avance) | Non (`EXA_API_KEY` boost) |
| 18 | Proactis/Delta eSourcing (40% council tenders exclusifs, RSS) | Non |
| 19 | LocalGov News (annonces 12-24m avant appel d'offres) | Non |
| 20 | LinkedIn ERP via Exa (postes IT = signal intention) | `EXA_API_KEY` |
| 21 | TED v3 Extended (UK/IE étendu, secteurs élargis) | `TED_API_KEY` optionnel |

### Sources World-Class (ajoutées — juin 2026)
| # | Source | Clé requise |
|---|--------|-------------|
| 22 | **Scrapfly ASP** (bypass Cloudflare/DataDome/Akamai/PerimeterX — 98% succès) | `SCRAPFLY_API_KEY` |
| 23 | **Linkup Search** (deep research 91% accuracy comme SOURCE de signaux) | `LINKUP_API_KEY` |

## VARIABLES D'ENVIRONNEMENT
```bash
ANTHROPIC_API_KEY=...    # Obligatoire (Haiku scorer + Sonnet enricher)
OPENAI_API_KEY=...       # Recommandé (embeddings text-embedding-3-small pour dedup sémantique)
TAVILY_API_KEY=...       # Recommandé (1000/mois gratuit)
EXA_API_KEY=...          # Très recommandé (1000/mois gratuit — neural search + Committee Minutes)
FIRECRAWL_API_KEY=...    # Très recommandé (/v2/agent autonomous, 5 runs/jour gratuit)
LINKUP_API_KEY=...       # Recommandé (enricher, 91% accuracy, linkup.so)
TED_API_KEY=...          # Optionnel
COMPANIES_HOUSE_API_KEY=... # Optionnel
BRAVE_API_KEY=...        # Optionnel
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1/erp_scraper
PORT=8002
SCAN_INTERVAL_HOURS=6
```

## INTELLIGENCE DIFFÉRENCIANTE : CONTRACT REGISTERS

Les councils UK publient légalement leurs registres de contrats sur **data.gov.uk**.
Ces registres contiennent : fournisseur ERP actuel, valeur, **date d'expiration**.

```python
# Score par mois restants avant expiration :
# ≤3 mois → 10/10 "Tender should be LIVE NOW"
# ≤6 mois → 10/10 "Tender imminent"
# ≤12 mois → 9/10 "Procurement starting"
# ≤18 mois → 8/10 "Planning phase"
```

**Avantage** : 12-18 mois d'avance sur n'importe quelle autre source.

## FRONTEND — 8 ONGLETS

| Onglet | Rôle |
|--------|------|
| 🏢 Accounts | Vue 360° par organisation — agrège signaux, contacts, buyer intel |
| 🤖 AI Signals | Signals live depuis backend, filtrables score/source/secteur |
| 📋 Tenders | CRM appels d'offres + auto-populate depuis signaux score ≥ 7 |
| 🎯 Pipeline | Kanban (Watching → Bid Submitted → Won/Lost) |
| 🔗 Sources | Annuaire 30+ portails UK |
| ⚡ Quick Links | URLs recherche pré-construites + codes CPV |
| 📋 Frameworks | Suivi inscriptions (G-Cloud, DOS, CCS…) |
| 🗺️ Strategy | Guide réponse appels d'offres |

---

## PATTERNS RÉUTILISABLES

### Pattern 1 : Architecture pipeline async
```python
signals, sources = await run_all_scrapers()  # 15 scrapers en parallèle
scored = await score_signals(signals)
enriched = await enrich_signals(scored)
enriched = await find_contacts_for_signals(enriched)
for s in enriched:
    if s.get("score", 0) >= 4:
        await insert_signal(s)
```

### Pattern 2 : Scraper avec fallback gracieux
```python
async def scrape_source() -> list[dict]:
    api_key = os.getenv("SOURCE_API_KEY", "")
    if not api_key:
        logger.info("[source] no API_KEY — skipped")
        return []
```

### Pattern 3 : Enrichissement multi-fallback
```python
if exa_key:
    snippets = await _research_with_exa(org, exa_key)
if not snippets:
    snippets = await _research_with_jina(org)          # gratuit, 0 clé
if not snippets and tavily_key:
    snippets = await _research_with_tavily(org, tavily_key)
if snippets:
    intel = await _synthesise_with_gpt(org, snippets, openai_key)
```

### Pattern 4 : Scorer IA avec fallback keyword
```python
async def score_signal(signal):
    client = _get_client()  # None si pas d'OPENAI_API_KEY
    if not client:
        return _keyword_score(signal)  # heuristique gratuite
```

### Pattern 5 : Dedup par hash URL
```python
def _url_hash(url, title):
    raw = url.strip() if url else title.strip().lower()[:120]
    return hashlib.md5(raw.encode()).hexdigest()
# INSERT OR IGNORE + UPDATE score si nouveau score > ancien
```

### Pattern 6 : Colonnes variables CSV/Excel (Contract Registers)
```python
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

---

## DÉMARRAGE LOCAL (WSL2)
```bash
# Backend
cd /mnt/c/Erpscraper/backend
pip3 install -r requirements.txt --break-system-packages
python3 main.py  # → http://localhost:8002/health

# Frontend (dev)
cd /mnt/c/Erpscraper
npm install    # OBLIGATOIRE depuis WSL (node_modules Windows ≠ Linux)
npm run dev -- --host  # → http://localhost:5173

# Frontend (prod locale — plus stable)
npm run build
cd dist && python3 -m http.server 4000 --bind 0.0.0.0
```

## DEDUP SÉMANTIQUE — SOURCE_AUTHORITY (priorité en cas de conflit)
```python
# dedup.py — ordre décroissant = source gagne en cas de doublon
"Contract Register": 10      # données légales confirmées
"Find a Tender": 9           # appel d'offres officiel UK
"Contracts Finder": 8        # appel d'offres officiel UK
"TED Europa": 7              # appel d'offres officiel EU
"TED v3 Extended": 7         # idem
"Public Contracts Scotland": 7
"Sell2Wales": 7
"Proactis/Delta": 6          # portail tenders exclusif (40% councils)
"Exa Neural Search": 6
"Firecrawl Agent": 5
"Firecrawl Search": 5
"Crawl4AI": 5
"GCA Framework Intelligence": 5
"LinkedIn ERP (Exa)": 4      # signal intention poste IT
"Committee Minutes": 4       # 12-24m avant tender
"WhatDoTheyKnow FOI": 4
"LocalGov News": 3
"Tavily Search": 3
"Brave Search": 3
# non listé → default 2
```

## BUGS CORRIGÉS (2026-06-28)
1. **Duplicate `scrape_contract_registers()`** — fonction définie 2 fois. Première définition supprimée.
2. **Dead code Anthropic embedding** — `dedup.py` avait un bloc `if anthropic_key:` qui faisait `pass`. Supprimé.
3. **SOURCE_AUTHORITY incomplet** — les 4 sources P2 n'étaient pas dans la map. Ajoutées.

## WORLD-CLASS UPGRADES (2026-06-28)
4. **Fingerprint rotation** — `_session()` rotate entre 9 profils (chrome128→133a, safari17_5, firefox133, edge101). Chaque session a un profil aléatoire. Défait JA3/JA4 anti-bot.
5. **Smart retry** — `run_all_scrapers()` réécrit avec REGISTRY (références fonctions). Scrapers en erreur sont retentés 1x après 10s backoff. Métriques per-source exposées.
6. **Scrapfly** — `scrape_scrapfly()` : `asp=True` bypass Cloudflare/DataDome/Akamai. Targets: BidStats, Supply2, MyTenders UK. Extraction via Claude Haiku.
7. **Linkup comme SOURCE** — `scrape_linkup_search()` : 4 requêtes deep research → signaux directs + citations. Partagé avec enricher (même LINKUP_API_KEY).
8. **Self-healing** — `healer.py` nouveau module. Quand un scraper est vide 2x+ consécutifs → fetch anchor URL + Claude Haiku extrait les signaux peu importe la structure HTML.
9. **scraper_metrics DB** — table `scraper_metrics` : success_rate, total_signals, error_streak, empty_streak par source. Déclenche le healer automatiquement.
10. **Webhook alerts** — `WEBHOOK_URL` env var. POST immédiat sur score ≥ 9. Compatible Slack, Make.com, n8n.
11. **API endpoints** — `/api/metrics` (dashboard santé scrapers) + `/api/signals/hot` (signaux score ≥ 8).

## VARIABLES D'ENVIRONNEMENT (complètes)
```bash
ANTHROPIC_API_KEY=...    # Obligatoire (Haiku scorer/healer + Sonnet enricher)
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1/erp_scraper
REDIS_URL=redis://localhost:6379/0
OPENAI_API_KEY=...       # Recommandé (embeddings dedup sémantique)
TAVILY_API_KEY=...       # Recommandé
EXA_API_KEY=...          # Très recommandé (neural search)
FIRECRAWL_API_KEY=...    # Très recommandé (/v2/agent autonomous)
LINKUP_API_KEY=...       # Recommandé (enricher + scraper source)
SCRAPFLY_API_KEY=...     # Très recommandé (anti-bot bypass, free 1000/mois)
WEBHOOK_URL=             # Optionnel (Slack/Make/n8n — hot signals score ≥ 9)
BRAVE_API_KEY=...        # Optionnel
TED_API_KEY=...          # Optionnel
COMPANIES_HOUSE_API_KEY=... # Optionnel
PORT=8002
SCAN_INTERVAL_HOURS=6
```

## LEÇONS APPRISES
- **`export default` dans le mauvais composant** → page blanche.
- **CORS `allow_origins=["*"]` + `allow_credentials=True`** → invalide en navigateur.
- **SQLite** suffisant pour scraper mono-utilisateur. Ne pas surarchitecturer.
- **pandas sur WSL2 system Python** : `pip install pandas openpyxl --break-system-packages`
- **node_modules WSL2** : toujours `npm install` depuis WSL, jamais depuis PowerShell Windows.
- **data.gov.uk OCDS API** : retourne HTTP 301 → `follow_redirects=True` avec httpx.
- **Exa.ai** = meilleur outil recherche neurale gratuite (1000/mois). Excellent pour board papers non indexés par Google.
- **Jina Search** (`s.jina.ai/{query}`) = recherche web gratuite 100%, sans clé. Idéal fallback.
- **WhatDoTheyKnow FOI** : JSON API souvent 403 → toujours prévoir fallback RSS.
- **TED Europa v3** : filtre `CY: ["GB", "IE"]` pour UK/Ireland post-Brexit.

## ADAPTER À UN AUTRE DOMAINE (ex: France)

1. Remplacer sources UK par BOAMP, e-marchespublics.com, PLACE
2. Adapter `ERP_KEYWORDS` : "système d'information", "ERP", "progiciel de gestion intégré"
3. Adapter `scorer.py` SYSTEM_PROMPT pour le contexte FR
4. Adapter `contact_finder.py` : DSI/DAF au lieu de CIO/CFO
5. Frontend : changer labels UK → FR

**Effort estimé : 2-3 jours** pour adapter à un nouveau domaine/pays.

---

## FOOTBALL PREDICTOR WC 2026 — Adaptation du pattern scraper

> Créé le 2026-06-09. Adapte l'architecture ERP Scraper pour prédire les résultats de la Coupe du Monde 2026.
> **Path** : `/home/v-nbayonne/football-predictor-wc2026/`
> **Port backend** : 8003 (8001=CRM, 8002=ERP Scraper)

### Stack
```
Backend   → FastAPI + APScheduler + SQLite (aiosqlite) — port 8003
Frontend  → React 18 + Vite (dark UI, 4 onglets) — port 5175
IA        → Claude Sonnet 4.6 (analyse contextuelle matches)
Prédiction → Modèle Poisson (Maher 1982) + 50k simulations Monte Carlo
Sources   → football-data.org + eloratings.net + the-odds-api.com + fbref.com + api-football.com
DB        → SQLite (wc2026.db) — tables: teams, matches, scan_log
```

### Pipeline prédiction (5 étapes)
```
Scrapers (5 sources async en parallèle)
    ↓
Mise à jour ELO + xG par équipe en DB
    ↓
Modèle Poisson : λ_home = μ × α_home × β_away × elo_scale
    ↓
Monte Carlo 50k simulations → 1X2 proba + top 5 scorelines + BTTS + O/U
    ↓
Claude Sonnet 4.6 → analyse contextuelle 3-4 phrases (max 20/scan pour économiser quota)
```

### Sources de données
| Source | Données | Clé | Gratuit |
|--------|---------|-----|---------|
| football-data.org | Fixtures WC, résultats, groupes | Oui | Free (10 req/min) |
| eloratings.net | ELO ratings équipes nationales | Non | 100% |
| the-odds-api.com | Cotes bookmakers | Oui | 500/mois |
| fbref.com | xG stats équipes nationales | Non | Scraping HTML |
| api-football.com | Fallback fixtures | Oui | 100/jour |

### Fichiers clés
- `backend/db.py` — SQLite + seed 49 équipes qualifiées WC 2026 avec ELO/attack/defense de départ
- `backend/predictor.py` — Modèle Poisson + Monte Carlo + blend avec cotes bookmakers (25% poids market)
- `backend/scrapers.py` — 5 scrapers async + merge fixtures + mapping noms → codes FIFA
- `backend/claude_analyzer.py` — Claude Sonnet 4.6 analyse match + pronostic tournoi général
- `backend/scheduler.py` — Pipeline complet + limite 20 analyses Claude par scan

### Formule mathématique clé
```python
# elo_scale = exp(elo_diff / 1200)  — plus doux que la formule Elo standard
lambda_home = WC_AVG_GOALS_PER_TEAM * attack_home * defense_away * elo_scale_home * home_factor
lambda_away = WC_AVG_GOALS_PER_TEAM * attack_away * defense_home * elo_scale_away

# Monte Carlo : np.random.default_rng().poisson(lambda, 50_000) pour chaque équipe
# Indice confiance : fonction du prob_gap |home_win - away_win|
```

### Blend cotes bookmakers (innovation vs ERP Scraper)
```python
# Les cotes contiennent info supplémentaire (blessures, météo, état de forme live)
prediction = blend_with_odds(prediction, odds_probs, odds_weight=0.25)
# 75% modèle Poisson + 25% marché bookmakers
```

### Démarrage
```bash
# Backend
cd /home/v-nbayonne/football-predictor-wc2026/backend
source venv/bin/activate && python3 main.py

# Frontend
cd /home/v-nbayonne/football-predictor-wc2026/frontend
npm run dev  # → http://localhost:5175
```

### APIs à enregistrer (clés gratuites)
- football-data.org/client → Plan free, 10 req/min (suffit largement)
- app.the-odds-api.com → 500 req/mois gratuits
- Pour l'Anthropic API : utiliser la clé existante

---

*Mis à jour : 2026-05-31 — extrait de happi_brain.md v22 (Section 21)*
*Ajout : 2026-06-09 — Football Predictor WC 2026 (Section Football)*
