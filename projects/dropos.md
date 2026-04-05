---
name: DropOS
type: saas-platform
status: planning/mvp
client: B2B SaaS (dropshippers)
sector: E-commerce / Dropshipping
repo: DropOS-DropShipping
---

# DropOS — L'OS du Dropshipping

## Vision
Remplacer 6-7 outils payants fragmentés par une seule plateforme qui combine analytics, fulfillment, sourcing et marketing.

**Target** : Dropshippers $10K–$200K/mois, frustrés par des stacks à $400–$1000/mois
**Pricing** : $99–149/mois (remplace $400–1000/mois d'outils)

## Stack
- **Frontend** : Next.js (web-first)
- **Backend** : FastAPI + PostgreSQL
- **Auth** : JWT
- **Intégrations** : Shopify Partner API, tarifs douaniers US HTS / EU TARIC
- **Deploy** : Docker + Vercel/Railway

## Roadmap
| Phase | Focus | Status |
|-------|-------|--------|
| Phase 1 — MVP | Analytics (profit réel, landed cost, dashboard multi-boutiques) | Planning |
| Phase 2 | Fulfillment (sync fournisseurs, failover stock, retours) | Backlog |
| Phase 3 | Sourcing (recherche produits, scoring fournisseurs, tendances) | Backlog |
| Phase 4 | Marketing (flows email, automation avis, tracking ads) | Backlog |

## Différenciation clé
Ce qu'aucun outil SMB ne propose actuellement :
1. Failover stock multi-fournisseurs en temps réel
2. Profit net réel (duties, chargebacks, fees, remboursements)
3. Dashboard consolidé multi-boutiques
4. Scoring fournisseurs + routage automatique
5. Orchestration retours unifiée
6. Calculateur landed cost avec données tarifaires live

## Structure repo
```
frontend/     → Next.js
backend/      → FastAPI + PostgreSQL
docs/         → Documentation
```

## Leçons apprises
- Le calcul du "vrai" profit net est le pain point #1 des dropshippers
- Multi-boutiques est indispensable dès le MVP (les gros players ont 3-5 boutiques)
- Le failover fournisseur = énorme avantage concurrentiel
