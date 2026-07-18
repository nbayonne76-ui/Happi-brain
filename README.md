# 🧠 Happi Brain

> Base de connaissance centrale de H'appi — cerveau évolutif de Claude pour tous les projets.

## Structure

```
happi_brain.md          ← Cerveau historique : sections 1-13 (stack, patterns, clients, règles
                           Claude) + ~90 sections "Veille Tech" ajoutées chaque jour depuis avril
                           2026 par l'agent automatique — toujours actif, ne pas archiver
README.md               ← Ce fichier

projects/               ← Fiche détaillée de chaque projet (curées à la main)
  sav-bot-meuble-de-france.md    ← Chatbot SAV Mobilier de France ⭐
  innatural-chatbot.md           ← Chatbot e-commerce INnatural (cosmétiques)
  happi-secretary.md             ← Secrétariat IA vocal 24h/24
  happi-foundry.md               ← Playground Claude IA (interne)
  dropos.md                      ← SaaS dropshipping DropOS
  quality-tracking-app.md        ← App mobile suivi livraisons meubles
  happi-website.md               ← Site vitrine H'appi
  demos-clients.md               ← 18 démos HTML clients (multi-secteurs)
  toptiercollection.md           ← Site e-commerce Top Tier Collection
  microsoft-sales-app.md         ← Sales intelligence + agents autonomes (pattern SaaS réutilisable)

memory/                 ← Mémoire Claude Code, réorganisée en 10 fichiers thématiques (juillet 2026)
  MEMORY.md                      ← Index de ces 10 fichiers — À LIRE EN PREMIER
  happi_brain_core.md            ← Identité, stack, env dev WSL2, deploy
  happi_brain_chatbots.md        ← SAV-Bot, INnatural, Secretary, 18 showcases
  happi_brain_platforms.md       ← DropOS, Quality Tracking, TopTier, Microsoft Sales App
                                    (journal de session le plus à jour pour ce dernier)
  happi_brain_crm.md             ← Happi CRM — 28+ sprints, 130+ endpoints
  happi_brain_scraper.md         ← ERP Scraper UK — 23 scrapers
  happi_brain_website.md         ← Site vitrine H'appi (détails techniques)
  happi_brain_prompts.md         ← Règles IA, prompts, checklists
  happi_brain_inspiration.md     ← Veille GitHub (patterns réutilisables)
  happi_brain_microsoft_kb.md    ← Catalogue des 67 solutions Microsoft (contenu KB, pas l'archi)
  happi_brain_automate.md        ← H'appi Automate (nouveau SaaS, roadmap)
  MEMORY_global.md               ← Mémoire globale (antérieure à la réorg. de juillet)
  MEMORY_quality_tracking.md     ← Mémoire spécifique Quality Tracking App
  project_dropos.md              ← Mémoire spécifique DropOS
  project_happi_foundry.md       ← Mémoire spécifique Happi Foundry
  project_microsoft_sales_app.md ← Constat stratégique : pattern SaaS réutilisable, PAS un CDP

claude-config/
  CLAUDE.md             ← Instructions globales Claude Code (pointe vers ce brain)
```

> ⚠️ Deux systèmes coexistent : `happi_brain.md` (racine) est le cerveau historique, mis à jour
> quotidiennement par l'agent de veille tech. Le dossier `memory/` est la mémoire Claude Code,
> réorganisée en 10 fichiers thématiques en juillet 2026 — **`memory/MEMORY.md` est l'index à
> consulter pour retrouver l'état le plus à jour d'un projet donné.**

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
| [Microsoft Sales App](projects/microsoft-sales-app.md) | Sales intelligence (agents + KB, multi-tenant) | Production |
| H'appi Automate *(repo séparé : `happi-automate`)* | Orchestrateur workflows (comparable Azure Logic Apps) — voir `memory/happi_brain_automate.md` | MVP / Sprint 1 |
| Happi CRM *(pas de fiche `projects/` dédiée)* | CRM complet — voir `memory/happi_brain_crm.md` | Production |
| ERP Scraper UK *(pas de fiche `projects/` dédiée)* | Intelligence appels d'offres UK — voir `memory/happi_brain_scraper.md` | Production |

## Démos clients (18 showcases HTML)

Voir [projects/demos-clients.md](projects/demos-clients.md) — secteurs couverts :
Meuble · Hôtellerie · Agroalimentaire · BTP · Industrie · Transport · Notariat · Finance · Sport · E-commerce · KYC

## Mise à jour automatique

L'agent **Happi Brain — Veille Tech Quotidienne** tourne chaque jour à **9h00 (GMT+2)** et ajoute une section veille tech dans `happi_brain.md`.

Sources : HackerNews · DEV.to · GitHub Trending · The New Stack · InfoQ

## Comment utiliser

1. Claude Code charge automatiquement `~/CLAUDE.md` → pointe vers ce brain
2. Pour l'état le plus récent d'un projet : commencer par `memory/MEMORY.md`, puis le fichier
   thématique correspondant (ex. `memory/happi_brain_platforms.md` pour Microsoft Sales App)
3. Après chaque nouveau projet terminé, dis à Claude : **"mets à jour le Happi Brain"**
4. Faire un `git pull` dans le repo local pour récupérer la veille du matin

---
*H'appi — happi-bot.com | Franco-égyptienne, chatbots IA sur-mesure*
