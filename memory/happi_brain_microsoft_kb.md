---
name: happi-brain-microsoft-kb
description: "Microsoft Sales App — catalogue complet des 67 solutions Azure/D365/M365 : statut enrichissement, connaissances produits clés, pricing 2026, nouvelles features, competitive intelligence — source de vérité commerciale Microsoft"
metadata: 
  node_type: memory
  type: project
  originSessionId: ed270155-6401-415a-8194-ac260c7f6e2e
---

# HAPPI BRAIN — MICROSOFT SALES APP : CATALOGUE PRODUITS & KB

## État général (17 juillet 2026)

- **URL prod** : https://microsoft-sales-app.vercel.app
- **Repo** : github.com/nbayonne76-ui/microsoft-sales-app (branch `main`)
- **JSON data** : `data/azure-solutions.json` — **67 solutions**
- **KB markdown** : `templates/knowledge-base/` — 33 fichiers MD

---

## Catégories des 67 solutions

| Catégorie | Nb | Solutions |
|-----------|----|----|
| `business` | 26 | Toutes les D365 + Power Apps/Automate/Copilot Studio |
| `ai` | 6 | Azure ML, Azure OpenAI, AI Services, AI Search, Microsoft Foundry (NEW) |
| `analytics` | 4 | Fabric, Power BI, Synapse, Data Factory |
| `compute` | 6 | VMs, VMSS, AKS, App Service, Functions, AVD |
| `management` | 8 | Advisor, Arc, Cost Management, Log Analytics, Monitor, Policy, Reservations, Blueprints (migration) |
| `development` | 4 | DevOps, Repos, DevTest Labs, Application Insights (créé 17 juil 2026) |
| `security` | 4 | Key Vault, Defender for Cloud, Sentinel, D365 Fraud Protection |
| `storage` | 3 | Blob Storage, SQL Database, Cosmos DB |
| `integration` | 3 | API Management, Logic Apps, Service Bus |
| `networking` | 2 | VNet, ExpressRoute |
| `modern-work` | 1 | Microsoft 365 Copilot |
| `iot` | 1 | Azure IoT Hub |

**Règle tab UI** : `category === 'business'` → onglet **Dynamics** | reste → onglet **Azure**

---

## Statut enrichissement JSON (17 juillet 2026)

### ✅ 100% complets (7 champs : keyFeaturesFr+benefitsFr+useCasesFr+salesContext)

| Solution | keyF | benef | useC | Notes |
|----------|------|-------|------|-------|
| Azure Machine Learning | 17 | 9 | 6 | Event Grid, Power BI, Workload Identity Fed. |
| Microsoft 365 Copilot | 14 | 9 | 6 | Work IQ, Cowork, Scout, multi-model |
| Azure Virtual Desktop (AVD) | 13 | 9 | 6 | Autoscaling GA, RDP Multipath GA |
| Azure Policy | 13 | 9 | 6 | 30+ frameworks réglementaires, K8s, Arc |
| Azure Blueprints (migration) | 9 | 7 | 4 | isActive: false — guide migration Deployment Stacks |
| Microsoft Foundry (Azure AI Foundry) | 14 | 9 | 6 | NOUVELLE ENTRÉE — 1900+ modèles |
| Dynamics 365 Customer Insights | - | - | - | Manque seulement useCasesFr |
| Dynamics 365 Field Service | - | - | - | Manque seulement useCasesFr |

### ⚠️ 57% (manquent keyFeaturesFr + benefitsFr + useCasesFr + salesContext)
Toutes les autres solutions (58 sur 67) — ont EN mais pas FR ni salesContext.

### ⚠️ 42% (aussi manque salesContext EN)
D365 Customer Voice, D365 Marketing, D365 Customer Service, D365 HR, D365 Commerce, D365 Contact Center

---

## Protocole enrichissement KB

### Méthode (établie 17 juil 2026)
1. Utilisateur envoie : URL page produit + URL page docs principale
2. Claude fetche hub docs → identifie sous-pages (overview, whats-new, concepts, pricing, prerequisites)
3. Fetche 4-6 sous-pages en **parallèle**
4. Crée/enrichit l'entrée JSON avec tous les champs
5. Commit + `git push origin main` → Vercel auto-deploy
6. **Utilisateur N'A PAS besoin d'envoyer les sous-liens manuellement**

