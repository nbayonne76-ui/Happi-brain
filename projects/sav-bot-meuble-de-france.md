---
name: SAV-BOT Mobilier de France
type: chatbot
status: production-ready
client: Mobilier de France
sector: Meuble / Retail
repo: SAV-BOT-Meuble-de-france
---

# SAV-BOT Mobilier de France ⭐ (projet phare)

## Contexte
Chatbot SAV après-vente pour Mobilier de France (enseigne meuble française). Projet le plus complet et le plus avancé techniquement du portfolio H'appi.

## Stack
- **Backend** : FastAPI (Python 3.13) + PostgreSQL + Redis + Alembic
- **Frontend** : React 18.2
- **IA** : OpenAI GPT (intégration Claude possible)
- **Deploy** : Docker + docker-compose + Railway
- **CI/CD** : GitHub Actions + Codecov
- **Tests** : 351+ tests, couverture backend 62%, frontend 53%

## Features
- Dialogue naturel multilingue : FR, EN, AR, IT, DE
- Recommandations produits intelligentes (AI-powered)
- Upload photo + analyse défauts visuels
- Ticketing automatique avec priorité P0-P3
- Support vocal (speech recognition + synthesis)
- Emotion detection sur les messages vocaux
- Monitoring santé + métriques
- Sécurité : JWT auth, rate limiting, CORS

## Système de tickets
| Priorité | Cas | Délai |
|----------|-----|-------|
| P0 | Urgence sécurité | Immédiat |
| P1 | Produit inutilisable | <4h |
| P2 | Problème fonctionnel | <24h |
| P3 | Cosmétique / info | <72h |

## Architecture backend
```
backend/
  app/
    main.py
    routers/    → chat, auth, tickets, webhooks, voice
    models/     → DB models (SQLAlchemy)
    services/   → openai_service, email_service, voice_service
  alembic/      → migrations DB
  data/         → catalogue produits
  tests/
```

## Fichiers clés
- `VOICE_EMOTION_PRIORITY_SYSTEM.md` — système vocal + émotions
- `TICKET_CREATION_FLOW.md` — flow de création de tickets
- `CHATBOT_ENHANCED_v2.md` — architecture chatbot v2
- `CATALOGUE_INTEGRATION.md` — intégration catalogue produits

## Deploy Railway
- `railway.json` + `nixpacks.toml` + `Procfile`
- Variables d'env : `OPENAI_API_KEY`, `DATABASE_URL`, `REDIS_URL`

## Leçons apprises
- Toujours intégrer un système de priorité de tickets (P0-P3)
- Les clients SAV ont besoin de photos — prévoir upload dès le départ
- Le multilingue est critique (AR important pour clientèle française)
- Redis indispensable pour les sessions et le rate limiting
- La détection d'émotion améliore la priorisation automatique
