---
name: Happi Secretary
type: vocal-ai
status: production-ready
client: Multi-clients (SaaS)
sector: Secrétariat IA / Téléphonie
repo: Happi-Secretary
---

# Happi Secretary — Secrétariat IA Vocal 24h/24

## Contexte
Système de secrétariat IA vocal pour entreprises. Répond aux appels entrants 24h/24, prend des RDV en direct, transcrit et notifie. Produit SaaS multi-clients.

## Stack
- **Backend** : FastAPI + PostgreSQL + SQLAlchemy async
- **IA** : Claude (Anthropic) — conversation + analyse post-appel
- **Téléphonie** : Vapi.ai — appels entrants/sortants, latence <500ms
- **Voice** : ElevenLabs (TTS) + Deepgram (STT)
- **Calendar** : Cal.com API — prise de RDV en direct pendant l'appel
- **Notifications** : Resend (email) + Twilio (SMS)
- **Dashboard** : Next.js 14 + Tailwind CSS
- **Deploy** : Docker + docker-compose

## Flow d'appel complet
```
Appelant → Vapi.ai → POST /api/vapi/webhook (assistant-request)
                   → Claude construit réponse avec KB client + règles
                   → ElevenLabs synthétise la voix
                   → [book_appointment] → Cal.com API
                   → [transfer_call]   → Transfert Vapi
                   → [take_message]    → Email + SMS instantané
Fin d'appel → POST /api/vapi/webhook (end-of-call-report)
            → Claude analyse : résumé + sentiment + intention
            → Email transcript + SMS résumé envoyés
            → Webhook CRM déclenché
```

## Features
- Réponse appels entrants 24h/7j avec message d'accueil personnalisé
- Prise de RDV pendant l'appel (sync Cal.com temps réel)
- FAQ depuis base de connaissance configurable (PDF, URL, texte)
- Routage intelligent avec résumé pour l'humain
- Prise de message + transcription email/SMS instantanée
- Support niveau 1 avec auto-escalation
- Prise de commandes
- Détection sentiment (positif / négatif / urgent)
- Reconnaissance appelants VIP
- Analyse IA post-appel (résumé, intention, résultat)
- Dashboard analytique (Next.js)
- Webhook CRM push (HubSpot, Pipedrive, Zapier, Make)
- Multilangue auto-detect (FR/EN/ES)
- Enregistrement appels (RGPD compliant)

## Structure backend
```
backend/
  app/
    main.py
    routers/
      vapi.py      → webhooks Vapi.ai
      calls.py     → historique appels
      clients.py   → gestion clients multi-tenant
      kb.py        → base de connaissance
    services/
      claude_service.py   → conversation + analyse
      calendar_service.py → Cal.com intégration
      notification_service.py → Resend + Twilio
      crm_service.py      → webhooks CRM
    models/        → DB models
  requirements.txt

dashboard/         → Next.js 14 analytics
docker-compose.yml
```

## Configuration par client (multi-tenant)
Chaque client configure :
- Message d'accueil personnalisé
- Base de connaissance (FAQ, produits, procédures)
- Règles de routage et escalation
- Intégrations CRM et calendar
- VIP list

## Leçons apprises
- Vapi.ai est le meilleur pour la téléphonie IA (latence <500ms)
- Claude supérieur à GPT pour les analyses post-appel (compréhension contexte long)
- Toujours intégrer webhook CRM dès le départ — les clients le demandent toujours
- Cal.com API simple à intégrer et fiable
- ElevenLabs + Deepgram = meilleure combinaison TTS/STT qualité/prix
- La détection VIP améliore énormément la satisfaction client