### Champs obligatoires par enrichissement
```
keyFeaturesEn  : 12-14 items (features détaillées avec contexte 2025/2026)
keyFeaturesFr  : même nombre (traduction adaptée + contexte commercial)
benefitsEn     : 7-9 items (ROI, différenciateurs, stats chiffrées)
benefitsFr     : même nombre
useCasesEn     : 4-6 cas (title, description, industries, businessImpact)
useCasesFr     : même nombre (traduction enrichie)
salesContext   : JSON avec targetPersonas, keyStats, painPoints,
                 keyDifferentiators, competitiveEdge, whyNow, nextSteps
```

### Champs complémentaires à enrichir
```
shortDescriptionEn/Fr  : 1-2 phrases (mise à jour avec features 2026)
fullDescriptionEn/Fr   : paragraphes complets (architecture + nouveautés)
estimatedCost/En       : pricing 2026 précis
implementationTime/En  : 3 niveaux (quick win / standard / enterprise)
idealCustomerSize/En   : PME / ETI / Enterprise avec contexte
securityFeatures       : liste JSON FR
complianceCerts        : liste JSON
pricingTiers           : 3-6 tiers JSON
targetIndustries       : liste 6-10 secteurs
targetPersonas         : liste 5-7 personas
```

---

## Connaissances produits clés — 2026

### Microsoft Foundry (ex Azure AI Foundry, ex Azure AI Studio)

**Rebrandings** : Azure AI Studio → Azure AI Foundry → **Microsoft Foundry** (2026)
**Portal** : https://ai.azure.com
**SDK unifié** : `azure-ai-projects` 2.x (remplace 5+ packages précédents)
**Endpoint** : compatible OpenAI — code SDK OpenAI fonctionne avec modifications minimales

**Catalogue 1 900+ modèles** :
- GPT-5 : le plus puissant, raisonnement + multimodal
- GPT-4.1 / mini : production équilibre/vitesse, $2/1M tokens / $0.15/1M tokens
- Claude Sonnet 5 / Opus 4.8 (Anthropic) : raisonnement, code, multimodal — $3/1M tokens
- Grok (xAI) : raisonnement, coding
- Mistral : multilingue, code
- DeepSeek-R1 : open-weight raisonnement
- Phi-4 : on-device, edge
- Meta Llama : open, fine-tunable

**Features clés (toutes disponibles depuis juillet 2026)** :
- **Foundry IQ** : RAG enterprise intégré (SharePoint/OneDrive/web) avec citations
- **Work IQ** (preview) : agents connectés contenu M365 (Teams/Outlook/SharePoint)
- **Fabric IQ** (preview) : agents connectés données Microsoft Fabric
- **A2A endpoints** (preview) : agents exposés comme endpoints découvrables
- **Voice agents** (preview) : speech-to-speech hébergé
- **Routines** (preview) : workflows multi-étapes réutilisables
- **Model routing** (Responses API) : sélection automatique modèle optimal
- **Instant access** (preview) : appel modèle par nom sans déploiement
- **Foundry Local** : LLMs on-device **GRATUIT** (HuggingFace, sans Azure)
- **Foundry Labs** : hub preview ai.azure.com/labs (recherches IA Microsoft)
- **AI Red Teaming Agent** (preview) : tests adversariaux automatisés
- **Foundry Control Plane** : gestion agents à grande échelle, limites tokens

**Pricing** : Plateforme GRATUITE. GPT-5 ~$2.50/1M. Claude Sonnet 5 ~$3/1M. Local = GRATUIT.
**ROI Calculator** : aka.ms/Foundry-ROI-Calculator

---

### Azure Blueprints — Retrait (URGENT)

| Date | Ce qui change |
|------|--------------|
| 31 juil 2026 (PASSÉ) | Impossible créer nouvelles définitions/versions |
| 31 oct 2026 | Impossible modifier définitions + créer nouvelles assignations |
| 31 déc 2026 | Impossible modifier assignations existantes |
| 31 jan 2027 | Retrait total — données non exportées SUPPRIMÉES DÉFINITIVEMENT |

**Remplacement recommandé** :
- **Azure Deployment Stacks** (GA) = lifecycle + deny settings (DenyDelete/DenyWriteAndDelete, actionOnUnmanage: deleteAll/deleteResources/detachAll)
- **Template Specs** (GA) = stockage/versioning templates ARM/Bicep
- **Pattern migration** : Template Specs + Deployment Stacks = 100% parité Blueprints

**Opportunité commerciale** : Azure Advisor identifie les clients utilisant Blueprints → engagement migration conseil bornée dans le temps (deadline Jan 2027)

---

### Azure Policy (renommé depuis "Azure Policy & Blueprints")

