---
name: INnatural Stores Chatbot
type: chatbot
status: production-ready
client: INnatural (innaturalstores.com)
sector: E-commerce / Cosmétiques naturels
repo: Innaturalstores-Chatbot
---

# INnatural Stores Chatbot

## Contexte
Chatbot e-commerce bilingue (Arabe/Anglais) pour INnatural, boutique de cosmétiques naturels. Premier chatbot H'appi utilisant Claude (Anthropic) directement.

## Stack
- **Backend** : Node.js (Express) + Redis (sessions)
- **IA** : Claude (Anthropic) — `claudeService.js`
- **Frontend** : Widget JS embeddable (1 script tag)
- **Deploy** : Docker + Railway + Vercel (widget)

## Features
- Bilingue Arabe / Anglais (auto-detect)
- Recommandations par type de cheveux et problèmes capillaires
- Support produits, ingrédients, usage
- Aide commandes et suivi livraison
- Collecte de leads (nom, email, téléphone)
- Widget embeddable sur n'importe quel site
- Qualification en 3 phases
- Redis session manager
- Monitoring et compression

## Architecture
```
widget/
  chatbot.js      → logique principale du widget
  chatbot.css     → styles
  embed.js        → 1 script tag pour intégrer
  index.html      → page démo

backend/
  server.js           → serveur Express
  claudeService.js    → intégration Claude AI
  productKnowledge.js → moteur recommandations
  qualification-system.js → qualification 3 phases
  guided-flow-manager.js  → gestion du flow conversationnel
  redis-session-manager.js → sessions Redis
  benefitsMatchingSystem.js → matching besoins/produits
  monitoring.js       → métriques et logs
  synonyms.js         → dictionnaire synonymes
  
config/
  products.json       → catalogue produits (éditable par client)
  faqs.json           → FAQ (éditable par client)
  bot-personality.json → personnalité et ton du bot

prisma/             → schema DB (optionnel)
scripts/            → scripts d'import catalogue
```

## Système de qualification 3 phases
```
Phase 1 — Identification : type de cheveux, problèmes, routine actuelle
Phase 2 — Qualification  : produits qui correspondent, ingrédients actifs
Phase 3 — Conversion     : recommandation finale + collecte lead
```

## Intégration widget (côté client)
```html
<script src="https://ton-domaine.com/embed.js"></script>
```

## Leçons apprises
- La qualification en 3 phases convertit mieux qu'un simple Q&A
- Les fichiers JSON de config permettent au client de modifier sans dev
- Toujours prévoir un widget embeddable — les clients ont déjà un site
- Redis indispensable pour maintenir le contexte entre messages
- Le matching synonymes améliore la compréhension (cheveux secs = cheveux déshydratés)
- Prévoir des tests de scénarios complets (`test-chatbot-scenarios.js`)
