---
name: Happi Foundry
type: platform
status: production-ready
client: Interne H'appi
sector: Outils IA internes
repo: Happi-Foundry
---

# Happi Foundry — Playground Claude IA

## Contexte
Plateforme interne H'appi pour tester et gérer les prompts Claude. Inspiré d'Azure AI Foundry et de l'OpenAI Playground. Utilisé pour affiner les prompts avant déploiement client.

## Stack
- **Frontend** : Next.js 14 (App Router) + TypeScript + Tailwind CSS
- **Backend** : FastAPI + SQLAlchemy + Alembic + PostgreSQL
- **IA** : Anthropic Claude SDK (`anthropic`)
- **Deploy** : Local / Docker

## Features
- **Playground** : Chat interactif avec Claude (streaming, model selector, température, max-tokens, save-as-prompt)
- **Bibliothèque de prompts** : Créer, éditer, rechercher, organiser avec tags
- **Catalogue de modèles** : Capacités et pricing de chaque modèle Claude
- **Dashboard usage** : Suivi tokens, coûts, historique requêtes

## Structure
```
frontend/          → Next.js 14
backend/
  app/
    main.py
    routers/
    models/
  alembic/
  requirements.txt
```

## Usage principal
- Tester des prompts système pour nouveaux clients
- Comparer les performances entre modèles Claude
- Stocker et réutiliser les prompts qui marchent
- Suivre les coûts d'utilisation API par projet

## Leçons apprises
- Indispensable avant tout déploiement client : tester en playground d'abord
- Le streaming améliore drastiquement l'UX (pas d'attente)
- Toujours tagger les prompts par secteur client (meuble, hôtel, BTP...)