**8 effets policy** : Deny, Audit, Modify, DeployIfNotExists, AuditIfNotExists, Append, Disabled, DenyAction

**30+ frameworks réglementaires intégrés** :
ISO 27001:2013, NIST SP 800-53 Rev.4/5, NIST SP 800-171 R2, CIS Azure Benchmarks (v1.1→2.0), FedRAMP High/Moderate, HIPAA HITRUST, PCI DSS 3.2.1/4.0, SOC 2, CMMC Level 3, SWIFT CSP-CSCF, Spain ENS, NL BIO, UK OFFICIAL/NHS, Australian ISM, Canada PBMM, Microsoft Cloud Security Benchmark, Microsoft Cloud for Sovereignty (Confidential/Global)

**Features avancées** :
- `requestContext().identity` : enforce MFA à la création, bloquer suppression manuelle
- Azure Policy for Kubernetes : Gatekeeper/OPA sur AKS + clusters Arc-enabled (pod security, image registries, resource limits)
- Machine Configuration : audit/enforcement OS VMs (pas seulement propriétés ARM)
- Azure Arc : mêmes policies on-premises + multi-cloud
- Policy-as-Code : GitHub Actions / Azure DevOps pipelines
- Remédiation jusqu'à 50 000 ressources par tâche

**Pricing** : GRATUIT pour ressources Azure. Machine Configuration OS : $0.60/serveur/mois.

---

### Azure Virtual Desktop (AVD)

