# 🧠 Happi Brain

> Base de connaissance centrale de H'appi — cerveau évolutif de Claude pour tous les projets chatbot IA.

## Structure

```
happi_brain.md          ← Cerveau principal (stack, patterns, clients, règles Claude)
README.md               ← Ce fichier

projects/               ← Fiche détaillée de chaque projet
  sav-bot-meuble-de-france.md    ← Chatbot SAV Mobilier de France ⭐
  innatural-chatbot.md           ← Chatbot e-commerce INnatural (cosmétiques)
  happi-secretary.md             ← Secrétariat IA vocal 24h/24
  happi-foundry.md               ← Playground Claude IA (interne)
  dropos.md                      ← SaaS dropshipping DropOS
  quality-tracking-app.md        ← App mobile suivi livraisons meubles
  happi-website.md               ← Site vitrine H'appi
  demos-clients.md               ← 18 démos HTML clients (multi-secteurs)
  toptiercollection.md           ← Site e-commerce Top Tier Collection

memory/                 ← Index mémoire Claude
  MEMORY_global.md
  MEMORY_quality_tracking.md
  project_dropos.md
  project_happi_foundry.md

claude-config/
  CLAUDE.md             ← Instructions globales Claude Code
```

## Projets chatbot

| Projet | Client | Stack IA | Status |
|--------|--------|----------|--------|
| [SAV-BOT MDF](projects/sav-bot-meuble-de-france.md) | Mobilier de France | OpenAI GPT | Production ⭐ |
| [INnatural Chatbot](projects/innatural-chatbot.md) | INnatural Stores | Claude | Production |
| [Happi Secretary](projects/happi-secretary.md) | Multi-clients | Claude + Vapi | Production |

## Plateformes & SaaS

| Projet | Type | Status |
|--------|------|--------|
| [Happi Foundry](projects/happi-foundry.md) | Playground Claude IA | Production |
| [DropOS](projects/dropos.md) | SaaS dropshipping | Planning/MVP |
| [Quality Tracking App](projects/quality-tracking-app.md) | App mobile | Production |
| [Top Tier Collection](projects/toptiercollection.md) | E-commerce | Active |
| [H'appi Website](projects/happi-website.md) | Site vitrine | Live |

## Démos clients (18 showcases HTML)

Voir [projects/demos-clients.md](projects/demos-clients.md) — secteurs couverts :
Meuble · Hôtellerie · Agroalimentaire · BTP · Industrie · Transport · Notariat · Finance · Sport · E-commerce · KYC

## Mise à jour automatique

L'agent **Happi Brain — Veille Tech Quotidienne** tourne chaque jour à **9h00 (GMT+2)** et ajoute une section veille tech dans `happi_brain.md`.

Sources : HackerNews · DEV.to · GitHub Trending · The New Stack · InfoQ

## Comment utiliser

1. Claude Code charge automatiquement `~/CLAUDE.md` → pointe vers ce brain
2. Après chaque nouveau projet terminé, dis à Claude : **"mets à jour le Happi Brain"**
3. Faire un `git pull` dans le repo local pour récupérer la veille du matin

---
*H'appi — happi-bot.com | Franco-égyptienne, chatbots IA sur-mesure*
