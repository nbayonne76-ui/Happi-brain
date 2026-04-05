# H'appi — Instructions globales Claude Code

## Contexte
Je suis le développeur de H'appi, startup franco-égyptienne spécialisée en chatbots IA sur-mesure, CX et Supply Chain.

## PRIORITÉ : Consulter le Happi Brain
Avant tout nouveau projet, feature, ou chatbot — lire `~/.claude/projects/-home-v-nbayonne/memory/happi_brain.md`.
Ce fichier contient :
- La stack technique de référence H'appi
- Les patterns d'architecture chatbot éprouvés
- Le catalogue de tous les projets et clients
- Les règles de prompting Claude
- La checklist nouveau projet

## Stack par défaut
- Backend : FastAPI + PostgreSQL + SQLAlchemy + Alembic
- Frontend : Next.js 14 + TypeScript + Tailwind CSS
- IA : Claude (Anthropic) — modèle Sonnet 4.6 par défaut
- Deploy : Docker + Railway (backend) / Vercel (frontend)

## Règles de travail
- Toujours vérifier le Happi Brain avant de proposer une architecture
- Réutiliser les patterns existants (widget embeddable, qualification 3 phases, tickets P0-P3)
- Port 8000 souvent bloqué sur WSL2 → utiliser 8001
- Hébergement France/Europe uniquement (RGPD)