**Exclusivité** : seul cloud avec Windows 11/10 Enterprise multi-session (Citrix/VMware ne peuvent pas l'offrir sur Azure) → coût VDI -50-60%

**Nouvelles features 2026** :
- Automated Host Pools + **Dynamic Autoscaling GA juin 2026** : crée/supprime VMs automatiquement → coût inactif = 0
- **RDP Multipath GA juillet 2026** : redondance TCP automatique, aucune config requise
- AVD sur Azure Local (Arc-Enabled Servers) — **Public Preview mai 2026**
- External Identity Support **GA novembre 2025** : contractors sans licence M365
- FSLogix cloud-only/external identities **GA mai 2026**
- App Attach Windows Server 2025/2022 **GA avril 2026**
- RDP Shortpath UDP over Private Link **GA février 2026**
- HEVC/H.265 GPU acceleration **GA juin 2025**
- QuickStart (host pool Windows 11 multi-session en ~20 min) **GA mars 2025**

**Compétiteurs** : VMware Horizon (Broadcom acquisition = vague migration massive vers AVD), Citrix DaaS, Windows 365 (moins flexible), Amazon WorkSpaces

**Pricing** : Service AVD GRATUIT. VMs ~$0.10-1.14/h selon taille. Multi-session poolé $20-80/user/mois tout compris.

---

### Microsoft 365 Copilot

**Pricing** : $30/user/mois add-on sur E3/E5/Business Standard/Premium
**OU** Microsoft 365 **E7 : $99/user/mois** (E5 + Copilot + Agent 365 + Entra Suite — économie $18/user/mois = $216/user/an vs achat séparé)

**Features GA 2026** :
- **Copilot Cowork** GA juin 2026 : fastest Frontier adoption ever. Multi-model routing (GPT-5.5 + Claude Sonnet 5 + Claude Opus 4.8)
- **Claude Sonnet 5** dans Copilot : juillet 2026
- **Claude Opus 4.8** dans Copilot : mai 2026
- **GPT-5.5 Instant** : mai 2026 (faible latence)
- **Agent 365** GA mai 2026 : plan de contrôle universel agents IA
- **Work IQ APIs** GA juin 2026 : accès programmatique à l'intelligence organisationnelle
- **Finance Workflows Excel** GA juin 2026 : données financières vérifiées + connecteurs ERP/SAP
- **Agentic Capabilities Word/Excel/PPT** GA avril 2026 : planification et exécution multi-étapes

**Features Preview (Frontier)** :
- Microsoft **Scout** Public Preview juin 2026 : agent personnel proactif (fichiers locaux + web)
- **Legal Agent** (Word) : révision contrats avec modifications suivies
- **Copilot Agentic Email/Calendar** (Outlook) : planification automatique + relances
- **Agent Mode** Word/Excel/PPT : génération de bout en bout

---

### Pricing Microsoft 2026 (mis à jour 1er juillet 2026)

**M365 Plans** :
| Plan | Prix |
|------|------|
| Business Basic | $7/user/mois |
| Apps for Business | $10/user/mois |
| Business Standard | $14/user/mois |
| Business Premium | $26/user/mois |
| M365 E3 | $39/user/mois |
| M365 E5 | $60/user/mois |
| M365 F1 | $3/user/mois |
| M365 F3 | $10/user/mois |
| Microsoft 365 Copilot add-on | $30/user/mois |
| **Microsoft 365 E7** | **$99/user/mois** (E5+Copilot+Agent 365+Entra Suite) |

**D365 Plans** :
| Solution | Prix |
|----------|------|
| D365 Sales | $65/user/mois (Pro) |
| D365 Customer Service | $50/user/mois (Pro) |
| D365 Finance | $180/user/mois |
| D365 Business Central | $70/user/mois (Essential) |

---

## Fichiers KB markdown (33 fichiers)

Répertoire : `templates/knowledge-base/`
Fichiers clés pour vendeurs :
- `m365-roadmap-fy27.md` — roadmap FY27 complète (Copilot Cowork, E7, Agent 365, Work IQ, Scout, Legal Agent)
- `m365-pricing-2025.md` — tarifs M365 mis à jour juillet 2026
- `dynamics-365-ai-agents-complete.md` — référence complète agents IA D365
- `dynamics-365-fo-modules-architecture.md` — architecture F&O modules
- `microsoft-licensing-contracts-guide.md` — EA, CSP, MCA, NCE
- `csp-vs-mca-decision-guide.md` — guide décision contrats
- `m365-e3-vs-e5-decision-guide.md` — guide décision E3/E5
- `azure-pricing-2025.md` — tarifs Azure IaaS/PaaS
- `modern-workplace-security-framework.md` — Zero Trust + Conditional Access

---

## Architecture KB Service (lib/kb-service.js)

**2 couches** :
1. **PRIORITÉ 1** : Articles de blog (`lib/blog-articles.js`) — infos les plus récentes
2. **PRIORITÉ 2** : Fichiers MD (`templates/knowledge-base/`) — référence détaillée

**Impact** : ajouter un blog article → Account Intel, Email Generator, Séquences, Agent IA utilisent automatiquement les nouvelles infos.

**Mapping blog → KB** :
```javascript
const BLOG_TO_KB = {
  m365: ['m365'], copilot: ['m365'], azure: ['azure'],
  dynamics: ['dynamics'], securite: ['security'],
};
```

---

## CRITIQUE — Architecture API route (app/api/azure-solutions/route.js)

### Filtre isActive (ligne 48)
```javascript
let solutions = loadSolutions().filter(s => s.isActive !== false);
```
- `isActive: true` ou `isActive: undefined` → inclus dans l'API
- `isActive: false` → **EXCLU** de TOUT (KB page, Agent IA, Email Generator, Séquences)
- **Azure Blueprints** (`isActive: false`) est invisible à toutes les features IA
- Si on veut que le guide migration soit accessible à l'Agent IA → changer `isActive: true` et/ou créer un fichier MD dans `templates/knowledge-base/`

### JSON_FIELDS — champs auto-parsés string → objet (ligne 15)
```javascript
const JSON_FIELDS = [
  'keyFeatures','benefits','useCases',
  'targetIndustries','targetPersonas','pricingTiers','keywords','tags',
  'keyFeaturesEn','benefitsEn','useCasesEn',
  'keyFeaturesFr','benefitsFr','useCasesFr'  // ← nos nouveaux champs ✅
];
```
- Ces champs stockés comme `json.dumps([...])` dans le JSON → auto-parsés en tableaux JS
- **`salesContext` N'EST PAS dans cette liste** → reste une string JSON côté frontend

### salesContext — string JSON non parsée
- Stocké comme `json.dumps({...})` dans le JSON
- L'API le renvoie tel quel (string, pas objet)
- Le frontend/backend doit faire `JSON.parse(salesContext)` manuellement si nécessaire
- **Comportement actuel** : fonctionne car les composants font déjà ce parse (pattern établi)

### applyLang — champs traduits par langue (ligne 28-38)
```javascript
const LANG_FIELDS = [
  'shortDescription','fullDescription',
  'keyFeatures','benefits','useCases',   // ← prend keyFeaturesFr si lang=fr
  'estimatedCost','implementationTime','idealCustomerSize'
];
```
- Pour `lang=fr` : `out['keyFeatures'] = s['keyFeaturesFr']` (si existe)
- Pour `lang=en` : `out['keyFeatures'] = s['keyFeaturesEn']` (si existe)
- **Les champs `keyFeaturesFr/benefitsFr/useCasesFr` qu'on ajoute alimentent exactement ce mécanisme** ✅

### WebFetch — pattern de fiabilité
- `azure.microsoft.com/products/...` → **souvent timeout** (CDN lourd)
- `learn.microsoft.com/...` → **fiable**, préférer pour les enrichissements
- Stratégie : fetcher hub page docs → identifier sous-pages → fetcher overview + whats-new + concepts + pricing en parallèle

---

## CRITIQUE — Structure des champs OLD vs NEW (gotcha technique)

La plupart des solutions ont **3 couches de champs** :

```
ANCIENS champs (FR, legacy, NE PAS supprimer) :
  keyFeatures    → liste FR (base de départ pour keyFeaturesFr)
  benefits       → liste FR
  useCases       → liste FR (souvent très basique, 2-3 items)
  fullDescription → texte FR
  shortDescription → texte FR (parfois EN)

NOUVEAUX champs EN (ajoutés lors de l'enrichissement initial) :
  keyFeaturesEn  ✅ présents sur toutes les solutions
  benefitsEn     ✅ présents
  useCasesEn     ✅ présents (4-6 items bien documentés)
  fullDescriptionEn ✅
  shortDescriptionEn ✅

NOUVEAUX champs FR (À AJOUTER — c'est le travail en cours) :
  keyFeaturesFr  ❌ manquants sur 60/67 solutions
  benefitsFr     ❌ manquants
  useCasesFr     ❌ manquants
  fullDescriptionFr → parfois présent, parfois = fullDescription
  shortDescriptionFr → parfois présent
```

**Pattern lors de l'enrichissement FR** :
1. Lire `keyFeatures` (ancien FR) comme BASE pour `keyFeaturesFr`
2. Lire `keyFeaturesEn` (nouveau EN) pour le contenu structuré
3. Traduire/enrichir en créant `keyFeaturesFr` (12-14 items)
4. NE PAS supprimer les anciens champs (`keyFeatures`, `benefits`, `useCases`)
5. La fonction `applyLang()` dans l'API route prend le champ `keyFeaturesFr` si `lang=fr`

**Script Python de vérification** (à lancer dans le répertoire du projet) :
```python
import json
with open('data/azure-solutions.json') as f:
    data = json.load(f)

def score(s):
    fields = ['keyFeaturesEn','keyFeaturesFr','benefitsEn','benefitsFr',
              'useCasesEn','useCasesFr','salesContext']
    ok = sum(1 for f in fields if s.get(f))
    return ok*100//len(fields)

for s in sorted(data, key=lambda x: score(x)):
    if score(s) < 100:
        print(f'{score(s)}% [{s["category"]}] {s["officialName"]}')
```

---

## Priorité d'enrichissement — Ordre recommandé

### 🔴 P10 encore à enrichir (URGENT)

| Solution | Catégorie | Manque |
|----------|-----------|--------|
| **Azure OpenAI Service** | ai | keyFeaturesFr/benefitsFr/useCasesFr/salesContext |
| **Microsoft Fabric** | analytics | keyFeaturesFr/benefitsFr/useCasesFr/salesContext |
| **Azure Monitor** | management | keyFeaturesFr/benefitsFr/useCasesFr/salesContext |
| **Sales in Microsoft 365 Copilot** | business | keyFeaturesFr/benefitsFr/useCasesFr/salesContext |
| **Service in Microsoft 365 Copilot** | business | keyFeaturesFr/benefitsFr/useCasesFr/salesContext |
| **Microsoft Sustainability Manager** | business | keyFeaturesFr/benefitsFr/useCasesFr/salesContext |

### 🟠 P9 encore à enrichir

Azure Virtual Machines, Azure App Service, AKS, Azure DevOps, Azure Advisor, Azure Cost Management, Azure Log Analytics, Application Insights, Azure SQL Database, Microsoft Defender for Cloud, Azure Key Vault, Microsoft Power Apps, Microsoft Power Automate, D365 Business Central, D365 Sales, D365 Finance, D365 Supply Chain, D365 Customer Insights (85%), D365 Field Service (85%), D365 Project Operations, Microsoft Power BI

---

## IDs des nouvelles entrées (format différent)

Les entrées créées en juillet 2026 utilisent un format ID personnalisé :
- `"cmp_blueprints_migration_2026"` — Azure Blueprints migration
- `"cmp_microsoft_foundry_2026"` — Microsoft Foundry

Les entrées existantes utilisent le format cuid : `"cmpckzx..."`.
**Pas de problème fonctionnel** (JSON-based, pas de validation DB), mais noter l'incohérence.

---

## Pattern Python pour update JSON solutions

```python
import json

with open('data/azure-solutions.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# Trouver et modifier une solution existante
sol = next(s for s in data if s.get('officialName') == 'Nom Exact')
sol['keyFeaturesFr'] = json.dumps([...], ensure_ascii=False)
sol['benefitsFr'] = json.dumps([...], ensure_ascii=False)
sol['useCasesFr'] = json.dumps([...], ensure_ascii=False)
sol['salesContext'] = json.dumps({...}, ensure_ascii=False)
sol['updatedAt'] = "2026-07-17T00:00:00.000Z"

# Ajouter une nouvelle solution
data.append({...})  # champs complets

with open('data/azure-solutions.json', 'w', encoding='utf-8') as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# Toujours vérifier après
print(json.loads(sol['keyFeaturesFr']))
```

**Règle** : `ensure_ascii=False` OBLIGATOIRE pour conserver les accents français.

---

## Pricing Azure models (Foundry) — Juillet 2026

| Modèle | Input | Output |
|--------|-------|--------|
| GPT-4.1 mini | ~$0.15/1M tokens | ~$0.60/1M tokens |
| GPT-4.1 | ~$2/1M tokens | ~$8/1M tokens |
| GPT-5 | ~$2.50/1M tokens | ~$10/1M tokens |
| Claude Sonnet 5 | ~$3/1M tokens | ~$15/1M tokens |
| Claude Opus 4.8 | ~$15/1M tokens | ~$75/1M tokens |
| DeepSeek-R1 | ~$0.55/1M tokens | ~$2.19/1M tokens |
| Phi-4 | ~$0.07/1M tokens | ~$0.14/1M tokens |

---

## Infos produits complémentaires (non capturées ailleurs)

**Azure Virtual Desktop** :
- Per-user access pricing pour externes : ~$4.90/user/mois (enrôlement Azure Subscription)
- Context-based Redirections (Preview juin 2026) : contrôle côté serveur presse-papier/imprimante/USB selon conformité device
- Token Protection GA août 2025 sur Windows App Windows (via Conditional Access)
- Redirections désactivées par défaut sur nouveaux host pools depuis juillet 2025 (sécurité)
- 39 régions Azure avec infrastructure TURN relay (IP range 51.5.0.0/16)

**Microsoft 365 Copilot** :
- Copilot Chat (BizChat) = version GRATUITE limitée (sans intégration apps Word/Excel/Teams)
- Agent 365 seul = $15/user/mois → inclus dans E7 $99
- Entra Suite = $12/user/mois → inclus dans E7 $99
- Anthropic = sous-traitant opt-in pour les modèles Claude dans Copilot (opt-in admin requis)
- Work Trend Index 2026 : concept "Frontier Professionals" — écart productivité croissant

**Azure Policy** :
- Limites importantes : 500 définitions/périmètre, 200 initiatives/périmètre, 2500 initiatives/tenant
- 50 000 ressources max par tâche de remédiation
- Azure Virtual Network Manager utilise Azure Policy pour les groupes dynamiques
- `requestContext().identity` : accès à `user.objectId`, `app.displayName`, etc.

**Microsoft Foundry** :
- Foundry (classic) = ancien hub-based projects, toujours accessible
- Toggle "New Foundry" dans la bannière = version nouvelle
- Réponses API vs Assistants API : nouvelles terminologies : Conversations/Items/Responses/Agent Versions
- Foundry Labs : https://ai.azure.com/labs (pas de URL fixe documentée, peut changer)
- Foundry Local : supporte HuggingFace models via compilation
- `azure-ai-projects` 2.x = package Python principal (remplace `azure-ai-inference`, `azure-ai-generative`, `azure-ai-ml`)

**Azure Blueprints** :
- Azure Advisor = outil GRATUIT pour identifier les abonnements utilisant Blueprints
- Export avant le 31 octobre 2026 (avant le gel des modifications) = deadline opérationnelle réelle
- `actionOnUnmanage: deleteAll/deleteResources/detachAll` = choix lors migration Deployment Stacks
- Max 5 principals exclus des deny-settings dans Deployment Stacks
- Deployment Stacks Contributor (gestion sans créer deny-assignments) vs Deployment Stacks Owner (avec)

---

*Mis à jour : 2026-07-17 — Complété avec gotcha technique, priorités, scripts, pricing modèles, infos manquantes*
