---
name: H'appi Website
type: corporate-website
status: live
client: H'appi (interne)
sector: Site vitrine startup
repo: h-appi-website
deploy: h-appi-website.vercel.app
---

# H'appi Website — Site Vitrine Corporate

## Contexte
Site corporate de H'appi. Présente les services (chatbots, apps web, mobile, supply chain), les cas clients, les tarifs et un atelier de configuration de bot.

## Stack
- **Framework** : Next.js + TypeScript
- **Styling** : Tailwind CSS
- **Internationalisation** : next-intl (routes `[locale]/`)
- **Deploy** : Vercel

## Structure des pages
```
app/[locale]/
  page.tsx           → Home
  atelier/           → Atelier de configuration bot (BotConfigurator)
  blog/              → Blog / News (NewsSection)
  ...

components/
  atelier/
    BotConfigurator.tsx  → Configurateur de chatbot interactif
  blog/
    NewsSection.tsx      → Section actualités
```

## Features
- Site multilingue (FR minimum)
- Atelier : configurateur de chatbot interactif pour prospects
- Blog / veille tech (alimenté par Happi Brain Agent ?)
- Présentation services + pricing
- Case studies clients

## Leçons apprises
- L'atelier de configuration est un excellent outil de conversion (prospects peuvent voir leur futur bot)
- next-intl pour l'i18n : structure `app/[locale]/` + fichiers de traduction
