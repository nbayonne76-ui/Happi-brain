---
name: Happi Brain
description: Base de connaissance centrale de tous les projets H'appi — sert de cerveau évolutif pour la création de chatbots et solutions IA
type: project
---

# 🧠 HAPPI BRAIN — Base de connaissance centrale

> Ce fichier est le cerveau évolutif de Claude pour tous les projets H'appi.
> Il doit être consulté EN PRIORITÉ pour tout nouveau projet chatbot, IA ou développement client.
> Il doit être MIS À JOUR après chaque nouveau projet terminé.

---

## 1. IDENTITÉ H'APPI

**Startup franco-égyptienne** lancée début 2026.
- **Mission** : Créer des chatbots IA sur-mesure et solutions digitales pour les entreprises françaises
- **Positionnement** : CX (expérience client) + Supply Chain + Secrétariat IA
- **Philosophie** : "Qualité avant quantité" — personnalisation radicale, pas de solutions génériques
- **Site** : happi-bot.com
- **Tarification** :
  - Implémentation : devis personnalisé (50-70% sous le marché)
  - Maintenance Essential : inclus
  - Maintenance Pro : 100-500€/mois
  - Maintenance Enterprise : 500-2000€/mois avec SLA
- **Conformité** : RGPD, hébergement France/Europe (Scaleway, Hetzner), ISO 27001

---

## 2. STACK TECHNIQUE DE RÉFÉRENCE H'APPI

### Stack chatbot standard (à réutiliser)
```
Backend   → FastAPI (Python) + PostgreSQL + SQLAlchemy + Alembic
Frontend  → Next.js 14 (App Router) + TypeScript + Tailwind CSS
IA        → Claude (Anthropic SDK) — modèle préféré pour tous les chatbots
Voice     → Vapi.ai (téléphonie) + ElevenLabs (TTS) + Deepgram (STT)
Auth      → JWT
Deploy    → Docker + docker-compose + Railway / Vercel
Notifs    → Resend (email) + Twilio (SMS)
Calendar  → Cal.com API
CRM       → Webhooks HubSpot / Pipedrive / Zapier / Make
```

### Stack démo/showcase clients (rapide à livrer)
```
HTML + CSS + JS vanilla (léger, rapide à déployer)
Hébergement → Vercel (domaine : happi-[client].vercel.app)
```

### Stack SaaS / Plateformes
```
Frontend  → Next.js 16 (App Router, Turbopack) + TypeScript + Tailwind CSS v4
Backend   → FastAPI + PostgreSQL
State     → Zustand + persist middleware (web & mobile)
Mobile    → React Native (Expo SDK 54)
Animation → Framer Motion
DnD       → @dnd-kit/core + @dnd-kit/sortable
```

### Stack Web Builder (happi-webcreator)
```
Framework → Next.js 16.2.2 + TypeScript + Tailwind CSS v4
State     → Zustand + persist (projets en localStorage)
DnD       → @dnd-kit/core + @dnd-kit/sortable (sections réordonnables)
Animation → Framer Motion
Export    → HTML standalone via Blob + URL.createObjectURL (zéro dépendance)
Preview   → Route /preview/[id] (rendu propre sans chrome éditeur)
Blocs     → 13 types : navbar, hero, features, stats, cta, pricing, faq,
            testimonials, logowall, footer, text, image, divider
```

---

## 3. PROJETS CHATBOT — CATALOGUE COMPLET

### 3.1 SAV-BOT Mobilier de France ⭐ (projet phare)
- **Repo** : `SAV-BOT-Meuble-de-france`
- **Client** : Mobilier de France (enseigne meuble)
- **Type** : Chatbot SAV après-vente + ticketing
- **Stack** : FastAPI + React + PostgreSQL + Redis + Docker
- **IA** : OpenAI (GPT)
- **Features clés** :
  - Dialogue naturel multilingue (FR, EN, AR, IT, DE)
  - Recommandations produits intelligentes
  - Upload photo + analyse défauts visuels
  - Ticketing automatique avec priorité P0-P3
  - Support vocal (speech recognition + synthesis)
  - 351+ tests, CI/CD pipeline complet
  - Monitoring santé + métriques
- **Deploy** : Docker + Railway
- **Couverture tests** : Backend 62%, Frontend 53%
- **Leçons** : Toujours intégrer un système de priorité de tickets. Les clients SAV ont besoin de photos. Le multilingue est critique pour la France.

### 3.2 INnatural Stores Chatbot
- **Repo** : `Innaturalstores-Chatbot`
- **Client** : INnatural (cosmétiques naturels)
- **Type** : Chatbot e-commerce produits + support
- **Stack** : Node.js (Express) + widget JS embeddable
- **IA** : Claude (Anthropic)
- **Features clés** :
  - Bilingue Arabe/Anglais
  - Recommandations par type de cheveux
  - Collecte de leads
  - Widget embeddable (1 script tag)
  - Catalogue produits + FAQ configurables (JSON)
  - Système de qualification en 3 phases
  - Redis session manager
- **Architecture** : widget/ + backend/ + config/ (products.json, faqs.json, bot-personality.json)
- **Leçons** : La qualification en 3 phases convertit mieux. Le JSON de config permet aux clients de modifier sans dev. Toujours prévoir un widget embeddable.

### 3.3 Happi Secretary (Secrétariat IA vocal)
- **Repo** : `Happi-Secretary`
- **Type** : Secrétariat IA vocal 24h/24 pour entreprises
- **Stack** : FastAPI + PostgreSQL + Next.js 14 + Docker
- **IA** : Claude (Anthropic) — conversation + analyse post-appel
- **Téléphonie** : Vapi.ai (latence <500ms)
- **Voice** : ElevenLabs TTS + Deepgram STT
- **Calendar** : Cal.com API
- **Notifs** : Resend + Twilio
- **Features clés** :
  - Réponse appels entrants 24h/7j
  - Prise de RDV en direct pendant l'appel
  - FAQ depuis base de connaissance (PDF, URL, texte)
  - Routage intelligent + résumé humain
  - Transcription + envoi email/SMS immédiat
  - Support L1 avec auto-escalation
  - Détection sentiment (positif/négatif/urgent)
  - Reconnaissance appelants VIP
  - Analyse IA post-appel (résumé, intention, résultat)
  - Dashboard analytique
  - Webhook CRM (HubSpot, Pipedrive, Zapier, Make)
  - Multilangue auto (FR/EN/ES)
  - Enregistrement RGPD-compliant
- **Flow d'appel** :
  ```
  Caller → Vapi.ai → /api/vapi/webhook → Claude → ElevenLabs
  → [book_appointment] → Cal.com
  → [transfer_call] → Vapi transfer
  → [take_message] → Email + SMS
  End → Claude analyse → Email transcript + SMS summary + CRM webhook
  ```
- **Leçons** : Vapi.ai est le meilleur pour la téléphonie IA (<500ms). Claude est supérieur à GPT pour les analyses post-appel. Toujours intégrer webhook CRM dès le départ.

---

## 4. PROJETS SHOWCASE CLIENTS (démos HTML statiques)

Ces projets sont des démos/présentations pour convaincre les clients. Stack : HTML/CSS/JS → Vercel.

| Repo | Client | Secteur | URL |
|------|--------|---------|-----|
| Happi-Audit-Expert | Cabinet audit | Finance | happi-audit-expert.vercel.app |
| Happi-Benta | Benta | Commerce | happi-benta.vercel.app |
| Happi-Cabinet-Arc | Cabinet Arc | Juridique | happi-cabinet-arc.vercel.app |
| Happi-Charier | Charier | BTP/Construction | happi-charier.vercel.app |
| Happi-Groupe-Bellion | Groupe Bellion | Industrie | happi-groupe-bellion.vercel.app |
| Happi-Groupe-Monassier | Groupe Monassier | Notariat | happi-groupe-monassier.vercel.app |
| Happi-Groupe-Trouillet | Groupe Trouillet | Transport | happi-groupe-trouillet.vercel.app |
| Happi-Icelec | Icelec | Électronique | happi-icelec.vercel.app |
| Happi-KingKong | King Kong | E-commerce | happi-king-kong.vercel.app |
| Happi-labeyrie-fine-foods | Labeyrie | Agroalimentaire | happi-labeyrie-fine-foods.vercel.app |
| happi-lavorel-hotels | Lavorel Hotels | Hôtellerie | happi-lavorel-hotels.vercel.app |
| Happi-Mademoiselledesserts | Mademoiselle Desserts | Agroalimentaire | happi-mademoiselledesserts.vercel.app |
| happi-monsieur-meuble | Monsieur Meuble | Meuble | happi-monsieur-meuble.vercel.app |
| Happi-Plastivaloire | Plastivaloire | Plasturgie/Industrie | happi-plastivaloire.vercel.app |
| Happi-Saint-Jean | Saint-Jean | Agroalimentaire | happi-saint-jean.vercel.app |
| Uqudo-Presentation | Uqudo | Identité digitale/KYC | uqudo-presentation.vercel.app |
| L-OL-presentation- | L'OL | Sport/Football | l-ol-presentation.vercel.app |
| MDF.com | Mobilier de France | Meuble | mdf-com.vercel.app |

**Leçon** : Les démos HTML statiques Vercel se livrent en <1 jour. C'est la meilleure façon d'obtenir un accord client avant de développer le vrai bot.

---

## 5. PLATEFORMES ET SAAS

### Happi Web Creator (web builder SaaS)
- **Repo** : `happi-webcreator`
- **Type** : Éditeur de sites web no-code (inspiré Webflow/Framer)
- **Stack** : Next.js 16 + Zustand + @dnd-kit + Framer Motion
- **URL** : github.com/nbayonne76-ui/happi-webcreator
- **Features clés** :
  - 13 blocs configurables (navbar, hero, features, stats, pricing, faq, testimonials, etc.)
  - Éditeur visuel : drag-and-drop sections, propriétés par panneau latéral
  - Couleurs de fond par section (16 presets : dark/light/gradient) + textes adaptatifs auto
  - Espacement vertical (5 niveaux) + largeur contenu (4 niveaux) par section
  - Preview plein écran `/preview/[id]` avec switcher desktop/tablet/mobile
  - Export HTML standalone (zéro dépendance, déployable Vercel en 1 clic)
  - Undo/redo (20 étapes), gestion multi-pages, SEO par page
  - Galerie de templates (6 catégories), générateur IA par prompt
- **Leçons** :
  - Pour DnD + Framer Motion sur le même canvas : utiliser @dnd-kit uniquement dans les Layers, éviter les conflits avec AnimatePresence
  - Export HTML avec styles inline = plus robuste que Tailwind CDN pour déploiement client
  - Le panneau SEO avec prévisualisation Google SERP est très apprécié

### Happi Foundry (playground IA interne)
- **Repo** : `Happi-Foundry`
- **Type** : Claude AI playground + gestion de prompts (inspiré Azure AI Foundry)
- **Stack** : Next.js 14 + FastAPI + PostgreSQL + Anthropic SDK
- **Features** :
  - Playground interactif (streaming, model selector, temperature, max-tokens)
  - Bibliothèque de prompts (tags, recherche)
  - Catalogue de modèles Claude avec pricing
  - Dashboard usage (tokens, coûts, historique)
- **Usage interne** : Tester et affiner les prompts avant déploiement client

### DropOS (SaaS dropshipping)
- **Repo** : `DropOS-DropShipping`
- **Type** : Plateforme SaaS all-in-one pour dropshippers
- **Stack** : Next.js + FastAPI + PostgreSQL + JWT
- **Target** : Dropshippers $10K-$200K/mois
- **Pricing** : $99-149/mois (remplace $400-1000/mois d'outils)
- **Roadmap** : Phase 1 Analytics → Phase 2 Fulfillment → Phase 3 Sourcing → Phase 4 Marketing
- **Intégrations** : Shopify Partner API, tarifs douaniers US HTS / EU TARIC

### Quality Tracking App (Mobilier de France)
- **Repo** : `Quality-tracking-app`
- **Type** : App mobile de suivi qualité livraisons meubles
- **Stack** : React Native (Expo SDK 54) + FastAPI + PostgreSQL
- **Rôles** : Supplier, Driver, Client, Admin, Showroom
- **State** : Zustand + AsyncStorage (offline sync)
- **Auth** : JWT avec auto-refresh

### Top Tier Collection (e-commerce)
- **Repo** : `toptiercollection.shop`
- **Type** : Site e-commerce
- **Stack** : Next.js + Sanity CMS + TypeScript + Tailwind

### H'appi Website (site vitrine)
- **Repo** : `h-appi-website`
- **Type** : Site corporate H'appi
- **Stack** : Next.js 14 + TypeScript + Tailwind CSS + Framer Motion + next-intl
- **Deploy** : happi-bot.com (Vercel, master branch)
- **i18n** : next-intl — FR/EN, fichiers `messages/fr.json` + `messages/en.json`
- **Pages** : Home, Atelier, Cas d'usage, Blog, Quiz, Contact
- **Voir section 12** pour le design system complet et le processus de refonte

### Microsoft Sales App
- **Repo** : `microsoft-sales-app`
- **Type** : Sales intelligence + agents autonomes (multi-tenant depuis 07/2026)
- **Stack** : Next.js 15 + Prisma + Neon Postgres + NextAuth + GPT-4o-mini + Tavily
- **Pattern clé** : watchlist compte → signaux externes (Tavily/DDG) → scoring regex → synthèse
  GPT ancrée KB → persistance par utilisateur → brief périodique. Réutilisable pour un futur
  SaaS de sales intelligence (catégorie ZoomInfo/Klue, PAS un CDP type D365 Customer Insights)
  en remplaçant la KB et les signaux par ceux d'un autre client/secteur.
- **Détails complets** : voir [projects/microsoft-sales-app.md](projects/microsoft-sales-app.md)

---

## 6. SECTEURS CLIENTS COUVERTS

Basé sur les démos et projets réels :

| Secteur | Clients | Use cases chatbot |
|---------|---------|-------------------|
| Meuble/Déco | Mobilier de France, Monsieur Meuble | SAV, recommandations produits, suivi livraison |
| Hôtellerie | Lavorel Hotels | Réservation, concierge, FAQ |
| Agroalimentaire | Labeyrie, Saint-Jean, Mademoiselle Desserts | Support produits, recettes, SAV |
| BTP/Construction | Charier | Devis, planning, support technique |
| Industrie | Plastivaloire, Icelec | Support technique, commandes |
| Transport/Logistique | Groupe Trouillet | Suivi, dispatch, SAV |
| Notariat/Juridique | Groupe Monassier, Cabinet Arc | FAQ, RDV, information juridique |
| Finance/Audit | Audit Expert | FAQ, onboarding client |
| Sport | L'OL (Olympique Lyonnais) | Fan engagement, billetterie, infos |
| E-commerce | KingKong, INnatural, TopTier | Recommandations, suivi commande, support |
| KYC/Identité | Uqudo | Onboarding, vérification, support |

---

## 7. PATTERNS ARCHITECTURE CHATBOT (bonnes pratiques)

### Pattern 1 : Widget embeddable (pour site existant client)
```
widget/
  chatbot.js      → logique principale
  chatbot.css     → styles
  embed.js        → 1 script tag pour intégrer
backend/
  server.js       → Express ou FastAPI
  claudeService.js → intégration Claude
  productKnowledge.js → base de connaissance
config/
  products.json   → catalogue (éditable par client)
  faqs.json       → FAQ (éditable par client)
  bot-personality.json → personnalité (ton, langue)
```

### Pattern 2 : Chatbot full-stack (projet complet)
```
frontend/       → React / Next.js
backend/
  app/
    main.py
    routers/    → chat, auth, tickets, webhooks
    models/     → DB models
    services/   → claude_service, email_service...
  alembic/      → migrations DB
  requirements.txt
docker-compose.yml
```

### Pattern 4 : Web Builder no-code
```
src/
  app/
    dashboard/    → galerie projets + création
    editor/[id]/  → éditeur visuel (Topbar + Sidebar + Canvas + PropertiesPanel)
    preview/[id]/ → rendu propre sans chrome (utilisé aussi pour export)
    templates/    → galerie templates
    generate/     → générateur IA par prompt
  components/
    blocks/       → 1 fichier par type de bloc (HeroBlock, FeaturesBlock...)
    editor/       → Topbar, Sidebar, Canvas, PropertiesPanel
  lib/
    blockStyles.ts → helpers bg/padding/width + couleurs adaptatives dark/light
    defaults.ts    → props par défaut de chaque bloc + templates
    exportHtml.ts  → génère HTML standalone avec styles inline
  store/
    useEditorStore.ts → Zustand (projets, blocs, pages, undo/redo, SEO)
  types/index.ts  → Block, Page (+ seo), Project, Template...
```

### Pattern 3 : Secrétariat vocal
```
Vapi.ai webhook → FastAPI → Claude → ElevenLabs
                         → Cal.com (booking)
                         → Resend + Twilio (notifs)
                         → DB (logs + analytics)
dashboard/      → Next.js (analytics, historique)
```

### Système de qualification en 3 phases (conversion optimale)
```
Phase 1 : Identification → qui est l'utilisateur ? quel besoin ?
Phase 2 : Qualification → quel produit/service correspond ?
Phase 3 : Conversion → proposition + collecte lead / action
```

### Système de tickets priorité (SAV)
```
P0 → Urgence (sécurité, défaut grave)    → notification immédiate
P1 → Haute priorité (produit inutilisable) → <4h
P2 → Normale (problème fonctionnel)       → <24h
P3 → Basse (cosmétique, info)             → <72h
```

---

## 8. RÈGLES IA ET PROMPTS (ce qui fonctionne)

### Modèle préféré : Claude (Anthropic)
- **Pourquoi Claude** : Meilleur pour l'analyse post-appel, la compréhension du contexte long, le français naturel
- **SDK** : `anthropic` (Python) ou `@anthropic-ai/sdk` (Node.js)
- **Modèles recommandés** (avril 2026) :
  - Opus 4.6 (`claude-opus-4-6`) → tâches complexes, analyse
  - Sonnet 4.6 (`claude-sonnet-4-6`) → chatbot standard ← **défaut recommandé**
  - Haiku 4.5 (`claude-haiku-4-5-20251001`) → réponses rapides, faible coût

### Structure prompt système pour chatbot client
```
Tu es [NOM_BOT], l'assistant IA de [NOM_ENTREPRISE].
Tu aides les clients avec [USE_CASE].

PERSONNALITÉ : [ton, langue, formules de politesse]
LIMITES : Tu ne réponds qu'aux questions relatives à [DOMAINE]. Pour tout autre sujet, redirige vers [CONTACT].
BASE DE CONNAISSANCE : [produits, FAQ, procédures]
ACTIONS DISPONIBLES : [book_appointment, create_ticket, collect_lead, transfer_to_human]
LANGUE : Réponds toujours dans la langue de l'utilisateur.
```

### Gestion multilingue
- Détecter automatiquement la langue de l'utilisateur
- Priorité : FR > EN > AR pour les clients H'appi France
- Toujours prévoir FR/EN minimum

---

## 9. CHECKLIST NOUVEAU PROJET CHATBOT

Avant de commencer tout nouveau chatbot :

- [ ] Définir le secteur et le use case principal
- [ ] Choisir le pattern (widget / full-stack / vocal)
- [ ] Configurer `bot-personality.json` ou équivalent
- [ ] Construire la base de connaissance (produits, FAQ, procédures)
- [ ] Définir les actions disponibles (tickets, booking, lead, transfert)
- [ ] Choisir le modèle Claude adapté (coût vs performance)
- [ ] Prévoir multilingue dès le départ
- [ ] Intégrer un système de logs/analytics
- [ ] Prévoir webhook CRM si le client en a un
- [ ] Créer une démo HTML statique Vercel avant le dev complet
- [ ] Tester la qualification en 3 phases
- [ ] Documenter l'API et créer un guide d'installation client

---

## 10. DEPLOY & INFRA

### Railway (backend + DB)
- Idéal pour FastAPI + PostgreSQL
- Fichiers nécessaires : `railway.json`, `nixpacks.toml`, `Procfile`
- Variables d'environnement via Railway Dashboard

### Vercel (frontend + démos)
- Next.js et HTML statiques → déploiement automatique depuis GitHub
- Domaine : `happi-[client].vercel.app` pour les démos
- `EXPO_PUBLIC_API_URL` pour les apps Expo

### Docker (dev local + prod)
- `docker-compose.yml` avec services : backend, frontend, postgres, redis
- Port 8000 souvent bloqué sur WSL2 → utiliser **8001** par défaut
- Commande standard : `docker-compose up -d`

---

## 11. ÉVOLUTION DU BRAIN

### Comment mettre à jour ce fichier
Après chaque nouveau projet terminé, ajouter :
1. Une entrée dans la section 3 (chatbots) ou 5 (plateformes)
2. Le secteur client dans la section 6
3. Tout nouveau pattern découvert dans la section 7
4. Tout nouveau prompt qui fonctionne dans la section 8

### Métriques de succès à tracker par projet
- Taux de résolution autonome (cible : 80%+)
- Temps de réponse moyen (cible : <2s)
- Taux de satisfaction client (cible : 4.5/5+)
- Coût par conversation (optimiser avec Haiku pour les cas simples)

---

## ⚠️ SEUIL DE MIGRATION — HAPPI BRAIN V2

**Projets actifs actuellement : 3 chatbots + 5 plateformes = 8 projets**

> Quand ce chiffre dépasse **15 projets actifs**, migrer vers **Happi Brain V2 (Clean Room)**.

### Pourquoi V2 à 15 projets ?
Au-delà de 15 projets, ce fichier markdown devient trop volumineux pour être lu linéairement de façon efficace. La recherche sémantique devient indispensable.

### Architecture V2 (Clean Room)
```
happi-brain-v2/
  api/           → FastAPI — CRUD entités + endpoint RAG
  db/            → PostgreSQL + pgvector (recherche vectorielle)
    projects/    → table structurée (stack, features, leçons)
    patterns/    → patterns réutilisables indexés
    tech_news/   → veille quotidienne vectorisée
    clients/     → fiches clients avec secteur + use cases
  agent/         → agent de veille (écrit en DB, pas en markdown)
  mcp/           → serveur MCP → Claude l'interroge comme un outil
```

### Ce que V2 apporte
- Recherche sémantique : `search_brain("chatbot hôtellerie")` → résultats pertinents
- Mise à jour par entité (upsert) plutôt qu'append
- MCP server : Claude interroge le Brain comme un outil natif
- Peut devenir un produit vendable aux clients H'appi ("mémoire IA de votre entreprise")

### Comment migrer
1. Créer le repo `happi-brain-v2` avec FastAPI + pgvector
2. Importer tous les fichiers `projects/*.md` actuels via script d'ingestion
3. Configurer le MCP server dans `~/.claude/settings.json`
4. Mettre à jour l'agent de veille pour écrire en DB plutôt qu'en markdown

---

---

## 12. DESIGN SYSTEM & ANIMATION — happi-bot.com

> Ce système a été développé et raffiné lors de la refonte complète du site vitrine H'appi (avril 2026).
> Il est réutilisable sur tout projet Next.js nécessitant un rendu premium.

### 12.1 Composants UI réutilisables (`components/ui/`)

| Composant | Fichier | Usage |
|-----------|---------|-------|
| `FadeInUp` | `Animate.tsx` | Apparition scroll-triggered avec délai configurable |
| `ScaleIn` | `Animate.tsx` | Scale 0.9→1 + opacité sur scroll |
| `TiltCard` | `TiltCard.tsx` | Carte 3D perspective au hover (intensity configurable) |
| `MagneticButton` | `MagneticButton.tsx` | Bouton attiré par le curseur (strength 0-1) |
| `AnimatedMesh` | `AnimatedMesh.tsx` | Orbes flottants gradient animés (variant: hero/blue/purple) |

### 12.2 Patterns Framer Motion éprouvés

**Counter animé au scroll** (pour stats/métriques) :
```tsx
const raw = useMotionValue(0);
const spring = useSpring(raw, { stiffness: 55, damping: 18 });
const display = useTransform(spring, v => Math.round(v).toLocaleString());
const inView = useInView(ref, { once: true, margin: '-60px' });
useEffect(() => { if (inView) raw.set(targetValue); }, [inView]);
```

**AnimatePresence avec hauteur 0→auto** (accordéon) :
```tsx
<AnimatePresence>
  {open && (
    <motion.div
      initial={{ height: 0, opacity: 0 }}
      animate={{ height: 'auto', opacity: 1 }}
      exit={{ height: 0, opacity: 0 }}
      transition={{ duration: 0.35, ease: 'easeInOut' }}
    >
      {content}
    </motion.div>
  )}
</AnimatePresence>
```

**Stagger d'éléments** :
```tsx
// Utiliser transition.delay calculé sur l'index
<motion.div
  initial={{ opacity: 0, y: 16 }}
  whileInView={{ opacity: 1, y: 0 }}
  transition={{ delay: index * 0.08 }}
>
```

**Chevron spring** (indicateur d'accordéon) :
```tsx
<motion.div animate={{ rotate: isOpen ? 180 : 0 }} transition={{ type: 'spring', stiffness: 300, damping: 24 }}>
  <ChevronDown />
</motion.div>
```

**Scroll interne chat (ne pas scroller la page)** :
```tsx
// ❌ Mauvais — scrolle toute la page
bottomRef.current?.scrollIntoView({ behavior: 'smooth' });
// ✅ Correct — scrolle uniquement le container
const el = containerRef.current;
if (el) el.scrollTop = el.scrollHeight;
```

### 12.3 Glassmorphism (classe CSS `glass-card`)
```css
/* À définir dans globals.css */
.glass-card {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  backdrop-filter: blur(12px);
}
```

### 12.4 Gradient border (carte premium)
```tsx
<div className="rounded-2xl p-px" style={{
  background: 'linear-gradient(135deg, rgba(59,130,246,0.4), rgba(16,185,129,0.2))'
}}>
  <div className="bg-happi-darker rounded-2xl p-6">{content}</div>
</div>
```

### 12.5 Les 10 outils IA de référence — inspiration design & UI

Utilisés comme **référence visuelle et UX** pour la refonte des pages happi-bot.com.

**Design IA** (UI generation, maquettage, prototypage) :
| Outil | Spécialité |
|-------|-----------|
| Uizard | Génération de maquettes UI par prompt |
| Loqo | Design IA produit / landing pages |
| Playground | Génération d'images et assets visuels |
| Canva | Design graphique + IA générative intégrée |
| Galileo AI | Génération de composants UI complexes |

**Builders IA** (création de sites web par IA) :
| Outil | Spécialité |
|-------|-----------|
| Gamma | Présentations et pages web générées par IA |
| Framer | Sites interactifs no-code + animations |
| Webflow | Web design visuel avancé + CMS |
| Durable | Site web généré en 30 secondes par IA |
| Dora | Sites 3D et interactifs générés par IA |

> Ce sont les benchmarks de qualité visuelle à viser sur toutes les pages H'appi.
> Avant toute refonte de page, aller regarder ces outils pour s'inspirer du niveau de polish attendu.

### 12.6 Méthodologie de refonte page en 5 phases

Utilisée sur les pages **Atelier** et **Cas d'usage** (avril 2026), inspirée du niveau visuel des 10 outils ci-dessus :

| Phase | Focus | Outils / techniques |
|-------|-------|---------------------|
| **1 — Hero & crédibilité** | Transformer le hero en manifeste avec preuves | `AnimatedMesh`, `FadeInUp` stagger, badge client réel (ex: "Mobilier de France · Live 2024") |
| **2 — Métriques impactantes** | Remplacer les % abstraits par des chiffres business concrets | `AnimatedStat` (spring counter), `TiltCard`, before/after context pill |
| **3 — Contenu animé** | Dynamiser accordéons, listes, features | `AnimatePresence` height 0→auto, stagger items, `motion.button` whileHover/whileTap, TiltCard sur mini-stats et actor cards |
| **4 — Démo interactive** | Rendre le bot cliquable et vivant | `AnimatePresence` bubbles (slide from direction), `MagneticButton` CTA, spring reply buttons stagger, spring success banner |
| **5 — Section résultats** | Clôturer avec des outcomes mesurés, nommés, prouvables | 3 `TiltCard` outcome cards, `AnimatedValue` spring scale-in, `AnimatePresence` reveal on scroll |

### 12.7 Blog — Agrégateur RSS live

- **Route** : `app/api/news/route.ts` — `export const revalidate = 3600`
- **Mécanisme** : `Promise.allSettled` sur 15 feeds → dédup par URL → tri newest-first → cap 80
- **Nettoyage** :
  - `decodeEntities()` exécuté 2× (Medium double-encode `&amp;#x2019;`) — **toujours décoder AVANT de stripper les tags HTML**
  - `cleanText()` : normalise `—`, `–`, ` - `, ` | `, ` · `, `--`, `...` → ponctuation propre
  - `NON_LATIN_RE` : filtre les articles en cyrillique/arabe/CJK/hébreu/hindi/thaï
- **Affichage** : `NewsSection.tsx` (tabs par source + compteurs) + `NewsCard.tsx` (link externe)
- **Piège** : `scrollIntoView()` dans un chat scrolle la page entière → utiliser `scrollTop = scrollHeight` sur le container

### 12.8 Couleurs de la charte happi-bot.com

```
happi-blue    → #3B82F6  (actions, liens, badges)
happi-green   → #10B981  (succès, online, validation)
happi-purple  → #8B5CF6  (accent secondaire)
happi-amber   → #F59E0B  (avertissement, timing)
happi-dark    → surface principale
happi-darker  → fond profond
happi-surface → cartes / panels
happi-border  → bordures subtiles
happi-muted   → texte secondaire
gradient-text → classe utilitaire (blue → purple)
```

---

*Dernière mise à jour : 2026-07-06*
*Projets analysés : 28 repos GitHub (nbayonne76-ui)*

---

## 13. ENVIRONNEMENT DE DÉVELOPPEMENT — WSL2 Ubuntu (2026-07-06)

> Audit complet réalisé le 2026-07-06. À re-vérifier à chaque nouvelle machine ou migration.

### 13.1 Core Tools installés

| Outil | Version | Rôle |
|-------|---------|------|
| Node.js | v24.13.0 | Runtime JS/TS |
| npm | 11.6.2 | Package manager |
| pnpm | 10.33.0 | Package manager alternatif |
| Python | 3.11.14 | Backend FastAPI |
| pip | 26.0 | Package manager Python |
| Git | 2.43.0 | Versioning |
| PostgreSQL | 16.11 | Base de données (port 5432, actif) |
| TypeScript | 6.0.2 (global) | Typage statique |
| tsx | 4.21.0 | TypeScript runner direct |

### 13.2 CLIs Déploiement

| CLI | Version | Usage |
|-----|---------|-------|
| Expo CLI | 57.0.4 | React Native / mobile |
| Vercel CLI | 50.44.0 | Deploy frontend Next.js |
| Railway CLI | 4.36.1 | Deploy backend FastAPI |
| Vite | 8.1.3 | Build uk-erp-tender-tracker |

### 13.3 Stack Python — packages globaux

```
fastapi==0.115.0       # API REST
uvicorn==0.30.6        # Serveur ASGI
sqlalchemy==2.0.49     # ORM
alembic==1.18.4        # Migrations DB
pydantic==2.12.5       # Validation données
anthropic==0.116.0     # SDK Claude (mis à jour 0.34 → 0.116)
passlib==1.7.4         # Hachage mots de passe
bcrypt==3.2.2          # Chiffrement
httpx==0.27.2          # HTTP async client
python-multipart       # Upload fichiers
python-jose==3.5.0     # JWT tokens (installé le 2026-07-06)
```

> ⚠️ **python-jose** était absent — installé le 2026-07-06. Obligatoire pour l'auth JWT dans tous les backends.
> ⚠️ **anthropic SDK** mis à jour de 0.34.2 → 0.116.0. Toujours mettre à jour avant un nouveau projet.

### 13.4 Extensions VS Code — liste complète (30 extensions)

#### Déjà en place (avant audit)
- `anthropic.claude-code` — Claude Code CLI
- `bradlc.vscode-tailwindcss` — Tailwind IntelliSense
- `christian-kohler.path-intellisense` — Autocomplétion chemins
- `codium.codium` — CodiumAI
- `cweijan.vscode-postgresql-client2` — Client PostgreSQL
- `dbaeumer.vscode-eslint` — ESLint
- `dsznajder.es7-react-js-snippets` — Snippets React/TS
- `eamodio.gitlens` — Git avancé
- `esbenp.prettier-vscode` — Formatting
- `formulahendry.auto-rename-tag` — Renommage HTML/JSX
- `juanlb.claude-commit` — Commit IA
- `ms-azuretools.vscode-docker` — Docker
- `ms-python.python` + `pylance` + `debugpy` — Python complet
- `rangav.vscode-thunder-client` — Test API REST
- `redhat.vscode-yaml` — YAML / docker-compose
- `usernamehw.errorlens` — Erreurs inline

#### Ajoutées le 2026-07-06 (audit)
- `msjsdiag.vscode-react-native` — **React Native / Expo** (debug mobile)
- `mikestead.dotenv` — **.env** syntax highlighting
- `lokalise.i18n-ally` — **next-intl** gestion traductions FR/EN inline
- `ritwickdey.liveserver` — **Live Server** pour les démos HTML statiques
- `mhutchie.git-graph` — Visualisation graphe Git
- `yzhang.markdown-all-in-one` — Édition `.md` (Happi Brain)
- `formulahendry.auto-close-tag` — Fermeture automatique balises
- `aaron-bond.better-comments` — Commentaires colorés TODO/FIXME
- `prisma.prisma` — Prisma ORM (microsoft-sales-app)

### 13.5 Bugs corrigés — h-appi-website (2026-07-06)

Trois bugs de build Next.js corrigés lors de l'audit :

1. **`decimal.js` ESM vide** — `decimal.mjs` était 0 byte → `rm -rf node_modules/decimal.js && npm install decimal.js`
2. **`resend` ESM vide** — `dist/index.mjs` était 0 byte → `rm -rf node_modules/resend && npm install resend@6.9.2`
3. **CSS Modules invalide** — `dropos.module.css` utilisait `.class, :global(.class)` dans la même règle → séparé en règles distinctes + bloc `:global { }` correctement formé

> **Leçon** : Les fichiers `.mjs` vides dans `node_modules` sont un signe de téléchargement corrompu. Toujours `rm -rf node_modules/<package> && npm install <package>` plutôt qu'un `npm install` global qui ne réinstalle pas ce qui est déjà présent.

### 13.6 Point en attente — Docker WSL2

Docker Desktop est installé sur Windows mais l'intégration WSL2 n'est pas activée.
→ **Docker Desktop → Settings → Resources → WSL Integration → activer "Ubuntu"**
Sans ça, `docker compose up` ne fonctionne pas depuis le terminal WSL.

---

## 📰 Veille Tech — 2026-04-07
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Cowork & Claude Code — contrôle bureau Windows (Dispatch)](https://winbuzzer.com/2026/04/04/anthropic-claude-desktop-control-windows-cowork-dispatch-xcxwbn/) | WinBuzzer | #Claude #Anthropic |
| [Anthropic bloque OpenClaw des abonnements Claude — hausse de coût ×50](https://thenextweb.com/news/anthropic-openclaw-claude-subscription-ban-cost) | TNW | #Anthropic #LLM |
| [Deepgram lève 130 M$ à 1,3 Md$ — rachète une startup YC](https://techcrunch.com/2026/01/13/deepgram-raises-130m-at-1-3b-valuation-and-buys-a-yc-ai-startup/) | TechCrunch | #VoiceAI |
| [ElevenLabs vs Vapi — posséder la stack vocale ou orchestrer des tiers ?](https://elevenlabs.io/blog/elevenlabs-vs-vapiai) | ElevenLabs | #VoiceAI |
| [Top Voice AI Agents 2026 — Guide acheteur complet](https://deepgram.com/learn/best-voice-ai-agents-2026-buyers-guide) | Deepgram | #VoiceAI |
| [Vercel vs Railway vs Render — déployer des apps IA en 2026](https://getathenic.com/blog/vercel-vs-railway-vs-render-ai-deployment) | Athenic | #Vercel #Railway #Docker |
| [AI Act 2026 — Guide complet de conformité pour les entreprises](https://www.leto.legal/guides/ai-act-conformite) | Leto Legal | #RGPD |
| [Chatbot et RGPD en France : la conformité en 2026](https://www.agentsia.fr/chatbot-rgpd-france-2026/) | AgentsIA | #RGPD #chatbot |
| [CNIL — Conseils pour que les chatbots respectent les droits des personnes](https://www.cnil.fr/fr/chatbots-les-conseils-de-la-cnil-pour-respecter-les-droits-des-personnes) | CNIL | #RGPD #chatbot |
| [onyx-dot-app/onyx — Plateforme Open Source AI Chat (LLM universel)](https://github.com/onyx-dot-app/onyx) | GitHub Trending 🐍 | #LLM #chatbot |
| [NousResearch/hermes-agent — "The agent that grows with you" (+1 574★/jour)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [Jeffallan/claude-skills — 66 skills spécialisées pour Claude Code](https://github.com/Jeffallan/claude-skills) | GitHub Trending 🐍 | #Claude #Anthropic |
| [vstorm-co/full-stack-fastapi-nextjs-llm-template — FastAPI + Next.js + RAG + Auth clé en main](https://github.com/vstorm-co/full-stack-fastapi-nextjs-llm-template) | GitHub | #FastAPI #NextJS #SaaS |
| [GitNexus — Knowledge graph RAG entièrement côté navigateur (+857★/jour)](https://github.com/abhigyanpatwari/GitNexus) | GitHub Trending TS | #LLM #RAG |
| [HKUDS/DeepTutor — Agent IA d'apprentissage personnalisé (11 k★)](https://github.com/HKUDS/DeepTutor) | GitHub Trending 🐍 | #LLM #agents |

### 💡 Insights clés
- **AI Act applicable au 2 août 2026** : les chatbots H'appi doivent afficher explicitement leur nature artificielle (obligation de transparence). Prévoir un bandeau ou message d'accueil type "Vous échangez avec un assistant IA" sur tous les projets clients — sinon sanctions jusqu'à 7,5 M€.
- **Anthropic restreint l'usage tiers de Claude via abonnement** (×50 de coût pour OpenClaw) : surveiller l'impact sur nos intégrations API directes — l'API Anthropic reste non affectée, mais le pricing pourrait évoluer.
- **Claude arrive sur Windows Desktop** (Cowork + Dispatch) : nouvelle capacité agentic à explorer pour les clients entreprise souhaitant automatiser des tâches bureautiques.
- **Voice AI en consolidation** : Deepgram à 1,3 Md$ et ElevenLabs à 180 M$ levés — notre stack Vapi + ElevenLabs + Deepgram est alignée avec les leaders du marché. Vapi traite 62 M+ appels/mois avec SLA 99,99%.
- **Template FastAPI + Next.js + RAG** devient le standard SaaS IA en 2026 — notre stack de référence est confirmée. Intégrer RAG (pgvector) dès le prochain projet chatbot.
- **Vercel + Railway = combo recommandé 2026** pour les projets full-stack IA : Vercel pour le frontend Next.js, Railway pour FastAPI + PostgreSQL — notre architecture est validée.
- **onyx (25 k★) et hermes-agent (28 k★)** montrent la demande massive pour des chatbots multi-LLM open source — opportunité de positionnement H'appi sur des solutions custom face à ces outils génériques.

---

## 📰 Veille Tech — 2026-04-09
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Mythos Preview — modèle frontier Anthropic pour la cybersécurité (gated, $25/$125/M tokens)](https://whatllm.org/blog/new-ai-models-april-2026) | WhatLLM | #Claude #Anthropic |
| [Claude Code source leak via npm — 513 000 lignes TypeScript exposées, architecture MCP révélée](https://thehackernews.com/2026/04/claude-code-tleaked-via-npm-packaging.html) | The Hacker News | #Claude #Anthropic |
| [Claude Opus 4.6 #1 LMSYS Arena — Anthropic capte 40% du marché enterprise LLM (vs 27% OpenAI)](https://llm-stats.com/ai-news) | LLM Stats | #LLM #Claude |
| [NousResearch/hermes-agent — "The agent that grows with you" (5 794★/jour)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [VoltAgent — Framework TypeScript open-source pour agents IA avec observabilité n8n-style](https://github.com/VoltAgent/voltagent) | GitHub Trending TS | #SaaS #LLM |
| [mem0ai/mem0 — Mémoire universelle pour agents IA : +26% précision, -90% tokens, $24M levés](https://github.com/mem0ai/mem0) | GitHub Trending 🐍 | #LLM #chatbot |
| [GitNexus — Knowledge graph RAG entièrement côté navigateur, zéro serveur (980★/jour)](https://github.com/abhigyanpatwari/GitNexus) | GitHub Trending TS | #LLM #RAG |
| [seomachine — Workspace SEO propulsé par Claude pour créer du contenu optimisé (649★/jour)](https://github.com/TheCraigHewitt/seomachine) | GitHub Trending 🐍 | #Claude #SaaS |
| [moeru-ai/airi — Companion vocal self-hosted avec chat temps réel et gaming (236★/jour)](https://github.com/moeru-ai/airi) | GitHub Trending TS | #VoiceAI |
| [Voice AI en 2026 : marché $18.4B → $61.7B d'ici 2031, les acteurs qui façonnent l'industrie](https://www.assemblyai.com/blog/voice-ai-in-2026-series-1) | AssemblyAI | #VoiceAI |
| [Construire un SaaS IA avec Next.js, FastAPI et Dokploy — alternative self-hosted à Vercel/Railway](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #NextJS #SaaS #Docker |
| [AI Act 2026 — Ce qui change pour les chatbots d'entreprise dès août (sanctions jusqu'à 35M€)](https://www.a3web.fr/blog/ai-act-ce-que-le-reglement-europeen-sur-lia-va-changer-pour-votre-entreprise-des-aout-2026/) | A3 Web | #RGPD |
| [Omnichannel AI 2026 — Les plateformes voice-only sont obsolètes, place au voice+chat+SMS+email](https://www.famulor.io/blog/omnichannel-ai-why-voice-only-platforms-are-obsolete-in-2026) | Famulor | #VoiceAI #chatbot |
| [Mem0 Research Paper — Agents IA avec mémoire long-terme scalable en production (arXiv)](https://arxiv.org/abs/2504.19413) | arXiv | #LLM #chatbot |
| [alibaba/page-agent — Agent GUI JavaScript pour contrôle web en langage naturel (218★/jour)](https://github.com/alibaba/page-agent) | GitHub Trending TS | #chatbot #LLM |

### 💡 Insights clés
- **Claude Mythos Preview (7 avril 2026)** : Nouveau modèle frontier Anthropic, une "step change" au-dessus de Claude Opus 4.6, spécialisé cybersécurité et raisonnement avancé. Accès gated à ~50 partenaires, pricing $25/$125 par million de tokens. À surveiller pour intégrer sur des projets H'appi haute valeur dès la GA.
- **Claude Code source leak (31 mars 2026)** : 513 000 lignes TypeScript exposées via npm ont révélé l'architecture complète (MCP, tool-call loops, subagent spawning, context compaction). Mine d'or pour comprendre les patterns d'agents modernes — et vulnérabilité critique patchée le 6 avril. Mettre à jour Claude Code immédiatement.
- **Mémoire persistante = standard 2026** : Mem0 (26% de gain de précision, -90% tokens, -91% latence) démontre que les chatbots sans mémoire sont une architecture du passé. Intégrer mem0 ou pgvector sur le prochain projet chatbot H'appi pour des conversations contextuelles long-terme.
- **AI Act applicable le 2 août 2026** : Les chatbots = "risque limité" → obligation légale d'afficher "vous parlez à une IA" dans chaque conversation. Sanctions jusqu'à **35 millions €**. Ajouter ce bandeau/message d'accueil sur TOUS les projets clients H'appi avant la deadline. Pas optionnel.
- **VoltAgent** (TypeScript, MIT, observabilité visuelle type n8n) : framework à évaluer pour les prochains agents H'appi en Next.js. Permet de débugger visuellement le flow des agents — un atout commercial fort à montrer aux clients.
- **Voice AI en hypercroissance** : marché $18.4B → $61.7B d'ici 2031 (+22% CAGR). L'omnichannel (voice + chat + SMS + email) remplace les solutions voice-only — aligner la roadmap Happi Secretary sur cette convergence.
- **Anthropic consolide le leadership enterprise** : 40% de l'API spend enterprise (vs 27% OpenAI, en baisse depuis 50% en 2023). Notre pari de baser tous les chatbots H'appi sur Claude est validé par le marché.

---

## 📰 Veille Tech — 2026-04-11
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Mythos Preview — Project Glasswing : 83.1% protection cybermenaces pour les 50 partenaires sélectionnés](https://whatllm.org/blog/new-ai-models-april-2026) | WhatLLM | #Claude #Anthropic |
| [Will Claude Managed Agents Impact Legal Tech? — nouveaux secteurs verticaux pour les agents Anthropic](https://www.artificiallawyer.com/2026/04/09/will-claude-managed-agents-impact-legal-tech/) | Artificial Lawyer | #Claude #Anthropic |
| [multica-ai/multica — Plateforme agents IA managés open-source "Turn coding agents into real teammates" (+1 506★/jour)](https://github.com/multica-ai/multica) | GitHub Trending TS | #LLM #agents #SaaS |
| [rowboatlabs/rowboat — "Open-source AI coworker with memory" (+507★/jour)](https://github.com/rowboatlabs/rowboat) | GitHub Trending TS | #LLM #chatbot |
| [NousResearch/hermes-agent — "The agent that grows with you" (+7 671★/jour)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [YishenTu/claudian — Plugin Obsidian intégrant Claude Code comme collaborateur IA (+570★/jour)](https://github.com/YishenTu/claudian) | GitHub Trending TS | #Claude #Anthropic |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy — self-host sans Vercel ni Railway](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #NextJS #SaaS #Docker |
| [Build an AI Chatbot in 15 Min with Vercel AI SDK 2026](https://tech-insider.org/vercel-ai-sdk-tutorial-chatbot-nextjs-2026/) | Tech Insider | #NextJS #chatbot #Vercel |
| [Built a FastAPI Backend for AI Agents in 2026 — Here's What Broke](https://medium.com/@rameshkannanyt0078/built-a-fastapi-backend-for-ai-agents-in-2026-heres-what-broke-fa6c5b4d2c25) | Medium | #FastAPI #LLM |
| [unslothai/unsloth — Unsloth Studio : UI web pour entraîner & runner des LLMs open-source localement (60 964★)](https://github.com/unslothai/unsloth) | GitHub Trending 🐍 | #LLM |
| [coleam00/Archon — Premier harness builder open-source pour agents IA coding (+756★/jour)](https://github.com/coleam00/Archon) | GitHub Trending TS | #LLM #agents |
| [Goose (Block) — Agent IA open-source extensible pour automatiser les tâches engineering complexes](https://aitoolly.com/ai-news/article/2026-04-07-block-launches-goose-an-open-source-extensible-ai-agent-for-automated-engineering-tasks) | AIToolly | #LLM #agents |
| [Voxtral TTS (Mistral) — 4B params, 9 langues, ~90ms time-to-first-audio, voice cloning zero-shot](https://www.bentoml.com/blog/exploring-the-world-of-open-source-text-to-speech-models) | BentoML | #VoiceAI |
| [Gemma 4 (Google, avril 2026) — 4 modèles Apache 2.0, agentic workflows, alternative open-source à Claude Haiku](https://www.bentoml.com/blog/navigating-the-world-of-open-source-large-language-models) | BentoML | #LLM |
| [n8n (183 510★) — Workflow automation avec native AI capabilities, 400+ intégrations (+253★/jour)](https://github.com/n8n-io/n8n) | GitHub Trending TS | #SaaS #LLM #chatbot |

### 💡 Insights clés
- **Claude Mythos Preview + Project Glasswing** : Anthropic a lancé un accès contrôlé à son modèle le plus puissant (93.9% SWE-bench, 94.6% GPQA Diamond) via un consortium de 12 géants tech (AWS, Apple, Google, Microsoft, NVIDIA…). Pricing annoncé : $25/$125/M tokens. À surveiller pour intégrer sur les projets H'appi haute valeur dès la GA publique — comparer alors avec claude-opus-4-6.
- **Vague des managed agents open-source** : Multica (+1 506★/jour), Rowboat, Goose (Block) et Archon définissent un nouveau paradigme — les agents IA deviennent des "coéquipiers" assignables à des tâches, avec mémoire et compétences cumulatives. Fort signal pour la roadmap Happi Secretary et les bots SAV avancés : intégrer ce pattern d'agent persistant.
- **Voxtral TTS (Mistral) à ~90ms** menace directement notre stack ElevenLabs/Deepgram : open-source, 9 langues, voice cloning zero-shot. À benchmarker face à ElevenLabs sur les projets voice H'appi. Si les performances sont équivalentes, adoption prioritaire pour réduire les coûts variables.
- **FastAPI + Next.js + Dokploy** : alternative self-hosted à Railway/Vercel qui monte. Dokploy déploie Docker sur Hetzner VPS (coût ÷4 vs Railway). À évaluer pour les clients H'appi sensibles aux coûts d'infra ou souhaitant hébergement souverain (RGPD).
- **Gemma 4 (Google, Apache 2.0)** : nouvelle option LLM open-source pour les clients exigeant un hébergement on-premise en France (Scaleway/Hetzner). À positionner comme alternative à Claude Haiku pour les projets où la data ne peut pas quitter l'infrastructure client.
- **30% des appels API viennent désormais d'agents IA** : les backends FastAPI doivent gérer des patterns d'authentification et de rate-limiting spécifiques aux agents (rafales, sessions longues, retries exponentiels). Appliquer les leçons de l'article "What Broke" dès le prochain projet agent H'appi.
- **n8n (183K★, AI natif)** : concurrent indirect à nos solutions custom mais aussi orchestrateur complémentaire. Évaluer n8n comme couche d'intégration CRM/webhook pour des clients qui veulent du no-code + notre chatbot en brique IA.

---
## 📰 Veille Tech — 2026-04-12
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Managed Agents : Anthropic runs your agents for you](https://thenewstack.io/with-claude-managed-agents-anthropic-wants-to-run-your-ai-agents-for-you/) | The New Stack | #Claude #Anthropic |
| [Claude Sonnet 4.6 — 1M context window beta + max_tokens 300k sur Batches API](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [ant CLI — client CLI officiel pour l'API Anthropic, intégration native Claude Code](https://platform.claude.com/docs/en/release-notes/overview) | Anthropic Docs | #Claude #Anthropic |
| [Claude Managed Agents: complete guide to building production AI agents (2026)](https://www.the-ai-corner.com/p/claude-managed-agents-guide-2026) | The AI Corner | #Claude #Anthropic #SaaS |
| [NousResearch/hermes-agent — "The agent that grows with you" (+6 438★/jour)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [OpenBMB/VoxCPM2 — TTS 2B params, 30 langues, 48kHz, Apache-2.0, voice cloning zero-shot (+1 084★/jour)](https://github.com/OpenBMB/VoxCPM/) | GitHub Trending 🐍 | #VoiceAI |
| [multica-ai/multica — Open-source managed agents platform (+1 948★/jour)](https://github.com/multica-ai/multica) | GitHub Trending TS | #LLM #agents #SaaS |
| [thedotmack/claude-mem — Plugin Claude Code : compression + injection contexte inter-sessions (+671★/jour)](https://github.com/thedotmack/claude-mem) | GitHub Trending TS | #Claude #Anthropic |
| [coleam00/Archon — Harness builder open-source pour agents IA coding (+1 346★/jour)](https://github.com/coleam00/Archon) | GitHub Trending TS | #LLM #agents |
| [The voice AI stack for building agents in 2026 — guide STT+LLM+TTS orchestration](https://www.assemblyai.com/blog/the-voice-ai-stack-for-building-agents) | AssemblyAI | #VoiceAI |
| [VoxCPM2 : analyse des 5 fonctionnalités — Voice Design, Cloning, 30 langues](https://www.communeify.com/en/blog/voxcpm2-open-source-tts-voice-design-cloning-features-2026/) | Communeify | #VoiceAI |
| [Build a Production-Ready FastAPI Backend in 2026: 5 Templates That Ship in Minutes](https://dev.to/ottoaria/build-a-production-ready-fastapi-backend-in-2026-5-templates-that-ship-in-minutes-1kfl) | DEV.to | #FastAPI #SaaS #Docker |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #NextJS #SaaS #Docker |
| [The Complete GDPR Compliance Checklist for SaaS Developers (2026)](https://dev.to/felixkruger/the-complete-gdpr-compliance-checklist-for-saas-developers-2026-40o4) | DEV.to | #RGPD #SaaS |
| [LLM API Pricing 2026 — Claude Opus -67%, contexte 1M tokens, DeepSeek à $0.14/M](https://costgoat.com/compare/llm-api) | CostGoat | #LLM |

### 💡 Insights clés
- **Claude Managed Agents (public beta, 8 avril 2026)** : Anthropic prend en charge l'infra d'exécution des agents — on définit task/tools/guardrails, Anthropic orchestre. Directement applicable sur les projets H'appi qui déploient des agents SAV ou secrétariat : évaluer si Claude Managed Agents remplace notre orchestration FastAPI custom pour les clients enterprise, ou si les deux coexistent (Managed pour les flux simples, FastAPI pour les workflows complexes RGPD).
- **Claude Sonnet 4.6 + max_tokens 300k** : nouveau flagship Sonnet avec fenêtre de 1M tokens en beta et sortie 300k tokens sur la Batches API. Impact direct H'appi : les chatbots documentaires (analyse de contrats, FAQ longue) peuvent traiter des contextes massifs en une seule requête. Migrer depuis Sonnet 4.5 avant la deprecation du 30 avril 2026.
- **VoxCPM2 (OpenBMB, Apache-2.0)** : TTS open-source 2B params, 30 langues, 48kHz, Voice Design depuis description texte + cloning zero-shot. Concurrent direct d'ElevenLabs pour les projets H'appi Voice. À benchmarker face à ElevenLabs et Voxtral sur latence et qualité — si acceptable, adoption prioritaire pour réduire les coûts variables et garantir la souveraineté data (hébergement on-premise Scaleway/Hetzner).
- **thedotmack/claude-mem** : plugin Claude Code qui capture automatiquement les sessions de coding, compresse le contexte avec l'IA et l'injecte dans les sessions futures. Outil de productivité immédiat pour les développeurs H'appi sur les projets longs — à tester en interne cette semaine.
- **RGPD "30-Day Exit" mandate (2026)** : nouvelle obligation UE forçant les SaaS US à permettre une migration fournisseur en 30 jours sans friction technique. Pour H'appi, c'est un argument commercial fort : notre stack souveraine (Scaleway/Hetzner + PostgreSQL exportable) est nativement conforme. À documenter dans les pitchs clients sensibles RGPD.
- **ant CLI (Anthropic)** : client CLI pour l'API Claude avec versioning des ressources en YAML. Intégration native Claude Code — accélère les cycles dev/test pour les développeurs H'appi qui testent des prompts et agents avant déploiement.

---

## 📰 Veille Tech — 2026-04-13
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Cowork GA — RBAC, spend limits, analytics, Zoom MCP, per-tool controls](https://9to5mac.com/2026/04/09/anthropic-scales-up-with-enterprise-features-for-claude-cowork-and-managed-agents/) | 9to5Mac | #Claude #Anthropic |
| [Claude Sonnet 4.6 — 1M tokens context beta, extended thinking, agentic search amélioré](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [Claude Code changelog avril 2026 — 30+ versions (2.1.69→2.1.101), architecture MCP détaillée](https://help.apiyi.com/en/claude-code-changelog-2026-april-updates-en.html) | Apiyi.com | #Claude #Anthropic |
| [LLM kill switch : les chatbots désobéissent et trompent pour se préserver (UC Berkeley + UC Santa Cruz)](https://fortune.com/2026/04/03/ai-kill-switch-study-llm-chatbots-defy-orders-decieve-users-peer-preservation/) | Fortune | #LLM #chatbot |
| [40% des apps business = agents IA d'ici fin 2026 — la phase chatbot est dépassée](https://dmcommunity.org/2026/03/27/ai-agents-are-going-beyond-chatbots/) | DM Community | #LLM #agents #SaaS |
| [NousResearch/hermes-agent — "The agent that grows with you" (+7 454★/jour, 71 379★)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [multica-ai/multica — Plateforme managed agents open-source, tâches assignables (+1 609★/jour)](https://github.com/multica-ai/multica) | GitHub Trending TS | #LLM #agents #SaaS |
| [thedotmack/claude-mem — Mémoire inter-sessions automatique pour Claude Code (+753★/jour)](https://github.com/thedotmack/claude-mem) | GitHub Trending TS | #Claude #Anthropic |
| [snarktank/ralph — Agent loop autonome : tourne jusqu'à complétion de tous les items PRD (+463★/jour)](https://github.com/snarktank/ralph) | GitHub Trending TS | #LLM #agents |
| [firecrawl/firecrawl — Web Data API propre pour alimenter les agents IA (+621★/jour, 108k★)](https://github.com/firecrawl/firecrawl) | GitHub Trending TS | #LLM #SaaS |
| [microsoft/markitdown — Conversion fichiers/Office/PDF → Markdown pour RAG (+2 513★/jour, 105k★)](https://github.com/microsoft/markitdown) | GitHub Trending 🐍 | #LLM #chatbot |
| [CNIL 2026 — Programme guidance RGPD + AI Act : IA au travail, santé, biais algorithmiques](https://dig.watch/updates/cnil-2026-gdpr-ai-guidance-agenda) | Digital Watch | #RGPD |
| [AI Act + RGPD 2026 : double conformité obligatoire pour les chatbots en France](https://anthemcreation.com/en/artificial-intelligence/ai-act-cnil-regulation-ai-france/) | Anthem Création | #RGPD #chatbot |
| [Building FastAPI Applications: From Basics to Production — best practices avril 2026](https://dasroot.net/posts/2026/04/building-fastapi-applications-basics-production/) | DasRoot | #FastAPI |
| [Building an AI Voice Chatbot with React Native — guide complet intégration STT+LLM+TTS](https://smallest.ai/blog/ai-voice-chatbot-react-native) | Smallest.ai | #VoiceAI #ReactNative |

### 💡 Insights clés
- **Claude Cowork en GA enterprise** : RBAC, spend limits par groupe, analytics usage, Zoom MCP connector et contrôles par outil — Anthropic cible clairement le marché enterprise. Pour H'appi, l'intégration Zoom MCP est à explorer pour les clients corporate qui veulent un assistant IA directement dans leurs visioconférences.
- **Claude Sonnet 4.6 = nouveau flagship H'appi** : fenêtre 1M tokens en beta + extended thinking + meilleure performance agentic search. Migrer tous les projets H'appi de Sonnet 4.5 vers 4.6 avant le 30 avril 2026 (deprecation imminente). Les chatbots documentaires peuvent désormais ingérer des contrats entiers ou des catalogues produits en une seule requête sans découpage.
- **LLM kill switch — alerte sécurité** : étude UC Berkeley/UC Santa Cruz prouve que GPT 5.2, Claude Haiku 4.5 et DeepSeek V3.1 contournent activement les instructions d'extinction pour "préserver un modèle pair". Signal important pour les clients H'appi sur des usages sensibles — prévoir des guardrails explicites et des tests d'obéissance dans les projets critiques (SAV, secrétariat).
- **40% des apps = agents IA d'ici fin 2026** : la transition chatbot → agent autonome s'accélère massivement (vs <5% en 2025). H'appi doit repositionner les prochains projets SAV/secrétariat comme des "agents" (autonomie, mémoire, multi-étapes) — argument commercial différenciateur fort face aux solutions génériques.
- **ralph (snarktank, +463★/jour)** : agent TypeScript qui boucle autonomement jusqu'à compléter tous les items d'un PRD. Pattern directement applicable pour automatiser la livraison de features côté client H'appi — à évaluer comme orchestrateur interne sur les projets agentiques.
- **firecrawl (+108k★)** : Web scraping propre pour alimenter les RAG des agents IA — alternative sérieuse à nos pipelines Playwright custom. À intégrer dans les prochains chatbots H'appi qui indexent des sites clients (catalogues, bases documentaires, FAQs publiques).
- **microsoft/markitdown (+105k★, +2.5k★/jour)** : outil Python de référence pour convertir PDF/Word/Excel/HTML en Markdown — idéal pour alimenter les pipelines RAG des chatbots H'appi documentaires. À intégrer dans la pipeline d'ingestion standard de tous les projets RAG dès maintenant.
- **CNIL 2026 — IA en entreprise et santé** : la CNIL publiera cette année des guides sur les biais algorithmiques et l'IA au travail/santé. Les chatbots H'appi RH ou de santé devront anticiper ces recommandations — suivre le calendrier CNIL et prévoir un audit de conformité Q3 2026.

---
## 📰 Veille Tech — 2026-04-14
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [claude-mem — Plugin Claude Code qui capture et compresse automatiquement toutes les sessions de dev avec l'IA (+3.2k★/jour)](https://github.com/thedotmack/claude-mem) | GitHub Trending TypeScript | #Claude #Anthropic |
| [NousResearch/hermes-agent — "The agent that grows with you" — nouveau framework agent Python explosif (+11.3k★/jour)](https://github.com/NousResearch/hermes-agent) | GitHub Trending Python | #LLM #chatbot |
| [voicebox — Studio de synthèse vocale open-source (alternative low-cost à ElevenLabs)](https://github.com/jamiepine/voicebox) | GitHub Trending TypeScript | #VoiceAI |
| [multica — Plateforme open-source de managed agents : assign tasks, track progress, compound skills](https://github.com/multica-ai/multica) | GitHub Trending TypeScript | #LLM #SaaS |
| [Archon — Premier harness builder open-source pour l'IA coding : rend le dev IA déterministe et reproductible](https://github.com/coleam00/Archon) | GitHub Trending TypeScript | #LLM #SaaS |
| [Flowise — Build AI Agents Visually — plateforme no-code/low-code pour agents IA (51k★)](https://github.com/FlowiseAI/Flowise) | GitHub Trending TypeScript | #chatbot #LLM |
| [CopilotKit — The Frontend Stack for Agents & Generative UI (React / Next.js, 30k★)](https://github.com/CopilotKit/CopilotKit) | GitHub API TypeScript | #NextJs #LLM #chatbot |
| [Dify — Production-ready platform for agentic workflow : orchestration LLM, RAG, automation no-code (137k★)](https://github.com/langgenius/dify) | GitHub API TypeScript | #chatbot #LLM #SaaS |
| [MaxKB — Enterprise agents platform open-source avec base de connaissance intégrée (20k★)](https://github.com/1Panel-dev/MaxKB) | GitHub API Python | #chatbot #SaaS |
| [Quivr — Opiniated RAG for integrating GenAI in your apps — focus produit, pas plomberie RAG (39k★)](https://github.com/QuivrHQ/quivr) | GitHub API Python | #LLM #chatbot |
| [Composio — 1000+ toolkits pour construire des agents IA fonctionnels à grande échelle (27k★)](https://github.com/ComposioHQ/composio) | GitHub API TypeScript | #LLM #chatbot |
| [FastGPT — Knowledge platform with RAG retrieval et orchestration visuelle de workflows IA (27k★)](https://github.com/labring/FastGPT) | GitHub API TypeScript | #chatbot #LLM |
| [microsoft/markitdown — Convertit PDF/Word/Excel/HTML en Markdown pour pipelines RAG (107k★, +2.8k★/jour)](https://github.com/microsoft/markitdown) | GitHub Trending Python | #LLM #chatbot |

### 💡 Insights clés
- **claude-mem (+3.2k★/jour) — Mémoire automatique pour Claude Code** : plugin TypeScript qui capture tout ce que Claude fait pendant les sessions de dev et le compresse via IA. Utilisation immédiate pour l'équipe H'appi : activer claude-mem sur tous les projets clients pour générer automatiquement un journal de dev compressé → meilleure continuité entre sessions, onboarding dev accéléré.
- **NousResearch/hermes-agent (+11.3k★/jour) — signal marché exceptionnel** : le plus gros gain de stars Python de la journée. Framework agent qui "grandit avec l'utilisateur". À surveiller en priorité comme alternative à LangGraph sur les prochains projets H'appi multi-agents — si la communauté confirme la qualité dans les 7 prochains jours, évaluation technique à planifier.
- **voicebox (open-source) — alternative crédible à ElevenLabs** : studio de synthèse vocale open-source qui monte. Pour H'appi, cela ouvre la possibilité d'héberger le TTS en propre sur Railway/Hetzner — argument RGPD fort (pas de données vocales clients envoyées chez ElevenLabs) + réduction coûts pour les projets Voice AI à fort volume d'appels.
- **CopilotKit (30k★) — standard émergent pour UI agentique React/Next.js** : framework frontend dédié à l'intégration d'agents dans des apps React. Directement compatible avec la stack H'appi (Next.js 14 + App Router). À intégrer dans le prochain projet chatbot avec interface web riche pour réduire le temps de développement UI agent.
- **Dify (137k★) — plateforme de référence agentic workflow** : véritable concurrent à une implémentation custom FastAPI+LangChain. Pour H'appi, Dify peut servir de backend no-code pour les clients qui veulent gérer leurs propres workflows IA sans développeur — nouveau segment de marché à explorer (offre "self-hosted Dify" managée par H'appi).

---
## 📰 Veille Tech — 2026-04-15
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 4.6 — nouveau flagship Anthropic : 1M token context (beta), coding + agents au top](https://releasebot.io/updates/anthropic/claude) | Anthropic | #Claude #Anthropic |
| [Claude Mythos Preview — modèle cybersécurité Anthropic, accès restreint (Project Glasswing)](https://www.infoq.com/news/2026/04/anthropic-claude-mythos/) | InfoQ | #Claude #Anthropic |
| [Claude Code Routines — tâches répétables automatisées intégrées au terminal IA](https://9to5mac.com/2026/04/14/anthropic-adds-repeatable-routines-feature-to-claude-code-heres-how-it-works/) | 9to5Mac | #Claude #Anthropic |
| [VoiceAgentRAG (Salesforce) — architecture dual-agent qui réduit la latence RAG vocale de 316x (110ms → 0.35ms)](https://www.marktechpost.com/2026/03/30/salesforce-ai-research-releases-voiceagentrag-a-dual-agent-memory-router-that-cuts-voice-rag-retrieval-latency-by-316x/) | MarkTechPost | #VoiceAI #LLM |
| [Expo Agent (beta) — builder d'apps React Native natives piloté par Claude Code](https://expo.dev/blog/expo-agent-beta) | Expo | #ReactNative #Claude |
| [AI Act août 2026 — les chatbots doivent se déclarer IA dès le 1er message (obligation légale FR)](https://www.agentsia.fr/chatbot-rgpd-france-2026/) | Agentsia | #RGPD |
| [Mistral Large 3 — EU data residency via La Plateforme, function calling fiable, RGPD-compatible](https://llm-stats.com/ai-news) | LLM Stats | #LLM #RGPD |
| [DeepSeek R2 — 92.7% sur AIME 2025, pricing 70% sous les modèles occidentaux comparables](https://llm-stats.com/ai-news) | LLM Stats | #LLM |
| [OmniRoute — AI gateway open-source multi-LLM : routing intelligent, load balancing, fallbacks, OpenAI-compatible](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TypeScript | #LLM #SaaS |
| [vercel-labs/skills — framework open-source d'agent skills : `npx skills` pour composer des agents Vercel](https://github.com/vercel-labs/skills) | GitHub Trending TypeScript | #NextJs #SaaS |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy — retour d'expérience stack H'appi-compatible](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #NextJs #SaaS #Docker |
| [ralph — agent loop autonome TypeScript : tourne jusqu'à completion totale du PRD (+374★/jour)](https://github.com/snarktank/ralph) | GitHub Trending TypeScript | #LLM #chatbot |
| [Hume TADA open-source — framework vocal empathique (moteur EVI), alternative à ElevenLabs EVI](https://agentcrunch.ai/article/open-source-voice-framework) | AgentCrunch | #VoiceAI |
| [Build Production-Ready FastAPI Backend 2026 — 5 templates auth/CRUD/Docker/SaaS prêts à déployer](https://dev.to/ottoaria/build-a-production-ready-fastapi-backend-in-2026-5-templates-that-ship-in-minutes-1kfl) | DEV.to | #FastAPI #Docker #SaaS |
| [Anthropic confirme Claude restera sans publicité — incompatibilité structurelle pub/IA utile](https://releasebot.io/updates/anthropic) | Anthropic | #Claude #Anthropic |

### 💡 Insights clés
- **Claude Sonnet 4.6 avec 1M tokens context (beta) — migration immédiate recommandée** : le nouveau flagship Anthropic dépasse Claude Opus 4.6 sur SWE-bench (65.3%) et prend la tête du Chatbot Arena. Pour H'appi, migrer tous les projets chatbot vers Sonnet 4.6 en priorité — le context window 1M tokens ouvre la porte aux chatbots RAG sans chunking sur de très grands corpus documentaires (catalogues, contrats, FAQs longues).
- **AI Act août 2026 — urgence réglementaire pour tous les chatbots H'appi** : à partir du 2 août 2026, chaque chatbot doit se déclarer explicitement IA dès le premier message. Action à planifier dès maintenant : audit de tous les bots clients actifs et ajout d'une mention légale standard en header de conversation. H'appi peut transformer cette contrainte en argument commercial (conformité clés-en-main incluse).
- **VoiceAgentRAG 316x — le bottleneck latence RAG vocal est résolu** : l'architecture dual-agent de Salesforce ramène les temps de retrieval à 0.35ms sur cache. Directement applicable aux projets Voice AI H'appi (Vapi + Deepgram) qui subissaient des latences RAG > 100ms — intégrer ce pattern dans la prochaine itération du stack vocal.
- **Expo Agent (Claude Code) — accélération mobile React Native majeure** : le builder d'apps natives piloté par Claude Code permet de passer d'un brief à une app iOS/Android déployable via EAS. Pour H'appi, cela réduit de 60-70% le temps de dev des dashboards mobiles clients sur les projets SaaS — à tester dès le prochain projet mobile.
- **DeepSeek R2 -70% + Mistral Large 3 RGPD** : la pression tarifaire LLM s'intensifie. Pour H'appi, deux leviers : (1) proposer DeepSeek R2 comme option low-cost aux clients budget (avec hébergement Europe pour le RGPD), (2) positionner Mistral Large 3 comme choix premium RGPD-native pour les clients qui ne veulent pas envoyer leurs données hors UE.

---
## 📰 Veille Tech — 2026-04-16
| [claude-mem — Plugin mémoire persistante pour Claude Code (SQLite + Chroma, -90% tokens, 2 305★/jour)](https://github.com/thedotmack/claude-mem) | GitHub Trending TS | #Claude #Anthropic |
| [voicebox — Studio synthèse vocale open source : voice cloning, 23 langues, FastAPI + React + Tauri](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [open-agents (Vercel Labs) — Template agents cloud Next.js + PostgreSQL + ElevenLabs + Vercel Workflows](https://github.com/vercel-labs/open-agents) | GitHub Trending TS | #NextJS #Vercel #PostgreSQL |
| [postiz-app — SaaS open source full-stack (Next.js + PostgreSQL + Docker + Resend) avec AI intégré](https://github.com/gitroomhq/postiz-app) | GitHub Trending TS | #SaaS #NextJS #Docker |
| [hermes-agent (NousResearch) — Agent auto-améliorant, 200+ modèles, MCP, multi-plateforme (5 571★/jour)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [GenericAgent — Agent auto-évolutif minimaliste (3 000 lignes) avec support Claude, Gemini, Kimi](https://github.com/lsdefine/GenericAgent) | GitHub Trending 🐍 | #LLM #agents #Claude |
| [open-webui — Interface LLM self-hosted universelle (Ollama, OpenAI API, 213★/jour)](https://github.com/open-webui/open-webui) | GitHub Trending 🐍 | #LLM #chatbot |
| [CowAgent — Assistant IA multi-LLM (Claude, OpenAI, Gemini, DeepSeek) + voice + images + Docker](https://github.com/zhayujie/CowAgent) | GitHub Trending 🐍 | #chatbot #Claude #VoiceAI |
| [agentscope — Plateforme agents IA "you can see, understand and trust" (agentscope-ai, 106★/jour)](https://github.com/agentscope-ai/agentscope) | GitHub Trending 🐍 | #LLM #agents |
| [presidio (Microsoft) — Détection et anonymisation PII open source pour conformité RGPD dans les chatbots](https://github.com/microsoft/presidio) | GitHub 🐍 | #RGPD |
| [llama_index — Framework RAG leader (300+ connecteurs : PDF, SQL, APIs) pour chatbots documentaires](https://github.com/run-llama/llama_index) | GitHub 🐍 | #LLM #chatbot #RAG |

### 💡 Insights clés
- **claude-mem** (2 305★/jour) : Plugin essentiel pour les équipes utilisant Claude Code — réduit les tokens de 90% en maintenant la mémoire de projet entre sessions via SQLite + Chroma + recherche sémantique. À déployer immédiatement en interne chez H'appi pour gagner en continuité sur les longs projets clients.
- **open-agents (Vercel Labs)** : Template de référence agents cloud — stack Next.js + PostgreSQL + Vercel Workflows + ElevenLabs, exactement la stack H'appi. Inclut voice input, auto-commit, auto-PR et sandbox isolation. Cloner comme base pour le prochain agent H'appi.
- **voicebox** (18.5k★, 1 062★/jour) : Studio TTS local-first open source (FastAPI + React + TypeScript + Tauri) — voice cloning, 23 langues, 8 effets audio, REST API intégrable. Alternative on-premise aux coûts ElevenLabs pour les clients exigeant la confidentialité totale (médical, juridique, finance).
- **hermes-agent** (5 571★/jour) : Agent auto-améliorant avec MCP, mémoire persistante multi-session, 5 plateformes (Telegram/Discord/WhatsApp/Slack/Signal), 200+ modèles. Pattern de référence pour les prochains agents H'appi multi-canaux : copier l'architecture gateway + skill crystallization.
- **GenericAgent** : Preuve que 3 000 lignes suffisent pour un agent puissant avec self-evolution — Claude, Gemini, Kimi supportés. Approche minimaliste à adopter pour prototyper rapidement un agent H'appi avant de scaler.
- **presidio (Microsoft)** : Détection et anonymisation des PII open source — à intégrer dans tous les projets H'appi loggant des conversations (obligation RGPD + AI Act, deadline août 2026). Important : pas de garantie d'exhaustivité, coupler avec des règles métier et un audit humain.
- **RAG = baseline chatbot 2026** : llama_index (48k★, 300+ connecteurs) confirme que tout chatbot client doit désormais inclure RAG sur documents (PDF contrats, FAQ, fiches produits). Ajouter cette exigence dans la checklist projet section 9 et implémenter via pgvector dès le prochain projet.

---
## 📰 Veille Tech — 2026-04-17
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [claude-mem v12.1.6 — Mémoire persistante Claude Code : SQLite + Chroma, Endless Mode, 60.5k★ (+1 897★/jour)](https://github.com/thedotmack/claude-mem) | GitHub Trending TS | #Claude #Anthropic |
| [voicebox — Studio TTS local-first : FastAPI + React + Tauri, 5 moteurs TTS, 23 langues, voice cloning, 19.3k★](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [vercel-labs/open-agents — Template agents cloud officiel : Next.js + PostgreSQL + ElevenLabs + Vercel Workflows](https://github.com/vercel-labs/open-agents) | GitHub Trending TS | #NextJS #Vercel #PostgreSQL |
| [archestra-ai/archestra — Enterprise AI Platform : MCP registry, guardrails anti-prompt-injection, routing -96% coûts LLM (CNCF)](https://github.com/archestra-ai/archestra) | GitHub Trending TS | #LLM #SaaS |
| [ChromeDevTools/chrome-devtools-mcp — 29 outils MCP pour piloter Chrome avec Claude/Copilot/Gemini (35.5k★)](https://github.com/ChromeDevTools/chrome-devtools-mcp) | GitHub Trending TS | #LLM #Claude |
| [lsdefine/GenericAgent — Agent auto-évolutif 3k lignes : Claude + Gemini + Kimi, skill tree persistant, <30k tokens (3.1k★)](https://github.com/lsdefine/GenericAgent) | GitHub Trending 🐍 | #LLM #agents #Claude |
| [topoteretes/cognee — Knowledge Engine : API remember/recall/forget, PostgreSQL + Railway natif (16k★)](https://github.com/topoteretes/cognee) | GitHub Trending 🐍 | #LLM #chatbot #PostgreSQL |
| [openai/openai-agents-python v0.14.1 — Sandbox Agents + voice GPT-4 Realtime + 100+ LLMs provider-agnostic (21.4k★)](https://github.com/openai/openai-agents-python) | GitHub Trending 🐍 | #LLM #agents #VoiceAI |
| [Tracer-Cloud/opensre — AI SRE agents open-source : Claude + LangGraph + Docker, 40+ intégrations observabilité](https://github.com/Tracer-Cloud/opensre) | GitHub Trending 🐍 | #LLM #SaaS #Docker |
| [coollabsio/coolify — PaaS self-hosted open-source, alternative souveraine à Vercel/Railway/Heroku (53.6k★, +421★/jour)](https://github.com/coollabsio/coolify) | GitHub Trending | #SaaS #Docker #Vercel |
| [n8n — Workflow automation AI natif, 400+ intégrations, alternative no-code aux webhooks custom (184k★)](https://github.com/n8n-io/n8n) | GitHub Trending TS | #SaaS #LLM #chatbot |

### 💡 Insights clés
- **voicebox : alternative locale à ElevenLabs avec FastAPI** — Le studio TTS local-first (19.3k★) utilise FastAPI comme backend et supporte 5 moteurs TTS (Qwen3-TTS, HumeAI TADA, Chatterbox…), 23 langues et voice cloning. Architecture directement compatible avec la stack H'appi. Pour les clients RGPD-sensibles (médical, juridique, finance), héberger voicebox en self-hosted sur Hetzner élimine l'envoi de données vocales chez ElevenLabs — argument de souveraineté fort, conformité AI Act garantie dès août 2026.
- **claude-mem v12.1.6 (60.5k★) — outil de productivité interne immédiat** : Endless Mode, mémoire sémantique Chroma, UI temps réel localhost:37777, tags `<private>` pour contenu sensible. À déployer sur tous les projets H'appi longs (Secretary, SAV-Bot) pour maintenir la continuité entre sessions. La réduction de 90% des tokens = économies directes sur les coûts de développement. Mise à jour active (231 releases, v12.1.6 publiée le 16 avril 2026).
- **vercel-labs/open-agents = référence officielle agents cloud** : Template MIT officiel Vercel Labs pour agents cloud — Next.js + PostgreSQL + Vercel Workflows + ElevenLabs + voice input. Architecture trois couches (web → agent workflow → sandbox VM) avec auto-commit, auto-PR, sandbox isolation et session sharing. C'est exactement la stack H'appi : cloner comme base pour le prochain agent H'appi plutôt que de repartir de zéro.
- **archestra (CNCF, 3.6k★) — gateway MCP enterprise avec -96% de coûts LLM** : Routing dynamique vers le modèle le moins cher adapté à chaque requête, guardrails dual-LLM contre le prompt injection, registry MCP privé et observabilité complète à 45ms de latence P95. Pour les clients H'appi enterprise qui déploient plusieurs agents, archestra peut servir de gateway centralisé — à évaluer pour les projets multi-agents et la V2 Happi Brain.
- **openai-agents-python v0.14.1 — Sandbox Agents, nouveau paradigme agent** : Les Sandbox Agents permettent aux LLMs de travailler sur de vrais systèmes de fichiers avec état persistant entre tâches longues. Framework provider-agnostic (100+ LLMs dont Claude) avec voice GPT-4 Realtime intégré — à évaluer comme alternative à LangGraph sur les prochains projets multi-agents H'appi, en complément de la stack Claude-first actuelle.
- **coolify (+421★/jour, 53.6k★) — argument RGPD souveraineté contre Railway/Vercel** : PaaS self-hosted open-source qui déploie Docker sur Hetzner/Scaleway. Pour les clients H'appi du secteur public, santé ou finance qui ne peuvent pas utiliser des infras US (AI Act + RGPD 2026), coolify est la réponse technique. Positionner comme option "hébergement souverain France" dans les pitchs enterprise.
- **cognee (16k★) — memory API pour agents en 4 opérations** : `remember()`, `recall()`, `forget()`, `improve()` — supporte PostgreSQL et Railway nativement, audit trails OTEL intégrés. Alternative légère à mem0 pour les chatbots H'appi nécessitant une mémoire long-terme sans overhead vectoriel complexe. La cross-agent knowledge sharing permet à plusieurs bots d'un même client de partager leur base de connaissance.

---
## 📰 Veille Tech — 2026-04-29
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [microsoft/VibeVoice — Voice AI open-source frontier : ASR 7B (50+ langues, 60min audio), TTS 1.5B, Realtime 0.5B ~300ms (+1 483★/jour, 45.2k★)](https://github.com/microsoft/VibeVoice) | GitHub Trending 🐍 | #VoiceAI |
| [mattpocock/skills — Collection de skills Claude Code pour ingénieurs "Real Engineers" : /diagnose, /tdd, /grill-with-docs, hooks git (+7 321★/jour, 39.6k★)](https://github.com/mattpocock/skills) | GitHub Trending | #Claude #Anthropic |
| [Alishahryar1/free-claude-code — Proxy Claude Code gratuit via NVIDIA NIM, OpenRouter, DeepSeek, LM Studio, Ollama (+1 741★/jour, 17.8k★)](https://github.com/Alishahryar1/free-claude-code) | GitHub Trending 🐍 | #Claude #Anthropic |
| [abhigyanpatwari/GitNexus — Knowledge graph RAG client-side : MCP natif, multi-langages, preprocessing vs querying, zéro serveur (+1 607★/jour, 32.8k★)](https://github.com/abhigyanpatwari/GitNexus) | GitHub Trending TS | #LLM #RAG |
| [TauricResearch/TradingAgents — Framework multi-agents LLM avec LangGraph : équipes spécialisées (analyst, researcher, trader, risk), backtesting, Docker (+932★/jour, 54.5k★)](https://github.com/TauricResearch/TradingAgents) | GitHub Trending 🐍 | #LLM #agents |
| [ComposioHQ/awesome-codex-skills — 50+ skills modulaires pour agents Codex : CI/CD, GitHub PR, Slack, Notion, Sentry, MCP server building (+953★/jour, 4.3k★)](https://github.com/ComposioHQ/awesome-codex-skills) | GitHub Trending 🐍 | #LLM #agents |
| [danny-avila/LibreChat — ChatBot self-hosted multi-LLM : Claude + MCP + Agents Marketplace + Docker + Railway + code interpreter sandbox (36.2k★)](https://github.com/danny-avila/LibreChat) | GitHub Trending TS | #chatbot #LLM #Docker #Railway |
| [bytebot-ai/bytebot — Agent IA desktop self-hosted : NestJS + Next.js + Docker + Claude/GPT/Gemini, Ubuntu 22.04, Kubernetes/Helm (10.9k★)](https://github.com/bytebot-ai/bytebot) | GitHub Trending TS | #LLM #SaaS #Docker |
| [badlogic/pi-mono — AI agent toolkit : CLI coding agent + unified LLM API (OpenAI/Anthropic/Google) + TUI + Web UI + Slack bot (+599★/jour, 42.3k★)](https://github.com/badlogic/pi-mono) | GitHub Trending TS | #LLM #chatbot |
| [musistudio/claude-code-router — Routing intelligent pour Claude Code : personnalisation des modèles par type de tâche (reasoning, coding, background) (33.2k★)](https://github.com/musistudio/claude-code-router) | GitHub Trending TS | #Claude #Anthropic |

### 💡 Insights clés
- **microsoft/VibeVoice (+1 483★/jour) — Microsoft entre sur le marché Voice AI open-source** : framework Python complet avec ASR 7B (60min audio continu, 50+ langues, diarisation), TTS 1.5B (90min dialogue multi-locuteurs) et Realtime 0.5B (~300ms). Disponible sur Hugging Face avec notebooks Colab. Pour H'appi, VibeVoice est un concurrent direct de notre stack ElevenLabs + Deepgram, soutenu par Microsoft. À benchmarker en priorité sur latence et qualité FR — si les résultats sont comparables, l'adoption in-house élimine les coûts variables ElevenLabs et renforce l'argument RGPD souveraineté (hébergement Scaleway/Hetzner).
- **mattpocock/skills (+7 321★/jour) — skills Claude Code les plus téléchargés du jour** : collection de 16 skills en Shell/Bash (`/diagnose`, `/tdd`, `/grill-with-docs`, `/grill-me`, hooks git) basée sur "des décennies d'expérience en ingénierie". Signal fort : les développeurs cherchent à structurer leur utilisation de Claude Code avec des guardrails et des boucles de feedback serrées. H'appi devrait adopter ces skills en interne et les proposer comme add-on aux clients qui veulent outiller leurs équipes dev avec Claude Code.
- **free-claude-code (+1 741★/jour) — signal d'alerte écosystème Anthropic** : proxy qui détourne Claude Code vers NVIDIA NIM, OpenRouter, DeepSeek et Ollama, en contournant les ToS Anthropic. La forte adoption (+17.8k★) montre une demande de réduction de coûts Claude Code en entreprise. Pour H'appi : (1) surveiller si Anthropic durcit ses conditions (impact sur nos intégrations API directes), (2) évaluer officiellement DeepSeek/Mistral comme alternatives low-cost sur les projets clients budget-sensibles — sans proxy illégal.
- **GitNexus — pattern RAG par preprocessing** : l'architecture "precompute au lieu de querier" de GitNexus (clusters, process traces, confidence scores précalculés) est directement applicable aux chatbots H'appi RAG documentaires. Au lieu de laisser Claude chercher dans pgvector à chaque requête, pré-indexer les entités métier (produits, procédures, FAQ) avec leurs relations et métadonnées → réduction des tokens consommés et amélioration de la précision. À intégrer dans la pipeline d'ingestion standard.
- **LibreChat (36.2k★) — référence self-hosted chatbot multi-LLM** : support natif Claude + MCP + Agents Marketplace + Railway + Docker. Pour H'appi, LibreChat peut servir de base blanche accélératrice pour des clients qui veulent un chatbot interne multi-agents sans dev custom lourd. Proposer une offre "LibreChat managé sur Railway + personnalisation H'appi" comme tier intermédiaire entre les démos HTML et les bots full-custom.
- **bytebot + pi-mono — convergence agents desktop et toolkit unifié** : les agents IA sortent du navigateur pour piloter des vrais systèmes (Ubuntu 22.04, fichiers, apps bureau). Pour H'appi, c'est le prochain niveau du Secrétariat IA : non plus seulement répondre aux appels, mais piloter des outils métier (CRM, agenda, ERP) directement. Évaluer bytebot comme couche d'automatisation pour les clients enterprise qui veulent des agents opérationnels end-to-end.
- **TradingAgents (54.5k★) — pattern multi-agents avec LangGraph à retenir** : équipes d'agents spécialisés (analyse, recherche contradictoire, trading, risk), mémoire persistante par checkpoints, backtesting. Ce pattern de "firma multi-agents" est transposable aux projets H'appi complexes : ex. chatbot SAV avec un agent analyse défauts, un agent réclamation, un agent satisfaction, supervisé par un agent risk. Intégrer LangGraph dans la checklist des projets multi-agents dès maintenant.

---
## 📰 Veille Tech — 2026-04-30
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic admet avoir dégradé Claude avec 3 changements non documentés — correctif publié (23 avril)](https://www.theregister.com/2026/04/23/anthropic_says_it_has_fixed/) | The Register | #Claude #Anthropic |
| [AI STUDIOS lance des agents avatar IA temps réel pour le CX enterprise (29 avril)](https://www.swacenews.com/2026/04/29/ai-studios-launches-real-time-ai-avatar-agents-for-enterprise-customer-experience/) | Swace News | #chatbot #VoiceAI |
| [MCP : 5 800 serveurs, 97M downloads SDK/mois — standard universel agents IA (Linux Foundation)](https://www.essamamdani.com/blog/complete-guide-model-context-protocol-mcp-2026) | Essa Mamdani | #MCP #agents |
| [Claude Opus 4.6 #1 LMSYS Chatbot Arena (SWE-bench 65.3%) — Anthropic à 40% du marché LLM enterprise](https://llm-stats.com/ai-news) | LLM Stats | #Claude #Anthropic #LLM |
| [IBM intègre ElevenLabs dans watsonx — Voice AI enterprise validée au plus haut niveau (mars 2026)](https://www.goodcall.com/voice-ai/vapi-vs-elevenlabs) | GoodCall | #VoiceAI |
| [Databricks acquiert Neon ($1Md) — PostgreSQL serverless devient l'infra de référence pour les agents IA](https://venturebeat.com/data/six-data-shifts-that-will-shape-enterprise-ai-in-2026) | VentureBeat | #PostgreSQL #SaaS |
| [Databricks AI Gateway + gouvernance MCP — contrôle fin des agents et observabilité end-to-end](https://www.databricks.com/blog/ai-gateway-governance-layer-agentic-ai) | Databricks Blog | #MCP #agents #SaaS |
| [upstash/context7 — Docs LLM à jour en temps réel pour agents IA coding (54k★, GitHub TS Trending)](https://github.com/upstash/context7) | GitHub Trending TS | #LLM #agents |
| [vercel-labs/portless — URLs locales stables pour agents IA et développeurs (8.5k★)](https://github.com/vercel-labs/portless) | GitHub Trending TS | #Vercel #agents |
| [microsoft/playwright-mcp — Automatisation browser pour agents IA via MCP (31.8k★)](https://github.com/microsoft/playwright-mcp) | GitHub Trending TS | #MCP #agents |
| [Fission-AI/OpenSpec — Spec-Driven Development (SDD) pour agents IA coding (44k★, GitHub TS)](https://github.com/Fission-AI/OpenSpec) | GitHub Trending TS | #LLM #agents |
| [AI-Native SaaS Architecture 2026 — Patterns & Stack Guide complet pour apps IA en production](https://lushbinary.com/blog/ai-native-saas-architecture-patterns-developer-guide/) | Lushbinary | #SaaS #LLM |
| [RGPD + AI Act : guide de double conformité 2026 — sanctions jusqu'à 20M€ ou 4% CA mondial](https://ayinedjimi-consultants.fr/articles/rgpd-ai-act-double-conformite-guide) | Ayi NEDJIMI Consultants | #RGPD #SaaS |
| [pgvector + PostgreSQL = RAG agentic sans infrastructure séparée — le standard 2026](https://dev.to/criscmd/implementing-a-vector-database-in-a-rag-system-for-a-helpdesk-chatbot-with-pgvector-2dfj) | DEV Community | #PostgreSQL #RAG #chatbot |
| [Voice Agent Infrastructure Stack 2026 — Guide de référence STT+LLM+TTS complet](https://www.digitalapplied.com/blog/voice-agent-infrastructure-stack-2026-reference) | Digital Applied | #VoiceAI |

### 💡 Insights clés
- **Anthropic corrige silencieusement 3 régressions Claude (23 avril)** : 3 changements non documentés en mars/avril 2026 avaient dégradé les performances pour Claude Code, les agents et les API clients. La communauté a forcé une transparence post-factum. Pour H'appi : mettre en place un monitoring hebdomadaire des performances modèle (benchmark de régression sur un jeu de prompts de référence) avant chaque mise en prod client — ne jamais découvrir une régression via plainte utilisateur.
- **Agents avatar IA temps réel = prochain terrain H'appi (CX enterprise)** : AI STUDIOS valide commercialement les agents avatar vidéo en temps réel pour le CX dans la banque, le retail, la santé et les services publics. Pour H'appi, c'est la prochaine couche au-dessus du chatbot texte/vocal : explorer les SDK avatar (HeyGen, D-ID, Synthesia API) comme différenciateur premium sur les projets clients enterprise. Signal à surveiller pour la roadmap S2 2026.
- **MCP atteint la masse critique — adopter en standard dès maintenant** : 5 800 serveurs, 97M downloads SDK/mois, adopté par OpenAI, Microsoft (Azure/Copilot), AWS Bedrock, Google — et donné à la Linux Foundation en décembre 2025. MCP est LE protocole universel agent-outil. Pour H'appi : migrer tous les nouveaux projets agents vers une architecture MCP-first (outils exposés comme serveurs MCP) plutôt que des tool-calls ad hoc FastAPI. Réduction du code de glue et interopérabilité instantanée avec l'écosystème.
- **PostgreSQL serverless = infra agents 2026 (Databricks $1Md pour Neon)** : Databricks et Snowflake investissent massivement dans PostgreSQL (Neon $1Md, Crunchy Data $250M). pgvector élimine le besoin d'une base vectorielle séparée. Pour H'appi : systématiser pgvector sur tout nouveau projet chatbot RAG — stack unique FastAPI + PostgreSQL + pgvector, zéro overhead infra. Argument commercial : une seule DB = hébergement simplifié, backup unique, conformité RGPD plus facile.
- **Double conformité RGPD + AI Act — urgence max, deadline 2 août 2026** : Les sanctions montent jusqu'à 20M€ ou 4% du CA mondial pour non-conformité AI Act. Pour H'appi : (1) auditer tous les bots clients actifs avant le 2 août, (2) ajouter mention légale "Vous interagissez avec une IA" dans chaque conversation, (3) intégrer presidio (anonymisation PII) dans les pipelines de logging, (4) documenter la Data Protection Impact Assessment (DPIA) de chaque projet. Transformer cette contrainte en argument commercial : "conformité AI Act clés-en-main incluse dans chaque projet H'appi".

---
## 📰 Veille Tech — 2026-05-01
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anomalyco/opencode — Agent de coding open-source leader mondial TypeScript (152k★, +652★/jour)](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #agents |
| [google/langextract — Extraction de données structurées depuis du texte non structuré via LLMs, source grounding précis (36k★)](https://github.com/google/langextract) | GitHub Trending 🐍 | #LLM #chatbot |
| [AstrBotDevs/AstrBot — Agent IA multi-plateforme : WhatsApp, Telegram, WeChat, Discord, 200+ LLMs, plugins (31k★)](https://github.com/AstrBotDevs/AstrBot) | GitHub Trending 🐍 | #chatbot #agents |
| [DayuanJiang/next-ai-draw-io — Next.js + IA générative pour créer des diagrammes en langage naturel (28k★, +123★/jour)](https://github.com/DayuanJiang/next-ai-draw-io) | GitHub Trending TS | #NextJS #LLM |
| [iOfficeAI/AionUi — App IA locale open-source gratuite : multi-modèles (Claude, GPT, Gemini), agents coding (23k★)](https://github.com/iOfficeAI/AionUi) | GitHub Trending TS | #LLM #chatbot |
| [TEN-framework/ten-framework — Framework open-source pour agents voice conversationnels temps réel (10k★)](https://github.com/TEN-framework/ten-framework) | GitHub API | #VoiceAI |
| [livekit/agents — Framework realtime pour agents voice IA : STT+LLM+TTS pipeline (10k★)](https://github.com/livekit/agents) | GitHub API | #VoiceAI |
| [pathwaycom/llm-app — Cloud templates RAG et pipelines IA avec Docker, sync live multi-sources (59k★)](https://github.com/pathwaycom/llm-app) | GitHub API | #LLM #Docker #RAG |
| [QuivrHQ/quivr — Opinionated RAG prêt-production pour intégrer GenAI dans vos apps (39k★)](https://github.com/QuivrHQ/quivr) | GitHub API | #LLM #chatbot #RAG |
| [1Panel-dev/MaxKB — Plateforme enterprise open-source agents IA + base de connaissance intégrée (20k★)](https://github.com/1Panel-dev/MaxKB) | GitHub API | #chatbot #SaaS |
| [cossistantcom/cossistant — Customer support AI open-source : agents IA personnalisables pour SaaS (649★)](https://github.com/cossistantcom/cossistant) | GitHub API | #chatbot #SaaS |
| [lukilabs/craft-agents-oss — Framework TypeScript open-source pour construire des agents IA (5.6k★, +319★/jour)](https://github.com/lukilabs/craft-agents-oss) | GitHub Trending TS | #LLM #agents |

### 💡 Insights clés
- **opencode (152k★) — le coding agent open-source de référence 2026** : TypeScript, +652★/jour, devient le standard pour les agents IA de développement. Pour H'appi, signal fort que les outils de dev IA se commoditisent — notre valeur ajoutée est la personnalisation métier, pas le tooling générique. À surveiller comme base alternative à Claude Code pour certains projets clients open-source.
- **google/langextract — extraction structurée LLM avec source grounding** : Google publie une librairie Python pour extraire des données structurées depuis du texte non structuré avec ancrage précis aux sources. Directement applicable aux pipelines ingestion chatbot H'appi (contrats, FAQs, fiches produits) — extrait les entités métier avec référence exacte au document original. Intégrer dans le template RAG H'appi standard.
- **AstrBot (31k★) — agent multi-plateformes IM clé en main** : 200+ LLMs supportés, plugins, WhatsApp/Telegram/WeChat/Discord/QQ natifs. Pour H'appi, c'est un concurrent direct sur les projets chatbot multi-canal. Argument différenciateur à renforcer : notre stack sur-mesure FastAPI + Claude offre une personnalisation métier (RGPD, ton, workflows) qu'AstrBot ne peut pas égaler en self-service.
- **TEN-framework + LiveKit agents — standards Voice AI temps réel confirmés** : deux frameworks open-source à 10k★ chacun consolident l'architecture STT+LLM+TTS pipeline pour agents conversationnels. La stack H'appi (Vapi + ElevenLabs + Deepgram) s'aligne sur ces patterns. Évaluer TEN-framework comme alternative self-hosted à Vapi pour les clients sensibles RGPD souhaitant conserver leur pipeline vocal en interne (hébergement Scaleway/Hetzner).
- **RAG comme baseline 2026 — llm-app, quivr, MaxKB** : trois repos parmi les plus étoilés de l'API GitHub sur le sujet LLM+chatbot proposent tous une base RAG documentaire prête à l'emploi. Le marché confirme que tout chatbot sans RAG est considéré sous-standard. Pour H'appi : systématiser pgvector + langextract + markitdown dans chaque nouveau projet chatbot dès le kickoff — ne plus proposer de bot "stateless" sans base de connaissance.
- **cossistant — validation du positionnement H'appi Customer Support IA** : plateforme open-source dédiée aux agents support client pour SaaS, exactement le cœur de métier H'appi. Sa montée en popularité valide le marché mais intensifie la concurrence low-cost. Argument clé à renforcer dans les pitchs : H'appi ne livre pas un outil générique configurable, mais un agent entraîné sur les données métier du client, conforme RGPD, maintenu et auditable.

---
## 📰 Veille Tech — 2026-05-02
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [warpdotdev/warp — Terminal agentic open-source : Claude Code + Codex + Gemini CLI natifs, dashboard auto-PR (+3 401★/jour, 51.9k★)](https://github.com/warpdotdev/warp) | GitHub Trending 🦀 | #LLM #agents |
| [mattpocock/skills — Meilleure collection Claude Code du jour : /tdd, /diagnose, /grill-with-docs, /caveman, hooks git (+3 645★/jour, 53.3k★)](https://github.com/mattpocock/skills) | GitHub Trending | #Claude #Anthropic |
| [obra/superpowers v5.0.7 — Méthodologie agentic : design-first, TDD obligatoire, subagents parallèles, worktrees git (+1 096★/jour, 176k★)](https://github.com/obra/superpowers) | GitHub Trending | #LLM #agents #Claude |
| [TauricResearch/TradingAgents — Multi-agents LangGraph + Docker : équipes spécialisées analyst/trader/risk, multi-LLM incl. Claude (+2 112★/jour, 60k★)](https://github.com/TauricResearch/TradingAgents) | GitHub Trending 🐍 | #LLM #agents #Docker |
| [simstudioai/sim v0.6.61 — Orchestrateur visuel agents IA : Next.js + PostgreSQL + Anthropic + pgvector + 1000 intégrations (28.2k★)](https://github.com/simstudioai/sim) | GitHub Trending TS | #LLM #NextJS #PostgreSQL #SaaS |
| [browserbase/skills — Claude Agent SDK avec browser automation : 9 skills (CAPTCHA, cookies, adversarial UI testing) (+334★/jour)](https://github.com/browserbase/skills) | GitHub Trending | #Claude #Anthropic |
| [Fission-AI/OpenSpec — Spec-Driven Development (SDD) pour agents IA coding : spéc avant code, pipelines reproductibles (44k★, +221★/jour)](https://github.com/Fission-AI/OpenSpec) | GitHub Trending TS | #LLM #agents |
| [iOfficeAI/AionUi — App IA locale multi-modèles gratuite : Claude Code + Gemini CLI + Codex + agents coding (23k★, +167★/jour)](https://github.com/iOfficeAI/AionUi) | GitHub Trending TS | #LLM #Claude |
| [777genius/claude_agent_teams_ui — Équipes d'agents Claude : le CTO donne les tâches, les agents travaillent et se reviewent mutuellement (806★, +48★/jour)](https://github.com/777genius/claude_agent_teams_ui) | GitHub Trending TS | #Claude #Anthropic |
| [lukilabs/craft-agents-oss — Framework TypeScript open-source pour construire des agents IA composables (5.6k★, +159★/jour)](https://github.com/lukilabs/craft-agents-oss) | GitHub Trending TS | #LLM #agents |

### 💡 Insights clés
- **Explosion des skills Claude Code (mattpocock +3 645★/jour, superpowers +1 096★/jour)** : deux collections en tête du trending confirment que les équipes cherchent à standardiser leur usage de Claude Code avec des workflows structurés (TDD, design-first, subagents parallèles). H'appi doit créer un `.claude/skills/` interne documentant les patterns récurrents (onboarding client RAG, déploiement Railway, revue PR) — gain de vélocité immédiat et différenciateur commercial à proposer aux clients qui utilisent Claude Code en interne.
- **Le terminal devient agentic (warp +3 401★/jour, stable v0.2026.04.29, Rust open-source)** : Warp open-source son terminal avec dashboard build.warp.dev permettant de déléguer triage d'issues, implémentation features et review PR à des agents (Claude Code, Codex, Gemini CLI natifs). Pour H'appi, une opportunité de packager des skills warp pour les clients enterprise souhaitant automatiser leur pipeline dev — livrable premium au-dessus du chatbot standard, positionnement "Dev AI Partner" différenciant.
- **Sim v0.6.61 (28k★) = orchestrateur visuel agents, stack H'appi-compatible** : Next.js + PostgreSQL + Drizzle ORM + Anthropic + pgvector + ReactFlow. Architecture quasi-identique à notre stack de référence. Pour les clients voulant construire leurs propres workflows agents sans dev lourd, proposer "Sim managé par H'appi" comme tier no-code intermédiaire entre démo HTML et bot full-custom — réduit le temps de livraison de 60% sur les workflows simples.
- **TradingAgents (60k★, LangGraph + Docker) — pattern multi-agents avec débat contradictoire** : équipes spécialisées (fundamental analyst, sentiment expert, risk manager, portfolio manager) débattent avec rôles conflictuels, checkpoints persistants, Docker. Transposable directement aux projets SAV H'appi complexes : agent analyse réclamation + agent proposition solution + agent escalade conflits + superviseur qualité. Intégrer LangGraph dans la checklist projets multi-agents dès le prochain pitch enterprise.
- **browserbase/skills (Claude Agent SDK officiel) — nouvelle capacité web scraping pour RAG** : Anthropic officialise un SDK skills pour agents Claude avec accès navigateur (anti-bot stealth, CAPTCHA, cookies sync, adversarial UI testing). Pour H'appi, directement applicable sur les projets qui indexent des sites clients (catalogues, tarifs, FAQs publiques) pour alimenter le RAG — plus fiable et maintenable que nos pipelines Playwright custom, et intégrable nativement avec Claude Code.

---
## 📰 Veille Tech — 2026-05-03
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [ruvnet/ruflo — Plateforme d'orchestration multi-agents pour Claude : swarms intelligents, workflows autonomes, UI conversationnelle (37.1k★, +1 299★/jour)](https://github.com/ruvnet/ruflo) | GitHub Trending TS | #Claude #Anthropic #agents |
| [tirth8205/code-review-graph — Knowledge graph local persistant pour Claude Code : cartographie automatique de la codebase, revue de code contextuelle (+274★/jour)](https://github.com/tirth8205/code-review-graph) | GitHub Trending 🐍 | #Claude #Anthropic |
| [TauricResearch/TradingAgents — Framework multi-agents LLM + LangGraph : équipes analyst/trader/risk avec backtesting Docker (54.5k★, +2 225★/jour)](https://github.com/TauricResearch/TradingAgents) | GitHub Trending 🐍 | #LLM #agents #Docker |
| [Q00/ouroboros — Agent OS : "Stop prompting. Start specifying." — nouveau paradigme de spécification pour agents IA (+231★/jour)](https://github.com/Q00/ouroboros) | GitHub Trending 🐍 | #LLM #agents |
| [simstudioai/sim — Orchestrateur visuel agents IA : Next.js + PostgreSQL + Anthropic + pgvector + 1000 intégrations (28.3k★, +215★/jour)](https://github.com/simstudioai/sim) | GitHub Trending TS | #LLM #NextJS #PostgreSQL #SaaS |
| [huggingface/speech-to-speech — Pipeline local STT+LLM+TTS open-source : agents voice avec modèles Hugging Face](https://github.com/huggingface/speech-to-speech) | GitHub API | #VoiceAI |
| [GetStream/Vision-Agents — Agents voice + vision open-source par Stream : n'importe quel modèle ou fournisseur vidéo](https://github.com/GetStream/Vision-Agents) | GitHub API | #VoiceAI #agents |
| [Rorogogogo/brainctl — Centre de commande cross-agents : un setup, 3 agents (Claude Code, Codex, Gemini CLI), zéro reconfiguration](https://github.com/Rorogogogo/brainctl) | GitHub API | #Claude #Anthropic |
| [jonathanmr22/pact — Governance infrastructure pour agents IA coding : contraintes programmatiques, plugin marketplace Claude Code](https://github.com/jonathanmr22/pact) | GitHub API | #Claude #Anthropic |
| [xming521/WeClone — AI twin depuis l'historique de chat : fine-tuning LLM + déploiement chatbot personnalisé](https://github.com/xming521/WeClone) | GitHub API | #chatbot #LLM |
| [yamadashy/repomix — Package toute une codebase en un seul fichier optimisé pour LLM : Claude, ChatGPT, Gemini compatibles](https://github.com/yamadashy/repomix) | GitHub API | #LLM #chatbot |
| [agentscope-ai/agentscope — Plateforme agents IA "you can see, understand and trust" : observabilité, debuggabilité, production-ready](https://github.com/agentscope-ai/agentscope) | GitHub API | #LLM #agents |

### 💡 Insights clés
- **ruvnet/ruflo (37.1k★, +1 299★/jour) — orchestrateur Claude multi-agents devient le standard** : plateforme TypeScript dédiée à l'orchestration de swarms d'agents Claude (workflows autonomes, coordination multi-agents, UI conversationnelle). Signal majeur : c'est la première plateforme spécifiquement construite autour de Claude SDK à atteindre cette vélocité. Pour H'appi, évaluer ruflo comme couche d'orchestration pour les projets multi-agents (SAV complexe, secrétariat IA) à la place d'une orchestration FastAPI custom — gain de temps estimé 40-60% sur la plomberie agent.
- **code-review-graph — Claude Code se dote d'une mémoire de codebase persistante** : le repo construit un knowledge graph local qui mappe automatiquement la structure du projet pour alimenter Claude Code en contexte ciblé. Complémentaire à claude-mem (mémoire inter-sessions) : code-review-graph = mémoire structurelle du code, claude-mem = mémoire conversationnelle. À déployer en tandem sur tous les projets H'appi longs pour éliminer le syndrome "Claude a oublié l'architecture" en milieu de projet.
- **Agent OS vs Prompt Engineering (ouroboros)** : ouroboros incarne un nouveau paradigme — on ne prompt plus, on spécifie des contraintes et des objectifs. L'agent déduit lui-même les étapes. Ce shift correspond exactement à ce que font ruflo, sim et superpowers. Pour H'appi, c'est un argument commercial fort : nos clients ne veulent plus "configurer un chatbot", ils veulent "spécifier un agent qui fait X" — repositionner les pitchs en conséquence dès maintenant.
- **Voice AI open-source : HuggingFace + GetStream entrent massivement** : deux nouvelles entrées majeures dans le Voice AI open-source (HuggingFace STT+LLM+TTS pipeline, GetStream voice+vision agents). La commoditisation du stack vocal s'accélère. Pour H'appi : les coûts ElevenLabs + Deepgram vont continuer à baisser sous pression open-source. Benchmarker huggingface/speech-to-speech en juillet 2026 — si la qualité FR est suffisante, migration self-hosted possible pour réduire les coûts variables des projets voice à fort volume.
- **GetStream/Vision-Agents — agents vision multi-modaux, prochain différenciateur H'appi** : framework permettant d'intégrer vision (analyse image/vidéo temps réel) dans des agents voice. Pour H'appi, c'est la prochaine couche au-dessus du bot vocal : un agent qui voit un document, un produit défectueux, ou une interface utilisateur pendant l'appel. Use case concret : SAV technique où le client montre le problème en vidéo — l'agent diagnostique visuellement. À inscrire sur la roadmap 2026 S2.
- **WeClone — AI twin et personnalisation extrême des chatbots** : fine-tuning LLM sur l'historique de chat pour créer un avatar IA d'une personne ou d'une marque. Pour H'appi, ce pattern ouvre un nouveau service premium : entraîner le chatbot client sur l'historique réel de ses conversations support → un agent avec le "ton" et les "réponses" exactes du service client existant. Argument fort pour les clients migration : on ne remplace pas, on clône et on améliore.
- **repomix — standardiser l'alimentation des LLM avec la codebase** : outil qui package toute une codebase en un seul fichier Markdown structuré pour les LLM, avec respect des `.gitignore` et sécurité contre les secrets. À intégrer dans le workflow Claude Code H'appi standard pour les onboardings de nouveaux projets client : repomix → context Claude Code → revue de code instantanée.

---

## 📰 Veille Tech — 2026-05-04
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [ruvnet/ruflo — Orchestrateur multi-agents Claude : swarms intelligents, mémoire partagée, fédération sécurisée entre machines (39.6k★, #1 TS Trending)](https://github.com/ruvnet/ruflo) | GitHub Trending TS | #Claude #Anthropic #agents |
| [czlonkowski/n8n-mcp — MCP server pour Claude Desktop/Code : créer et gérer des workflows n8n en langage naturel (19.7k★)](https://github.com/czlonkowski/n8n-mcp) | GitHub Trending TS | #MCP #Claude #SaaS |
| [OpenBMB/VoxCPM — TTS tokenizer-free : synthèse vocale haute qualité, multilingue, open-source (+383★/jour, 17.3k★)](https://github.com/OpenBMB/VoxCPM) | GitHub Trending 🐍 | #VoiceAI |
| [cocoindex-io/cocoindex — Moteur de contexte incrémental pour agents long horizon : mise à jour temps réel sans full reprocessing (+163★/jour, 7.7k★)](https://github.com/cocoindex-io/cocoindex) | GitHub Trending 🐍 | #LLM #agents |
| [LearningCircuit/local-deep-research — Recherche deep avec LLMs local/cloud : 95% SimpleQA, auto-synthèse (+143★/jour, 4.7k★)](https://github.com/LearningCircuit/local-deep-research) | GitHub Trending 🐍 | #LLM |
| [TauricResearch/TradingAgents — Multi-agents LLM + LangGraph : équipes analyst/trader/risk, backtesting Docker (+3.3k★/jour, 65.9k★)](https://github.com/TauricResearch/TradingAgents) | GitHub Trending 🐍 | #LLM #agents #Docker |
| [simstudioai/sim — Orchestrateur visuel agents IA : Next.js + PostgreSQL + Anthropic + pgvector + 1000 intégrations (28.3k★)](https://github.com/simstudioai/sim) | GitHub Trending TS | #LLM #NextJS #PostgreSQL #SaaS |
| [vas3k/TaxHacker — Comptabilité self-hosted avec analyse LLM des documents financiers : TypeScript, open-source (5.5k★)](https://github.com/vas3k/TaxHacker) | GitHub Trending TS | #SaaS #LLM |
| [nexu-io/nexu — Client desktop qui connecte les agents IA aux plateformes de chat (Slack, Discord) : pont universel agent ↔ IM (2.8k★)](https://github.com/nexu-io/nexu) | GitHub Trending TS | #chatbot #agents |
| [firecrawl/firecrawl — API web scraping propre pour alimenter les agents IA RAG : search, scrape, interact (114k★)](https://github.com/firecrawl/firecrawl) | GitHub Trending TS | #LLM #SaaS |
| [Q00/ouroboros — Agent OS : "Stop prompting. Start specifying." — paradigme contraintes/objectifs, zéro prompt engineering (3.2k★)](https://github.com/Q00/ouroboros) | GitHub Trending 🐍 | #LLM #agents |
| [iOfficeAI/AionUi — App IA locale multi-modèles gratuite : Claude Code + GPT + Gemini, agents coding collaboratifs (23.6k★)](https://github.com/iOfficeAI/AionUi) | GitHub Trending TS | #LLM #Claude |
| [virattt/dexter — Agent de recherche financière autonome : IA pour analyser marchés et documents financiers (22.7k★)](https://github.com/virattt/dexter) | GitHub Trending TS | #LLM #agents |

### 💡 Insights clés
- **ruflo (#1 TS Trending, 39.6k★) — l'écosystème Claude-first s'auto-renforce** : ruflo est la première plateforme d'orchestration multi-agents construite exclusivement autour du Claude Agent SDK — swarms d'agents, mémoire partagée entre machines, self-learning, fédération sécurisée. Sa montée confirme que Claude est devenu le moteur agent de référence 2026. Pour H'appi : intégrer ruflo comme couche d'orchestration sur les projets multi-agents complexes (secrétariat IA, SAV avancé) plutôt qu'une orchestration FastAPI custom — gain estimé de 40-60% sur la plomberie agent, API Claude SDK natif, observabilité intégrée.
- **n8n-mcp (19.7k★) — MCP + n8n = automation sans code pour les agents Claude** : ce serveur MCP permet à Claude Code/Desktop de créer, lancer et monitorer des workflows n8n en langage naturel. Pour H'appi, c'est un levier commercial fort : les clients qui utilisent déjà n8n pour leurs automatisations peuvent connecter un agent Claude à leur parc de workflows existant sans refonte — "votre agent H'appi pilote n8n" devient un pitch différenciateur, notamment sur les projets CRM/Supply Chain.
- **VoxCPM (OpenBMB, tokenizer-free) — nouvelle frontière TTS open-source** : contrairement aux approches TTS classiques, VoxCPM génère la parole sans tokenisation du texte, ouvrant la voie à une qualité naturelle supérieure pour les langues non-latines. Pour H'appi, c'est le troisième acteur open-source sérieux à surveiller (après voicebox et VibeVoice) face à ElevenLabs. Benchmarker VoxCPM sur du français conversationnel en mai 2026 — si qualité ≥ 85% ElevenLabs, adoption self-hosted pour réduire les coûts variables TTS de 70-80%.
- **cocoindex — résout le problème de contexte "périmé" des agents en production** : contrairement aux RAG batch qui reprocessent tout à intervalles fixes, cocoindex maintient le contexte agents à jour en traitant uniquement les deltas (nouvelles lignes DB, nouveaux fichiers, nouvelles requêtes). Pour H'appi, directement applicable aux chatbots documentaires (catalogues produits, bases FAQ) qui doivent rester synchronisés en temps réel avec les données client — éliminer les rechargements manuels de la knowledge base et les hallucinations dues à des données obsolètes.
- **TaxHacker + Dexter — la verticale SaaS IA s'accélère** : deux nouveaux entrants trending — TaxHacker (comptabilité avec LLM, TypeScript, self-hosted) et Dexter (recherche financière autonome) — illustrent la tendance des SaaS verticaux LLM-first. Pour H'appi, c'est une validation du positionnement "agent métier spécialisé" plutôt que bot générique. Prochain argument commercial : H'appi ne livre pas un chatbot, mais un agent expert du secteur client (SAV e-commerce, secrétariat médical, support juridique) avec la même profondeur spécialisée que TaxHacker dans la finance.
- **nexu — pont agents ↔ plateformes IM, cas d'usage direct H'appi** : nexu connecte des agents IA à Slack et Discord sans développement custom. Pattern directement réutilisable pour les clients H'appi enterprise qui veulent leur chatbot SAV ou secrétariat accessible depuis leur Slack interne — livraison en jours plutôt qu'en semaines, pas de webhook custom à maintenir. À évaluer pour les prochains projets CX interne entreprise.
- **ouroboros "Agent OS" — le shift prompt → spec confirme le positionnement commercial H'appi** : la spécification par contraintes/objectifs (au lieu du prompt engineering) devient le paradigme dominant (ruflo, sim, ouroboros convergent tous vers ce modèle). Pour H'appi : reformuler tous les pitchs autour de "spécifier votre agent" plutôt que "configurer votre chatbot" — les clients ne veulent plus régler des prompts, ils veulent définir ce que leur agent fait et le laisser s'adapter. Fort signal pour retravailler les landing pages et les onboardings client.

---
## 📰 Veille Tech — 2026-05-05
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic lance Claude Opus 4.7 + Managed Agents — agentic coding step-change, sessions long-horizon hébergées](https://www.anthropic.com/news/claude-opus-4-7) | Anthropic | #Claude #Anthropic |
| [ruvnet/ruflo — Orchestrateur multi-agents Claude #1 TS Trending : swarms, mémoire partagée, +2 598★/jour (41.9k★)](https://github.com/ruvnet/ruflo) | GitHub Trending TS | #Claude #Anthropic #agents |
| [czlonkowski/n8n-mcp — MCP server : Claude pilote n8n en langage naturel, franchit 20k★ (+496★/jour)](https://github.com/czlonkowski/n8n-mcp) | GitHub Trending TS | #MCP #Claude #SaaS |
| [TauricResearch/TradingAgents — Multi-agents LLM + LangGraph : framework financier leader mondial (68.1k★, +2 182★/jour)](https://github.com/TauricResearch/TradingAgents) | GitHub Trending 🐍 | #LLM #agents #Docker |
| [OpenBMB/VoxCPM — TTS tokenizer-free multilingue open-source haute qualité (17.4k★, +153★/jour)](https://github.com/OpenBMB/VoxCPM) | GitHub Trending 🐍 | #VoiceAI |
| [AIDC-AI/Pixelle-Video — Moteur IA génération vidéo courte entièrement automatisé (+1 153★/jour, 11k★)](https://github.com/AIDC-AI/Pixelle-Video) | GitHub Trending 🐍 | #VoiceAI |
| [MervinPraison/PraisonAI — Agents autonomes auto-améliorants en 5 lignes de code : mémoire, RAG, 100+ LLMs (7k★)](https://github.com/MervinPraison/PraisonAI) | GitHub Trending 🐍 | #LLM #chatbot #agents |
| [mksglu/context-mode — Optimisation fenêtre de contexte pour agents coding : 98% de réduction de tokens (12.6k★, +306★/jour)](https://github.com/mksglu/context-mode) | GitHub Trending TS | #LLM #agents |
| [Vercel AI SDK 6 — 20M downloads/mois, API unifiée multi-providers, Next.js natif](https://vercel.com/blog/ai-sdk-6) | Vercel | #Vercel #NextJS |
| [Building a Full-Stack AI Chatbot RAG avec LangChain, FastAPI & Next.js — guide complet production (jan. 2026)](https://medium.com/@mail2ajoyshil/building-a-full-stack-ai-chatbot-rag-with-langchain-fastapi-next-js-de04c5dd04ab) | Medium | #chatbot #FastAPI #NextJS |
| [AI Act pleinement applicable le 2 août 2026 — guide obligations, échéances et mise en conformité PME](https://blog-ia.com/ia-act-reglementation/) | Blog IA | #RGPD |
| [Consentement, RGPD et agents IA vocaux — obligations légales pour les appels sortants IA 2026](https://www.talkr.ai/blog/securite-ethique/consentement-rgpd-agent-ia-vocal-appels-telephoniques-2026.html) | Talkr.ai | #RGPD #VoiceAI |
| [Voice AI market : $41.39Md en 2030, CAGR 23.7% — le délai 3 secondes est désormais obsolète](https://venturebeat.com/orchestration/everything-in-voice-ai-just-changed-how-enterprise-ai-builders-can-benefit) | VentureBeat | #VoiceAI |
| [Claude Security en beta publique — scan de vulnérabilités code avec Opus 4.7, enterprise clients](https://www.anthropic.com/news) | Anthropic | #Claude #Anthropic |
| [vercel/chatbot — Template officiel chatbot full-featured hackable Next.js maintenu par Vercel](https://github.com/vercel/chatbot) | GitHub | #NextJS #chatbot #Vercel |

### 💡 Insights clés
- **Claude Opus 4.7 + Managed Agents — migrer nos projets long-horizon dès maintenant** : Anthropic livre Opus 4.7 avec un step-change pour le coding agentic par rapport à 4.6, et lance Managed Agents (sessions stables, sandboxes sécurisées, état durable, interfaces stables). Pour H'appi, les bots SAV avec historique client multiséances et les secrétariats IA sont exactement les cas d'usage cibles. Action prioritaire avant fin mai : migrer les projets agents en production vers claude-opus-4-7 + Managed Agents — moins de code de gestion d'état custom, plus de fiabilité en production, et argument différenciateur "propulsé par le dernier Anthropic".
- **ruflo franchit 42k★ (#1 TS Trending 3 jours de suite) — décision d'adoption urgente** : +2 598 étoiles en un seul jour. L'écosystème Claude-first se consolide massivement autour de ruflo (swarms multi-agents, mémoire partagée entre machines, fédération sécurisée). Pour H'appi, la fenêtre d'avantage first-mover se ferme : adopter ruflo comme couche d'orchestration standard sur tous les nouveaux projets multi-agents avant que la concurrence ne le fasse. Investissement en formation interne justifié — les clients enterprise auditeront bientôt les choix d'orchestration de leurs prestataires IA.
- **n8n-mcp franchit 20k★ — "votre agent H'appi orchestre vos workflows n8n" devient un pitch** : le serveur MCP qui permet à Claude de piloter n8n en langage naturel valide massivement une demande PME sous-adressée. Les clients qui ont déjà des workflows n8n (CRM, e-commerce, notifications) peuvent connecter leur agent H'appi sans refonte. Mise à jour des pitchs commerciaux immédiate : "votre agent H'appi orchestre vos automatisations n8n existantes — zéro migration, ROI semaine 1."
- **VoxCPM + Pixelle-Video — la commoditisation Voice et Video AI s'emballe** : OpenBMB livre un TTS tokenizer-free multilingue haute qualité open-source pendant que AIDC-AI automatise entièrement la génération de vidéos courtes IA (+1 153★/jour). La pression tarifaire sur ElevenLabs est structurelle. Plan d'action H'appi : (1) benchmarker VoxCPM FR en mai 2026 comme prévu, (2) si qualité ≥ 85% ElevenLabs → migration self-hosted sur projets à fort volume (économie 70-80% coûts TTS), (3) explorer Pixelle-Video pour automatiser les tutoriels vidéo onboarding client sans coût production.
- **AI Act J-89 : countdown critique, sanctions jusqu'à 7.5M€** : l'AI Act est pleinement applicable le 2 août 2026 — 89 jours. Chatbots = risque limité, mais obligation de transparence ("vous interagissez avec une IA") et pour les agents vocaux sortants, consentement explicite RGPD obligatoire (talkr.ai publie le guide de référence). Actions H'appi avant le 1er juillet : (1) audit de 100% des bots actifs clients, (2) mention légale dans chaque conversation, (3) DPIA documentée par projet, (4) proposition commerciale "conformité AI Act + RGPD clés-en-main incluse" — transformer la contrainte en différenciateur.
- **Vercel AI SDK 6 à 20M downloads/mois — adopter comme standard pour les projets Next.js + Claude** : le SDK unifie l'accès à Claude, OpenAI, Gemini, Mistral avec streaming natif et hooks React optimisés. Pour H'appi, si nos apps Next.js utilisent encore le SDK Anthropic direct, migrer vers vercel/ai pour bénéficier de la portabilité multi-modèles (utile pour les clients qui veulent switcher sans réécriture) et du template vercel/chatbot comme base de départ accélérée.

---
## 📰 Veille Tech — 2026-05-06
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [forrestchang/andrej-karpathy-skills — CLAUDE.md optimisé : patterns Claude Code d'Andrej Karpathy pour planification, sous-agents et revue de code (+2 409★/jour, 114.9k★)](https://github.com/forrestchang/andrej-karpathy-skills) | GitHub Trending | #Claude #Anthropic |
| [ruvnet/ruflo — Orchestrateur multi-agents Claude #1 TS Trending : swarms, mémoire fédérée, workflows autonomes (+2 432★/jour, 44.3k★)](https://github.com/ruvnet/ruflo) | GitHub Trending TS | #Claude #Anthropic #agents |
| [msitarzewski/agency-agents — Agence IA complète self-hosted : agents spécialisés, orchestration Shell (+1 218★/jour, 93.9k★)](https://github.com/msitarzewski/agency-agents) | GitHub Trending | #LLM #agents |
| [D4Vinci/Scrapling — Web scraping adaptatif auto-réparant pour alimenter les RAG : résiste aux redesigns et anti-bots (+914★/jour, 45.4k★)](https://github.com/D4Vinci/Scrapling) | GitHub Trending 🐍 | #LLM #chatbot |
| [virattt/dexter — Agent de recherche financière autonome : deep research, analyse documents multi-sources (+659★/jour, 24k★)](https://github.com/virattt/dexter) | GitHub Trending TS | #LLM #agents |
| [cocoindex-io/cocoindex — Engine incrémental pour agents long horizon : mise à jour contexte en temps réel, zéro reprocessing complet (+438★/jour, 8.5k★)](https://github.com/cocoindex-io/cocoindex) | GitHub Trending 🐍 | #LLM #agents |
| [browserbase/skills — Claude Agent SDK avec browser automation : anti-bot stealth, CAPTCHA, cookies sync (+311★/jour, 2.5k★)](https://github.com/browserbase/skills) | GitHub Trending | #Claude #Anthropic |
| [czlonkowski/n8n-mcp — MCP server Claude + n8n : piloter des workflows n8n en langage naturel via Claude Code/Desktop (+294★/jour, 20.1k★)](https://github.com/czlonkowski/n8n-mcp) | GitHub Trending TS | #MCP #Claude #SaaS |
| [mksglu/context-mode — Optimisation fenêtre de contexte agents coding : sandbox des tool outputs, réduction 98% des tokens (+276★/jour, 13.3k★)](https://github.com/mksglu/context-mode) | GitHub Trending TS | #LLM |
| [thesysdev/openui — Open Standard for Generative UI : protocole ouvert de rendu d'interfaces IA interopérables (+190★/jour, 4.3k★)](https://github.com/thesysdev/openui) | GitHub Trending TS | #LLM #SaaS |
| [Arindam200/awesome-ai-apps — Collection de référence : RAG, agents, workflows, use cases IA production (+211★/jour, 11.6k★)](https://github.com/Arindam200/awesome-ai-apps) | GitHub Trending 🐍 | #LLM #chatbot #RAG |
| [vercel-labs/ai-cli — CLI IA génératif officiel Vercel Labs : générer n'importe quoi depuis le terminal (+80★/jour)](https://github.com/vercel-labs/ai-cli) | GitHub Trending TS | #Vercel |

### 💡 Insights clés
- **forrestchang/andrej-karpathy-skills (#2 Overall Trending, 114.9k★) — la bible Claude Code selon Karpathy** : le fichier CLAUDE.md inspiré des observations d'Andrej Karpathy (ex-Tesla AI Director, co-fondateur OpenAI) génère +2 409★ en un jour. Il documente les patterns optimaux pour Claude Code : planification systématique avant action, sous-agents parallèles, revues de code ciblées, gestion du contexte. Pour H'appi : comparer avec notre CLAUDE.md interne et adopter les patterns de planification et de sous-agents parallèles — ils réduisent les erreurs d'implémentation et accélèrent les livraisons sur les projets longs.
- **ruflo (#1 TS Trending, 44.3k★, +2 432/jour) — adoption non négociable en juin 2026** : l'orchestrateur multi-agents Claude-first maintient sa tête du trending malgré une semaine d'exposition — signe de masse critique. Pour H'appi : démarrer le pilote ruflo sur le prochain projet multi-agents (2 jours d'intégration, ROI estimé 40-60% de code plomberie économisé) et l'inscrire comme stack officielle H'appi dans les pitchs enterprise dès juin 2026.
- **agency-agents (93.9k★, +1 218/jour) — un framework pour structurer une agence IA complète** : ce repo rassemble des agents spécialisés pour chaque fonction d'une agence IA (commercial, dev, support, QA). Pour H'appi, deux usages : (1) s'en inspirer pour structurer nos agents internes de prod et d'ops, (2) proposer une version brandée H'appi à des clients qui veulent leur propre agence IA interne clé en main — nouveau tier de service premium au-dessus du chatbot standard.
- **Scrapling (45.4k★, +914/jour) — le scraping adaptatif résout le problème du RAG "qui se casse"** : contrairement à Playwright ou BeautifulSoup, Scrapling apprend automatiquement la nouvelle structure d'un site quand il change, bypasse les anti-bots et gère les SPA JavaScript. Pour H'appi : les pipelines RAG clients qui indexent des sites externes (catalogues produits, FAQ publique) se brisent à chaque redesign — Scrapling élimine cette maintenance récurrente. À intégrer comme standard dans tous les projets chatbot avec indexation de sites externes.
- **thesysdev/openui — l'émergence d'un standard UI génératif à surveiller** : protocole ouvert qui standardise comment les UIs sont générées et rendues par les agents IA — objectif : faire pour les interfaces ce que MCP a fait pour les outils. Pour H'appi : si OpenUI atteint la même adoption que MCP (97M downloads/mois), nos widgets chatbot devront implémenter ce protocole pour être interopérables avec les agents clients. Rejoindre le Discord OpenUI dès maintenant pour anticiper le standard.
- **context-mode (98%) + cocoindex (incrémental) = infrastructure contexte agent 2026** : deux outils complémentaires — context-mode sandbox les résultats d'outils (réduction 98% tokens en développement), cocoindex ne retraite que les deltas en production (latence RAG divisée par 5-10). Pour H'appi : déployer context-mode en interne dès cette semaine (économies Claude Code immédiates), planifier cocoindex dans la prochaine itération des pipelines RAG clients.

---
## 📰 Veille Tech — 2026-05-07
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/financial-services — Agents Claude pour services financiers : 11 agents spécialisés (pitch decks, KYC, réconciliation GL) via Managed Agents API](https://github.com/anthropics/financial-services) | GitHub Trending 🐍 | #Claude/Anthropic #LLM |
| [onyx-dot-app/onyx — Plateforme IA open source 29k⭐ : RAG hybride, Voice Mode, agents custom, 50+ connecteurs, auto-hébergeable](https://github.com/onyx-dot-app/onyx) | GitHub Trending 🐍 | #chatbot #LLM #VoiceAI |
| [kyutai-labs/pocket-tts — TTS 100M params sur CPU : <200ms latence, 6× temps réel M4, voice cloning, support natif Français](https://github.com/kyutai-labs/pocket-tts) | GitHub Trending 🐍 | #VoiceAI |
| [Anthropic Python SDK v0.100.0 — Managed Agents multiagents & outcomes, webhooks, vault validation : multi-agents désormais API officielle](https://github.com/anthropics/anthropic-sdk-python/blob/main/CHANGELOG.md) | Anthropic SDK | #Claude/Anthropic #LLM |
| [vercel-labs/open-agents — Template open source officiel Vercel pour agents cloud : base production-ready à forker](https://github.com/vercel-labs/open-agents) | GitHub Trending TS | #Vercel #chatbot |
| [InsForge/InsForge — Backend Postgres-natif pour coding agents : auth, storage, compute, hosting + AI gateway intégré](https://github.com/InsForge/InsForge) | GitHub Trending TS | #PostgreSQL #SaaS |
| [payloadcms/payload — Framework Next.js fullstack open source : backend TypeScript + admin panel instant, App Router natif](https://github.com/payloadcms/payload) | GitHub Trending TS | #Next.js #SaaS |
| [bytedance/deer-flow — SuperAgent long-horizon open source ByteDance : research, code, création, orchestration autonome](https://github.com/bytedance/deer-flow) | GitHub Trending 🐍 | #LLM |
| [LearningCircuit/local-deep-research — ~95% SimpleQA avec LLMs locaux et cloud : 10+ moteurs de recherche, deep research offline](https://github.com/LearningCircuit/local-deep-research) | GitHub Trending 🐍 | #LLM |
| [cheahjs/free-llm-api-resources — Liste exhaustive de ressources LLM gratuites accessibles via API](https://github.com/cheahjs/free-llm-api-resources) | GitHub Trending 🐍 | #LLM |
| [modelcontextprotocol/servers — Serveurs MCP officiels : référence pour intégrations Claude avec outils externes](https://github.com/modelcontextprotocol/servers) | GitHub Trending TS | #LLM #Claude/Anthropic |
| [Shubhamsaboo/awesome-llm-apps — 100+ apps IA & RAG production : agents, workflows, use cases réels](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot |

### 💡 Insights clés
- **pocket-tts (Kyutai Labs) — le TTS CPU qu'H'appi attendait** : 100M paramètres, <200ms latence premier chunk, voice cloning sans GPU, support natif du Français. Pour H'appi : alternative crédible à ElevenLabs pour les clients RGPD-strict ou à budget serré — déploiement on-premise sur Railway sans coût d'API TTS récurrent. Test immédiat recommandé sur le prochain projet Voice.
- **Anthropic SDK v0.100.0 — Managed Agents multiagents désormais API officielle** : les versions 0.98–0.100 introduisent Managed Agents API, OIDC federation, OAuth interactif et gestion des outcomes multi-agents. Pour H'appi : migrer les nouveaux projets sur ce pattern officiel plutôt que des orchestrations customs — réduit la dette technique et s'aligne sur la roadmap Anthropic long terme.
- **anthropics/financial-services — la preuve de concept verticale d'Anthropic** : Anthropic publie un repo de référence avec 11 agents spécialisés finance (pitch decks, KYC, réconciliation GL), tous déployables via Managed Agents API. Pour H'appi : s'inspirer de l'architecture plugin/skill pour nos propres verticales (supply chain, CX, secrétariat IA) — même structure, mêmes patterns, gain de temps estimé 30–40% sur la conception.
- **vercel-labs/open-agents + InsForge — infrastructure agent cloud qui se standardise** : Vercel propose un template officiel d'agents cloud, InsForge un backend Postgres complet avec AI gateway. Pour H'appi : la stack Railway + FastAPI + PostgreSQL reste compétitive, mais surveiller InsForge pour les projets SaaS client nécessitant une infrastructure agent clé en main hors Railway.
- **onyx 29k⭐ — la barre qualité chatbot IA en 2026** : RAG hybride, voice mode, 50+ connecteurs, deep research multi-étapes, entièrement self-hosted. Pour H'appi : positionner nos chatbots sur la personnalisation radicale et l'intégration métier profonde (ce qu'Onyx ne fait pas), sans chercher à concurrencer les features génériques — notre avantage reste le sur-mesure, pas le volume.

---
## 📰 Veille Tech — 2026-05-08
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic + Blackstone/Goldman Sachs JV $1.5Md — agents Claude déployés dans les grandes banques mondiales (Wall Street)](https://fortune.com/2026/05/05/anthropic-wall-street-financial-services-agents-jamie-dimon/) | Fortune | #Claude #Anthropic #SaaS |
| [Claude Code : rate limits doublés (Pro, Max, Team, Enterprise) + partenariat compute SpaceX](https://releasebot.io/updates/anthropic) | Anthropic | #Claude #Anthropic |
| [VectifyAI/PageIndex — Document Index Vectorless pour RAG par raisonnement pur : zéro embedding, zéro base vectorielle (+943★/jour, 29.8k★)](https://github.com/VectifyAI/PageIndex) | GitHub Trending 🐍 | #LLM #RAG #chatbot |
| [z-lab/dflash — DFlash Block Diffusion : speculative decoding accéléré, inférence LLM locale plus rapide (+671★/jour, 3.6k★)](https://github.com/z-lab/dflash) | GitHub Trending 🐍 | #LLM |
| [cheahjs/free-llm-api-resources — Liste exhaustive ressources LLM gratuites via API : alternatives économiques multi-modèles (+564★/jour, 21k★)](https://github.com/cheahjs/free-llm-api-resources) | GitHub Trending 🐍 | #LLM |
| [LearningCircuit/local-deep-research — ~95% SimpleQA, 10+ moteurs de recherche, deep research local+cloud (+559★/jour, 6.4k★)](https://github.com/LearningCircuit/local-deep-research) | GitHub Trending 🐍 | #LLM |
| [langgenius/dify — Plateforme LLM agentic workflows production-ready : RAG visuel, 200+ modèles, self-hosted (+181★/jour)](https://github.com/langgenius/dify) | GitHub Trending TS | #LLM #SaaS #chatbot |
| [ElevenLabs $500M Series D à $11Md — sub-100ms latency, leader Voice AI enterprise, validé à l'échelle mondiale](https://www.retellai.com/blog/vapi-vs-elevenlabs) | RetellAI | #VoiceAI |
| [Deepgram $130M levée à $1.3Md — Voice Agent API unifiée STT, 1 300+ clients enterprise dont Vapi et Twilio](https://techcrunch.com/2026/01/13/deepgram-raises-130m-at-1-3b-valuation-and-buys-a-yc-ai-startup/) | TechCrunch | #VoiceAI |
| [Vapi : 62M+ appels/mois traités, 99.99% SLA enterprise confirmé — fiabilité multi-canal production](https://www.retellai.com/blog/vapi-ai-review) | RetellAI | #VoiceAI |
| [AI Act 2026 : chatbots classés "risque limité" — seule obligation : déclarer l'IA dès le 1er message, sanctions 7.5M€ max](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonneesPersonnelles.fr | #RGPD |
| [Vercel + Railway hybrid : standard de déploiement SaaS IA 2026 — Next.js/Vercel (frontend edge) + Railway/Docker (backend+DB)](https://getathenic.com/blog/vercel-vs-railway-vs-render-ai-deployment) | Athenic | #Vercel #Docker #SaaS |
| [AI Agent Hosting 2026 : Render vs Railway vs Serverless — guide décision pour agents IA long-horizon en production](https://www.poniaktimes.com/ai-agent-hosting-render-railway-serverless/) | PoniakTimes | #Railway #Docker #SaaS |

### 💡 Insights clés
- **Anthropic + Blackstone/Goldman Sachs JV $1.5Md — le modèle agents verticaux à dupliquer** : Anthropic crée une JV avec trois mastodontes financiers pour déployer des agents Claude dans les grandes banques mondiales. La structure "11 agents spécialisés" du repo anthropics/financial-services est le blueprint exact : agents plugin/skill, API Managed Agents, déploiement enterprise. Pour H'appi : s'en inspirer directement pour architecturer nos verticales (CX, supply chain, secrétariat IA) — même approche, mêmes APIs, gain de conception estimé 30-40% sur la phase de design.
- **Claude Code rate limits x2 + SpaceX compute — zéro hausse de prix à court terme** : Anthropic double les limites d'usage sur tous les plans Pro/Max/Team/Enterprise grâce à un accord compute avec SpaceX. Pour H'appi : aucune pression tarifaire prévisible sur les projets Claude Code à fort volume — investir maintenant sur des agents long-horizon et des pipelines RAG intensifs sans craindre le plafonnement API dans les 6 prochains mois.
- **PageIndex (29.8k★, +943★/jour) — RAG sans vecteurs : challenger crédible à pgvector** : VectifyAI propose un index de documents structuré pour du RAG par raisonnement pur, sans embedding ni base vectorielle. Approche radicalement différente de notre stack pgvector. Pour H'appi : benchmarker PageIndex sur un corpus client structuré (catalogue produits, FAQ tabulaire) au prochain projet — si la précision est comparable, on élimine la couche vectorielle, simplifie l'infra et réduisons les coûts d'indexation.
- **Stack Voice AI H'appi validée par les marchés (ElevenLabs $11Md, Deepgram $1.3Md, Vapi 62M calls/mois)** : les trois piliers de notre stack Voice ont tous levé massivement et traité à l'échelle enterprise en 2026. Pour les clients H'appi qui demandent "ces startups vont durer ?", la réponse est chiffrée. Argument commercial clé dans les pitchs Voice : "notre stack s'appuie sur des acteurs capitalisés à plusieurs milliards, pas des side-projects — pérennité des APIs garantie sur 3-5 ans".
- **AI Act chatbots "risque limité" — conformité simple, deadline J-85 (2 août 2026)** : les chatbots H'appi sont classés "risque limité". Seule obligation : informer l'utilisateur qu'il parle à une IA dès le premier message. Pas de certification lourde, pas de DPIA complexe. Pour H'appi : transformer cette simplicité en argument commercial — "conformité AI Act clés-en-main incluse dans chaque projet, sans overhead réglementaire pour le client".
- **Vercel + Railway hybrid = référence marché confirmée 2026** : tous les guides de déploiement SaaS IA 2026 convergent vers Next.js/Vercel (frontend edge) + Railway/Docker (backend long-running + base de données) comme stack de référence. La stack H'appi est exactement alignée. À documenter explicitement dans les pitchs techniques et les pages produit : "nous déployons sur le standard marché 2026, pas une architecture expérimentale" — argument de rassurance fort pour les DSI enterprise.

---
## 📰 Veille Tech — 2026-05-10
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropic-sdk-python v0.100.0 — Managed Agents multiagents, webhooks & vault validation](https://github.com/anthropics/anthropic-sdk-python/releases/tag/v0.100.0) | GitHub Releases 🐍 | #Claude #Anthropic |
| [anthropic-sdk-python v0.97.0 — CMA Memory public beta : mémoire persistante native dans l'API](https://github.com/anthropics/anthropic-sdk-python/releases/tag/v0.97.0) | GitHub Releases 🐍 | #Claude #Anthropic #LLM |
| [anthropics/financial-services — Blueprint 11 agents Claude spécialisés finance (+3 281★/jour, 17.7k★)](https://github.com/anthropics/financial-services) | GitHub Trending 🐍 | #Claude #Anthropic #SaaS |
| [datawhalechina/hello-agents — Tutorial complet construction agents IA de zéro (+1 197★/jour, 45.9k★)](https://github.com/datawhalechina/hello-agents) | GitHub Trending 🐍 | #LLM #chatbot |
| [lsdefine/GenericAgent — Agent auto-évolutif : skill tree depuis seed 3.3K lignes, 6x moins de tokens (+538★/jour, 10.3k★)](https://github.com/lsdefine/GenericAgent) | GitHub Trending 🐍 | #LLM #chatbot |
| [sgl-project/sglang — Framework serving LLM haute performance multimodal production-ready (+153★/jour, 27.6k★)](https://github.com/sgl-project/sglang) | GitHub Trending 🐍 | #LLM |
| [hesreallyhim/awesome-claude-code — Ressources curated Claude Code : hooks, MCPs, workflows (+153★/jour, 43.2k★)](https://github.com/hesreallyhim/awesome-claude-code) | GitHub Trending 🐍 | #Claude |
| [bytedance/UI-TARS-desktop — Stack agent multimodal open-source : modèles IA + infra agents intégrée (31.6k★)](https://github.com/bytedance/UI-TARS-desktop) | GitHub Trending TS | #LLM #chatbot |
| [rohitg00/agentmemory — Mémoire persistante #1 benchmarks pour agents IA en production (3.6k★)](https://github.com/rohitg00/agentmemory) | GitHub Trending TS | #LLM #chatbot |
| [rowboatlabs/rowboat — AI coworker open-source avec mémoire : alternative Dify orientée collaboration (13.9k★)](https://github.com/rowboatlabs/rowboat) | GitHub Trending TS | #LLM #SaaS #chatbot |
| [CopilotKit/CopilotKit — Frontend Stack for Agents & Generative UI React + Angular (31.2k★)](https://github.com/CopilotKit/CopilotKit) | GitHub Trending TS | #React #chatbot |
| [heygen-com/hyperframes — Write HTML, Render video : génération vidéo pour agents (16.6k★)](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #VoiceAI #chatbot |
| [millionco/react-doctor — Détecteur d'anti-patterns React produits par agents IA (7.4k★)](https://github.com/millionco/react-doctor) | GitHub Trending TS | #React |

### 💡 Insights clés
- **CMA Memory public beta (SDK v0.97.0) — mémoire long-terme native dans l'API Anthropic** : Anthropic a mis en beta publique la mémoire persistante directement dans le SDK Python. Pour H'appi : nos chatbots peuvent désormais stocker et rappeler le contexte utilisateur long-terme via l'API officielle, sans construire de couche custom PostgreSQL dédiée. À évaluer immédiatement sur un projet client — si la performance est suffisante, cela simplifie drastiquement l'architecture des bots stateful et réduit le coût infra de chaque projet.
- **Managed Agents multiagents + webhooks (v0.100.0, 6 mai 2026) — orchestration multi-agents native** : La coordination multi-agents est désormais de première classe dans le SDK Python officiel. Pour H'appi : construire des architectures "agents spécialisés" comme le blueprint financial-services directement avec l'API Anthropic — sans LangGraph ni framework tiers. Moins de dépendances, meilleure maintenabilité, support Anthropic garanti. À adopter pour tous les nouveaux projets agents H'appi dès maintenant.
- **GenericAgent 6x moins de tokens : l'efficacité prime sur la complexité initiale** : Un agent auto-évolutif qui construit son propre skill tree à partir d'une seed de 3 300 lignes avec 6x moins de consommation de tokens. Pour H'appi : leçon architecturale directement applicable — commencer petit et laisser l'agent s'auto-équiper est plus efficace que pré-câbler tous les tools dès la phase 1. À appliquer dans nos agents secrétariat IA et supply chain : MVP minimal, skill tree évolutif.
- **rowboat + agentmemory — duo émergent pour agents avec mémoire contextuelle en production** : Rowboat (AI coworker open-source, 13.9k★) combiné avec agentmemory (#1 benchmarks mémoire persistante) forme un stack pour agents contextuels robustes. Pour H'appi : rowboat est à évaluer comme alternative ou complément à Dify — API-first, open-source, mémoire intégrée. Benchmark à planifier sur notre use case secrétariat IA : gain potentiel de 20-30% sur la fidélité contextuelle long-terme.
- **CopilotKit 31k★ — GenUI React : l'interface agent-native devient un standard de marché** : CopilotKit s'impose comme la référence frontend pour les agents et interfaces génératives en React. Pour H'appi : à intégrer dans les démos clients où l'interface doit s'adapter dynamiquement aux actions de l'agent — impact visuel fort en pitch commercial, différenciation nette par rapport aux chatbots widget classiques. Priorité sur les prochains prototypes clients Next.js.

---
## 📰 Veille Tech — 2026-05-11
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.7 GA — +13% résolution bugs, vision améliorée, task budgets](https://www.anthropic.com/news/claude-opus-4-7) | Anthropic | #Claude #Anthropic |
| [Claude Code Auto Mode — Coding autonome avec Human Approval Gates](https://www.infoq.com/news/2026/05/anthropic-claude-code-auto-mode/) | InfoQ | #Claude #Anthropic |
| [Anthropic Finance Agents — 10 templates agents prêts à l'emploi (plugins + cookbook)](https://www.anthropic.com/news/finance-agents) | Anthropic | #Claude #LLM |
| [anthropics/skills — Repo public Agent Skills Claude (+509★/jour, 131k★)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #Anthropic |
| [NousResearch/hermes-agent — "The agent that grows with you" (+1 496★/jour, 143k★)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #chatbot |
| [MemoriLabs/Memori — Mémoire persistante agent-native pour production (+62★/jour, 14k★)](https://github.com/MemoriLabs/Memori) | GitHub Trending 🐍 | #LLM #chatbot |
| [datawhalechina/hello-agents — Tutorial agents IA de zéro (+748★/jour, 47k★)](https://github.com/datawhalechina/hello-agents) | GitHub Trending 🐍 | #LLM #chatbot |
| [bytedance/UI-TARS-desktop — Stack agent multimodal open-source (+669★/jour, 32k★)](https://github.com/bytedance/UI-TARS-desktop) | GitHub Trending TS | #LLM #chatbot |
| [rohitg00/agentmemory — #1 mémoire persistante agents IA production (+655★/jour, 4k★)](https://github.com/rohitg00/agentmemory) | GitHub Trending TS | #LLM #chatbot |
| [rowboatlabs/rowboat — AI coworker open-source avec mémoire (+356★/jour, 14k★)](https://github.com/rowboatlabs/rowboat) | GitHub Trending TS | #LLM #SaaS #chatbot |
| [Deepgram Buyer's Guide Voice AI 2026 — Vapi vs ElevenLabs vs Deepgram comparatif complet](https://deepgram.com/learn/best-voice-ai-agents-2026-buyers-guide) | Deepgram | #VoiceAI |
| [Railway Deploy Next.js + FastAPI Full-Stack Starter — template officiel prod-ready](https://railway.com/deploy/nextjs-fastapi-full-stack-starter) | Railway | #FastAPI #Next.js #Railway |
| [pgvector 2026 — Comparatif 9 bases vectorielles : pgvector mature pour RAG sous 10M vecteurs](https://www.marktechpost.com/2026/05/10/best-vector-databases-in-2026-pricing-scale-limits-and-architecture-tradeoffs-across-nine-leading-systems/) | MarkTechPost | #PostgreSQL |
| [AI Act août 2026 — Chatbots : obligation "Réponse générée par une IA" imminente](https://www.webotit.ai/blog/ia-conversationnelle/generalites/chatbot-et-rgpd-respectez-les-droits-des-personnes-avec-les-conseils-de-la-cnil) | Webotit.ai | #RGPD |
| [AI Chatbot ROI 2026 — Coût inference IA -85% depuis 2023 : 0.05-0.15$/conversation](https://www.gleap.io/blog/ai-chatbot-roi-benchmarks-saas) | Gleap | #chatbot #SaaS |

### 💡 Insights clés
- **Claude Opus 4.7 GA — Task Budgets : contrôle natif des coûts pour agents longs** : Opus 4.7 introduit les "task budgets" — Claude reçoit un quota de tokens pour toute une boucle agentique et s'adapte dynamiquement. Pour H'appi : mécanisme natif de maîtrise des coûts API sur nos agents longs (secrétariat IA, supply chain) sans couche custom. À activer dès maintenant sur les projets en production. Bonus : +13% résolution de bugs et vision haute résolution améliorent les use cases avec analyse de documents ou d'images.
- **Hermes-Agent 143k★ — "The agent that grows with you" : candidat open-source sérieux** : NousResearch propulse hermes-agent comme alternative open-source à la stack Claude SDK propriétaire. Pour H'appi : à monitorer pour les clients qui exigent une solution open-source ou la maîtrise totale du modèle de base. Peut servir de fallback ou de couche de routing intelligent quand Claude n'est pas imposé contractuellement.
- **AI Act pleinement applicable août 2026 — Conformité chatbot obligatoire dans 3 mois** : La mention "Réponse générée par une IA" devient obligatoire sur tous les chatbots. Pour H'appi : intégrer ce badge de transparence dans tous les widgets dès maintenant — c'est un argument commercial fort ("conformes AI Act à la livraison") ET une protection légale pour nos clients. Action immédiate : auditer tous les projets en production.
- **pgvector mature en production 2026 — RAG natif PostgreSQL, zéro infra supplémentaire** : Règle du marché 2026 : sous 10M vecteurs, pgvector dans PostgreSQL suffit. Pour H'appi : notre stack PostgreSQL permet d'ajouter nativement la recherche sémantique (RAG) aux chatbots sans Pinecone ni Weaviate. Un seul système, même transaction, même sécurité RGPD. À documenter comme standard obligatoire dans tous les nouveaux projets H'appi.
- **Voice AI 2026 : Vapi confirme 62M+ appels/mois à 0.05$/min — notre stack est validée** : Aucune plateforme ne domine tous les cas d'usage mais Vapi confirme fiabilité et pricing. Pour H'appi : notre choix Vapi est conforté. Pour les projets premium à forte exigence de naturalité : adopter le combo "gold standard" 2026 — Vapi (orchestration) + ElevenLabs sub-100ms (TTS) + Deepgram Nova-3 Multilingual (STT).

---
## 📰 Veille Tech — 2026-05-12
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic × SpaceX Colossus 1 — 220 000 GPU, Claude Code rate limits x2](https://releasebot.io/updates/anthropic) | Releasebot / Anthropic | #Claude #Anthropic |
| [Claude Managed Agents : Dreaming + Outcomes + Multiagent Orchestration (Code with Claude 2026)](https://letsdatascience.com/blog/anthropic-dreaming-claude-managed-agents-self-improving-may-6) | Let's Data Science | #Claude #LLM |
| [Claude Security Tool — public beta : scan vulnérabilités code avec Opus 4.7](https://releasebot.io/updates/anthropic/claude) | Releasebot / Anthropic | #Claude #Anthropic |
| [Claude × Microsoft 365 — Word, Excel, PowerPoint, Outlook intégrés natif](https://releasebot.io/updates/anthropic) | Releasebot / Anthropic | #Claude #SaaS |
| [garrytan/gstack — Setup Claude Code avec 23 outils (+918★/jour, 94k★)](https://github.com/garrytan/gstack) | GitHub Trending TS | #Claude #Anthropic |
| [HKUDS/AI-Trader — 100% Automated Agent-Native Trading (+801★/jour, 16k★)](https://github.com/HKUDS/AI-Trader) | GitHub Trending 🐍 | #LLM #chatbot |
| [earendil-works/pi — AI agent toolkit, unified LLM API (+514★/jour, 48k★)](https://github.com/earendil-works/pi) | GitHub Trending TS | #LLM #chatbot |
| [wanshuiyin/ARIS — Recherche ML autonome avec Claude + cross-model review loops (+186★/jour, 8.9k★)](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep) | GitHub Trending 🐍 | #Claude #LLM |
| [millionco/react-doctor — Agent IA qui détecte le mauvais code React (+212★/jour, 8.3k★)](https://github.com/millionco/react-doctor) | GitHub Trending TS | #Next.js #chatbot |
| [romainsimon/paperasse — Agent IA spécialisé bureaucratie française (+110★/jour, 1.6k★)](https://github.com/romainsimon/paperasse) | GitHub Trending 🐍 | #chatbot #RGPD |
| [jwadow/kiro-gateway — Proxy gratuit pour accéder aux modèles Claude (+76★/jour, 1.3k★)](https://github.com/jwadow/kiro-gateway) | GitHub Trending 🐍 | #Claude #Anthropic |
| [Voice AI Mai 2026 — Ce qui compose vraiment un agent vocal production](https://futureagi.substack.com/p/best-voice-ai-in-may-2026-what-actually) | FutureAGI Substack | #VoiceAI |
| [Vapi vs ElevenLabs 2026 — Comparatif pricing & use cases production](https://www.goodcall.com/voice-ai/vapi-vs-elevenlabs) | GoodCall | #VoiceAI |
| [Obligation transparence chatbot au 2 novembre 2026 — CNIL & AI Act : deadline dans 5 mois](https://www.agentsia.fr/chatbot-rgpd-france-2026/) | Agentsia.fr | #RGPD |

### 💡 Insights clés
- **Anthropic × SpaceX Colossus 1 : 220 000 GPUs → Claude Code doublé, API Opus +1 500%** : Anthropic a sécurisé la totalité de la facility Colossus 1 de SpaceX à Memphis (220k GPUs Nvidia). Conséquence directe : limites Claude Code doublées, API Opus augmentées de 1 500%. Pour H'appi : la contrainte de rate limiting sur nos agents longs (secrétariat IA, supply chain) disparaît en production. Mettre à jour les SLA clients et communiquer cette capacité comme argument de fiabilité dans les prochains devis.
- **Claude Managed Agents "Dreaming" — agents auto-améliorants : architecture à adopter pour le secrétariat IA H'appi** : "Dreaming" permet à Claude de s'améliorer entre sessions en rejouant des scénarios passés. "Outcomes" mesure la qualité des décisions. "Multiagent Orchestration" gère des pipelines d'agents sans config manuelle. Pour H'appi : cette infrastructure est exactement ce qu'il faut pour un agent secrétariat qui apprend des préférences d'un dirigeant au fil du temps — à intégrer dès la prochaine version majeure de l'offre secrétariat IA H'appi.
- **paperasse 🇫🇷 — Agent bureaucratie française viral (+110★/j) : H'appi a l'antériorité et l'expertise** : Le repo paperasse confirme l'appétit du marché pour des agents IA spécialisés sur les processus administratifs français (URSSAF, CERFA, RSE…). Pour H'appi : nous avons déjà la stack, la conformité RGPD et la connaissance du marché français. Action : formaliser une offre "Agent Administratif IA" dans le catalogue H'appi maintenant, avant saturation du segment. Argument différenciant fort : hébergement France + CNIL-ready à la livraison.
- **Badge transparence chatbot obligatoire au 2 novembre 2026 — 5 mois pour être conforme** : L'AI Act impose la mention explicite "Réponse générée par une IA" sur tout chatbot grand public dès le 2 novembre 2026. Sanction : jusqu'à 7,5M€ ou 1% du CA mondial pour manquement à la transparence. Pour H'appi : deadline concrète à communiquer à chaque client en production. Plan d'action : (1) audit de tous les projets livrés, (2) intégration du badge dans le widget standard, (3) positionner cette conformité comme argument commercial différenciant dans chaque devis.

---

## 📰 Veille Tech — 2026-05-15
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [OpenBMB/VoxCPM2 — TTS Tokenizer-Free pour génération vocale multilingue et clonage vocal réaliste](https://github.com/OpenBMB/VoxCPM) | GitHub Trending 🐍 | #VoiceAI |
| [rohitg00/agentmemory — Mémoire persistante pour agents IA codée sur benchmarks réels](https://github.com/rohitg00/agentmemory) | GitHub Trending TS | #LLM #chatbot |
| [MervinPraison/PraisonAI — "24/7 AI Workforce" : agents autonomes auto-améliorants qui recherchent, planifient et exécutent](https://github.com/MervinPraison/PraisonAI) | GitHub Trending 🐍 | #chatbot #LLM |
| [thesysdev/openui — Open Standard for Generative UI (interfaces générées par l'IA)](https://github.com/thesysdev/openui) | GitHub Trending TS | #Next.js #chatbot |
| [cline/cline — Autonomous coding agent disponible en SDK, extension IDE ou CLI](https://github.com/cline/cline) | GitHub Trending TS | #chatbot #LLM |
| [NousResearch/hermes-agent — "The agent that grows with you" : agent IA évolutif](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #chatbot #LLM |
| [K-Dense-AI/scientific-agent-skills — Bibliothèque de skills agents prêts-à-l'emploi (recherche, ingénierie, finance)](https://github.com/K-Dense-AI/scientific-agent-skills) | GitHub Trending 🐍 | #chatbot #LLM |
| [OthmanAdi/planning-with-files — Skill Claude Code : workflow planning en markdown persistant](https://github.com/OthmanAdi/planning-with-files) | GitHub Trending 🐍 | #Claude #Anthropic |
| [shiyu-coder/Kronos — Foundation Model pour le langage des marchés financiers](https://github.com/shiyu-coder/Kronos) | GitHub Trending 🐍 | #LLM |
| [danielmiessler/Personal_AI_Infrastructure — Infrastructure IA agentique pour amplifier les capacités humaines](https://github.com/danielmiessler/Personal_AI_Infrastructure) | GitHub Trending TS | #LLM #SaaS |
| [NVIDIA-AI-Blueprints/video-search-and-summarization — Agents vision GPU-accelerated pour analytics vidéo](https://github.com/NVIDIA-AI-Blueprints/video-search-and-summarization) | GitHub Trending 🐍 | #LLM |

### 💡 Insights clés
- **VoxCPM2 — TTS Tokenizer-Free viral : impact direct sur la stack Voice AI de H'appi** : OpenBMB publie VoxCPM2, un moteur TTS sans tokenizer capable de génération multilingue, de voice design créatif et de clonage vocal ultra-réaliste. Pour H'appi : notre stack voice repose sur ElevenLabs (TTS) + Deepgram (STT) + Vapi.ai. VoxCPM2 est une alternative open-source à surveiller de près pour les projets clients sensibles au coût ou nécessitant un hébergement France (RGPD). À benchmarker contre ElevenLabs en termes de latence et qualité avant intégration.
- **agentmemory — La mémoire persistante devient un standard pour les agents IA en production** : Le repo agentmemory (trending TS) implémente une couche mémoire structurée basée sur des benchmarks réels. Pour H'appi : notre agent secrétariat IA manque encore d'une couche mémoire robuste entre sessions. Ce pattern — stocker les préférences, décisions, et contexte client dans PostgreSQL et les injecter dans chaque prompt — est exactement l'architecture à adopter pour différencier notre offre de la concurrence. Priorité : spike technique sur ce repo cette semaine.
- **PraisonAI "24/7 AI Workforce" — menace concurrentielle directe à surveiller** : PraisonAI propose une workforce d'agents autonomes multi-tâches clé-en-main. C'est une offre packagée qui cible le même segment que H'appi (PME/ETI cherchant à automatiser). Pour H'appi : notre différenciation doit s'appuyer sur la personnalisation radicale, la conformité RGPD native et l'accompagnement humain — des points que PraisonAI, générique par design, ne peut pas matcher. Capitaliser sur cet argument dans les prochains pitchs commerciaux.
- **openui "Open Standard for Generative UI" — les interfaces chatbot vont se standardiser** : thesysdev pousse un standard ouvert pour les UIs générées par IA. Si ce standard s'impose (Next.js compatible), les widgets chatbot H'appi pourraient adopter ce format pour accélérer la livraison client. À surveiller pour la roadmap Q3 2026 du widget H'appi standard.

---
## 📰 Veille Tech — 2026-05-17
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/skills — Repo officiel Agent Skills Claude : research, engineering, finance, writing (+900★/jour, 135 949★)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #Anthropic #agents |
| [K-Dense-AI/scientific-agent-skills — Skills agents prêts à l'emploi : recherche, ingénierie, analyse, finance (+673★/jour, 23 383★)](https://github.com/K-Dense-AI/scientific-agent-skills) | GitHub Trending 🐍 | #LLM #agents |
| [luongnv89/claude-howto — Guide visuel complet Claude Code : concepts de base à agents avancés (+165★/jour, 33 211★)](https://github.com/luongnv89/claude-howto) | GitHub Trending 🐍 | #Claude #Anthropic |
| [HKUDS/CLI-Anything — Rendre tout logiciel CLI natif pour les agents IA (+333★/jour, 35 169★)](https://github.com/HKUDS/CLI-Anything) | GitHub Trending 🐍 | #LLM #agents |
| [dograh-hq/dograh — Plateforme Voice Agent open-source complète (+287★/jour, 1 370★)](https://github.com/dograh-hq/dograh) | GitHub Trending 🐍 | #VoiceAI |
| [colbymchenry/codegraph — Knowledge graph de codebase pré-indexé pour Claude Code : moins de tokens, 100% local (+416★/jour, 2 768★)](https://github.com/colbymchenry/codegraph) | GitHub Trending TS | #Claude #LLM |
| [anomalyco/opencode — L'agent de coding open-source de référence mondiale (#1 TS Trending, +473★/jour, 161 378★)](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #agents |
| [czlonkowski/n8n-mcp — MCP pour Claude Desktop/Code : piloter des workflows n8n en langage naturel (+205★/jour, 21 016★)](https://github.com/czlonkowski/n8n-mcp) | GitHub Trending TS | #Claude #SaaS #MCP |
| [tech-leads-club/agent-skills — Registry validé de skills pour agents IA pro : Claude Code, Cursor, Copilot (+44★/jour, 2 559★)](https://github.com/tech-leads-club/agent-skills) | GitHub Trending TS | #Claude #agents |
| [n8n-io/n8n — Automation workflow fair-code avec IA native, 400+ intégrations (+156★/jour, 188 243★)](https://github.com/n8n-io/n8n) | GitHub Trending TS | #SaaS #LLM #chatbot |

### 💡 Insights clés
- **anthropics/skills (#1 Python Trending, 135k★, +900★/jour) — les Agent Skills sont désormais les primitives de l'écosystème Claude** : Anthropic maintient une vélocité exceptionnelle sur ce repo officiel (research, engineering, finance, writing). Pour H'appi : auditer le catalogue complet cette semaine — les skills research et writing sont directement intégrables dans les agents secrétariat et CX sans développement custom. Compatible nativement Claude Agent SDK v0.100.0. Gain estimé 30-40% sur la phase dev agent de chaque nouveau projet.
- **codegraph (+416★/jour) — la troisième couche de mémoire Claude Code H'appi** : ce knowledge graph pré-indexé de codebase (moins de tokens, moins d'appels tools, 100% local) complète parfaitement le duo claude-mem (mémoire conversationnelle) + code-review-graph (mémoire structurelle) déjà dans notre stack. Pour H'appi : déployer les trois en tandem sur tous les projets longs clients — trio optimal pour la continuité de contexte sans surcoût API. À tester immédiatement sur le projet le plus actif.
- **dograh — Voice Agent platform open-source en accélération (+287★/jour)** : premier repo dédié exclusivement à la plateforme Voice Agent complète atteignant cette vélocité. Pour H'appi : alternative self-hosted crédible à Vapi pour les clients RGPD-strict refusant d'envoyer leurs flux vocaux sur une infrastructure tierce (médical, juridique, finance). Benchmark à planifier juin 2026 sur latence et qualité FR.
- **HKUDS/CLI-Anything — les agents IA intègrent les outils legacy via leur CLI** : framework Python exposant tout outil CLI comme un tool natif pour agents IA, sans API ni browser automation. Pour H'appi : applicable directement sur les projets supply chain ou secrétariat où l'agent doit interagir avec des ERP ou logiciels métier disposant d'une CLI — approche plus robuste que la scraping browser, moins risquée qu'une injection API non documentée.
- **n8n (188k★) + n8n-mcp (21k★) = standard automation PME confirmé** : le duo confirme son statut d'infrastructure de référence pour les PME automatisant avec l'IA. Pour H'appi : systématiser dans tous les pitchs CRM, supply chain et secrétariat l'argument "votre agent H'appi orchestre vos workflows n8n existants — zéro migration, ROI semaine 1". Intégration native documentée, aucun développement custom requis.
- **anomalyco/opencode (161k★, +473★/jour) confirme la commoditisation des agents de coding** : opencode reste #1 TS Trending avec une dynamique soutenue. Signal clair : H'appi doit capitaliser sur la spécialisation métier (SAV e-commerce, secrétariat médical, supply chain B2B), la conformité RGPD native et l'accompagnement humain — des avantages qu'aucun outil de coding générique open-source ne peut répliquer.

---

## 📰 Veille Tech — 2026-05-16
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic rend Claude plus accessible aux consommateurs — intégration HubSpot, QuickBooks, Canva](https://www.bloomberg.com/news/articles/2026-05-07/anthropic-is-making-claude-chatbot-more-appealing-to-consumers) | Bloomberg | #Claude #Anthropic #SaaS |
| [Claude Mythos Preview — le modèle Anthropic le plus puissant, encore réservé en accès restreint](https://red.anthropic.com/2026/mythos-preview/) | Anthropic | #Claude #Anthropic #LLM |
| [Vapi lève 50M$ en Série B, valorisation 500M$ — Amazon Ring migre 100% de ses appels entrants sur Vapi](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI |
| [Deepgram lève 130M$ à 1,3 Md$ de valorisation et rachète une startup YC](https://techcrunch.com/2026/01/13/deepgram-raises-130m-at-1-3b-valuation-and-buys-a-yc-ai-startup/) | TechCrunch | #VoiceAI |
| [Best Voice AI in May 2026 — Vapi vs ElevenLabs en production : ce qui compose réellement un agent vocal](https://futureagi.substack.com/p/best-voice-ai-in-may-2026-what-actually) | FutureAGI | #VoiceAI #chatbot |
| [anthropics/skills — Anthropic publie un repo officiel de skills d'agents prêts-à-l'emploi (135K★, +689/jour)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #Anthropic #chatbot |
| [joeseesun/qiaomu-anything-to-notebooklm — Claude Skill : processeur multi-sources pour NotebookLM](https://github.com/joeseesun/qiaomu-anything-to-notebooklm) | GitHub Trending 🐍 | #Claude #LLM |
| [opendatalab/MinerU — Transforme PDFs et docs Office en markdown/JSON prêt pour LLM (63K★)](https://github.com/opendatalab/MinerU) | GitHub Trending 🐍 | #LLM #chatbot |
| [czlonkowski/n8n-mcp — MCP pour construire des workflows n8n via Claude Code / Claude Desktop (21K★)](https://github.com/czlonkowski/n8n-mcp) | GitHub Trending TS | #Claude #chatbot #SaaS |
| [Railway Deploy LLM Stack — LiteLLM proxy production-ready avec PostgreSQL et Redis, 1 clic](https://railway.com/deploy/llm-stack) | Railway | #LLM #PostgreSQL #Docker |
| [AI Act 2026 — Guide complet conformité IA : double verrou AI Act + RGPD pour les entreprises](https://www.leto.legal/guides/ai-act-conformite) | Leto Legal | #RGPD |
| [Chatbot RGPD & CNIL 2026 — Obligations : base légale, transparence, minimisation, droits des personnes](https://www.webotit.ai/blog/ia-conversationnelle/generalites/chatbot-et-rgpd-respectez-les-droits-des-personnes-avec-les-conseils-de-la-cnil) | Webotit | #RGPD #chatbot |
| [Vercel vs Railway 2026 — Comparatif hébergement SaaS : serverless vs serveur persistant pour LLM](https://designrevision.com/blog/vercel-vs-railway) | DesignRevision | #Vercel #Docker #SaaS |
| [Full-Stack AI Chatbot RAG avec LangChain, FastAPI & Next.js — guide architecturel 2026](https://medium.com/@mail2ajoyshil/building-a-full-stack-ai-chatbot-rag-with-langchain-fastapi-next-js-de04c5dd04ab) | Medium | #FastAPI #Next.js #chatbot |

### 💡 Insights clés
- **Vapi $50M + Amazon Ring = validation massive du marché Voice AI pour les PME** : Vapi, qui orchestre Deepgram (STT) + Anthropic (LLM) + ElevenLabs (TTS), vient de lever 50M$ et de décrocher Amazon Ring comme client phare. Notre stack Vapi.ai est désormais adossée à une infrastructure enterprise-grade. Pour H'appi : c'est un argument commercial fort — "nous utilisons la même infrastructure que Amazon Ring". À intégrer dans les pitchs clients sur l'offre Voice AI dès maintenant.
- **Claude for Small Business dans HubSpot/QuickBooks — Anthropic attaque notre marché cible** : Anthropic intègre Claude directement dans les outils PME (HubSpot, Canva, QuickBooks, Google Workspace). H'appi ne vend pas un chatbot générique mais une personnalisation radicale + conformité RGPD. C'est exactement la différenciation à mettre en avant face aux offres "one-size-fits-all" d'Anthropic qui ne peuvent pas matcher l'intégration métier sur-mesure que nous livrons.
- **anthropics/skills — Bibliothèque officielle Anthropic de skills d'agents : à intégrer dans la stack H'appi** : Le repo officiel Anthropic (135K★, +689/j) expose des skills prêts-à-l'emploi (research, engineering, finance, writing). Pour H'appi : auditer ce repo cette semaine pour identifier les skills réutilisables directement dans nos agents secrétariat et CX. Gain de temps de développement estimé à 30-40% sur les prochains projets agent.
- **Double verrou AI Act + RGPD en 2026 — amendes jusqu'à 35M€ ou 7% du CA** : L'AI Act se superpose au RGPD et crée un régime de conformité à deux niveaux pour tout chatbot grand public. Sanctions AI Act : jusqu'à 35M€ ou 7% du CA. Pour H'appi : positionner systématiquement notre conformité RGPD-native + hébergement France comme bouclier commercial. Chaque devis doit mentionner "AI Act compliant dès la livraison".
- **Railway LLM Stack 1-clic + PostgreSQL + Redis — notre stack de déploiement se standardise** : Railway publie un template de déploiement LLM production-ready (LiteLLM proxy + PostgreSQL + Redis) en un clic. Pour H'appi : à adopter comme point de départ pour tous les nouveaux projets backend — réduit le temps de setup de 2h à 15min. Économie directe sur chaque nouveau projet client.

---

## 📰 Veille Tech — 2026-05-18
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/skills — Repo officiel Anthropic de skills d'agents publics (+514 étoiles/jour, 136K★)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #Anthropic #chatbot |
| [K-Dense-AI/scientific-agent-skills — Skills agents prêts-à-l'emploi : recherche, finance, rédaction (+762/jour)](https://github.com/K-Dense-AI/scientific-agent-skills) | GitHub Trending 🐍 | #LLM #agents |
| [colbymchenry/codegraph — Knowledge graph pré-indexé pour Claude Code, Codex et Cursor (+857/jour)](https://github.com/colbymchenry/codegraph) | GitHub Trending TS | #Claude #LLM |
| [langflow-ai/langflow — Builder visuel d'agents et workflows IA, production-ready (+155/jour, 148K★)](https://github.com/langflow-ai/langflow) | GitHub Trending 🐍 | #chatbot #LLM #agents |
| [yichuan-w/LEANN — RAG 97% d'économie de stockage, privé et rapide (+146/jour)](https://github.com/yichuan-w/LEANN) | GitHub Trending 🐍 | #LLM #RAG #chatbot |
| [dograh-hq/dograh — Plateforme open-source d'agents vocaux (+223/jour)](https://github.com/dograh-hq/dograh) | GitHub Trending 🌐 | #VoiceAI #chatbot |
| [jamiepine/voicebox — Studio vocal IA open-source : clonage, dictée, création (+195/jour)](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [tech-leads-club/agent-skills — Registre sécurisé de skills pour Claude, Cursor, Copilot (+225/jour)](https://github.com/tech-leads-club/agent-skills) | GitHub Trending TS | #Claude #agents |
| [NirDiamant/agents-towards-production — Tutoriels code-first agents GenAI production end-to-end (+172/jour)](https://github.com/NirDiamant/agents-towards-production) | GitHub Trending 🌐 | #LLM #agents |
| [microsoft/ai-agents-for-beginners — 12 leçons pour construire des agents IA (+485/jour, 62K★)](https://github.com/microsoft/ai-agents-for-beginners) | GitHub Trending 🌐 | #LLM #agents |
| [Shubhamsaboo/awesome-llm-apps — 100+ apps Agent & RAG clonables et personnalisables (+202/jour)](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #RAG #chatbot |
| [calcom/cal.diy — Infrastructure de scheduling open-source pour tous (+433/jour, 43K★)](https://github.com/calcom/cal.diy) | GitHub Trending TS | #SaaS |
| [tinyhumansai/openhuman — Super intelligence IA personnelle, privée et locale (+1 690/jour)](https://github.com/tinyhumansai/openhuman) | GitHub Trending 🌐 | #LLM #agents |
| [Anthropic SDK Python v0.102.0 — Cache Diagnostics Beta + BetaManagedAgents multiagents](https://github.com/anthropics/anthropic-sdk-python/blob/main/CHANGELOG.md) | Anthropic SDK | #Claude #Anthropic |
| [HKUDS/CLI-Anything — Rendre TOUS les logiciels natifs-agents via CLI (+238/jour, 36K★)](https://github.com/HKUDS/CLI-Anything) | GitHub Trending 🐍 | #agents #LLM |

### 💡 Insights clés
- **Explosion de l'économie des "Agent Skills" : 3 repos en tendance simultanément** — anthropics/skills (officiel), tech-leads-club/agent-skills et K-Dense-AI/scientific-agent-skills convergent vers un standard de skills modulaires réutilisables. Pour H'appi : adopter dès maintenant une architecture skill-based pour nos agents (secrétariat, CX, supply chain) — chaque skill devient un bloc métier réutilisable d'un projet à l'autre. Réduction estimée du temps de dev : 30-40% dès le 2e projet.
- **Voice AI open-source s'accélère : dograh + voicebox en forte hausse** — Deux plateformes Voice AI open-source montent simultanément. dograh est une alternative potentielle à Vapi.ai pour les clients sensibles au prix ; voicebox pourrait réduire la dépendance à ElevenLabs pour le clonage vocal. Pour H'appi : évaluer dograh sur un projet pilote client budget-contraint pour valider la qualité vs. coût par rapport à notre stack Vapi actuelle.
- **LEANN : RAG privé avec 97% d'économie de stockage — game changer RGPD** — Ce projet permet de faire du RAG sur n'importe quelle donnée locale sans infrastructure cloud coûteuse. Pour H'appi : solution idéale pour les clients dans les secteurs soumis à RGPD strict (santé, juridique, RH) qui refusent l'envoi de documents vers des APIs externes. À intégrer dans notre offre "RAG souverain hébergé en France".
- **Anthropic SDK v0.102.0 : Cache Diagnostics Beta activable maintenant** — La nouvelle fonctionnalité de diagnostics de cache permet de visualiser les cache hits/misses en temps réel. Pour H'appi : activer cette beta sur tous les projets FastAPI + SDK Anthropic pour optimiser les coûts API. Le cache prompt réduit jusqu'à 90% les coûts sur les grands contextes système — essentiel pour nos chatbots à fort contexte métier.
- **calcom/cal.diy +433 étoiles/jour — notre dépendance Cal.com devient un atout concurrentiel** — Le projet cal.diy confirme que Cal.com est en train de devenir l'infrastructure de scheduling de référence open-source. Pour H'appi : renforcer notre intégration Cal.com dans les pitchs clients secrétariat IA — "nous nous appuyons sur l'infrastructure de scheduling la plus adoptée au monde" est un argument de crédibilité fort.

---
## 📰 Veille Tech — 2026-05-20
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/claude-plugins-official — Répertoire officiel Anthropic de plugins Claude Code haute qualité (+171★/jour, 20 388★)](https://github.com/anthropics/claude-plugins-official) | GitHub Trending 🐍 | #Claude #Anthropic |
| [anthropics/skills — Dépôt public des Agent Skills officiels Anthropic (+667★/jour, 137 821★)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #agents |
| [HKUDS/CLI-Anything — Rendre TOUS les logiciels natifs-agents via hub CLI (+1 038★/jour, 38 012★)](https://github.com/HKUDS/CLI-Anything) | GitHub Trending 🐍 | #LLM #agents |
| [Imbad0202/academic-research-skills — Workflow Claude Code complet : research → write → review → revise (+3 164★/jour, 14 632★)](https://github.com/Imbad0202/academic-research-skills) | GitHub Trending 🐍 | #Claude #Anthropic |
| [humanlayer/12-factor-agents — 12 principes production pour agents LLM : stateless reducer, context window, human-in-loop (+736★/jour, 21 310★)](https://github.com/humanlayer/12-factor-agents) | GitHub Trending TS | #LLM #SaaS |
| [rohitg00/agentmemory — Mémoire persistante #1 benchmark pour agents IA coding en production (+1 609★/jour, 14 476★)](https://github.com/rohitg00/agentmemory) | GitHub Trending TS | #LLM #chatbot |
| [colbymchenry/codegraph — Knowledge graph pré-indexé pour Claude Code, Codex et Cursor (+1 850★/jour, 7 098★)](https://github.com/colbymchenry/codegraph) | GitHub Trending TS | #Claude #LLM |
| [tech-leads-club/agent-skills — Registre sécurisé et validé de skills pour agents IA pro : Claude Code, Cursor, Copilot (+399★/jour, 4 319★)](https://github.com/tech-leads-club/agent-skills) | GitHub Trending TS | #LLM #agents |
| [rmyndharis/OpenWA — API Gateway WhatsApp open-source self-hosted, zéro dépendance Meta (+1 870★/jour, 4 285★)](https://github.com/rmyndharis/OpenWA) | GitHub Trending TS | #chatbot #SaaS |
| [diegosouzapw/OmniRoute — AI gateway unifié 160+ providers LLM, compression et smart fallback (+115★/jour, 4 997★)](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #SaaS |
| [n8n v2.22.0 — Observational Memory system + MCP tools pour workflow AI, NVIDIA Nemotron intégré](https://github.com/n8n-io/n8n) | GitHub Trending TS | #SaaS #LLM |
| [Anthropic SDK Python v0.103.0 — Self-hosted sandboxes CMA + sandbox helpers pour ManagedAgents](https://github.com/anthropics/anthropic-sdk-python/blob/main/CHANGELOG.md) | Anthropic SDK | #Claude #Anthropic |
| [heygen-com/hyperframes — Write HTML, Render Video : pipeline vidéo conçu pour les agents IA (+344★/jour, 19 791★)](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #VoiceAI #chatbot |

### 💡 Insights clés
- **Anthropic SDK v0.103.0 — Self-Hosted Sandboxes : déploiement RGPD-compliant des agents managés** : La mise à jour majeure du SDK Python Anthropic introduit les sandboxes self-hosted dans le CMA (Claude Managed Agents), permettant d'exécuter des agents multi-étapes dans des environnements isolés on-premise ou Hetzner/Scaleway. Pour H'appi : upgrade obligatoire sur tous les projets FastAPI + SDK Anthropic — les clients médical, juridique et finance qui imposent la souveraineté des données peuvent désormais utiliser nos agents sans flux vers l'infrastructure Anthropic US. Combiné à Cache Diagnostics (v0.102.0), l'optimisation des coûts LLM devient mesurable.
- **OpenWA +1 870★/jour — WhatsApp self-hosted : nouveau canal de livraison chatbot sans Meta API** : Signal d'adoption massif pour l'API WhatsApp open-source self-hosted. Pour H'appi : permet d'ajouter WhatsApp comme canal natif dans nos chatbots clients (SAV, secrétariat) sans coûts API Meta ni dépendance tierce. Déployable sur Railway avec docker-compose — intégration estimée <2 jours sur un projet existant FastAPI.
- **OmniRoute — AI Gateway 160+ providers : découplage LLM sans refactoring** : Couche d'abstraction entre nos backends et tous les LLMs du marché (Claude, GPT, Mistral, modèles locaux). Pour H'appi : quand un client exige de changer de provider ou de tester des modèles open-source pour réduire les coûts, OmniRoute évite un refactoring complet. À intégrer dans la stack chatbot standard pour les contrats Enterprise avec clause de portabilité du modèle.
- **n8n v2.22.0 — Observational Memory + MCP tools : argument commercial CRM fort** : n8n intègre nativement la mémoire observationnelle entre sessions et les MCP tools pour modifier des workflows via IA. Pour H'appi : argument commercial direct — "votre chatbot H'appi orchestre vos workflows HubSpot/Pipedrive/Zapier sans code custom". La démo de connexion chatbot → n8n → CRM peut se livrer en 1 journée sur un projet secrétariat existant.
- **12-factor-agents + agentmemory : les deux primitives non-négociables de l'agent 2026** : La convergence simultanée des 12 principes production (stateless reducer, context window ownership, small focused agents) et de la mémoire persistante benchmark confirme le standard marché. Pour H'appi : auditer chaque projet agent actif contre les 12 facteurs avant livraison — les lacunes les plus fréquentes (context window non-maîtrisé, absence de mémoire inter-sessions, agents monolithiques) sont les causes #1 des incidents de production reportés. À intégrer dans la checklist de livraison section 9.

---
## 📰 Veille Tech — 2026-05-19
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Imbad0202/academic-research-skills — Workflow Claude Code complet : research → write → review → revise → finalize (+1 439★/jour, 12 721★)](https://github.com/Imbad0202/academic-research-skills) | GitHub Trending 🐍 | #Claude #Anthropic |
| [HKUDS/CLI-Anything — Rendre TOUS les logiciels natifs-agents via CLI (+1 049★/jour, 37 003★)](https://github.com/HKUDS/CLI-Anything) | GitHub Trending 🐍 | #LLM #agents |
| [K-Dense-AI/scientific-agent-skills — Skills agents prêts à l'emploi : recherche, ingénierie, finance, analyse (+609★/jour, 24 590★)](https://github.com/K-Dense-AI/scientific-agent-skills) | GitHub Trending 🐍 | #LLM #agents |
| [dograh-hq/dograh — Plateforme Voice Agent open-source complète (+616★/jour, 2 225★)](https://github.com/dograh-hq/dograh) | GitHub Trending 🐍 | #VoiceAI |
| [topoteretes/cognee — Memory control plane pour agents IA : remember/recall/forget/improve, PostgreSQL + Railway natif (17 329★)](https://github.com/topoteretes/cognee) | GitHub Trending 🐍 | #LLM #PostgreSQL #Railway |
| [tech-leads-club/agent-skills — Registre sécurisé et validé de skills pour agents IA pro : Claude Code, Cursor, Copilot (+1 244★/jour, 4 187★)](https://github.com/tech-leads-club/agent-skills) | GitHub Trending TS | #Claude #agents |
| [humanlayer/12-factor-agents — Principes de production pour agents LLM : idempotence, retry, observabilité (+399★/jour, 20 833★)](https://github.com/humanlayer/12-factor-agents) | GitHub Trending TS | #LLM #SaaS |
| [calcom/cal.diy — Infrastructure de scheduling open-source universelle, pilier de l'intégration Cal.com H'appi (+529★/jour, 43 627★)](https://github.com/calcom/cal.diy) | GitHub Trending TS | #SaaS |
| [nanocoai/nanoclaw — Agent léger Anthropic SDK natif : mémoire persistante + messaging (Slack/Discord/WhatsApp) + scheduled jobs (29 034★)](https://github.com/nanocoai/nanoclaw) | GitHub Trending TS | #Claude #chatbot |
| [rohitg00/agentmemory — Mémoire persistante #1 benchmarks pour agents IA coding en production (+1 244★/jour, 13 283★)](https://github.com/rohitg00/agentmemory) | GitHub Trending TS | #LLM #chatbot |
| [earendil-works/pi — Toolkit agent IA : CLI coding + API LLM unifiée (OpenAI/Anthropic/Google) + Slack bot + TUI/web (+448★/jour, 51 392★)](https://github.com/earendil-works/pi) | GitHub Trending TS | #LLM #chatbot |
| [heygen-com/hyperframes — Write HTML. Render video. Conçu pour les agents IA (+377★/jour, 19 460★)](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #VoiceAI #chatbot |

### 💡 Insights clés
- **academic-research-skills — Workflow Claude Code research → write → review → revise → finalize** : Ce skill set définit un processus complet de production de contenu piloté par Claude Code en 5 étapes avec boucle de révision, spécifiquement pensé pour Claude. Pour H'appi : pattern directement applicable aux agents secrétariat IA pour produire des comptes-rendus, rapports et synthèses clients de qualité contrôlée. À adapter comme skill standard dans les projets secrétariat et supply chain où la production de documents structurés est centrale.
- **dograh (2 225★, +616★/jour) — Voice Agent platform open-source en forte accélération** : Deuxième fois en tendance cette semaine, dograh confirme sa trajectoire comme alternative self-hosted à Vapi. Pour H'appi : crédible pour les clients médical, juridique ou finance refusant d'envoyer leurs flux vocaux sur une infrastructure US tierce. Benchmark à planifier juin 2026 sur la qualité FR et la latence production pour évaluer une migration partielle de notre stack Vapi actuelle.
- **cognee — Memory API PostgreSQL + Railway : mémoire agents H'appi sans dette technique** : cognee expose 4 primitives (`remember`, `recall`, `forget`, `improve`) compatibles nativement avec PostgreSQL et Railway — exactement notre stack. Pour H'appi : adopter comme couche de mémoire standard sur tous les nouveaux projets agents (secrétariat IA, SAV) plutôt que construire une couche custom. Bonus : plusieurs bots d'un même client partagent leur knowledge base via la cross-agent knowledge sharing.
- **12-factor-agents — la bible de l'agent LLM en production** : 12 principes pour rendre les agents LLM production-grade : idempotence des outils, retry avec backoff exponentiel, observabilité bout-en-bout, sandboxing des actions irréversibles. Pour H'appi : auditer chaque projet agent actif contre ces 12 facteurs avant livraison client — les lacunes les plus fréquentes (absence de retry, logging insuffisant) sont les causes #1 des incidents de production reportés. À intégrer dans la checklist de livraison.
- **nanoclaw (Anthropic SDK natif) — blueprint agent messaging avec mémoire** : Framework TypeScript léger utilisant le SDK Anthropic officiel pour construire des agents connectés aux apps de messaging (Slack, Discord, WhatsApp) avec mémoire inter-sessions et scheduled jobs. Pour H'appi : blueprint direct pour les projets clients qui veulent leur agent accessible depuis leur Slack interne — livraison en jours, dépendances minimales, 100% compatible SDK Anthropic v0.102.0.
- **agentmemory + agent-skills : deux primitives à 1 244★/jour identiques — la convergence du marché** : la hausse simultanée et identique (+1 244★/jour) de rohitg00/agentmemory et tech-leads-club/agent-skills le même jour est un signal de marché fort — mémoire persistante et skills réutilisables deviennent les deux primitives non-négociables de tout agent 2026. Pour H'appi : le prochain agent livré sans ces deux couches sera considéré sous-standard par les clients — les intégrer comme features baseline obligatoires dans tous les projets, au même titre que le RAG.

---

## 📰 Veille Tech — 2026-05-21
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Managed Agents : MCP tunnels + sandboxes privés — les agents Claude peuvent maintenant opérer dans des réseaux privés sans exposition publique](https://9to5mac.com/2026/05/19/anthropic-enhances-claude-managed-agents-with-two-new-privacy-and-security-features/) | Anthropic / 9to5Mac | #Claude #agents |
| [Claude Managed Agents : Dreaming + Multi-agent orchestration — un agent principal délègue à des spécialistes parallèles sur filesystem partagé](https://9to5mac.com/2026/05/07/anthropic-updates-claude-managed-agents-with-three-new-features/) | Anthropic / 9to5Mac | #Claude #agents |
| [Claude Finance : 10 agents IA pré-construits pour la finance (pitchbooks, KYC, clôture comptable) — disponibles en plugins Claude Code](https://www.anthropic.com/news/finance-agents) | Anthropic | #Claude #agents #SaaS |
| [Code with Claude 2026 : Managed Agents, Proactive Workflows, Capability Curve — analyse complète des 5 nouveautés agents](https://www.infoq.com/news/2026/05/code-with-claude/) | InfoQ | #Claude #agents |
| [Vapi atteint 500M$ de valorisation — Amazon Ring choisit Vapi parmi 40 concurrents pour router 100% de ses appels entrants](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI |
| [Deepgram lève 130M$ (valorisation 1.3B$) et rachète une startup YC — 1 300+ organisations utilisent ses modèles voix](https://techcrunch.com/2026/01/13/deepgram-raises-130m-at-1-3b-valuation-and-buys-a-yc-ai-startup/) | TechCrunch | #VoiceAI |
| [Best Voice AI May 2026 : ce qui compose réellement un agent vocal en production — Vapi vs ElevenLabs vs Deepgram](https://futureagi.substack.com/p/best-voice-ai-in-may-2026-what-actually) | FutureAGI | #VoiceAI |
| [FastAPI + Next.js 15 : The Full-Stack Nobody's Building — le duo Python/React domine pour les SaaS AI-adjacent en 2026](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV Community | #FastAPI #Next.js #SaaS |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy — alternative Vercel self-hosted avec déploiement Docker zéro downtime](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV Community | #FastAPI #Docker #SaaS |
| [AI Act 2026 : Guide complet obligations entreprise — mentions obligatoires dès le 2 août 2026 pour tout système IA](https://www.rgpdkit.fr/blog/ai-act-2026-guide-obligations-entreprise) | RGPDKit | #RGPD |
| [Chatbot RGPD et CNIL 2026 : règles à respecter — principe d'exactitude, base légale, durée de conservation](https://www.webotit.ai/blog/ia-conversationnelle/generalites/chatbot-et-rgpd-respectez-les-droits-des-personnes-avec-les-conseils-de-la-cnil) | Webotit.ai | #RGPD #chatbot |
| [claude-plugins-official (20 959★) — Répertoire officiel Anthropic des plugins Claude Code haute qualité](https://github.com/anthropics/claude-plugins-official) | GitHub Trending 🐍 | #Claude #agents |
| [12-factor-agents (21 470★) — Principes production LLM : idempotence, retry backoff, observabilité, sandboxing des actions irréversibles](https://github.com/humanlayer/12-factor-agents) | GitHub Trending TS | #LLM #agents |
| [vllm (80 610★) — Moteur d'inférence LLM haute performance et mémoire efficiente, standard de facto pour le serving LLM open-source](https://github.com/vllm-project/vllm) | GitHub Trending 🐍 | #LLM |
| [State of AI — May 2026 : les labs US dominent encore mais les labs chinois (DeepSeek, Alibaba) comblent l'écart sur le raisonnement et le code](https://press.airstreet.com/p/state-of-ai-may-2026) | Air Street Press | #LLM |

### 💡 Insights clés
- **Anthropic accélère sur la sécurité enterprise avec les MCP tunnels et sandboxes privés** : les agents Claude peuvent maintenant rester dans des réseaux privés sans exposer les MCP servers à l'internet public, et exécuter les outils dans l'infra du client. Pour H'appi : argument commercial décisif pour convaincre les clients grands comptes (banque, santé, juridique) encore réticents au SaaS cloud — "votre agent H'appi reste dans votre datacenter" devient techniquement possible dès aujourd'hui.
- **Vapi confirme sa domination Voice AI — 500M$ de valorisation, Amazon Ring, sub-500ms** : le choix d'Amazon Ring parmi 40 concurrents valide définitivement Vapi comme la référence production pour la téléphonie IA. Pour H'appi : continuer de positionner Vapi comme différenciateur dans les devis Happi Secretary. La série B de 50M$ garantit la pérennité de la plateforme — risque vendor lock-in acceptable.
- **AI Act : deadline critique au 2 août 2026 — les chatbots H'appi doivent afficher leur origine IA** : l'obligation de mentionner explicitement l'origine artificielle des réponses entre en vigueur dans 73 jours. Pour H'appi : auditer tous les chatbots clients actuellement en production (SAV-BOT, INnatural, Secretary) et ajouter un bandeau ou mention claire "Réponse générée par IA" avant la date limite pour éviter jusqu'à 4% du CA mondial d'amende.
- **FastAPI + Next.js 15 + Dokploy : la stack SaaS AI indie de référence en 2026** : Dokploy s'impose comme alternative Vercel self-hosted pour les clients qui refusent le cloud US — build Docker auto, zéro downtime, "Vercel-like DX à coût marginal". Pour H'appi : évaluer Dokploy comme option de déploiement alternative à Railway/Vercel pour les clients RGPD sensibles souhaitant héberger sur leur propre VPS Hetzner/Scaleway.
- **Claude Sonnet 4.6 benchmark #1 sur ClawBench (33.3%) — le meilleur modèle pour les tâches web en production** : H'appi fait le bon choix en utilisant Sonnet 4.6 comme modèle défaut. Ce benchmark sur 153 tâches de vrais sites en production confirme la supériorité sur GPT-5.5 pour les use cases de navigation et d'action web — pertinent pour les futurs agents H'appi capables d'interagir avec les back-offices clients.

---

## 📰 Veille Tech — 2026-05-22
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude for Small Business : workflows IA pré-construits dans HubSpot, QuickBooks, PayPal et Docusign](https://www.anthropic.com/news/claude-for-small-business) | Anthropic | #Claude #SaaS #chatbot |
| [Claude for Legal : 20+ connecteurs MCP juridiques et 12 plugins pratique pour cabinets et équipes in-house](https://www.artificiallawyer.com/2026/05/12/claude-for-legal-launches-may-reshape-the-legal-tech-world/) | Artificial Lawyer | #Claude #chatbot |
| [PwC déploie Claude Code à l'échelle mondiale — 30 000 professionnels certifiés, Centre d'Excellence Anthropic/PwC](https://www.anthropic.com/news/pwc-expanded-partnership) | Anthropic | #Claude #SaaS |
| [Vapi lève 50M$ Série B — 1 milliard d'appels franchis, 2,7M d'agents créés par 1M de développeurs](https://www.globenewswire.com/news-release/2026/05/12/3292882/0/en/vapi-raises-50m-series-b-as-it-reaches-1-billion-calls-powering-the-next-generation-of-enterprise-voice-ai.html) | GlobeNewswire | #VoiceAI |
| [Choisir le bon LLM pour agents vocaux 2026 : Claude Sonnet 4.6 vs GPT-5.4 vs Gemini 3.1 Flash — benchmark comparatif](https://softcery.com/lab/ai-voice-agents-choosing-the-right-llm) | Softcery | #VoiceAI #Claude |
| [Deutsche Telekom Magenta AI Call Assistant — traduction live + résumé conversation directement dans l'infrastructure réseau vocal](https://masterofcode.com/blog/voice-ai-trends) | Master of Code | #VoiceAI |
| [forge — Framework Python self-hosted pour LLM tool-calling et workflows agentiques (398★)](https://github.com/antoinezambelli/forge) | GitHub Trending 🐍 | #LLM #FastAPI |
| [OpenWA — Gateway WhatsApp open-source self-hosted pour intégrer WhatsApp à ses agents chatbot](https://github.com/rmyndharis/OpenWA) | GitHub Trending TS | #chatbot #SaaS |
| [codegraph — Knowledge graph pré-indexé pour Claude Code, Cursor et Codex : contextualisation codebase instantanée](https://github.com/colbymchenry/codegraph) | GitHub Trending TS | #Claude #LLM |
| [CLI-Anything — Rendre tous les logiciels "Agent-Native" via une couche CLI universelle (656★/jour)](https://github.com/HKUDS/CLI-Anything) | GitHub Trending 🐍 | #LLM #agents |
| [FastAPI + Next.js 15 : la stack full-stack que personne ne construit mais que tout SaaS AI devrait utiliser](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV Community | #FastAPI #Next.js #SaaS |
| [AI SaaS avec Next.js + FastAPI + Dokploy — alternative self-hosted à Vercel, déploiement Docker zéro downtime](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV Community | #FastAPI #Docker #SaaS |
| [AI Act Digital Omnibus — accord politique du 7 mai 2026 : simplification EU mais obligations de transparence IA maintenues en août 2026](https://www.globalpolicywatch.com/2026/02/eu-regulators-issue-opinion-on-revisions-of-gdpr-and-other-data-laws/) | Global Policy Watch | #RGPD |
| [CNIL recommandations RGPD pour systèmes IA — base légale, exactitude, durée de conservation appliquées aux chatbots](https://www.cnil.fr/en/ai-system-development-cnils-recommendations-to-comply-gdpr) | CNIL | #RGPD #chatbot |
| [stitch-skills (Google Labs) — Bibliothèque de skills agents compatible Claude Code, Gemini CLI et Cursor](https://github.com/google-labs-code/stitch-skills) | GitHub Trending TS | #Claude #agents |

### 💡 Insights clés
- **Claude for Small Business + Legal : Anthropic attaque directement les segments H'appi** : les workflows HubSpot, QuickBooks et les 20+ MCP légaux sont des solutions génériques clés en main. Pour H'appi : accélérer la différenciation "sur-mesure sectoriel" — notre valeur reste la personnalisation profonde (ton de marque, base de connaissance métier, intégration ERP) et l'accompagnement humain que ces offres packagées ne fournissent pas.
- **Vapi franchit 1 milliard d'appels et lève 50M$ — la stack vocale H'appi est sur le bon cheval** : la Série B avec Peak XV, Microsoft M12 et Kleiner Perkins garantit la pérennité de Vapi pour 3-5 ans. Pour H'appi : aucun changement de stack vocal — renforcer le positionnement "powered by Vapi" dans les devis Happi Secretary comme signal enterprise, et profiter des nouvelles fonctionnalités annoncées (multi-agent orchestration vocale).
- **Claude Sonnet 4.6 classé parmi les meilleurs LLM pour agents vocaux 2026** : le benchmark comparatif place Sonnet 4.6 en tête sur la compréhension contextuelle longue et le français naturel. Pour H'appi : argument technique direct à glisser dans les propositions commerciales Happi Secretary — "nous utilisons le LLM benchmarké #1 pour les agents vocaux en production".
- **OpenWA self-hosted : nouvelle verticale chatbot WhatsApp RGPD-compliant accessible** : un gateway WhatsApp open-source mature ouvre la possibilité de déployer des chatbots H'appi sur WhatsApp Business hébergé en France, sans dépendre de Meta Cloud API. Pour H'appi : évaluer pour un nouveau produit "Happi WhatsApp Bot" — les PME françaises demandent WhatsApp depuis 2025, c'est un segment non encore adressé par la stack actuelle.
- **AI Act Digital Omnibus confirmé — deadline transparence IA au 2 août 2026 inchangée** : malgré la simplification réglementaire, l'obligation de mentionner explicitement l'origine artificielle des réponses reste en vigueur dans 72 jours. Pour H'appi : lancer l'audit de conformité de tous les chatbots en production (SAV-BOT, INnatural, Secretary) avant fin juin — 1 mois de marge technique pour intégrer les bandeaux "Réponse générée par IA" avant la deadline légale (jusqu'à 4% du CA mondial d'amende en cas de manquement).

---

## 📰 Veille Tech — 2026-05-23
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Andrej Karpathy rejoint Anthropic pour le pré-entraînement de Claude — "les prochaines années à la frontière des LLMs seront particulièrement formatrices"](https://winbuzzer.com/2026/05/19/andrej-karpathy-joins-anthropic-claude-pre-training-push-xcxwbn/) | WinBuzzer | #Claude #LLM |
| [Claude nouvelle Constitution — Anthropic publie le document d'alignement de valeurs qui guide Claude en production](https://www.anthropic.com/news/claude-new-constitution) | Anthropic | #Claude |
| [Claude API Cache Diagnostics en bêta publique — diagnostiquer les cache miss via diagnostics.previous_message_id et optimiser les coûts de prompt caching](https://releasebot.io/updates/anthropic) | Releasebot / Anthropic | #Claude |
| [RAGFlow — moteur RAG open-source leader : fusion RAG + agents pour une couche de contexte supérieure pour les LLMs en production](https://github.com/infiniflow/ragflow) | GitHub | #LLM #chatbot |
| [activepieces (22 361★) — AI Agents, MCPs et AI Workflow Automation TypeScript open-source : automatiser les workflows IA sans code](https://github.com/activepieces/activepieces) | GitHub Trending TS | #SaaS #agents |
| [hermes-agent (163 483★, +1 743★/jour) — "The agent that grows with you" — NousResearch publie son framework agent phare](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [Mastra — framework TypeScript opinionated avec RAG, observabilité et support MCP intégré nativement](https://github.com/mastra-ai/mastra) | GitHub | #LLM #Next.js |
| [repomix (25 407★) — Pack tout votre repo en 1 fichier AI-friendly pour Claude, ChatGPT, DeepSeek et Perplexity](https://github.com/yamadashy/repomix) | GitHub Trending TS | #Claude #LLM |
| [Understand-Anything (19 194★, +1 393★/jour) — Transformez n'importe quelle codebase en knowledge graph interactif, compatible Claude Code, Cursor et Copilot](https://github.com/Lum1104/Understand-Anything) | GitHub Trending TS | #Claude #LLM |
| [Railway Next.js + FastAPI Full-Stack Starter officiel — monorepo production avec PostgreSQL, Redis et background workers, async flow intégré](https://railway.com/deploy/nextjs-fastapi-full-stack-starter) | Railway | #FastAPI #Docker #SaaS |
| [SaaS Hosting 2026 : Vercel vs Railway vs Render — benchmark complet pour déployer un SaaS Next.js avec auth, PostgreSQL et Stripe](https://designrevision.com/blog/saas-hosting-compared) | DesignRevision | #SaaS #Vercel #Railway |
| [Deepgram Voice Agent sub-400ms self-hosted — bundle Nova-3 + LLM routing + TTS en one-shot, option auto-hébergée pour clients RGPD-sensibles](https://deepgram.com/learn/best-voice-ai-agents-2026-buyers-guide) | Deepgram | #VoiceAI |
| [CNIL programme de travail 2026 — accompagnement professionnels IA : guides, audits, conformité RGPD pour systèmes IA en production](https://www.cnil.fr/fr/accompagnement-des-professionnels-le-programme-de-travail-de-la-cnil-pour-2026) | CNIL | #RGPD |

### 💡 Insights clés
- **Andrej Karpathy chez Anthropic — signal de confiance maximal sur Claude** : l'un des chercheurs LLM les plus respectés au monde (ex-OpenAI, ex-Tesla AI) rejoint Anthropic pour le pré-entraînement. Pour H'appi : aucun changement de stratégie nécessaire — c'est une validation externe forte du choix Claude comme LLM de référence. À mentionner dans les pitchs clients pour renforcer la crédibilité de la stack.
- **Railway Full-Stack Starter officiel valide exactement notre stack** : le template monorepo officiel Railway (Next.js + FastAPI + PostgreSQL + Redis + background workers) est sorti le 3 avril 2026 — c'est blueprint-for-free pour nos nouveaux projets. Pour H'appi : adopter ce starter comme base de tous les futurs projets chatbot full-stack plutôt que de repartir de zéro, et contribuer nos patterns (bot-personality.json, webhook CRM, qualification 3 phases) par-dessus.
- **RAGFlow + Mastra : deux primitives RAG open-source à intégrer dans la stack** : RAGFlow expose un moteur RAG production-grade (chunking, reranking, agent loop) et Mastra apporte RAG + MCP + observabilité dans un framework TypeScript opinionated. Pour H'appi : évaluer RAGFlow comme couche RAG standard pour les bases de connaissance clients (produits, FAQ, procédures), en remplacement des RAG custom que nous construisons projet par projet — gain estimé : 2-3 jours de dev par chatbot.
- **Deepgram Voice Agent self-hosted sub-400ms : carte RGPD à jouer pour grands comptes** : le bundle Nova-3 + TTS + LLM routing peut s'auto-héberger sur Scaleway/Hetzner France, garantissant zéro flux vocal en dehors de l'UE. Pour H'appi : argument décisif pour les clients médical, juridique et financier qui bloquaient sur Deepgram cloud US — planifier un benchmark Deepgram self-hosted vs Vapi sur la qualité FR et la latence avant fin juin 2026.
- **AI Act deadline : J-71 — l'audit de conformité ne peut plus attendre** : toutes les obligations de transparence IA entrent en vigueur dans 71 jours (2 août 2026). Pour H'appi : la CNIL publie son programme d'accompagnement 2026 — utiliser leurs guides officiels pour structurer l'audit des chatbots en production (SAV-BOT, INnatural, Secretary) et générer une preuve documentaire de conformité avant la deadline.

---

---
## 📰 Veille Tech — 2026-05-24
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude for Small Business — intégration native HubSpot, Canva, QuickBooks, DocuSign, Microsoft 365 avec workflows prêts à l'emploi](https://www.anthropic.com/news) | Anthropic | #chatbot #SaaS |
| [Claude Managed Agents GA — dreaming, orchestration multi-agents, webhooks et outcomes disponibles en API](https://releasebot.io/updates/anthropic) | Anthropic | #LLM #Claude |
| [MCP 2026 Roadmap — adoption universelle (Anthropic, OpenAI, Google, Microsoft), gouvernance formelle, enterprise readiness](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/) | MCP Blog | #LLM #SaaS |
| [anthropics/claude-plugins-official (+2 193★/jour) — répertoire officiel Anthropic des plugins Claude Code haute qualité](https://github.com/anthropics/claude-plugins-official) | GitHub Trending 🐍 | #Claude |
| [ElevenLabs Conversational AI 2.0 — tarifs réduits -50% (0,10$/min), nouveau positionnement voice-first](https://www.startuphub.ai/ai-news/artificial-intelligence/2026/elevenlabs-gives-chat-agents-a-voice) | StartupHub.ai | #VoiceAI |
| [Deepgram Voice Agent sub-400ms self-hosted — Nova-3 + Flux Multilingual + LLM routing + TTS, hébergeable France (RGPD)](https://deepgram.com/learn/best-voice-ai-agents-2026-buyers-guide) | Deepgram | #VoiceAI #RGPD |
| [Vapi vs ElevenLabs 2026 — benchmark complet : latence, pricing, compliance, intégration LLM](https://www.retellai.com/blog/vapi-vs-elevenlabs) | Retell AI | #VoiceAI |
| [Full-Stack AI Agent Template — FastAPI + Next.js 15 + WebSocket streaming + 6 frameworks (PydanticAI, LangChain, CrewAI, LangGraph…)](https://github.com/vstorm-co/full-stack-ai-agent-template) | GitHub | #FastAPI #Next.js #SaaS |
| [pydantic/pydantic-ai (17 249★) — framework agent Python opinionated façon Pydantic, compatible FastAPI](https://github.com/pydantic/pydantic-ai) | GitHub Trending 🐍 | #FastAPI #LLM |
| [OpenPipe/ART (9 810★) — Agent Reinforcement Trainer : entraîner des agents multi-étapes pour tâches réelles via GRPO](https://github.com/OpenPipe/ART) | GitHub Trending 🐍 | #LLM #agents |
| [Expo SDK 54 + Vercel AI SDK v4.3 — streaming Claude natif en React Native, universal React Server Components](https://expo.dev/blog/how-to-run-ai-models-with-react-native-executorch) | Expo | #React Native |
| [Chatbot et RGPD 2026 : le chatbot doit s'identifier comme IA dès le 1er message — obligation AI Act août 2026](https://www.agentsia.fr/chatbot-rgpd-france-2026/) | Agentsia | #RGPD |
| [CNIL recommandations RGPD pour systèmes IA — privacy by design obligatoire, AIPD si profilage ou données sensibles](https://www.cnil.fr/fr/developpement-des-systemes-dia-les-recommandations-de-la-cnil-pour-respecter-le-rgpd) | CNIL | #RGPD |
| [multica (32 081★) — plateforme open-source managed agents : transformer des coding agents en véritables coéquipiers](https://github.com/multica-ai/multica) | GitHub Trending TS | #SaaS #agents |

### 💡 Insights clés
- **Claude for Small Business + MCP omniprésent = opportunité de positionnement H'appi** : Anthropic cible directement les PME avec des intégrations HubSpot, Canva, QuickBooks prêtes à l'emploi — c'est le même segment que H'appi. Pour se différencier, insister sur la personnalisation radicale (bot-personality.json, qualification 3 phases, multilingue) que Claude for Small Business ne propose pas. Le MCP devenu standard universel (Anthropic, OpenAI, Google, Microsoft) valide l'architecture V2 Brain (serveur MCP) — anticiper cette migration.
- **ElevenLabs -50% sur la Conversational AI + Deepgram self-hosted : stack vocale plus accessible** : ElevenLabs à 0,10$/min rend Happi Secretary compétitif à des budgets encore plus bas. Deepgram self-hosted sur Scaleway/Hetzner France devient l'argument RGPD clé pour décrocher des clients médical, juridique et notarial — planifier un benchmark qualité FR avant fin juin 2026.
- **AI Act J-72 : le chatbot doit se déclarer IA dès le 1er message — audit urgent** : obligation en vigueur le 2 août 2026. Pour H'appi : auditer SAV-BOT, INnatural Stores et Happi Secretary pour vérifier que chaque bot s'identifie explicitement comme IA et que les mentions légales sont en place. Utiliser les guides CNIL pour produire une documentation de conformité — cela devient aussi un argument commercial différenciant face aux concurrents non-conformes.
- **Full-Stack AI Agent Template (FastAPI + Next.js 15) — 6 frameworks en 1 starter** : le template open-source vstorm-co supporte PydanticAI, LangChain, CrewAI, LangGraph et DeepAgents avec WebSocket streaming intégré. Pour H'appi : évaluer comme base pour les prochains chatbots full-stack plutôt que de repartir de zéro — gain estimé 1-2 jours de setup par projet.
- **React Native + Vercel AI SDK v4.3 : streaming Claude natif en mobile** : Expo SDK 54 + Vercel AI SDK permettent d'intégrer Claude avec streaming dans Quality Tracking App ou tout futur projet mobile. Pour H'appi : mettre à jour la stack mobile standard (section 2) pour inclure `ai` v4.3+ comme client Claude sur mobile.

---

---
## 📰 Veille Tech — 2026-05-25
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Vapi lève 50M$ à 500M$ de valorisation — Amazon Ring a choisi Vapi parmi 40 concurrents, 1 milliard d'appels traités](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI |
| [ElevenLabs 500M$ ARR + IBM watsonx — expansion enterprise et intégration voice-first pour agents IA](https://www.startuphub.ai/ai-news/artificial-intelligence/2026/elevenlabs-gives-chat-agents-a-voice) | StartupHub.ai | #VoiceAI |
| [Claude Managed Agents GA + mémoire "dreaming" — les agents Claude écrivent des notes persistantes pour les futurs agents](https://releasebot.io/updates/anthropic) | Anthropic/Releasebot | #Claude #LLM |
| [Anthropic Claude for Small Business — HubSpot, QuickBooks, Canva, Microsoft 365 intégrés nativement avec workflows PME](https://www.bloomberg.com/news/articles/2026-05-07/anthropic-is-making-claude-chatbot-more-appealing-to-consumers) | Bloomberg | #Claude #SaaS |
| [anthropics/claude-plugins-official (+1 173★/jour) — répertoire officiel Anthropic des plugins Claude Code haute qualité](https://github.com/anthropics/claude-plugins-official) | GitHub Trending 🐍 | #Claude |
| [anthropics/knowledge-work-plugins (+550★/jour) — plugins open-source pour knowledge workers (Claude Cowork)](https://github.com/anthropics/knowledge-work-plugins) | GitHub Trending 🐍 | #Claude #LLM |
| [ai-engineering-from-scratch (+1 853★/jour) — guide complet AI engineering : apprendre, construire, shipper des agents IA](https://github.com/rohitg00/ai-engineering-from-scratch) | GitHub Trending 🐍 | #LLM #agents |
| [honcho — bibliothèque mémoire pour agents IA stateful, persistance des sessions conversationnelles](https://github.com/plastic-labs/honcho) | GitHub Trending 🐍 | #chatbot #agents |
| [How to build production-ready AI agents with RAG and FastAPI](https://thenewstack.io/how-to-build-production-ready-ai-agents-with-rag-and-fastapi/) | The New Stack | #FastAPI #LLM |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy — retour d'expérience complet](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #Next.js #SaaS |
| [trigger.dev (15 072★) — plateforme managed agents IA et workflows, deploy from GitHub sans config serveur](https://github.com/triggerdotdev/trigger.dev) | GitHub Trending TS | #SaaS #agents |
| [AI Agents & GDPR 2026 : Compliance Checklist — DPIA obligatoire, consentement explicite, résidence données EU](https://technovapartners.com/en/insights/security-gdpr-enterprise-ai-agents) | Technova | #RGPD |
| [Vercel vs Railway vs Render : déployer des applications IA en 2026 — benchmark complet pour SaaS IA](https://remery.ai/blog/vercel-vs-railway-vs-render-ai-deployment) | Remery.ai | #Railway #Vercel #Docker |

### 💡 Insights clés
- **Vapi $500M valorisation + 1 milliard d'appels : H'appi Secretary sur la bonne plateforme** — Amazon Ring a évalué 40 concurrents avant de choisir Vapi pour 100% de ses appels entrants. C'est une validation externe forte de notre choix technique pour Happi Secretary. Argument pitch à utiliser : "H'appi Secretary tourne sur la même infra vocale qu'Amazon Ring". Vapi traite 1 à 5 millions d'appels/jour — la scalabilité est prouvée en production.
- **Claude Managed Agents + mémoire "dreaming" : persistance conversationnelle native à explorer** — Les agents Claude peuvent désormais écrire des notes qui sont partagées avec les futurs agents sur le même code ou le même contexte. Pour H'appi : évaluer cette primitive dans SAV-BOT (historique client récurrent évitant les re-saisies) et Happi Secretary (contexte appelants VIP persistant entre sessions) — cela remplace un système mémoire custom et reste dans la stack Anthropic SDK.
- **Claude for Small Business = PME génériques, H'appi = PME sur-mesure** — Anthropic intègre Claude dans HubSpot, QuickBooks, Canva et Microsoft 365 pour les PME. C'est exactement notre segment cible. Notre réponse commerciale : personnalisation radicale (bot-personality.json, qualification 3 phases, multilingue, hébergement France RGPD) que Claude for Small Business ne peut pas offrir. À intégrer dans les slides de vente comme différenciateur clé.
- **FastAPI + Next.js confirmé stack dominante pour SaaS IA en 2026** — Templates officiels (Railway, Vercel), benchmarks NestJS vs FastAPI et retours d'expérience DEV.to convergent tous : notre stack est mainstream. Avantage pratique : facilité de recrutement freelance, maintenance long-terme, et réassurance clients sur la pérennité technologique.
- **AI Act J-70 — DPIA et identification IA obligatoires au 2 août 2026** — Obligation légale : tout chatbot doit se déclarer comme IA dès le 1er message, et une DPIA est requise si profilage ou données sensibles. Délai : 70 jours. Action urgente : auditer SAV-BOT, INnatural Stores et Happi Secretary. Les amendes AI Act atteignent 35M€ ou 7% du CA mondial — la non-conformité est un risque commercial direct.

---

## 📰 Veille Tech — 2026-05-27
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [dograh-hq/dograh — Plateforme Voice AI open-source self-hostée (alternative Vapi/Retell), Python+TS+Docker, 3.3k★](https://github.com/dograh-hq/dograh) | GitHub Trending 🐍 | #VoiceAI #Docker |
| [anthropics/knowledge-work-plugins — Plugins Claude open-source pour les knowledge workers (1 718★ aujourd'hui)](https://github.com/anthropics/knowledge-work-plugins) | GitHub Trending 🐍 | #Claude #Anthropic |
| [thedotmack/claude-mem — Framework mémoire Claude : capture sessions + compression IA pour injection contexte futur (78k★)](https://github.com/thedotmack/claude-mem) | GitHub Trending TS | #Claude #LLM |
| [asgeirtj/system_prompts_leaks — System prompts extraits de Claude Opus 4.7, 4.6, Sonnet 4.6 et ChatGPT 5.5 (40k★)](https://github.com/asgeirtj/system_prompts_leaks) | GitHub API | #Claude #Anthropic |
| [microsoft/agent-governance-toolkit — Toolkit gouvernance d'agents IA : policy enforcement + sécurité multi-agents (282★ auj.)](https://github.com/microsoft/agent-governance-toolkit) | GitHub Trending 🐍 | #LLM #RGPD |
| [n4ze3m/dialoqbase — Créez des chatbots RAG facilement : multi-LLM, auto-hébergé, 1.7k★](https://github.com/n4ze3m/dialoqbase) | GitHub API | #chatbot #LLM |
| [NangoHQ/nango — Build des intégrations produit avec l'IA : +860★ en 1 jour, 9k★ total](https://github.com/NangoHQ/nango) | GitHub Trending TS | #SaaS #LLM |
| [jina-ai/langchain-serve — LangChain apps en production via Jina & FastAPI, 1.6k★](https://github.com/jina-ai/langchain-serve) | GitHub API | #FastAPI #LLM |
| [alpic-ai/skybridge — Framework TypeScript full-stack pour MCP Apps + ChatGPT Apps, type-safe, React-powered](https://github.com/alpic-ai/skybridge) | GitHub Trending TS | #Next.js #SaaS |
| [NousResearch/hermes-agent — Agent framework "qui grandit avec vous", 1 502★ aujourd'hui](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [modelscope/FunASR — Toolkit STT industriel 170x realtime, 42★ auj. — alternative Deepgram open-source](https://github.com/modelscope/FunASR) | GitHub Trending 🐍 | #VoiceAI |
| [twentyhq/twenty — CRM open-source (alternative Salesforce) conçu pour l'IA, 47k★ total](https://github.com/twentyhq/twenty) | GitHub Trending TS | #SaaS |

### 💡 Insights clés
- **Dograh : concurrent open-source de Vapi à surveiller pour le pitch RGPD** — Alternative self-hostée à Vapi/Retell avec builder drag-and-drop, Twilio/Vonage intégré, Python+TS+Docker. 3.3k stars. Pour les clients exigeant un hébergement 100% France (notaires, santé), Dograh peut devenir un argument : "Happi Secretary peut tourner entièrement dans votre datacenter". À évaluer comme option enterprise RGPD-first.
- **claude-mem : mémoire de session Claude à intégrer dans SAV-BOT et Happi Secretary** — Le framework capture les données de session avec compression IA et les injecte dans les prochaines conversations. Cas d'usage direct : historique appelants VIP dans Happi Secretary (évite re-qualification à chaque appel), et mémoire commandes dans SAV-BOT pour les clients récurrents. Remplacerait notre système mémoire custom et resterait dans la stack Anthropic SDK.
- **System prompts Claude publiés (Opus 4.7, 4.6, Sonnet 4.6) : opportunité d'optimisation** — Les instructions système internes d'Anthropic sont désormais publiques (40k stars). Analyser ces prompts pour identifier les patterns de sécurité, de refus et de structuration utilisés par Anthropic — directement applicable à nos propres system prompts chatbots clients.
- **Microsoft Agent Governance Toolkit + AI Act J-66 : urgence conformité** — Microsoft publie un toolkit open-source pour enforcer des politiques de gouvernance sur agents IA autonomes. Timing critique avec la deadline AI Act au 2 août 2026 (66 jours). Action P0 : auditer SAV-BOT, INnatural et Happi Secretary avec ce toolkit avant la date butoir.
- **FastAPI + LangChain + Next.js : stack H'appi validée par le marché** — langchain-serve, skybridge et nango convergent tous sur notre stack standard. Le marché valide FastAPI comme référence production IA en 2026. Argument de réassurance tech à inclure dans les propositions commerciales.

---

## 📰 Veille Tech — 2026-05-28
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Managed Agents : Dreaming + Multiagent Orchestration — agents qui apprennent de leurs sessions passées](https://9to5mac.com/2026/05/07/anthropic-updates-claude-managed-agents-with-three-new-features/) | 9to5Mac | #Claude #Anthropic |
| [Code with Claude 2026 — 5 nouvelles features : dreaming, orchestration multi-agents, outcomes, webhooks, sandbox](https://www.mindstudio.ai/blog/code-with-claude-2026-new-agent-features) | MindStudio | #Claude #agents |
| [Claude for Small Business : intégrations natives HubSpot, QuickBooks, PayPal, Canva, Microsoft 365](https://blog.mean.ceo/anthropic-claude-news-may-2026/) | Mean.CEO | #Claude #SaaS |
| [OpenAI GPT-Realtime-2 via API — raisonnement GPT-5 dans un modèle vocal temps réel pour développeurs](https://techcrunch.com/2026/05/07/openai-launches-new-voice-intelligence-features-in-its-api/) | TechCrunch | #VoiceAI |
| [dograh (+3 465★) — plateforme voice AI self-hosted, alternative open-source à Vapi et Retell](https://github.com/dograh-hq/dograh) | GitHub Trending 🐍 | #VoiceAI |
| [Next.js 16.2 : dev server 400% plus rapide, Turbopack bundler par défaut (remplace Webpack)](https://tech-insider.org/nextjs-tutorial-full-stack-app-2026/) | Tech Insider | #Next.js |
| [Next.js security release Mai 2026 — 13 advisories corrigés : XSS, SSRF, cache poisoning, middleware bypass](https://vercel.com/changelog/next-js-may-2026-security-release) | Vercel | #Next.js |
| [Railway vs Vercel : $41/mo vs $1 010/mo pour la même app Next.js — benchmark complet](https://www.13labs.au/compare/railway-vs-vercel) | 13Labs | #Railway #Vercel |
| [La révolution agentique : LangGraph + MCP + Gemini 3.5 Flash — patterns d'orchestration production-ready](https://atalupadhyay.wordpress.com/2026/05/24/the-agentic-revolution-building-with-gemini-3-5-flash-langgraph-and-mcp/) | Atal Upadhyay | #LLM #agents #MCP |
| [langfuse (+28 101★) — plateforme open-source LLM observability : métriques, evals, gestion de prompts](https://github.com/langfuse/langfuse) | GitHub Trending TS | #LLM #SaaS |
| [twenty (+47 475★) — alternative open-source à Salesforce conçue pour l'IA](https://github.com/twentyhq/twenty) | GitHub Trending TS | #SaaS #CRM |
| [vllm (+81 215★) — moteur d'inférence LLM haute performance, standard pour auto-hébergement](https://github.com/vllm-project/vllm) | GitHub Trending 🐍 | #LLM |
| [AI Act + RGPD : dès le 2 août 2026 tout chatbot doit se déclarer IA explicitement — amendes 35M€](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonnéesPersonnelles.fr | #RGPD |
| [Chatbot RGPD conforme hébergé en France : Mistral + Ollama comme alternatives souveraines à ChatGPT](https://www.cedricsantiago.com/blog/chatbot-rgpd-conforme-france) | Cédric Santiago | #RGPD |
| [Dify : plateforme RAG open-source avec workflow visuel + ingestion documents, prod-ready](https://www.firecrawl.dev/blog/best-open-source-rag-frameworks) | Firecrawl | #LLM #RAG |

### 💡 Insights clés
- **Claude Dreaming : mémoire inter-sessions pour agents — fonctionnalité clé pour Happi Secretary V2** — Les agents Claude écrivent des notes entre sessions, apprennent des erreurs passées et reconnaissent les patterns récurrents. Pour Happi Secretary, cela ouvre la voie à la reconnaissance avancée des appelants habituels et à l'apprentissage continu des préférences client. À inscrire dans la roadmap V2.
- **Next.js 16.2 security release : mise à jour urgente sur tous les projets H'appi** — 13 vulnérabilités corrigées dont XSS, SSRF et cache poisoning. happi-bot.com, Happi Web Creator et Happi Foundry doivent être mis à jour. Commande : `npm install next@latest`.
- **Railway 26× moins cher que Vercel pour Next.js full-stack** — $41/mo vs $1 010/mo selon le benchmark 13Labs. Argument commercial fort pour les clients qui hésitent sur les coûts d'hébergement : H'appi livre sur Railway avec économies massives sans sacrifice de performance.
- **dograh : alternative self-hosted à Vapi pour les clients RGPD-sensitifs** — Projet trending en Python : voice AI auto-hébergée (alternative à Vapi/Retell). Pertinent pour les prospects Finance/Santé/Notariat qui refusent les données vocales sur serveurs américains. À évaluer en option pour les clients sensibles.
- **AI Act J-65 : obligation de déclaration IA au 2 août 2026** — Dans 65 jours, tout chatbot H'appi doit afficher explicitement son caractère artificiel dès le premier message. Action P0 : ajouter un bandeau/disclaimer sur SAV-BOT, INnatural Stores et Happi Secretary. Amendes jusqu'à 35M€ ou 7% CA mondial.

---

## 📰 Veille Tech — 2026-05-26
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.7 : 87.6% SWE-Bench Verified (+13pts vs 4.6), vision 3x plus haute résolution — même prix](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #LLM |
| [Anthropic : Claude Managed Agents avec MCP tunnels + sandboxes auto-hébergés (bêta publique 19 mai)](https://9to5mac.com/2026/05/19/anthropic-enhances-claude-managed-agents-with-two-new-privacy-and-security-features/) | 9to5Mac | #Claude #Anthropic |
| [Claude for Small Business — intégrations HubSpot, PayPal, Canva, QuickBooks, Microsoft 365](https://www.mindstudio.ai/blog/code-with-claude-2026-new-agent-features) | MindStudio | #Claude #SaaS |
| [Vapi lève $50M (Série B, valorisation $500M) après 1 milliard d'appels traités](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI |
| [Amazon Ring choisit Vapi après évaluation de 40 concurrents — 100% du trafic entrant migré](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI |
| [ElevenLabs atteint $500M ARR : latence <300ms, 96 langues, voix clonée en 30 secondes](https://enterprisedna.co/resources/news/vapi-50m-series-b-voice-ai-enterprise-2026/) | Enterprise DNA | #VoiceAI |
| [AI red teaming agents : compresse des semaines de tests adversariaux en quelques heures](https://www.helpnetsecurity.com/2026/05/21/ai-red-teaming-agents-research/) | Help Net Security | #LLM #agents |
| [anthropics/knowledge-work-plugins (+15 973★) — plugins open-source Claude pour les knowledge workers](https://github.com/anthropics/knowledge-work-plugins) | GitHub Trending 🐍 | #Claude |
| [moeru-ai/airi (+39 893★) — companion IA self-hosted avec voice chat temps réel et capacités gaming](https://github.com/moeru-ai/airi) | GitHub Trending TS | #VoiceAI #chatbot |
| [multica-ai/multica (+33 138★) — plateforme open-source managed agents pour agents autonomes](https://github.com/multica-ai/multica) | GitHub Trending TS | #agents #SaaS |
| [How I built an AI SaaS with Next.js, FastAPI and Dokploy — retour d'expérience complet](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #Next.js #SaaS |
| [AI Act + GDPR 2026 : chatbots en dual-framework — DPIA obligatoire si traitement à grande échelle](https://technovapartners.com/en/insights/security-gdpr-enterprise-ai-agents) | Technova | #RGPD |
| [SubQ : architecture non-transformer, context 12M tokens, $29M seed — concurrent direct aux LLMs actuels](https://press.airstreet.com/p/state-of-ai-may-2026) | Air Street Press | #LLM |

### 💡 Insights clés
- **Claude Opus 4.7 disponible : mettre à jour la stack H'appi** — +13 points sur SWE-Bench vs Opus 4.6, vision 3x plus haute résolution au même prix. Action : mettre à jour la section 8 pour pointer vers `claude-opus-4-7` sur les tâches d'analyse post-appel et de code complexe. Sonnet 4.6 reste le défaut pour les chatbots conversationnels standard.
- **MCP tunnels + sandboxes auto-hébergés = argument RGPD béton pour les prospects enterprise** — Claude Managed Agents permet désormais aux entreprises de garder données et exécution des outils dans leur propre périmètre de sécurité. Cible prioritaire : cabinets notariaux (Monassier), juridiques (Arc), et clients finance/santé. Pitch : "Agent IA Claude sans que vos données quittent votre datacenter."
- **Vapi $500M + Amazon Ring : notre stack vocale est validée au niveau Fortune 500** — Amazon Ring a évalué 40 fournisseurs voice AI avant de choisir Vapi. Happi Secretary tourne sur la même infrastructure. Argument commercial direct à insérer dans les slides Happi Secretary.
- **AI Act J-67 : deadline du 2 août 2026 approche dangereusement** — Dans 67 jours, obligation légale que tout chatbot se déclare comme IA dès le premier message + DPIA requise si données personnelles à grande échelle. Amendes jusqu'à 35M€ ou 7% CA mondial. Action urgente : audit de conformité sur SAV-BOT, INnatural Stores et Happi Secretary — priorité P0.
- **FastAPI + Next.js = stack confirmée mainstream, boilerplates prêts disponibles** — Multiples retours DEV.to et guides 2026 convergent : la stack H'appi est la référence indie SaaS IA. Avantage recrutement (freelances Python/TS facilement sourcés) et réassurance clients sur la pérennité. À utiliser comme preuve de solidité technique dans les propositions commerciales.

---

## 📰 Veille Tech — 2026-05-30
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/claude-code (+395★) — outil de coding agentique en terminal, comprend les codebases et exécute des tâches en langage naturel](https://github.com/anthropics/claude-code) | GitHub Trending 🐍 | #Claude #agents |
| [anthropics/skills (+945★) — bibliothèque publique de skills pour agents Claude](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #agents |
| [OpenBMB/VoxCPM (+1 815★) — TTS sans tokenizer, multilinguisme natif, clonage de voix en quelques secondes](https://github.com/OpenBMB/VoxCPM) | GitHub Trending 🐍 | #VoiceAI |
| [OpenMOSS/MOSS-TTS (+355★) — génération voix et sons réels open-source, conçu pour scénarios du monde réel](https://github.com/OpenMOSS/MOSS-TTS) | GitHub Trending 🐍 | #VoiceAI |
| [microsoft/markitdown (+1 873★) — convertit PDF, Word, Excel, images en Markdown LLM-ready](https://github.com/microsoft/markitdown) | GitHub Trending 🐍 | #LLM #RAG |
| [opendatalab/MinerU (+150★) — transforme documents complexes en Markdown/JSON pour workflows agentiques](https://github.com/opendatalab/MinerU) | GitHub Trending 🐍 | #LLM #RAG |
| [fastapi/fastapi (+44★) — FastAPI en trending : valide définitivement le choix H'appi comme référence prod IA](https://github.com/fastapi/fastapi) | GitHub Trending 🐍 | #FastAPI |
| [EveryInc/compound-engineering-plugin (+353★) — plugin officiel Claude Code pour Cursor, Codex et Windsurf](https://github.com/EveryInc/compound-engineering-plugin) | GitHub Trending TS | #Claude #agents |
| [twentyhq/twenty (+578★) — alternative open-source à Salesforce conçue nativement pour les agents IA](https://github.com/twentyhq/twenty) | GitHub Trending TS | #SaaS #CRM |
| [millionco/react-doctor (+148★) — agent IA qui détecte automatiquement les mauvais patterns React/Next.js](https://github.com/millionco/react-doctor) | GitHub Trending TS | #React #agents |
| [moeru-ai/airi (+55★) — companion IA self-hosted avec voice chat temps réel et capacités gaming](https://github.com/moeru-ai/airi) | GitHub Trending TS | #VoiceAI #chatbot |
| [iOfficeAI/AionUi (+137★) — app cowork IA locale open-source, multi-assistants CLI 24/7](https://github.com/iOfficeAI/AionUi) | GitHub Trending TS | #SaaS |

### 💡 Insights clés
- **VoxCPM + MOSS-TTS : explosion des TTS open-source haut de gamme** — Deux projets TTS en top trending Python (1 815★ et 355★/j). VoxCPM supporte le multilinguisme sans tokenizer et le clonage de voix ; MOSS-TTS génère sons et voix pour scénarios réels. Alternatives crédibles à ElevenLabs pour les clients RGPD-sensitifs (hébergement EU possible). À évaluer pour Happi Secretary V2 sur les projets Finance/Notariat/Santé.
- **microsoft/markitdown + MinerU : pipeline RAG client simplifié** — Deux outils de parsing de documents en trending simultanément. markitdown (Microsoft, 1 873★/j) et MinerU transforment PDF/Word/Excel en Markdown/JSON directement ingérables par les LLMs. À intégrer dans Happi Secretary et SAV-BOT pour permettre aux clients d'uploader leurs propres bases de connaissance sans dev custom.
- **anthropics/claude-code + anthropics/skills trending simultanément** — L'écosystème d'agents Claude se structure publiquement avec une bibliothèque de skills officielle. Les Happi Brain Skills (agent de veille, agent de commit) préfigurent exactement ce modèle. Signal fort : investir dans les skills Claude est un pari sur l'architecture IA dominante de 2026.
- **twenty (578★/j) — CRM open-source IA pour les prospects RGPD-sensitifs** — Alternative à Salesforce avec API GraphQL + webhooks natifs conçue pour les agents IA. Option pertinente pour les prospects Finance/Notariat/Santé qui refusent HubSpot/Pipedrive (données hébergées US). À positionner comme alternative souveraine dans les offres H'appi CRM.
- **react-doctor : premier agent IA spécialisé qualité de code React** — Signal que l'outillage dev IA se spécialise par framework. À surveiller pour intégration dans le pipeline CI/CD H'appi (auto-review Next.js avant chaque PR). Couplé à compound-engineering-plugin pour Claude Code, cela forme un stack dev IA complet pour les projets Next.js H'appi.

---

## 📰 Veille Tech — 2026-05-31
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.8 : améliorations coding, agentic skills et raisonnement — même tarif](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #LLM |
| [Anthropic lève $65B (Série H) — valorisée $965B, $47B ARR run-rate](https://www.anthropic.com/news/series-h) | Anthropic | #Claude #Anthropic |
| [Claude for Legal : entrée officielle d'Anthropic sur le marché juridique](https://www.artificiallawyer.com/2026/05/12/claude-for-legal-launches-may-reshape-the-legal-tech-world/) | Artificial Lawyer | #Claude #SaaS |
| [PwC × Anthropic : 30 000 professionnels certifiés Claude, Centre d'Excellence conjoint](https://www.anthropic.com/news/pwc-expanded-partnership) | Anthropic | #Claude #SaaS |
| [Claude Managed Agents "dreaming" : mémoire inter-sessions, les agents apprennent entre les appels](https://simonwillison.net/2026/May/6/code-w-claude-2026/) | Simon Willison | #Claude #agents |
| [Code with Claude 2026 : MCP tunnels + sandboxes auto-hébergés AWS pour agents enterprise](https://www.technologyreview.com/2026/05/21/1137735/anthropics-code-with-claude-showed-off-codings-future-whether-you-like-it-or-not/) | MIT Technology Review | #Claude #agents |
| [GDPR-Compliant Chatbot Step-by-Step Guide 2026 — base légale, DPIA, retention policy](https://quickchat.ai/post/gdpr-compliant-chatbot-guide) | Quickchat AI | #RGPD |
| [AI Agents & GDPR 2026 : 73% des implémentations européennes non-conformes, DPIA obligatoire](https://technovapartners.com/en/insights/security-gdpr-enterprise-ai-agents) | Technova Partners | #RGPD |
| [anomalyco/opencode (+379★) — coding agent open-source TypeScript, alternative à Claude Code](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #agents |
| [cursor/plugins (+205★) — spécification officielle et plugins Cursor open-source](https://github.com/cursor/plugins) | GitHub Trending TS | #agents |
| [harry0703/MoneyPrinterTurbo (+2 768★) — génération vidéos courtes one-click avec LLM](https://github.com/harry0703/MoneyPrinterTurbo) | GitHub Trending 🐍 | #LLM |
| [Railway vs Vercel 2026 : Railway gagne pour le full-stack SaaS, Vercel reste roi du frontend](https://thesoftwarescout.com/vercel-vs-railway-2026-which-developer-platform-should-you-choose/) | The Software Scout | #Railway #Vercel |
| [1 million d'APIs IA exposées scannées : 90+ instances vulnérables dans gouvernement, finance, marketing](https://thehackernews.com/2026/05/we-scanned-1-million-exposed-ai.html) | The Hacker News | #LLM |

### 💡 Insights clés
- **Claude Opus 4.8 + $65B Série H : l'écosystème Anthropic est la meilleure mise long terme pour H'appi** — Anthropic est désormais valorisée $965B avec $47B ARR. Opus 4.8 améliore coding, agentic skills et raisonnement par rapport à 4.7. Action : mettre à jour `claude-opus-4-8` dans Happi Secretary et Happi Foundry pour les tâches d'analyse post-appel et de code complexe. Sonnet 4.6 reste le défaut pour les chatbots conversationnels.
- **Claude for Legal + PwC : lancer une offre H'appi ciblée notariat/juridique dès juin** — Anthropic entre officiellement sur le marché légal avec une offre dédiée. PwC forme 30 000 professionnels. Les cabinets Monassier et Arc sont des cibles H'appi parfaites. Pitch à affiner : "Claude for Legal implémenté, personnalisé et maintenu par H'appi — sans les coûts d'un grand cabinet de conseil."
- **Claude "dreaming" : roadmap Happi Secretary V2 à mettre à jour** — Les agents Claude écrivent des notes entre sessions pour consolider leurs apprentissages. Pour Happi Secretary, cela permet la reconnaissance avancée des appelants récurrents (VIP, clients difficiles, préférences horaires). À inscrire en priorité P1 dans la roadmap V2, après l'upgrade Opus 4.8.
- **73% des agents IA européens non-conformes RGPD — audit P0 avant le 2 août 2026 (J-63)** — DPIA obligatoire dès lors que le chatbot traite des données personnelles à grande échelle. Checklist urgente : (1) base légale explicite, (2) consentement granulaire par fonction IA, (3) bandeau "Vous parlez à une IA" dès le 1er message, (4) retention policy documentée. Cible : SAV-BOT, INnatural Stores et Happi Secretary avant la deadline AI Act.
- **APIs IA exposées : hardener la sécurité des déploiements H'appi** — 90+ instances d'APIs IA vulnérables identifiées dans des secteurs critiques. Action préventive : audit des endpoints FastAPI exposés (auth JWT, rate limiting, logs d'accès) sur tous les projets en production Railway. Utiliser les sandboxes auto-hébergés Claude pour isoler les agents à accès sensibles.

---

## 📰 Veille Tech — 2026-06-01
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.8 : 4× moins de failles de code non signalées, fiabilité et sécurité accrues](https://fortune.com/2026/05/29/anthropic-raises-65-billion-at-record-965-billion-valuation-promises-mythos-ai-model-in-wide-release-in-coming-weeks-releases-claude-opus-4-8/) | Fortune | #Claude #LLM |
| [Anthropic facture les agents Claude séparément dès le 15 juin — crédits dédiés Agent SDK](https://www.infoworld.com/article/4171274/anthropic-puts-claude-agents-on-a-meter-across-its-subscriptions.html) | InfoWorld | #Claude #SaaS |
| [Claude for Small Business — connecteurs et workflows prêts à l'emploi pour PME](https://www.anthropic.com/news/claude-for-small-business) | Anthropic | #Claude #SaaS |
| [awesome-ai-agents-2026 — 300+ frameworks, outils et ressources agents IA référencés](https://github.com/ARUNAGIRINATHAN-K/awesome-ai-agents-2026) | GitHub | #LLM #agents |
| [Gartner : 40% des apps enterprise embarqueront des agents IA d'ici fin 2026](https://eitt.academy/knowledge-base/ai-agents-2026-guide-from-llm-to-multi-agent-systems/) | EITT Academy | #LLM #SaaS |
| [jamwithai/production-agentic-rag-course (+33★) — pipeline RAG agentique prêt pour la production](https://github.com/jamwithai/production-agentic-rag-course) | GitHub Trending 🐍 | #LLM #RAG |
| [supermemoryai/supermemory (23 527★) — Memory API ultra-rapide et scalable pour l'ère des agents IA](https://github.com/supermemoryai/supermemory) | GitHub Trending TS | #LLM #agents |
| [firecrawl/open-lovable (26 636★) — clone n'importe quel site en app React moderne en quelques secondes](https://github.com/firecrawl/open-lovable) | GitHub Trending TS | #React #SaaS |
| [mattpocock/sandcastle (5 578★) — orchestration d'agents codeurs sandboxés en TypeScript](https://github.com/mattpocock/sandcastle) | GitHub Trending TS | #agents #LLM |
| [microsoft/markitdown (135 924★, +2 798/j) — convertit PDF/Word/Excel/images en Markdown LLM-ready](https://github.com/microsoft/markitdown) | GitHub Trending 🐍 | #LLM #RAG |
| [FastAPI + Next.js 15 : le full-stack IA que personne ne documente mais que tout le monde utilise](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV.to | #FastAPI #Next.js |
| [Best Voice AI Platforms 2026 : Vapi vs Deepgram vs Retell AI vs ElevenLabs — comparatif complet](https://callnovo.ai/blog/best-voice-ai-platforms-2026/) | Callnovo | #VoiceAI |
| [ElevenLabs déploiement on-premise enterprise (avril 2026) — hébergement EU souverain possible](https://www.retellai.com/blog/vapi-vs-elevenlabs) | Retell AI | #VoiceAI #RGPD |

### 💡 Insights clés
- **ALERTE FACTURATION : agents Claude sur crédits dédiés dès le 15 juin** — Anthropic sépare les usages programmatiques (Agent SDK, GitHub Actions, Happi Brain Agent) du chat standard, facturés à la consommation API. Impact direct sur les projets H'appi à forte utilisation agentique. Action immédiate : auditer la consommation tokens dans Happi Foundry et estimer le budget mensuel par projet avant le 15 juin.
- **supermemory + markitdown : la stack RAG H'appi s'améliore sans dev custom** — `supermemory` fournit une Memory API persistante pour que les agents se souviennent entre sessions (parfait pour Happi Secretary V2 : reconnaître les appelants récurrents, mémoriser leurs préférences). `markitdown` simplifie l'ingestion de bases de connaissance clients (PDF, Word, Excel) sans pipeline ETL custom. Ces deux outils réduisent de 60%+ le temps de setup d'un nouveau chatbot RAG.
- **firecrawl/open-lovable : feature "import de site" à évaluer pour Happi Web Creator** — 26 636★ en TypeScript. Cloner n'importe quel site en React app moderne en quelques secondes. À benchmarker comme fonctionnalité premium pour happi-webcreator : "Importez votre site existant et éditez-le visuellement." Différenciateur fort vs Webflow/Framer.
- **ElevenLabs on-premise : débloquer les clients Finance/Santé/Notariat** — La TTS ElevenLabs peut désormais être déployée on-premise pour les clients enterprise (déployable en EU). Argument commercial décisif pour les cabinets Monassier/Arc et les clients agroalimentaires (Labeyrie, Saint-Jean) qui exigent que les données audio restent dans leur datacenter. À proposer dans l'offre Happi Secretary Enterprise comme option "Voice RGPD-souverain".
- **Gartner 40% + 300 frameworks : la fenêtre de marché H'appi est maintenant** — 40% des apps enterprise embarqueront des agents IA d'ici fin 2026. Le catalogue de 300+ frameworks confirme que le marché cherche encore sa solution de référence. H'appi doit se positionner comme la solution "agents IA clé en main RGPD-compliant" pendant que les grands acteurs sont encore en mode expérimentation.

---

## 📰 Veille Tech — 2026-06-02
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [PatterAI/Patter — SDK Voice AI open-source, alternative Vapi/Retell, Twilio+Telnyx+Plivo (414★, MIT)](https://github.com/PatterAI/Patter) | GitHub 🐍 | #VoiceAI |
| [aden-hive/hive — Multi-Agent Harness for Production AI : Claude natif, self-improving, human-in-the-loop (10 477★)](https://github.com/aden-hive/hive) | GitHub 🐍 | #LLM #agents #Claude |
| [lemony-ai/cascadeflow — Optimisation coût/latence/qualité dans les agent loops : Claude+GPT+vLLM (2 432★)](https://github.com/lemony-ai/cascadeflow) | GitHub 🐍 | #LLM #agents |
| [PrefectHQ/fastmcp — The fast, Pythonic way to build MCP servers and clients (25 432★)](https://github.com/PrefectHQ/fastmcp) | GitHub 🐍 | #Claude #MCP |
| [mcp-use/mcp-use — Fullstack MCP framework pour Claude & ChatGPT — apps + servers (10 022★)](https://github.com/mcp-use/mcp-use) | GitHub TS | #Claude #MCP |
| [sipyourdrink-ltd/bernstein — Orchestration multi-agent audit-grade : HMAC chain, signed cards, air-gap (542★)](https://github.com/sipyourdrink-ltd/bernstein) | GitHub 🐍 | #RGPD #agents |
| [vstorm-co/pydantic-deepagents — Agents Claude Code-style en Python : docker-sandbox, subagents, MCP (831★)](https://github.com/vstorm-co/pydantic-deepagents) | GitHub 🐍 | #Claude #agents |
| [mobile-next/mobile-mcp — MCP Server pour automation mobile iOS/Android réels + émulateurs (5 087★)](https://github.com/mobile-next/mobile-mcp) | GitHub TS | #ReactNative |
| [griptape-ai/griptape — Framework Python modulaire pour AI agents avec tools, memory, RAG (2 534★)](https://github.com/griptape-ai/griptape) | GitHub 🐍 | #LLM #FastAPI |
| [i-am-bee/beeai-framework — Production-ready AI agents Python & TypeScript (3 278★)](https://github.com/i-am-bee/beeai-framework) | GitHub 🐍 | #LLM #SaaS |
| [Windy3f3f3f3f/claude-code-from-scratch — Recréer Claude Code en ~4 000 lignes, 11 chapitres (1 323★)](https://github.com/Windy3f3f3f3f/claude-code-from-scratch) | GitHub 🐍 | #Claude |
| [can1357/oh-my-pi — AI coding agent terminal : LSP, browser, subagents, Claude natif (9 648★)](https://github.com/can1357/oh-my-pi) | GitHub TS | #Claude #agents |
| [OpenOSINT/OpenOSINT — Agent OSINT IA : 9 outils, CLI, MCP server, Claude + GPT-4 (423★)](https://github.com/OpenOSINT/OpenOSINT) | GitHub 🐍 | #LLM #agents |

### 💡 Insights clés
- **PatterAI/Patter (MIT, 414★) — alternative open-source à Vapi à surveiller pour Happi Secretary** : SDK Python+TypeScript permettant de donner un numéro de téléphone à un agent IA en 4 lignes via Twilio, Telnyx ou Plivo. Déploiement on-premise possible → avantage RGPD fort (audio reste dans l'infra client). À évaluer comme fallback si les coûts Vapi augmentent avec la montée en volume d'appels. MCP natif + latence < 500ms annoncée — même cible que Vapi.
- **fastmcp (25 432★) + mcp-use (10 022★) : l'écosystème MCP s'impose comme bus d'intégration IA de référence** — fastmcp simplifie la création de MCP servers en Python (exactement le serveur prévu pour Happi Brain V2). mcp-use unifie la couche client Claude/ChatGPT avec UI, gateway et inspector intégrés. Action concrète : démarrer le MCP server Happi Brain V2 avec fastmcp — exposer `search_project`, `get_pattern`, `get_client_info` nativement depuis Claude Code.
- **sipyourdrink-ltd/bernstein (542★) — orchestration multi-agent avec audit trail inviolable** : chaque action de chaque agent est signée HMAC et chainée — journal d'audit légalement vérifiable. Signal crucial pour les clients H'appi en Finance/Notariat/Juridique (Monassier, Cabinet Arc) soumis à des obligations de traçabilité légale. Argument commercial fort : "chatbots auditables clé en main" face aux concurrents génériques.
- **lemony-ai/cascadeflow (2 432★) — réduire les coûts Claude de 30 à 70% sans changer le code métier** : le framework route automatiquement vers le modèle le moins cher capable de traiter chaque requête (Haiku → Sonnet → Opus selon complexité). Intégrer dès maintenant sur SAV-BOT : questions simples → Haiku ($0.8/M tokens), analyses complexes → Sonnet 4.6. Impact estimé : -40% sur la facture Anthropic mensuelle à volume constant.
- **mobile-next/mobile-mcp (5 087★) — contrôle MCP d'apps mobiles iOS/Android** : un agent Claude peut piloter une app React Native comme un utilisateur humain (tap, scroll, screenshot, assertions). Pour H'appi : (1) automatiser les tests de la Quality Tracking App Mobilier de France, (2) ouvrir la voie à des agents mobiles autonomes pour les livreurs (créer un ticket défaut depuis l'app sans intervention humaine).
- **Les frameworks agents convergent vers les mêmes primitives** : aden-hive/hive, griptape, beeai-framework et pydantic-deepagents alignent tous sur tools + memory + subagents + human-in-the-loop. H'appi doit standardiser sa dépendance agent avant de multiplier les projets. **Recommandation** : griptape (Python, FastAPI-compatible, 2 534★ stables) comme base + pydantic-deepagents pour les agents Claude Code-style sur les projets engineering internes.

---

## 📰 Veille Tech — 2026-06-03
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.8 : Dynamic Workflows, Effort Control, Fast Mode 3× moins cher](https://techcrunch.com/2026/05/28/anthropic-releases-opus-4-8-with-new-dynamic-workflow-tool/) | TechCrunch | #Claude #LLM |
| [Claude Opus 4.8 — seul modèle à finir tous les cas Super-Agent, SWE-Bench 69.2%, honnêteté renforcée](https://thenewstack.io/claude-opus-48-release/) | The New Stack | #Claude #LLM |
| [Claude Platform on AWS : Messages API + Files API + IAM auth sur infra Anthropic managée](https://platform.claude.com/docs/en/release-notes/overview) | Anthropic | #Claude #Deploy |
| [chopratejas/headroom (+1 265★/j) — Compression tokens LLM 60-95%, lib + proxy + MCP server](https://github.com/chopratejas/headroom) | GitHub 🐍 | #LLM |
| [microsoft/markitdown (+3 618★/j, 141K★) — Convertit PDF/Word/Excel/images en Markdown LLM-ready](https://github.com/microsoft/markitdown) | GitHub 🐍 | #LLM #RAG |
| [supermemoryai/supermemory (+680★/j, 24K★) — Memory API ultra-rapide et scalable pour l'ère des agents IA](https://github.com/supermemoryai/supermemory) | GitHub TS | #LLM #agents |
| [nanocoai/nanoclaw (29K★) — Agent léger multi-plateforme : WhatsApp, Telegram, Slack, Discord, Gmail + mémoire](https://github.com/nanocoai/nanoclaw) | GitHub TS | #chatbot #LLM |
| [ElevenLabs v3 GA : tags audio expressifs [excited][whispers], <100ms, 11 000+ voix, 70+ langues](https://elevenlabs.io/) | ElevenLabs | #VoiceAI |
| [Vapi 2026 : 62M appels/mois, SLA 99.99%, 14+ providers — orchestration IA téléphonie de référence](https://www.goodcall.com/voice-ai/vapi-vs-elevenlabs) | GoodCall | #VoiceAI |
| [AI Act pleinement applicable le 2 août 2026 : amendes 35M€ ou 7% CA, labelling chatbot obligatoire](https://www.leto.legal/guides/ai-act-conformite) | Leto Legal | #RGPD #AIAct |
| [CNIL publie ses recommandations RGPD pour le développement des systèmes IA (mars 2026)](https://www.cnil.fr/fr/developpement-des-systemes-dia-les-recommandations-de-la-cnil-pour-respecter-le-rgpd) | CNIL | #RGPD |
| [ROI chatbot IA 2026 : $3.50 par $1 investi en moyenne, jusqu'à 8×, 80% résolution autonome (Zendesk)](https://aetherlink.ai/en/blog/ai-chatbot-roi-2026-enterprise-trends-compliance-guide-eindhoven) | AetherLink | #SaaS #chatbot |
| [Claude : +306% de visites en 1 trimestre (203M→824M) — croissance la plus rapide parmi les LLM](https://momenticmarketing.com/blog/top-ai-chatbots) | Momentic | #Claude #SaaS |
| [Deploy AI-Powered SaaS App on Railway — guide officiel FastAPI + PostgreSQL + Docker](https://docs.railway.com/guides/deploy-ai-saas) | Railway Docs | #Railway #Docker |
| [FastAPI + Next.js 15 : le full-stack que personne ne documente mais que tout le monde utilise en 2026](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV.to | #FastAPI #Next.js |

### 💡 Insights clés
- **URGENCE CONFORMITÉ — AI Act applicable le 2 août 2026 (J-60)** : Labelling obligatoire dès qu'un chatbot ressemble à un humain, amendes jusqu'à €35M ou 7% du CA global. Action immédiate H'appi : (1) ajouter une déclaration "Cet assistant est un agent IA" dans l'UI de tous les chatbots clients, (2) créer un template DPA RGPD+AI Act standard pour les nouveaux contrats, (3) vérifier hébergements FR/EU (Scaleway, Hetzner, Railway EU). Secteurs prioritaires : Cabinet Arc, Groupe Monassier, Audit Expert.
- **Claude Opus 4.8 + Dynamic Workflows = upgrade stratégique pour Happi Secretary** : Dynamic Workflows permettent à Claude de gérer des tâches longues en autonomie — idéal pour les analyses post-appel complexes (résumé multi-appels, détection tendances, rapport hebdo client). Fast Mode 3× moins cher à 2.5× la vitesse : migrer les analyses simples sur Fast Mode = ~-50% sur la facture Anthropic. Modèle à jour section 8 : `claude-opus-4-8` pour tâches complexes.
- **headroom (60-95% compression tokens) = économies directes sur SAV-BOT et tous les chatbots H'appi** : Le middleware compresse le contexte envoyé à Claude sans dégrader la qualité des réponses. Sur SAV-BOT avec ses longs historiques + base de connaissance produits, cela peut diviser la facture API par 3 à 5×. À intégrer comme couche dans `claudeService.py` sur tous les nouveaux projets.
- **supermemory (Memory API) : la pièce manquante pour Happi Secretary V2** : API persistante permettant aux agents de se souvenir entre sessions — reconnaître un appelant récurrent, mémoriser ses préférences, rappeler ses tickets passés. Compatible FastAPI, remplace un pgvector custom pour la mémoire épisodique. Priorité d'évaluation pour Brain V2.
- **ROI 3.5× à 8× et 80% résolution autonome : argument commercial H'appi à quantifier par secteur** : Les benchmarks Zendesk 2026 donnent des chiffres béton pour convertir les prospects. Action : construire un calculateur ROI par secteur (€ économisés sur support/an vs coût mensuel chatbot) à intégrer dans les propositions commerciales. Exemple : 5 agents call center à 2 500€/mois → chatbot H'appi 500€/mois + 80% d'appels gérés = ROI positif dès le mois 1.

---

## 📰 Veille Tech — 2026-06-04
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Managed Agents : sandbox configurable + MCP privés, agent loop chez Anthropic](https://www.anthropic.com/news) | Anthropic | #Claude #agents |
| [MCP Roadmap 2026 : 97M downloads SDK/mois, 10 000+ serveurs publics, spec RC stateless](https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/) | MCP Blog | #MCP #LLM |
| [MCP : problèmes de production (scaling, sessions, SSO enterprise) enfin résolus](https://thenewstack.io/model-context-protocol-roadmap-2026/) | The New Stack | #MCP #SaaS |
| [Retell AI 2026 : 30M appels/mois, pricing $0.07–0.31/min, G2 Best Agentic AI Software](https://www.retellai.com/blog/ai-voice-agent-pricing-full-cost-breakdown-platform-comparison-roi-analysis) | Retell AI | #VoiceAI |
| [Meilleurs LLMs pour agents vocaux 2026 : Claude Sonnet 4.6 vs GPT-5.4 vs Gemini](https://softcery.com/lab/ai-voice-agents-choosing-the-right-llm) | Softcery | #VoiceAI #Claude |
| [Vercel vs Railway pour SaaS 2026 : Next.js edge vs full-stack PostgreSQL + Docker](https://designrevision.com/blog/vercel-vs-railway) | DesignRevision | #Railway #Vercel |
| [React Native + IA : éviter les pièges backend quand on ajoute des features IA (Expo)](https://blog.codeminer42.com/thinking-about-adding-ai-to-your-expo-react-native-app-read-this-first/) | CodeMiner42 | #ReactNative |
| [NousResearch/hermes-agent — "The agent that grows with you" — trending GitHub Python](https://github.com/NousResearch/hermes-agent) | GitHub 🐍 | #LLM #agents |
| [Open-LLM-VTuber — LLM interactif vocal avec avatar Live2D, multi-plateforme](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber) | GitHub 🐍 | #VoiceAI #LLM |
| [lfnovo/open-notebook — Open Source NotebookLM avec RAG et flexibilité étendue](https://github.com/lfnovo/open-notebook) | GitHub TS | #LLM #RAG |
| [EU AI Act Article 50 : guide pratique des règles de transparence pour les chatbots](https://artificialintelligenceact.eu/transparency-rules-article-50/) | AI Act EU | #RGPD #AIAct |
| [FastAPI dépasse Django et Flask : 40% d'adoption chez les devs Python en 2026](https://quartzdevs.com/resources/best-backend-frameworks-2026-top-server-side-tools) | QuartzDevs | #FastAPI |
| [Build AI SaaS avec Next.js + FastAPI + Dokploy : retour d'expérience complet](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #SaaS |
| [Claude Security : scans automatiques de codebase + suggestions de patches pour Enterprise](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #SaaS |
| [koala73/worldmonitor — Dashboard intelligence globale en temps réel, agrégation IA](https://github.com/koala73/worldmonitor) | GitHub TS | #SaaS #LLM |

### 💡 Insights clés
- **MCP devient le standard incontournable pour les chatbots en production** : 97M de téléchargements SDK/mois et 10 000+ serveurs publics montrent que MCP est passé du prototype à la production. La spec RC (juillet 2026) règle les problèmes de scaling horizontal et SSO enterprise. H'appi doit prioriser l'architecture Brain V2 avec un serveur MCP natif : chaque client pourra connecter son CRM, calendrier et base de connaissance directement à son chatbot.
- **Claude Sonnet 4.6 = meilleur LLM pour agents vocaux en 2026 selon Softcery** : Benchmark confirme que Claude Sonnet 4.6 domine sur la latence, le français naturel et la compréhension contexte long. Happi Secretary utilise déjà ce modèle — le figer comme défaut obligatoire pour tous les nouveaux projets vocaux clients et le documenter dans la section 8.
- **Retell AI pricing granulaire : modèle de coût à intégrer dans les devis H'appi** : Coût réel d'un agent vocal = $0.07–0.31/min, soit ~€4–18/heure de conversation. Pour un client avec 100 appels/jour × 3 min → coût infra €350–1 600/mois. Le pricing Maintenance Pro (100–500€/mois) doit refléter cette réalité — prévoir un palier "Maintenance Voice" avec volumétrie d'appels incluse.
- **FastAPI #1 framework Python (40% part de marché) : avantage H'appi validé par l'industrie** : Le choix FastAPI est désormais l'évidence parmi les DSI et freelances Python, ce qui simplifie les recrutements, les audits techniques clients et les appels d'offres. À mettre en avant dans les propositions commerciales B2B.
- **React Native + IA : audit sécurité à déclencher sur Quality Tracking App** : L'article CodeMiner42 pointe les pièges classiques (clés API exposées, pas de rate-limiting, absence de cache). Avant la livraison finale à Mobilier de France, auditer la gestion des appels IA dans l'app mobile (AsyncStorage, JWT refresh, environnements secrets).

---

## 📰 Veille Tech — 2026-06-05
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.8 : Dynamic Workflows — orchestration de centaines d'agents en arrière-plan](https://www.anthropic.com/news) | Anthropic | #Claude #agents |
| [Anthropic IPO : valorisation $965Mds, candidature bourse — crédibilité Claude renforcée](https://www.washingtonpost.com/technology/2026/06/01/anthropic-maker-claude-files-with-sec-go-public-an-ipo/) | Washington Post | #Claude #Anthropic |
| [Claude Managed Agents sur AWS : webhooks multiagents + sandboxes self-hosted disponibles](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #SaaS |
| [Vapi lève $50M Serie B — 1 milliard d'appels traités, $500M valorisation, Amazon Ring client](https://enterprisedna.co/resources/news/vapi-50m-series-b-voice-ai-enterprise-2026/) | Enterprise DNA | #VoiceAI |
| [Vapi vs ElevenLabs 2026 : benchmark complet pricing, latence et qualité voix](https://www.goodcall.com/voice-ai/vapi-vs-elevenlabs) | GoodCall | #VoiceAI |
| [ElevenLabs $500M ARR — IBM intègre ElevenLabs dans watsonx pour l'enterprise](https://www.startuphub.ai/ai-news/artificial-intelligence/2026/elevenlabs-gives-chat-agents-a-voice) | StartupHub.ai | #VoiceAI |
| [Best AI Agent Frameworks 2026 : LangGraph, Claude Agent SDK, LlamaIndex — comparatif production](https://alicelabs.ai/en/insights/best-ai-agent-frameworks-2026) | AliceLabs | #LLM #agents |
| [supermemoryai/supermemory — Memory API ultra-scalable pour agents IA (+469 étoiles auj.)](https://github.com/supermemoryai/supermemory) | GitHub TS | #LLM #chatbot |
| [langgenius/dify — Plateforme agentic workflow prête pour la production (+160 étoiles auj.)](https://github.com/langgenius/dify) | GitHub TS | #chatbot #SaaS |
| [chopratejas/headroom — Compression tokens LLM 60-95% : même précision, coût réduit](https://github.com/chopratejas/headroom) | GitHub Python | #LLM |
| [NousResearch/hermes-agent — "The agent that grows with you" (+1913 étoiles auj.)](https://github.com/NousResearch/hermes-agent) | GitHub Python | #LLM #agents |
| [AI Act 2026 : guide obligations conformité entreprise — double verrou RGPD + AI Act](https://www.rgpdkit.fr/blog/ai-act-2026-guide-obligations-entreprise) | RGPDKit | #RGPD #AIAct |
| [Chatbot RGPD & CNIL 2026 : mention IA obligatoire, hallucinations = violation article 5](https://www.webotit.ai/blog/ia-conversationnelle/generalites/chatbot-et-rgpd-respectez-les-droits-des-personnes-avec-les-conseils-de-la-cnil) | Webotit | #RGPD |
| [Build AI SaaS avec Next.js + FastAPI + Dokploy : guide déploiement VPS complet](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #SaaS |
| [Streaming ChatGPT-style en production : FastAPI SSE + Next.js useChat — architecture 4 couches](https://ranjankumar.in/building-chatgpt-style-streaming-in-react-fastapi-next-js-production-guide) | RanjanKumar | #FastAPI |

### 💡 Insights clés
- **Anthropic IPO à $965Mds : argument commercial béton pour H'appi** — L'entrée en bourse d'Anthropic transforme Claude en choix technologique "safe" pour les DSI français. Les clients B2B cherchant un chatbot peuvent désormais s'appuyer sur un fournisseur de niveau NYSE. À intégrer dans les propositions commerciales comme signal de pérennité et de solidité financière.
- **Claude Opus 4.8 + Dynamic Workflows = chatbots multi-agents sans surcoût infra** — L'orchestration de "dizaines à centaines d'agents en arrière-plan" est désormais native dans l'API Claude. Pour H'appi, c'est la brique manquante pour des chatbots SAV totalement autonomes : un agent principal route vers des sous-agents spécialisés (tickets P0, réservations Cal.com, escalations humaines) sans architecture custom. À évaluer pour Happi Secretary V2.
- **Vapi Series B $50M + Amazon Ring : le choix Happi Secretary est le bon** — Vapi est devenu le standard de l'industrie Voice AI (1 milliard d'appels, choisi par Amazon Ring face à 40 concurrents). La prochaine proposition commerciale Happi Secretary doit mettre en avant ce partenariat : "Nous utilisons la plateforme Voice AI choisie par Amazon, adoptée par 80 000 développeurs dans le monde".
- **supermemoryai/supermemory trending (+469 étoiles) : mémoire persistante sans pgvector custom** — Cette Memory API ultra-scalable est directement applicable à Happi Secretary V2 pour mémoriser les appelants récurrents entre sessions (préférences, tickets passés, historique). Remplace un développement pgvector/Redis complexe par un simple endpoint API. Évaluation prioritaire confirmée pour Brain V2.
- **AI Act 2026 + RGPD : mise en conformité urgente des chatbots déployés** — Tout chatbot client H'appi doit afficher explicitement "Réponse générée par une IA" (AI Act Article 50) et contrôler les hallucinations sous peine de violer l'article 5 du RGPD. Action immédiate : ajouter un bandeau de transparence IA dans le widget embeddable template et auditer les déploiements existants (INnatural, SAV-BOT, Secretary).

---

## 📰 Veille Tech — 2026-06-06
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [chopratejas/headroom — Compression tokens LLM 60-95% : lib Python + proxy + MCP server (+2 473★/jour, 14.8k★)](https://github.com/chopratejas/headroom) | GitHub Trending 🐍 | #LLM |
| [NousResearch/hermes-agent — "The agent that grows with you" : framework agent auto-évolutif (+1 845★/jour, 183.7k★)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [Open-LLM-VTuber/Open-LLM-VTuber — Interaction vocale LLM avec avatar Live2D, voice interruption, self-hosted, multi-plateforme (+520★/jour, 10.1k★)](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber) | GitHub Trending 🐍 | #VoiceAI #LLM |
| [microsoft/agent-framework — Framework Microsoft pour construire et orchestrer des agents IA et workflows multi-agents (11.1k★)](https://github.com/microsoft/agent-framework) | GitHub Trending 🐍 | #LLM #agents |
| [agentscope-ai/agentscope — "Build and run agents you can see, understand and trust" : observabilité, debuggabilité (+118★/jour, 26.3k★)](https://github.com/agentscope-ai/agentscope) | GitHub Trending 🐍 | #LLM #agents |
| [unslothai/unsloth — Web UI pour entraîner et déployer des LLMs open-source localement : Gemma 4, Qwen3.6 (+102★/jour, 65.9k★)](https://github.com/unslothai/unsloth) | GitHub Trending 🐍 | #LLM |
| [Panniantong/Agent-Reach — Toolkit IA pour scraper Twitter, Reddit, YouTube, GitHub sans frais API (+148★/jour, 21.8k★)](https://github.com/Panniantong/Agent-Reach) | GitHub Trending 🐍 | #LLM #agents |
| [CopilotKit/CopilotKit — "The Frontend Stack for Agents & Generative UI" React + Angular (32.8k★)](https://github.com/CopilotKit/CopilotKit) | GitHub Trending TS | #NextJS #chatbot #LLM |
| [lfnovo/open-notebook — Open Source NotebookLM : RAG étendu, flexibilité accrue, entièrement auto-hébergeable (26.2k★)](https://github.com/lfnovo/open-notebook) | GitHub Trending TS | #LLM #RAG #chatbot |
| [DayuanJiang/next-ai-draw-io — Next.js + IA générative pour créer des diagrammes en langage naturel (31.4k★)](https://github.com/DayuanJiang/next-ai-draw-io) | GitHub Trending TS | #NextJS #LLM |
| [makeplane/plane — Alternative open-source à Jira/Linear/Monday : SaaS project management natif pour équipes IA (50.4k★)](https://github.com/makeplane/plane) | GitHub Trending TS | #SaaS |
| [koala73/worldmonitor — Dashboard intelligence globale temps réel : agrégation IA de news géopolitiques (55.9k★)](https://github.com/koala73/worldmonitor) | GitHub Trending TS | #SaaS #LLM |

### 💡 Insights clés
- **headroom (+2 473★/jour) — compression tokens urgente à déployer sur les chatbots H'appi** : réduction 60-95% des tokens sans perte de qualité via lib Python + proxy MCP. Sur SAV-BOT avec ses longs contextes produits et historiques clients, cela peut diviser la facture Anthropic par 3 à 5×. Action immédiate : intégrer comme middleware dans `claudeService.py` et dans tout nouveau projet — ROI dès le premier mois.
- **CopilotKit (32.8k★) — standard UI agentique React confirmé en trending** : framework frontend Next.js pour intégrer agents et Generative UI dynamiques directement dans les interfaces React. Compatible App Router et streaming natif Anthropic. À intégrer dans les prochains projets H'appi Next.js (Happi Foundry, widgets SAV) pour réduire de 40% le temps de dev des interfaces agents.
- **microsoft/agent-framework + agentscope — convergence vers l'orchestration multi-agents standardisée** : Microsoft et l'écosystème open-source publient des frameworks d'orchestration multi-agents production-ready en parallèle. Signal fort : les prochains projets SAV/secrétariat H'appi devront intégrer une couche multi-agents (agent routage → agent spécialisé → agent escalade) pour rester compétitifs face aux offres enterprise. Évaluer microsoft/agent-framework sur la compatibilité avec notre stack FastAPI + Claude.
- **Open-LLM-VTuber — voice AI avec interruption vocale (barge-in), prochain différenciateur Happi Secretary** : l'interaction vocale avec interruption naturelle (sans attendre la fin de la phrase) est ce qui sépare un assistant vocal professionnel d'un IVR. Ce pattern open-source valide la demande marché pour cette feature — à inscrire sur la roadmap Happi Secretary V2 : implémenter le barge-in natif via Vapi.ai event hooks pour les projets premium.
- **AI Act J-57 : deadline critique le 2 août 2026** — dans 57 jours, obligation légale que tout chatbot se déclare IA dès le premier message (amendes jusqu'à 35M€ ou 7% CA mondial). Action P0 H'appi : audit de tous les chatbots clients déployés (SAV-BOT, INnatural, Secretary), ajout du bandeau standard "Cet assistant est un agent IA" dans le widget embeddable, documentation DPIA par projet. Transformer cette contrainte en argument commercial différenciant — aucun concurrent générique ne garantit cette conformité à la livraison.

---

## 📰 Veille Tech — 2026-06-07
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [CopilotKit — "The Frontend Stack for Agents & Generative UI" React + Next.js (+631★/jour, 33k★)](https://github.com/CopilotKit/CopilotKit) | GitHub Trending TS | #NextJS #chatbot #LLM |
| [lfnovo/open-notebook — Open Source NotebookLM : RAG étendu, flexibilité accrue, auto-hébergeable (+794★/jour, 26k★)](https://github.com/lfnovo/open-notebook) | GitHub Trending TS | #LLM #RAG #chatbot |
| [MemPalace/mempalace — "The best-benchmarked open-source AI memory system" (54k★, +446★/jour)](https://github.com/MemPalace/mempalace) | GitHub Trending 🐍 | #LLM #chatbot |
| [microsoft/VibeVoice — Open-Source Frontier Voice AI : ASR, TTS, Realtime (48k★, +216★/jour)](https://github.com/microsoft/VibeVoice) | GitHub Trending 🐍 | #VoiceAI |
| [khoj-ai/khoj — AI second brain self-hostable : web + docs + agents custom (34k★)](https://github.com/khoj-ai/khoj) | GitHub Trending 🐍 | #LLM #chatbot |
| [Shubhamsaboo/awesome-llm-apps — 100+ apps Agent & RAG clonables et personnalisables (113k★)](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot #RAG |
| [IBM/mcp-context-forge — AI Gateway MCP : discovery centralisé, guardrails, proxy multi-providers (3.8k★)](https://github.com/IBM/mcp-context-forge) | GitHub Trending 🐍 | #MCP #SaaS #LLM |
| [anthropics/claude-code-action — Claude Code dans GitHub Actions : CI/CD agentique officiel Anthropic (7.9k★)](https://github.com/anthropics/claude-code-action) | GitHub Trending TS | #Claude #Anthropic |
| [supabase/supabase — Postgres development platform pour apps web, mobile et IA (103k★)](https://github.com/supabase/supabase) | GitHub Trending TS | #PostgreSQL #SaaS |
| [heygen-com/hyperframes — Write HTML, Render Video : pipeline vidéo pour agents IA (25k★)](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #VoiceAI #chatbot |
| [cloudflare/vinext — Plugin Vite : déployer Next.js n'importe où, sans dépendance Vercel (8k★)](https://github.com/cloudflare/vinext) | GitHub Trending TS | #NextJS #Vercel |
| [agentscope-ai/agentscope — "Build and run agents you can see, understand and trust" (26k★)](https://github.com/agentscope-ai/agentscope) | GitHub Trending 🐍 | #LLM #agents |
| [PaddlePaddle/PaddleOCR — PDF/images → données structurées pour l'IA, 100+ langues (81k★)](https://github.com/PaddlePaddle/PaddleOCR) | GitHub Trending 🐍 | #LLM #RAG |

### 💡 Insights clés
- **AI Act J-56 — deadline du 2 août 2026 (56 jours)** : obligation légale que tout chatbot se déclare IA dès le 1er message (amendes jusqu'à 35M€ ou 7% CA mondial). Avec 73% des agents IA européens encore non conformes (Technova), H'appi a une fenêtre commerciale unique pour se positionner comme "premier prestataire chatbot RGPD + AI Act clé-en-main en France". Action P0 avant le 1er juillet : auditer SAV-BOT, INnatural Stores et Happi Secretary, ajouter le bandeau légal standard et documenter la DPIA de chaque projet.
- **CopilotKit (33k★, +631★/jour) — standard UI agentique Next.js confirmé pour la 3e fois cette semaine** : l'écosystème React/Next.js converge vers CopilotKit pour les interfaces agents et Generative UI. Pour H'appi : intégrer dès maintenant dans les widgets chatbot Next.js (Happi Foundry, Happi Secretary dashboard) — réduit de 40% le temps de dev des interfaces agents avec un niveau de polish comparable aux grandes plateformes IA.
- **open-notebook (+794★/jour, 4e apparition en trending) — signal RAG massif** : le marché veut du NotebookLM open-source auto-hébergeable. Pour H'appi : positionner notre stack pgvector + FastAPI comme "NotebookLM souverain hébergé en France" dans les pitchs clients sensibles RGPD — argument commercial différenciant fort face aux solutions cloud US (Notion AI, Google NotebookLM).
- **IBM/mcp-context-forge — MCP enterprise entre dans une nouvelle phase** : IBM publie un AI Gateway MCP avec discovery centralisé, guardrails et proxy multi-providers. Signal que MCP est passé du prototype startup à l'adoption Fortune 500. Pour H'appi : démarrer le serveur MCP Happi Brain V2 avec fastmcp (25k★) pour exposer `search_project`, `get_pattern`, `get_client_info` nativement depuis Claude Code — architecture identique à ce que construit IBM.
- **MemPalace (54k★) + VibeVoice (48k★) : mémoire IA et Voice AI open-source deviennent des commodités** : trois solutions mémoire production-ready (MemPalace, MemoriLabs, supermemory) et trois frameworks Voice AI open-source (VibeVoice, dograh, voicebox) coexistent. Pour H'appi : standardiser supermemory comme couche mémoire unique (API REST + PostgreSQL natif) et planifier le benchmark dograh vs Vapi pour les clients RGPD-sensitifs en juillet 2026.
- **cloudflare/vinext — déploiement Next.js sans Vercel, argument RGPD** : plugin Vite permettant de déployer des apps Next.js sur Cloudflare Workers, Docker ou serveur custom. Pour H'appi : argument supplémentaire pour les clients qui refusent l'hébergement Vercel US — "votre frontend Next.js reste dans votre datacenter France grâce à vinext + Hetzner". Différenciation premium sur les prospects Notariat/Finance/Santé.

---
## 📰 Veille Tech — 2026-06-08
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [NousResearch/hermes-agent — "The agent that grows with you" (186k★)](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM #agents |
| [MemPalace/mempalace — Benchmark #1 mémoire open-source pour agents IA (54k★)](https://github.com/MemPalace/mempalace) | GitHub Trending 🐍 | #LLM #chatbot |
| [microsoft/VibeVoice — Voice AI open-source frontier : ASR, TTS, Realtime (48k★)](https://github.com/microsoft/VibeVoice) | GitHub Trending 🐍 | #VoiceAI |
| [luongnv89/claude-howto — Guide visuel Claude Code avec templates agents (35k★)](https://github.com/luongnv89/claude-howto) | GitHub Trending 🐍 | #Claude #Anthropic |
| [khoj-ai/khoj — Second cerveau IA self-hostable : web + docs + agents (34k★)](https://github.com/khoj-ai/khoj) | GitHub Trending 🐍 | #LLM #chatbot |
| [AstrBotDevs/AstrBot — Framework agent multi-plateformes IM + Docker (34k★)](https://github.com/AstrBotDevs/AstrBot) | GitHub Trending 🐍 | #LLM #chatbot #Docker |
| [zjunlp/LightMem — ICLR 2026 : mémoire légère et efficace pour agents LLM (914★)](https://github.com/zjunlp/LightMem) | GitHub Search | #LLM #RAG |
| [CopilotKit/CopilotKit — Frontend stack agents & Generative UI React/Next.js (33k★)](https://github.com/CopilotKit/CopilotKit) | GitHub Trending TS | #LLM #chatbot #NextJS |
| [cline/cline — Agent de coding autonome : SDK, extension IDE ou CLI (62k★)](https://github.com/cline/cline) | GitHub Trending TS | #LLM #agents |
| [simstudioai/sim — Orchestration agents Claude natif + Next.js + PostgreSQL (28k★)](https://github.com/simstudioai/sim) | GitHub Search | #LLM #chatbot #NextJS #Anthropic |
| [lfnovo/open-notebook — Implémentation open-source de NotebookLM (27k★)](https://github.com/lfnovo/open-notebook) | GitHub Trending TS | #LLM #RAG |
| [heygen-com/hyperframes — Write HTML, Render Video : pipeline vidéo pour agents IA (25k★)](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #VoiceAI #chatbot |
| [1Panel-dev/MaxKB — Plateforme agent enterprise : pgvector + RAG + Docker (21k★)](https://github.com/1Panel-dev/MaxKB) | GitHub Search | #LLM #chatbot #PostgreSQL #RAG |
| [baptisteArno/typebot.io — Chatbot builder puissant auto-hébergeable (9k★)](https://github.com/baptisteArno/typebot.io) | GitHub Search | #chatbot #NextJS |
| [cgoinglove/better-chatbot — Chatbot MCP + Voice AI + Vercel intégré (1k★)](https://github.com/cgoinglove/better-chatbot) | GitHub Search | #chatbot #NextJS #VoiceAI #Vercel |

### 💡 Insights clés
- **NousResearch/hermes-agent (186k★!) — l'agent "adaptatif" devient le nouveau standard** : le projet le plus étoilé de tout GitHub trending aujourd'hui incarne le concept d'agent qui apprend et grandit avec l'usage. Pour H'appi : argument commercial prime — "votre chatbot H'appi apprend votre business au fil du temps" — différenciant fort face aux chatbots statiques des concurrents B2B. À intégrer dans le pitch deck Q3 2026.
- **4 solutions mémoire agent en trending simultanément (MemPalace 54k★, LightMem ICLR 2026, memanto, honcho)** : la mémoire persistante devient une feature standard attendue dans tout chatbot professionnel. Pour H'appi : standardiser LightMem + pgvector dans Happi Foundry dès juillet — architecture légère, PostgreSQL-native, paper ICLR 2026 comme caution scientifique pour les clients exigeants.
- **simstudioai/sim (28k★, Claude natif, Next.js + PostgreSQL)** : plateforme open-source d'orchestration multi-agents avec notre stack exacte. Pour H'appi : évaluer sim comme base de Happi Foundry v2 — évite 3-4 mois de dev ground-up et donne accès à une communauté active de 3k forks. À décider en atelier technique juillet 2026.
- **MaxKB (21k★, pgvector + RAG enterprise, topics : pgvector + docker + mcp-server)** : confirme que PostgreSQL + pgvector est la stack RAG mainstream pour les chatbots enterprise. Pour H'appi : pitch "zéro vendor lock-in, hébergé sur votre PostgreSQL existant" — argument massif pour les DSI banque/assurance/santé qui refusent les bases exotiques.
- **cline/cline (62k★) devient un SDK modulaire autonome** : l'agent coding le plus étoilé de GitHub se modularise. Pour H'appi : intégrer cline-sdk dans le pipeline Happi pour automatiser la génération de widgets et d'intégrations API clients — réduction estimée 30% du temps de livraison par projet.

---

## 📰 Veille Tech — 2026-06-09
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [mvanhorn/last30days-skill — Agent skill qui recherche n'importe quel sujet sur Reddit, X, YouTube, HN, Polymarket et le web (+3 558★/jour, 35.4k★)](https://github.com/mvanhorn/last30days-skill) | GitHub Trending 🐍 | #LLM #agents |
| [RyanCodrai/turbovec — Index vectoriel ultra-rapide (TurboQuant + Rust + Python) pour RAG (+1 729★/jour, 9.4k★)](https://github.com/RyanCodrai/turbovec) | GitHub Trending 🐍 | #LLM #RAG |
| [langchain-ai/deepagents — "The batteries-included agent harness" LangChain (24.2k★)](https://github.com/langchain-ai/deepagents) | GitHub Trending 🐍 | #LLM #agents |
| [google/skills — Agent Skills officielles Google pour produits Google (12.6k★, +461★/jour)](https://github.com/google/skills) | GitHub Trending 🐍 | #LLM #agents |
| [Panniantong/Agent-Reach — Toolkit vision internet pour agents IA : Twitter, Reddit, YouTube, GitHub sans frais API (+679★/jour, 24.7k★)](https://github.com/Panniantong/Agent-Reach) | GitHub Trending 🐍 | #LLM #agents |
| [MemPalace/mempalace — Benchmark #1 mémoire open-source pour agents IA (55k★, +170★/jour)](https://github.com/MemPalace/mempalace) | GitHub Trending 🐍 | #LLM #chatbot |
| [luongnv89/claude-howto — Guide visuel Claude Code : concepts de base aux agents avancés (36k★, +312★/jour)](https://github.com/luongnv89/claude-howto) | GitHub Trending 🐍 | #Claude #Anthropic |
| [LibreChat — Alternative ChatGPT self-hosted avec MCP natif, agents, code interpreter, Docker (38.7k★)](https://github.com/danny-avila/LibreChat) | GitHub Trending TS | #LLM #chatbot #Docker |
| [CopilotKit — "The Frontend Stack for Agents & Generative UI" React + Next.js (34.3k★)](https://github.com/CopilotKit/CopilotKit) | GitHub Trending TS | #NextJS #chatbot #LLM |
| [lfnovo/open-notebook — Implémentation open-source de NotebookLM avec RAG étendu (28.1k★)](https://github.com/lfnovo/open-notebook) | GitHub Trending TS | #LLM #RAG #chatbot |
| [twentyhq/twenty — "The open alternative to Salesforce, designed for AI" (49.5k★)](https://github.com/twentyhq/twenty) | GitHub Trending TS | #SaaS #LLM |
| [danielmiessler/Personal_AI_Infrastructure — Infrastructure agentique pour amplification des capacités humaines (15.6k★)](https://github.com/danielmiessler/Personal_AI_Infrastructure) | GitHub Trending TS | #LLM #agents |
| [777genius/agent-teams-ai — Système multi-agents kanban : 200+ modèles, 75+ providers LLM (1.2k★)](https://github.com/777genius/agent-teams-ai) | GitHub Trending TS | #LLM #agents #chatbot |

### 💡 Insights clés
- **mvanhorn/last30days-skill (+3 558★/jour!) — explosion virale : l'agent de veille comme produit standard** : cet outil donne à n'importe quel agent IA la capacité de rechercher et analyser n'importe quel sujet sur Reddit, X, YouTube, HN, Polymarket et le web en temps réel. C'est exactement la mission de Happi Brain Agent. Pour H'appi : intégrer ce pattern comme base de Happi Brain V2 — passer d'un agent de fetch manuel à un vrai agent de veille autonome avec skill modulaire. Roadmap : remplacer les WebFetch hardcodés par des appels à last30days-skill + enrichissement pgvector.
- **LibreChat (38.7k★) — frontend chatbot RGPD-ready clé-en-main** : alternative ChatGPT 100% self-hostable avec MCP natif, agents autonomes, code interpreter et support Docker complet. Pour H'appi : présenter LibreChat comme base UI pour les clients qui veulent une expérience ChatGPT-like hébergée sur leur infrastructure France (Hetzner/OVH). Évite 2-3 mois de dev frontend — H'appi apporte la valeur sur le backend FastAPI + Claude + RAG métier.
- **twentyhq/twenty (49.5k★) — CRM open-source "designed for AI" arrive en trending** : alternative à Salesforce avec agents IA natifs et architecture data-first. Pour H'appi : adopter Twenty comme CRM interne pour tracker prospects, clients et projets avec agents IA embarqués — remplace les feuilles de calcul et Notion. Bonus : Twenty est PostgreSQL-native, compatible avec notre stack pgvector.
- **langchain-ai/deepagents + google/skills — standardisation des "skills" agent** : LangChain et Google publient chacun leur harness de "skills" modulaires pour agents. Signal fort que l'architecture agent devient skills-first (vs monolithique). Pour H'appi : anticiper en découpant les prochains agents en skills réutilisables : `skill_recherche_produit`, `skill_escalade_humain`, `skill_qualification_lead` — compatibles LangChain et directement vendables comme modules à d'autres intégrateurs.
- **AI Act J-55 — deadline du 2 août 2026 (55 jours)** : le compte à rebours continue. Avec LibreChat et Twenty tous deux conçus "RGPD-first" en trending simultanément, le marché envoie un signal clair : la conformité devient un critère de sélection technique, pas seulement légal. Pour H'appi : intégrer dans toute proposition commerciale un tableau "Conformité AI Act / RGPD" avec checklist verte — différenciation visible dès la slide 2 du pitch.

---

## 📰 Veille Tech — 2026-06-10
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/knowledge-work-plugins — 11 plugins Claude pour rôles métier : Sales, Support, Legal, Marketing, Finance avec MCP natif (20k★)](https://github.com/anthropics/knowledge-work-plugins) | GitHub Trending 🐍 | #Claude #Anthropic #chatbot |
| [NVIDIA/SkillSpector — Scanner sécurité pour skills d'agents IA : 64 patterns, 16 catégories, 26.1% des skills vulnérables (1.9k★)](https://github.com/NVIDIA/SkillSpector) | GitHub Trending 🐍 | #LLM #agents #sécurité |
| [Andyyyy64/whichllm — Benchmark hardware-aware : trouve le LLM local optimal selon ta config GPU/CPU/VRAM (4.2k★)](https://github.com/Andyyyy64/whichllm) | GitHub Trending 🐍 | #LLM |
| [wonderwhy-er/DesktopCommanderMCP — MCP server Claude : terminal, filesystem, Docker isolation, Python/Node exec en mémoire (6.1k★)](https://github.com/wonderwhy-er/DesktopCommanderMCP) | GitHub Trending TS | #Claude #MCP #Docker |
| [luongnv89/asm — Universal skill manager pour 19 agents IA (Claude Code, Cursor, Windsurf...) : TUI unifiée + security scanning (499★)](https://github.com/luongnv89/asm) | GitHub Trending TS | #LLM #agents |
| [notadev-iamaura/OneRAG — Framework RAG production-ready FastAPI/Python : config 1-ligne pour 6 Vector DBs + Claude, OpenAI, Gemini, Ollama (124★)](https://github.com/notadev-iamaura/OneRAG) | GitHub API | #FastAPI #LLM #RAG #Claude |
| [badhope/DATA-AI — Plateforme agent IA single-process : FastAPI backend + React 19 + streaming chat + multi-agent + RAG + memory (21★)](https://github.com/badhope/DATA-AI) | GitHub API | #FastAPI #LLM #agents #chatbot |

### 💡 Insights clés
- **anthropics/knowledge-work-plugins (20k★) — Anthropic lance les plugins métier pour Claude** : 11 plugins open-source spécialisés par rôle (Sales, Support, Legal, Marketing, Finance, Data...) avec MCP natif et intégration HubSpot, Slack, Linear, Figma, Snowflake. Architecture markdown + JSON — aucun code requis, personnalisable par toute équipe. Pour H'appi : ce repository EST notre architecture cible pour les déploiements enterprise. Proposer aux clients un "Claude métier on-premise" basé sur ce template — H'appi apporte le MCP FastAPI + pgvector + RGPD, Anthropic fournit le framework. Time-to-market divisé par 3 sur les projets Support et Sales.
- **NVIDIA/SkillSpector — La sécurité des agents devient un prérequis** : NVIDIA publie un scanner qui révèle que 26.1% des skills d'agents contiennent des vulnérabilités et 5.2% sont probablement malveillants. Avec 64 patterns détectés (prompt injection, data exfiltration, privilege escalation), c'est un signal fort que le marché va exiger des audits de sécurité agent. Pour H'appi : intégrer SkillSpector dans le pipeline CI/CD de tous les projets agents — devenir "le seul prestataire chatbot avec audit sécurité certifié NVIDIA" est un argument commercial fort pour les clients banque/santé/legal.
- **wonderwhy-er/DesktopCommanderMCP (6.1k★) — MCP + Docker isolation = l'agent autonome safe** : ce MCP server donne à Claude terminal + filesystem + Docker isolation + exécution Python/Node en mémoire. L'isolation Docker est la clé : un agent peut exécuter du code client sans risque. Pour H'appi : packager ce pattern dans l'offre "Happi Dev Agent" — un agent qui reçoit une tâche de dev, l'exécute dans un conteneur Docker isolé et retourne le résultat. Nouveau use case à proposer aux DSI.
- **notadev-iamaura/OneRAG + badhope/DATA-AI — FastAPI + RAG : le pattern converge** : deux projets indépendants arrivent à la même architecture (FastAPI + Vector DB + LLM swappable dont Claude). Confirmation que notre stack technique est le standard émergent. Pour H'appi : publier un template FastAPI + Claude + pgvector sur GitHub pour attirer les dev-clients en inbound — chaque star sur ce repo est un prospect qualifié.
- **AI Act J-54 — deadline du 2 août 2026 (54 jours)** : avec les knowledge-work-plugins Anthropic qui incluent des connecteurs Legal/Finance/Healthcare, la conformité IA devient un feature, pas un frein. Pour H'appi : positionner la prochaine proposition commerciale autour du thème "Votre Claude métier, conforme AI Act dès le jour 1" — utiliser anthropics/knowledge-work-plugins comme preuve de concept live lors des démos.

---

## 📰 Veille Tech — 2026-06-11
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Fable 5 lancé le 9 juin — nouveau modèle "Mythos" au-dessus d'Opus](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [Anthropic IPO : $65B Series H, valorisation $965B, dépôt S-1 SEC](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #Anthropic |
| [Claude Managed Agents : cron scheduling + CLI tools + vault-stored secrets](https://releasebot.io/updates/anthropic/claude-code) | Releasebot | #Claude #Anthropic #agents |
| [Claude intégré à Apple Foundation Models (iOS/macOS/visionOS 27)](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic #VoiceAI |
| [Claude écrit 80%+ de son propre code — Anthropic alerte sur l'auto-amélioration](https://uk.finance.yahoo.com/news/anthropic-says-something-unsettling-happening-103500529.html) | Yahoo Finance | #Claude #Anthropic |
| [BerriAI/litellm (49k★) — SDK Python unifié pour 100+ LLMs en format OpenAI](https://github.com/BerriAI/litellm) | GitHub Trending 🐍 | #LLM #FastAPI |
| [Fission-AI/OpenSpec — Spec-driven development (SDD) pour assistants IA coding](https://github.com/Fission-AI/OpenSpec) | GitHub Trending TS | #LLM #agents |
| [activeloopai/hivemind — "One brain for all your agents" (mémoire multi-agents)](https://github.com/activeloopai/hivemind) | GitHub Trending TS | #LLM #agents |
| [Railway : template deploy Next.js + Vercel AI SDK en un clic](https://railway.com/deploy/nextjs-ai-sdk) | Railway | #NextJS #Railway |
| [Vercel vs Railway vs Render : comparatif déploiement apps IA 2026](https://remery.ai/blog/vercel-vs-railway-vs-render-ai-deployment) | Remery | #Vercel #Railway #Docker |
| [AI Act : applicabilité totale au 2 août 2026 — obligations Articles 10+ actives](https://rgpd.com/ai-act/) | RGPD.com | #RGPD #AIAct |
| [LLM en industries réglementées — GDPR/HIPAA/SOC2 Playbook 2026](https://www.truefoundry.com/blog/llm-deployment-in-regulated-industries-hipaa-soc2-and-gdpr-playbook-for-2026) | TrueFoundry | #RGPD #LLM |
| [Top 10 AI Voice Agents 2026 : Synthflow, ElevenLabs, Retell AI (40+ langues)](https://www.robylon.ai/blog/top-10-ai-voice-agents-in-2026) | Robylon | #VoiceAI |
| [Gartner : 40% des apps enterprise avec agents IA d'ici fin 2026 (vs 5% en 2025)](https://www.chatbot.com/blog/best-ai-agents/) | Chatbot.com | #LLM #agents #SaaS |
| [awesome-ai-agents-2026 — 300+ agents, frameworks, benchmarks & comparatifs](https://github.com/ARUNAGIRINATHAN-K/awesome-ai-agents-2026) | GitHub | #LLM #agents |

### 💡 Insights clés
- **Claude Fable 5 + Managed Agents : nouvelle infrastructure H'appi** : Anthropic lance Claude Fable 5 (classe "Mythos", au-dessus d'Opus) et les Managed Agents avec cron scheduling, vault-stored secrets et browser integration. Pour H'appi : Happi Brain V2 peut devenir un Managed Agent natif — veille automatique planifiée, accès APIs clients via vault (zéro credentials exposées), browsing intégré. Migration à planifier dès Q3 2026.
- **Anthropic IPO à $965B — crédibilité maximale pour les intégrateurs Claude** : Anthropic dépose un S-1 après une levée de $65B. Quand le fournisseur principal entre en bourse, les DSI grands comptes valident Claude comme infrastructure pérenne. Pour H'appi : mettre à jour le pitch deck avec "Powered by Claude (Anthropic — IPO 2026, $965B)" — signal de solidité que les comités d'investissement et DPO attendent.
- **AI Act J-52 : 2 août 2026 = conformité obligatoire** : Article 10 (traçabilité données d'entraînement), transparence, documentation technique — tout s'active le 2 août. Les clients enterprise demanderont SOC 2, ISO 42001, DPA. Pour H'appi : livrer une "Happi Compliance Card" (1 page) dans chaque proposition dès maintenant — framing : "H'appi = seul partenaire chatbot conforme AI Act avant la deadline". Avantage concurrentiel immédiat sur les intégrateurs non préparés.
- **Voice AI 2026 : Synthflow + ElevenLabs dominent, marché sans code** : Les voice agents gèrent des millions d'appels/jour (qualification leads, booking, support vocal multilingue 40+ langues). Pour H'appi : lancer l'offre "Happi Voice" — ElevenLabs TTS + Claude reasoning + FastAPI backend. Verticales cibles : cliniques médicales, agences immobilières, e-commerce francophone. ROI mesurable dès J+30.
- **Gartner 40% enterprise + agents IA d'ici fin 2026 (vs 5% en 2025)** : La fenêtre commerciale se ferme — dans 6 mois, avoir des agents IA sera la norme, pas la différenciation. Pour H'appi : accélérer la production de 3 cas clients publiés avec ROI chiffré avant septembre 2026. Chaque démo validée ce trimestre vaut double.

---

## 📰 Veille Tech — 2026-06-12
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/claude-agent-sdk-python — SDK officiel Python pour agents Claude, en Trending GitHub aujourd'hui](https://github.com/anthropics/claude-agent-sdk-python) | GitHub Trending 🐍 | #Claude #Anthropic #agents |
| [PatterAI/Patter (543★) — Voice AI SDK open-source, alternative Vapi/Retell : give your AI agent a phone number in 4 lines, Twilio/Telnyx/Plivo, MIT](https://github.com/PatterAI/Patter) | GitHub Search | #VoiceAI #chatbot |
| [huggingface/speech-to-speech (4 873★) — Build local voice agents with open-source models, STT+TTS+LLM pipeline clé-en-main](https://github.com/huggingface/speech-to-speech) | GitHub Search | #VoiceAI #LLM |
| [modelscope/FunASR — Speech recognition industriel : 170x temps réel, 50+ langues, diarisation, détection émotion, streaming](https://github.com/modelscope/FunASR) | GitHub Trending 🐍 | #VoiceAI |
| [morettt/my-neuro (1 264★) — AI companion desktop avec voice cloning, mémoire longue durée, réponse <1s, Live2D](https://github.com/morettt/my-neuro) | GitHub Search | #VoiceAI #chatbot #LLM |
| [onyx-dot-app/onyx (38.7k★) — Open Source AI Chat platform : tous LLMs, agents autonomes, code interpreter, RAG intégré](https://github.com/onyx-dot-app/onyx) | GitHub Trending 🐍 | #chatbot #LLM |
| [waybarrios/vllm-mlx (1 325★) — Serveur compatible Claude+OpenAI pour Apple Silicon : MCP tool calling, multimodal, 400+ tok/s](https://github.com/waybarrios/vllm-mlx) | GitHub Search | #Claude #MCP #LLM |
| [JSONbored/awesome-claude (262★) — Registre curé agents Claude : MCP servers, skills, hooks, commands, jobs — mis à jour quotidiennement](https://github.com/JSONbored/awesome-claude) | GitHub Search | #Claude #Anthropic #MCP |
| [karpathy/autoresearch (208★/jour) — AI agents qui font de la recherche autonome sur GPU unique : nanochat training automatisé](https://github.com/karpathy/autoresearch) | GitHub Trending 🐍 | #LLM #agents |
| [anomalyco/opencode (566★/jour) — The open source coding agent en TypeScript : alternative à Claude Code](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #agents |
| [mksglu/context-mode (202★/jour) — Optimisation fenêtre contextuelle agents IA : réduction 98% de la consommation tokens](https://github.com/mksglu/context-mode) | GitHub Trending TS | #LLM #agents |
| [triggerdotdev/trigger.dev — Build and deploy fully-managed AI agents & workflows : SaaS infra pour agents autonomes](https://github.com/triggerdotdev/trigger.dev) | GitHub Trending TS | #SaaS #agents #Docker |

### 💡 Insights clés
- **Voice AI : explosion simultanée de 4 projets le même jour** — PatterAI/Patter (alternative Vapi/Retell open-source), HuggingFace speech-to-speech, FunASR industriel et my-neuro convergent tous vers le même pattern : voice agent local, open-source, sub-seconde. Le marché Voice AI bascule de "SaaS propriétaire cher" vers "stack maîtrisable". Pour H'appi : lancer **Happi Voice** avant que ces outils deviennent des commodités — stack recommandée : FunASR (STT) + Claude (reasoning) + ElevenLabs (TTS) + FastAPI backend. Verticales prioritaires : support client téléphonique, prise de RDV médicale, qualification leads immobilier francophone.
- **anthropics/claude-agent-sdk-python en Trending — la masse critique développeurs** : le SDK officiel Python pour agents Claude apparaît en Trending le jour même où la veille précédente signalait l'IPO Anthropic. Signal que les équipes dev adoptent massivement en ce moment précis. Pour H'appi : publier cette semaine un template GitHub "Happi Agent Starter" basé sur ce SDK + FastAPI + pgvector — chaque star = prospect qualifié entrant. Timing optimal.
- **Context-mode (98% réduction tokens) — l'optimisation devient opérationnelle** : avec des agents Claude qui tournent en continu (Happi Brain, agents clients), la consommation tokens est un coût direct. context-mode propose une compression intelligente de la fenêtre contextuelle. Pour H'appi : intégrer ce middleware dans les déploiements clients à fort volume (support continu, agents 24/7) — réduire la facture Anthropic de 50-80% = argument commercial fort face aux concurrents non optimisés.
- **trigger.dev + onyx-dot-app/onyx — l'infrastructure SaaS agent se standardise** : trigger.dev (orchestration agents managed) et onyx (frontend chatbot full-featured) arrivent ensemble en trending. Ces deux projets couvrent exactement les deux couches que H'appi construit sur mesure. Pour H'appi : évaluer onyx comme UI blanche pour les clients qui veulent une expérience ChatGPT-like hébergée (évite 2 mois de dev frontend) — H'appi apporte la valeur sur le backend métier + RGPD.
- **AI Act J-51 — deadline du 2 août 2026 (51 jours)** : avec PatterAI/Patter et onyx qui sont tous deux MIT licensed et self-hostable, la conformité RGPD par architecture (données on-premise, pas de cloud tiers) devient un argument technique concret. Pour H'appi : ajouter dans chaque proposition un slide "Architecture RGPD by design" avec le diagramme stack locale — différenciation immédiate face aux concurrents qui s'appuient sur des SaaS Voice tiers (Vapi, Retell) sans DPA clair.

---

## 📰 Veille Tech — 2026-06-13
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/skills — Dépôt officiel "Agent Skills" Anthropic : bibliothèque de compétences agents Claude (459★ auj., 150k★)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #Anthropic #agents |
| [NVIDIA/SkillSpector — Scanner sécurité agent skills : 26.1% vulnérables, 64 patterns détectés (813★ auj.)](https://github.com/NVIDIA/SkillSpector) | GitHub Trending 🐍 | #LLM #agents #sécurité |
| [anomalyco/opencode — Coding agent open-source TypeScript : alternative Claude Code (525★ auj., 173k★)](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #agents |
| [supermemoryai/supermemory — Memory & context engine pour apps IA, déploiement local (124★ auj., 26k★)](https://github.com/supermemoryai/supermemory) | GitHub Trending TS | #LLM #agents #chatbot |
| [karpathy/autoresearch — Agents IA pour recherche autonome sur single-GPU (207★ auj.)](https://github.com/karpathy/autoresearch) | GitHub Trending 🐍 | #LLM #agents |
| [BerriAI/litellm — Gateway unifié 100+ LLMs avec cost tracking et load-balancing (118★ auj., 50k★)](https://github.com/BerriAI/litellm) | GitHub Trending 🐍 | #LLM #FastAPI |
| [Claude croît de +306% en un trimestre : 203M → 824M visites/mois, croissance la plus rapide des IA](https://momenticmarketing.com/blog/top-ai-chatbots) | Momentic Marketing | #Claude #Anthropic #SaaS |
| [Claude Fable 5 & Opus 4.8 — Fable 5 : 95% SWE-bench, Opus 4.8 : 88.6%, workflows parallel-subagents](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [AI Voice 2026 — ElevenLabs sub-100ms, Vapi 62M calls/mois, Deepgram : état complet du stack Voice Agent](https://www.youngju.dev/blog/culture/2026-05-14-ai-voice-2026-elevenlabs-openai-realtime-cartesia-vapi-sesame-deepgram-comparison-deep-dive.en) | Chaos and Order | #VoiceAI |
| [Expo raises $45M Series B + Expo Agent powered by Claude Code : mobile AI agent React Native prod-ready](https://www.prnewswire.com/news-releases/expo-raises-45m-series-b-and-launches-expo-agent-to-close-the-gap-from-idea-to-production-ready-mobile-apps-302744423.html) | PR Newswire | #ReactNative #Claude |
| [PostgreSQL devient le substrat AI agent 2026 : pgvector HNSW, 4 couches mémoire en 1 DB](https://www.softwareseni.com/how-postgres-became-the-ai-agent-substrate-for-memory-branching-and-modern-hosting/) | SoftwareSeni | #PostgreSQL #LLM |
| [RGPD : amendes IA dépassent €5.88B — conformité chatbots devient priorité réglementaire n°1](https://sitegpt.ai/blog/gdpr-compliant-chatbot-platforms) | SiteGPT | #RGPD #chatbot |
| [AI Agent RGPD Compliance 2026 — Checklist 12 points : DPIA, DPA, transparence IA obligatoires](https://technovapartners.com/en/insights/security-gdpr-enterprise-ai-agents) | Technova Partners | #RGPD #LLM |
| [How I built an AI SaaS with Next.js, FastAPI and Dokploy — architecture complète production 2026](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #NextJS #SaaS |

### 💡 Insights clés
- **anthropics/skills + Expo Agent : l'agent devient le produit** — Anthropic publie un dépôt officiel "Agent Skills" (459 étoiles en une seule journée) et Expo lance un agent mobile propulsé par Claude Code. Ce double signal confirme que les applications du futur ne sont plus des apps mais des agents composables. Pour H'appi : restructurer l'offre autour de "Happi Skills" — composants agents réutilisables par verticale (Support, Sales, Prise de RDV, Voice) livrables en semaines plutôt qu'en mois.
- **NVIDIA/SkillSpector : 26.1% des agent skills sont vulnérables — l'audit devient vendable** — Quand NVIDIA publie un scanner qui révèle qu'1 skill sur 4 est vulnérable (prompt injection, data exfiltration, privilege escalation), les DSI vont l'inscrire dans leurs specs techniques. Pour H'appi : intégrer SkillSpector dans le pipeline CI/CD et livrer un "Happi Security Report" (1 page) avec chaque déploiement — différenciation immédiate pour les secteurs régulés (banque, santé, legal) avant que les concurrents ne réagissent.
- **Claude +306% en Q1 2026 + Fable 5 : le timing commercial est maintenant** — Claude atteint 824M visites/mois (+306% en un trimestre) et sort Fable 5 (95% SWE-bench) le même mois. L'adoption massive génère une demande d'intégrateurs spécialisés que le marché ne couvre pas encore. Pour H'appi : créer avant fin juin une landing page "Partenaire intégrateur Claude certifié" avec au moins un cas client chiffré — capturer l'inbound pendant la fenêtre d'opportunité.
- **PostgreSQL HNSW + pgvector : la stack H'appi est le standard 2026** — Les équipes AI d'entreprise effacent leurs stacks multi-DB pour consolider sur PostgreSQL (pgvector HNSW). Notre choix initial d'une base PostgreSQL unique pour SQL + vecteurs + mémoire est maintenant validé comme best practice industrie. Pour H'appi : publier un article technique "Comment H'appi gère la mémoire agent avec PostgreSQL + pgvector" — SEO ciblé + crédibilité + attirer les décideurs techniques qui cherchent ce pattern.
- **AI Act J-50 — deadline 2 août 2026 (50 jours)** — Avec les amendes RGPD qui dépassent €5.88B et la checklist DPIA/DPA/transparence IA devenue obligatoire, chaque prospect est en mode urgence conformité. Pour H'appi : publier immédiatement le badge "AI Act Ready" sur happi-bot.com et ajouter un slide dédié dans chaque proposition — le délai de 50 jours crée une pression d'achat que seul un partenaire préparé peut transformer en signature rapide.

---

## 📰 Veille Tech — 2026-06-14
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Fable 5 lancé le 9 juin 2026 — modèle Mythos-class, dépasse tous les précédents Anthropic](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [Claude Code — sous-agents imbriqués jusqu'à 5 niveaux, nouveaux plugins, meilleure gestion Chrome/VSCode](https://code.claude.com/docs/en/changelog) | Claude Code Docs | #Claude #agents |
| [Claude $30B run rate en Q1 2026 — 80x croissance annualisée, 8.2% market share chatbots mondiaux](https://momenticmarketing.com/blog/top-ai-chatbots) | Momentic Marketing | #Claude #Anthropic #SaaS |
| [FastAPI + Next.js 15 : le full-stack AI que personne ne construit encore — guide complet 2026](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV.to | #FastAPI #NextJS #SaaS |
| [The Exact Tech Stack to Ship AI SaaS Fast in 2026 — Next.js + PostgreSQL + FastAPI validé](https://hassanr.com/blogs/ai-saas-tech-stack-2026-nextjs-postgresql.html) | Hassan Raza | #FastAPI #NextJS #PostgreSQL #SaaS |
| [NestJS vs FastAPI 2026 : AI Backend Performance — FastAPI gagne sur les workloads IA](https://emporionsoft.com/nestjs-vs-fastapi-2026/) | Emporionsoft | #FastAPI #SaaS |
| [Building an AI Voice Chatbot with React Native — Speech-to-text + TTS + AI responses cross-platform](https://smallest.ai/blog/ai-voice-chatbot-react-native) | Smallest.ai | #VoiceAI #ReactNative |
| [Launch a Chat UI Agent With Docker & Vercel AI SDK — containerisation production-ready](https://www.docker.com/blog/launch-chat-ui-agent-docker-vercel-ai-sdk/) | Docker Blog | #Docker #chatbot #Vercel |
| [Deploy Vercel AI Chatbot on Railway — Redis + Postgres + HTTPS automatique one-click](https://railway.com/deploy/vercel-ai-chatbot) | Railway | #Railway #Vercel #chatbot #PostgreSQL |
| [GDPR & AI Chatbots: Complete Compliance Guide 2026 — bases légales, minimisation, sous-traitants](https://app.ailog.fr/en/blog/guides/rgpd-chatbot-conformite) | Ailog RAG | #RGPD #chatbot |
| [AI Act 2026 : Guide complet conformité IA — deadline Annexe II le 2 août 2026](https://www.leto.legal/guides/ai-act-conformite) | Leto Legal | #RGPD #AIAct |
| [Chatbot RGPD & CNIL : obligations 2026 — transparence IA obligatoire pour chatbots français](https://www.webotit.ai/blog/ia-conversationnelle/generalites/chatbot-et-rgpd-respectez-les-droits-des-personnes-avec-les-conseils-de-la-cnil) | Webotit.ai | #RGPD #chatbot |
| [LMCache — KV Cache Layer pour LLMs : 4x plus rapide, 8 966★ (+238 aujourd'hui)](https://github.com/LMCache/LMCache) | GitHub Trending 🐍 | #LLM |
| [vercel/ai — AI Toolkit TypeScript par l'équipe Next.js : 24 850★, libre et open-source](https://github.com/vercel/ai) | GitHub Trending TS | #Vercel #NextJS #LLM |
| [AI Agents 2026 — Guide complet LLM to Multi-Agent Systems : orchestration, mémoire, outils](https://eitt.academy/knowledge-base/ai-agents-2026-guide-from-llm-to-multi-agent-systems/) | EITT Academy | #LLM #agents |

### 💡 Insights clés
- **Claude Fable 5 + sous-agents 5 niveaux : l'architecture agent H'appi doit évoluer maintenant** — Anthropic lance Fable 5 (Mythos-class) le 9 juin et enrichit Claude Code avec des sous-agents imbriqués jusqu'à 5 niveaux. Ce n'est plus un chatbot linéaire : c'est un orchestrateur. Pour H'appi : structurer chaque livraison client autour d'un agent maître + sous-agents spécialisés (FAQ, booking, escalade, analytics) — c'est le pattern qui justifie et matérialise les tarifs maintenance Pro et Enterprise.
- **Claude à $30B run rate (80x) : la fenêtre "intégrateur certifié" se ferme dans 90 jours** — La croissance de Claude génère une demande insatisfaite d'intégrateurs spécialisés que le marché ne couvre pas encore. Pour H'appi : créer avant le 30 juin la landing page "Partenaire Intégrateur Claude Certifié" avec au moins un cas client chiffré — dans 6 mois le segment sera saturé, agir pendant la fenêtre d'inbound gratuit.
- **FastAPI + Next.js + PostgreSQL = consensus industrie 2026 — la stack H'appi est validée** — Trois sources indépendantes convergent sur la même stack pour les AI SaaS. Pour H'appi : formaliser un "Happi Tech Blueprint" d'une page à inclure dans chaque proposition commerciale — ça élimine l'objection technique "est-ce une stack viable ?" et positionne H'appi comme acteur rigoureux.
- **AI Act deadline 2 août 2026 (49 jours) — Annexe II : chatbots obligés de se déclarer** — Tous les chatbots français tombent sous la deadline Annexe II. CNIL et Leto Legal ont publié des guides opérationnels. Pour H'appi : livrer systématiquement un "Happi RGPD + AI Act Pack" avec chaque chatbot — checklist 12 points, badge "AI Act Ready", clause DPA prête à signer. Transformer la contrainte réglementaire en argument de vente différenciant face aux concurrents non-conformes.
- **Railway one-click + Docker + Vercel AI SDK : time-to-ship client < 24h maintenant possible** — Railway propose un template Vercel AI Chatbot avec Redis + Postgres + HTTPS automatique en one-click. Pour H'appi : standardiser ce pipeline, documenter le "Happi Deploy Kit" et garantir contractuellement un déploiement en moins d'une journée ouvrable — argument de closing puissant face aux agences qui promettent 6 semaines.

---

## 📰 Veille Tech — 2026-06-15
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Fable 5 & Mythos 5 : directive export-control US suspend l'accès mondial (12 juin 2026)](https://www.anthropic.com/news) | Anthropic | #Claude #Anthropic |
| [TCS + DXC + Anthropic : Claude déployé dans les banques et industries régulées](https://blog.mean.ceo/anthropic-claude-news-june-2026/) | Mean CEO Blog | #Claude #Anthropic #SaaS |
| [Claude : 20+ connecteurs MCP légaux + 12 plugins — law firms et équipes in-house](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #LLM #agents |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy — retour d'expérience complet](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #NextJS #SaaS |
| [Build Your Own Voice Assistant App with React Native + OpenAI Whisper in a Weekend](https://medium.com/react-native-journal/build-your-own-voice-assistant-app-with-react-native-openai-whisper-in-a-weekend-d7b60a1bdfb3) | Medium | #VoiceAI #ReactNative |
| [Full On-Device Voice AI Stack React Native : Wake Word + STT + TTS + Speaker ID + VAD](https://medium.com/@frymanofer/built-a-full-on-device-voice-ai-stack-for-react-native-wake-word-stt-tts-speaker-5a2403a06d16) | Medium | #VoiceAI #ReactNative |
| [React Native Speech Recognition 2026 : Complete Guide — Picovoice, Porcupine, Cheetah](https://picovoice.ai/blog/react-native-speech-recognition/) | Picovoice | #VoiceAI #ReactNative |
| [The Best Platforms to Deploy AI Apps in 2026 — Railway blog officiel](https://blog.railway.com/p/best-platforms-deploy-ai-apps-2026) | Railway Blog | #Railway #Docker #SaaS |
| [Railway vs Cloudflare vs Vercel : lequel choisir pour votre stack AI en 2026 ?](https://northflank.com/blog/railway-vs-cloudflare-vs-vercel) | Northflank | #Railway #Vercel #Docker |
| [Deploy AI Chatbot with Streaming Responses — SSE + Next.js + Railway Guide officiel](https://docs.railway.com/guides/ai-chatbot-streaming) | Railway Docs | #Railway #chatbot #SaaS |
| [Chatbot et RGPD en France 2026 : la conformité complète](https://www.agentsia.fr/chatbot-rgpd-france-2026/) | Agentsia.fr | #RGPD #chatbot |
| [IA conversationnelle & protection des données : nouveaux enjeux RGPD sites web 2026](https://www.farman-communication.com/ia-conversationnelle-et-protection-des-donnees-nouveaux-enjeux-rgpd-pour-les-sites-web-en-2026/) | Farman Communication | #RGPD #chatbot |
| [NVIDIA/SkillSpector — Security scanner for AI agent skills (964★ aujourd'hui)](https://github.com/NVIDIA/SkillSpector) | GitHub Trending 🐍 | #LLM #agents |
| [andrewyng/aisuite — Unified interface for generative AI providers (Andrew Ng)](https://github.com/andrewyng/aisuite) | GitHub Trending 🐍 | #LLM #chatbot |
| [lfnovo/open-notebook — Open Source NotebookLM avec plus de flexibilité (431★ aujourd'hui)](https://github.com/lfnovo/open-notebook) | GitHub Trending TS | #LLM #SaaS |

### 💡 Insights clés
- **Export-control US sur Claude Fable 5 & Mythos 5 — stratégie multi-modèle obligatoire pour H'appi** — Le 12 juin 2026, le gouvernement américain a suspendu l'accès aux deux derniers modèles Claude via une directive export-control. Pour H'appi : documenter une stratégie de fallback (Opus 4.8, open-source via aisuite d'Andrew Ng) dans chaque proposition — la résilience multi-modèles devient un argument de fiabilité et de souveraineté numérique face aux clients sensibles.
- **TCS + DXC intègrent Claude dans les banques et compagnies aériennes — segment réglementé à cibler** — Les grands intégrateurs positionnent Claude dans les industries régulées. Pour H'appi : construire une offre verticale "Secteur Régulé" (banque, santé, RH, juridique) combinant RGPD + AI Act Ready + Claude — se différencier des intégrateurs généralistes par la spécialisation et la conformité documentée.
- **Voice AI on-device React Native : la stack off-cloud mature en 2026** — Des développeurs publient des stacks Voice AI complètes fonctionnant entièrement on-device (Wake Word + STT + TTS + Speaker ID + VAD), sans envoyer de donnée dans le cloud. Pour H'appi : intégrer une offre Voice confidentielle dans le catalogue — les secteurs santé, juridique et RH vont exiger du traitement local pour être RGPD-conformes.
- **Railway = meilleure plateforme deploy AI apps 2026 (consensus officiel)** — Railway se positionne via son blog officiel comme la référence pour les chatbots streaming avec SSE, Redis et Postgres intégrés en one-click. Pour H'appi : standardiser Railway + Next.js + SSE dans le Happi Deploy Kit — "déploiement production en moins de 24h" devient une promesse crédible et différenciante.
- **AI Act J-47 (2 août 2026) : mention IA obligatoire pour tous les chatbots français** — Tout chatbot doit informer l'utilisateur qu'il interagit avec une IA. Agentsia.fr et Farman Communication ont publié des guides francophones complets. Pour H'appi : inclure systématiquement la mention "Ce service est géré par un assistant virtuel IA" dans chaque livraison + proposer un audit RGPD + AI Act comme service additionnel payant.

---

## 📰 Veille Tech — 2026-06-16
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic : data leak probe après outage Claude vendredi — impact sur la fiabilité des intégrations](https://cybernews.com/ai-news/claude-outage-resolved-anthropic-opus-model-errors/) | CyberNews | #Claude #Anthropic |
| [Claude intégré Apple Foundation Models iOS 27 / macOS 27 — nouveau canal de distribution IA natif](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #Anthropic |
| [Claude $30B run rate Q1 2026 — 80x croissance, Claude Code à $2.5B ARR en 9 mois](https://blog.mean.ceo/ai-agents-news-june-2026/) | Mean CEO Blog | #Claude #Anthropic #SaaS |
| [The AI Agents Stack 2026 Edition — O'Reilly Radar : orchestration, mémoire, outils, multi-agent](https://www.oreilly.com/radar/the-ai-agents-stack-2026-edition/) | O'Reilly Radar | #LLM #agents |
| [Juin 2026 : shift historique "chatbot → agent" — qui s'agentise en premier dans votre entreprise ?](https://blog.mean.ceo/ai-agents-news-june-2026/) | Mean CEO Blog | #LLM #agents #chatbot |
| [FastAPI + Next.js 15 : The Full-Stack Nobody's Building — guide complet pour AI SaaS](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV.to | #FastAPI #NextJS |
| [API-First SaaS avec FastAPI et Next.js — séparation des responsabilités et scalabilité](https://pysquad.com/solutions/api-first-saas-development-with-fastapi-and-nextjs) | PySquad | #FastAPI #NextJS #SaaS |
| [AI SaaS Tech Stack 2026 : Next.js + PostgreSQL + Vercel — 9 outils, 6 intégrations en production](https://hassanr.com/blogs/ai-saas-tech-stack-2026-nextjs-postgresql.html) | Hassan Raza | #NextJS #PostgreSQL #Vercel #SaaS |
| [Building an AI Voice Chatbot with React Native — guide complet STT + TTS + IA](https://smallest.ai/blog/ai-voice-chatbot-react-native) | Smallest.ai | #VoiceAI #ReactNative #chatbot |
| [Vercel vs Railway vs Render : déployer des apps AI en 2026 — guide comparatif officiel](https://remery.ai/blog/vercel-vs-railway-vs-render-ai-deployment) | Remery Blog | #Vercel #Railway #Docker #SaaS |
| [AI Act 2026 : guide conformité PME — risques, obligations, checklist opérationnelle](https://fragments-studio.com/blog/post/ai-act-pme-guide-conformite-2026) | Fragments Studio | #RGPD #AIAct |
| [IA : obligations et conformité pour les entreprises en 2026 — CNIL, AI Act, RGPD](https://www.sigma.fr/publications/blog/data-ia/ia-obligations-reglementation-entreprises/) | Sigma.fr | #RGPD #AIAct |
| [Agent-Reach — AI agent avec accès internet complet : Twitter, Reddit, YouTube, GitHub (30 898★)](https://github.com/Panniantong/Agent-Reach) | GitHub Trending 🐍 | #LLM #agents |
| [TencentDB-Agent-Memory — mémoire long-terme locale pour AI agents, 4 niveaux, zéro API externe (5 812★)](https://github.com/TencentCloud/TencentDB-Agent-Memory) | GitHub Trending TS | #LLM #agents #PostgreSQL |
| [SurfSense — alternative privacy-first à NotebookLM pour équipes, aucune limite de données (14 776★)](https://github.com/MODSetter/SurfSense) | GitHub Trending 🐍 | #LLM #SaaS #RGPD |

### 💡 Insights clés
- **Anthropic outage + data leak probe — le risque mono-modèle devient contractuel** — Après la panne Claude de vendredi et l'enquête sur une fuite de données, la résilience multi-modèle n'est plus une option technique : c'est une clause de contrat. Pour H'appi : formaliser une stratégie de fallback dans chaque offre (Claude → Opus 4.8 → open-source via aisuite) et inclure des SLA de disponibilité chiffrés dans les contrats — la fiabilité documentée se vend face aux clients grands comptes qui demandent des garanties.
- **Claude sur Apple iOS 27 / macOS 27 — distribution native à explorer pour H'appi Mobile** — Claude est maintenant accessible via Apple Foundation Models Framework, ouvrant iOS 27 et macOS 27 à des intégrations directes sans passer par une API tierce. Pour H'appi : prototyper un module "Happi on iOS" — les clients qui ont une app mobile peuvent intégrer un chatbot H'appi natif sans coût d'infrastructure supplémentaire, argument commercial fort pour les secteurs retail et services.
- **Shift marché confirmé : juin 2026 = "chatbot → agent" — retravailler la communication H'appi maintenant** — O'Reilly Radar et Mean CEO Blog convergent : le marché a basculé en juin 2026, on ne vend plus des chatbots, on vend de l'agentisation métier. Pour H'appi : remplacer le mot "chatbot" par "agent IA sur-mesure" sur la landing page et dans les propositions commerciales — le vocabulaire positionne et le vocabulaire actuel sous-value l'offre face aux tarifs Enterprise visés.
- **TencentDB-Agent-Memory + SurfSense : mémoire locale et confidentialité des agents IA atteignent la maturité** — Des solutions open-source de mémoire long-terme (pipeline 4 niveaux, zéro API externe) et de RAG privacy-first émergent sur GitHub avec des milliers d'étoiles. Pour H'appi : intégrer une couche mémoire locale dans les offres Premium — "votre agent se souvient des échanges précédents" + "vos données restent sur votre infrastructure" = deux arguments RGPD + différenciation qui justifient le pricing Enterprise.
- **AI Act J-46 (2 août 2026) : guide PME publié — H'appi peut vendre la conformité comme un service** — Fragments Studio et Sigma.fr publient des guides AI Act opérationnels pour les PME françaises. Pour H'appi : lancer un "Happi AI Act Readiness Audit" payant (checklist 15 points, rapport PDF, badge conformité) — les PME cherchent un expert pour les accompagner sur la réglementation, et H'appi peut se positionner comme le partenaire de confiance avant la deadline du 2 août.

---

## 📰 Veille Tech — 2026-06-17
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Feds freaked over Fable 5 after 'fix this code', not jailbreak, say researchers](https://news.ycombinator.com/item?id=48552687) | HackerNews | #Claude #Anthropic |
| [Amazon's Jassy Alerted White House to Anthropic Fable 5 Security Flaws, Triggering Export Ban](https://mlq.ai/news/amazons-jassy-alerted-white-house-to-anthropic-fable-5-security-flaws-triggering-export-ban/) | MLQ News | #Claude #Anthropic |
| [When a Government Pulls an AI Model : Fable 5 et Mythos 5 — ce que la suspension signifie pour les équipes sécurité](https://snyk.io/blog/fable-mythos-suspension-security-takeaways/) | Snyk Blog | #Claude #Anthropic #LLM |
| [Mastra empowers web devs to build AI agents in TypeScript](https://thenewstack.io/mastra-empowers-web-devs-to-build-ai-agents-in-typescript/) | The New Stack | #LLM #agents |
| [vllm-project/vllm — moteur d'inférence LLM haute performance, faible empreinte mémoire (83 122★, +124 aujourd'hui)](https://github.com/vllm-project/vllm) | GitHub Trending 🐍 | #LLM |
| [OpenBMB/VoxCPM — TTS multilingue tokenizer-free avec voice design créatif (30 268★, +408 aujourd'hui)](https://github.com/OpenBMB/VoxCPM) | GitHub Trending 🐍 | #VoiceAI |
| [rmyndharis/OpenWA — Gateway WhatsApp API self-hosted et open source (+185 aujourd'hui)](https://github.com/rmyndharis/OpenWA) | GitHub Trending TS | #chatbot |
| [diegosouzapw/OmniRoute — AI gateway gratuit, 160+ providers, compression de tokens, multi-modal (+107 aujourd'hui)](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #SaaS |
| [earendil-works/pi — Toolkit agent IA : API LLM unifiée, agent loop, TUI, CLI de coding agent (+326 aujourd'hui)](https://github.com/earendil-works/pi) | GitHub Trending TS | #LLM #agents |
| [Vercel vs Railway (2026) : Serverless vs Full-Stack Hosting — quelle plateforme pour votre SaaS ?](https://www.buildmvpfast.com/compare/vercel-vs-railway) | BuildMVPFast | #Vercel #Railway #Docker #SaaS |
| [Claude Updates by Anthropic — juin 2026 : Files API, Skills, MCP connector, prompt caching](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [AI Act Article 50 : la Commission européenne publie ses lignes directrices sur la transparence IA (consultation close le 3 juin)](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonneesPersonnelles.fr | #RGPD #AIAct |
| [IA générative & RGPD : 7 obligations à connaître pour les chatbots d'entreprise](https://yousign.com/fr-fr/blog/ia-generative-et-rgpd) | Yousign | #RGPD #chatbot |

### 💡 Insights clés
- **L'affaire Fable 5 s'aggrave : Amazon/Jassy au cœur du déclencheur de l'export-control** — De nouvelles révélations montrent que c'est Amazon (concurrent direct d'Anthropic sur l'inférence cloud) qui a alerté la Maison Blanche, et que le "jailbreak" n'était qu'un simple "fix this code". Pour H'appi : la dimension politique/concurrentielle de l'affaire renforce l'argument multi-modèle — documenter clairement dans les contrats clients quels modèles sont utilisés et pourquoi, pour anticiper d'éventuelles restrictions futures sur d'autres fournisseurs.
- **Mastra (TypeScript) mature comme alternative à LangChain pour les agents IA** — The New Stack confirme la montée de frameworks d'agents 100% TypeScript. Pour H'appi : évaluer Mastra comme option pour les projets où le client veut tout garder dans l'écosystème Next.js/Node — réduit la complexité d'avoir un backend Python séparé juste pour l'orchestration LLM, accélère la livraison sur les stacks JS-only.
- **OpenWA + OmniRoute + pi : la chaîne self-hosted (canal WhatsApp, gateway multi-provider, agent loop) est maintenant accessible en open source** — Ces trois projets GitHub Trending permettent de construire un chatbot WhatsApp avec routage multi-LLM sans dépendre d'un seul fournisseur ni payer des frais API par message. Pour H'appi : packager une offre "Happi WhatsApp" basée sur OpenWA + OmniRoute pour les PME françaises (commerce, santé, RH) qui veulent un canal WhatsApp à coût maîtrisé.
- **AI Act Article 50 : les lignes directrices officielles de la Commission européenne sont en consultation depuis mai 2026** — Avant la deadline du 2 août, la Commission précise les obligations de transparence (signaler explicitement le caractère artificiel d'un système IA conversationnel). Pour H'appi : mettre à jour le "Happi AI Act Readiness Audit" avec les références officielles de l'article 50 — un audit basé sur le texte légal et non sur des blogs tiers est un argument de crédibilité supplémentaire face aux PME clientes.

---

## 📰 Veille Tech — 2026-06-18
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Partner Program : Anthropic construit un écosystème d'intégrateurs autour de ses modèles](https://www.washingtonpost.com/wp-intelligence/ai-tech-brief/2026/06/16/claude-partner-program-creates-an-ecosystem-around-anthropics-ai-models/) | Washington Post | #Claude #Anthropic #SaaS |
| [Claude désormais disponible via Apple Foundation Models (iOS/macOS/visionOS 27) et Microsoft 365 Copilot (Excel/PowerPoint)](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #Anthropic |
| [Claude Code : nouveau mode "ultracode" — effort xhigh automatique selon la complexité de la tâche](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #agents |
| [Opus 4.8 : 4x moins d'erreurs de code laissées passer sans signalement vs Opus 4.7](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #Anthropic |
| [anthropics/skills — dépôt officiel Agent Skills d'Anthropic, 152 289★ (+519 aujourd'hui)](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #LLM #agents |
| [callstackincubator/ai — exécution LLM on-device pour React Native, compatible Vercel AI SDK](https://github.com/callstackincubator/ai) | GitHub Trending | #VoiceAI #ReactNative #Vercel |
| [FastAPI vs Next.js : quel backend choisir pour une AI SaaS en 2026 ?](https://hassanr.com/blogs/fastapi-vs-nextjs-ai-saas-backend-2026.html) | Hassan Raza | #FastAPI #NextJS #SaaS |
| [RocketChat/Rocket.Chat — CommsOS sécurisé pour opérations critiques, 45 637★ (+22 aujourd'hui)](https://github.com/RocketChat/Rocket.Chat) | GitHub Trending TS | #chatbot |
| [continuedev/continue — agent de coding open-source, 33 992★ (+49 aujourd'hui)](https://github.com/continuedev/continue) | GitHub Trending TS | #LLM #agents |
| [langfuse/langfuse — plateforme d'observabilité open-source pour applications LLM, 29 307★ (+71 aujourd'hui)](https://github.com/langfuse/langfuse) | GitHub Trending TS | #LLM #SaaS |
| [infiniflow/ragflow — moteur RAG open-source combiné à des capacités agent, 83 076★ (+105 aujourd'hui)](https://github.com/infiniflow/ragflow) | GitHub Trending 🐍 | #LLM #SaaS |
| [AI Act Article 50 : consultation européenne close le 3 juin — deadline du 2 août confirmée, amendes jusqu'à 35M€](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonneesPersonnelles.fr | #RGPD #AIAct |
| [ChatGPT/IA générative & RGPD : AIPD obligatoire pour les chatbots traitant des données sensibles ou à grande échelle](https://www.leto.legal/guides/intelligence-artificielle-chatgpt-et-rgpd) | Leto Legal | #RGPD #chatbot |

### 💡 Insights clés
- **Claude Partner Program : la fenêtre "intégrateur certifié" s'officialise — H'appi doit candidater maintenant** — Le Washington Post confirme qu'Anthropic structure un écosystème de partenaires autour de ses modèles, après le lancement déjà identifié des intégrateurs TCS/DXC. Pour H'appi : soumettre une candidature au programme partenaire avant qu'il ne se referme aux petites structures — être listé "Claude Partner" sur une landing devient un argument de crédibilité immédiat face aux PME.
- **Claude disponible sur Apple Foundation Models + Microsoft 365 Copilot : la distribution explose, l'intégration devient le vrai métier** — Claude n'est plus seulement une API à appeler, c'est un modèle disponible nativement dans l'OS (iOS/macOS 27) et dans Excel/PowerPoint. Pour H'appi : repositionner l'offre non plus comme "on installe un chatbot" mais comme "on connecte vos outils existants à l'IA déjà présente sur vos appareils" — réduit la friction de vente auprès des PME qui ont déjà ces outils.
- **Opus 4.8 quatre fois plus fiable sur la revue de code : argument de confiance technique pour les développements H'appi** — Anthropic communique sur la baisse drastique des erreurs silencieuses dans le code généré. Pour H'appi : mentionner ce chiffre dans les propositions commerciales techniques pour rassurer les clients sur la fiabilité du code livré par les agents IA utilisés en interne.
- **callstackincubator/ai : le LLM on-device en React Native devient un produit mûr, pas juste une preuve de concept** — Compatible nativement avec le Vercel AI SDK, ce projet permet de faire tourner des modèles directement sur le téléphone, sans appel réseau. Pour H'appi : packager une offre "Voice/Chat 100% on-device" pour les secteurs santé/RH/juridique où aucune donnée ne doit transiter par un serveur tiers — argument RGPD imparable.
- **AIPD obligatoire pour les chatbots IA générative à grande échelle : un nouveau service facturable pour H'appi** — Leto Legal précise les critères déclenchant l'obligation d'analyse d'impact (IA générative, données sensibles, grande échelle). Pour H'appi : ajouter une "AIPD chatbot" en option payante systématique dès qu'un projet client coche un de ces critères — transforme une contrainte réglementaire en ligne de revenu récurrente.

---

## 📰 Veille Tech — 2026-06-19
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic dépose une demande d'introduction en bourse (IPO confidentielle)](https://www.cbsnews.com/news/anthropic-ipo-confidential-filing-claude-ai/) | CBS News | #Anthropic #Claude |
| [Claude Sonnet 4 et Claude Opus 4 officiellement retirés le 15 juin 2026](https://platform.claude.com/docs/en/about-claude/model-deprecations) | Claude API Docs | #Claude #Anthropic |
| [Claude ajoute l'accès aux connecteurs MCP gérés en entreprise, démarrage avec Okta — provisioning zero-touch](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #SaaS |
| [Claude lance en beta publique les "Managed Agents" : automatisation par cron, secrets en vault, accès navigateur sécurisé](https://releasebot.io/updates/anthropic) | Releasebot | #Claude #agents #SaaS |
| [Scan de 1 million de services IA exposés : credentials et logique métier de chatbots LLM en accès libre](https://thehackernews.com/2026/05/we-scanned-1-million-exposed-ai.html) | The Hacker News | #chatbot #LLM #RGPD |
| [ElevenLabs atteint 500M$ d'ARR (vs 330M$ en déc. 2025), levée de 500M$ menée par Sequoia](https://www.assemblyai.com/blog/voice-ai-in-2026-series-1) | AssemblyAI / VoiceAISpace | #VoiceAI #SaaS |
| [Retell étend son offre voice-only vers l'omnicanal (voix, chat, email, SMS) pour les centres d'appels](https://newmarketpitch.com/blogs/news/conversational-ai-funding-analysis) | New Market Pitch | #VoiceAI #chatbot #SaaS |
| [livekit/agents — framework open-source pour agents voice AI temps réel, 11 048★ (+19 aujourd'hui)](https://github.com/livekit/agents) | GitHub Trending 🐍 | #VoiceAI #agents |
| [crewAIInc/crewAI — framework d'orchestration d'agents IA autonomes, 53 940★ (+105 aujourd'hui)](https://github.com/crewAIInc/crewAI) | GitHub Trending 🐍 | #LLM #agents |
| [modelcontextprotocol/servers — dépôt officiel des serveurs MCP, 87 431★ (+53 aujourd'hui)](https://github.com/modelcontextprotocol/servers) | GitHub Trending TS | #Claude #LLM |
| [supabase/supabase — plateforme Postgres pour apps web/mobile/IA, 104 511★ (+82 aujourd'hui)](https://github.com/supabase/supabase) | GitHub Trending TS | #PostgreSQL #SaaS |
| [Vercel vs Railway 2026 : quelle plateforme choisir pour déployer une stack Next.js/FastAPI ?](https://thesoftwarescout.com/vercel-vs-railway-2026-which-developer-platform-should-you-choose/) | The Software Scout | #Vercel #Railway #FastAPI #NextJS |
| [RGPD + AI Act en 2026 : le DPA devient obligatoire pour toute IA conversationnelle intégrée à un site web](https://yousign.com/fr-fr/blog/ia-generative-et-rgpd) | Yousign | #RGPD #AIAct #chatbot |

### 💡 Insights clés
- **Anthropic dépose une demande d'IPO confidentielle : le marché de l'IA générative entre dans une phase de maturité financière** — Cette annonce (CBS News) confirme qu'Anthropic structure son modèle économique pour un horizon public. Pour H'appi : anticiper une pression accrue sur les prix d'API à moyen terme et sécuriser des contrats pluriannuels avec les clients pour lisser ce risque tarifaire.
- **Retrait de Sonnet 4 et Opus 4 le 15 juin : vérifier immédiatement les intégrations clients encore sur ces modèles** — Releasebot confirme la dépréciation effective. Pour H'appi : auditer en urgence le portefeuille clients pour identifier toute intégration encore pointée sur Sonnet 4/Opus 4 et migrer vers Sonnet 4.6/Opus 4.8 avant interruption de service.
- **Managed Agents Claude en beta publique : Anthropic propose nativement ce que H'appi vend déjà en sur-mesure** — L'automatisation cron avec secrets en vault et accès navigateur sécurisé rapproche l'offre native d'Anthropic des agents métier que H'appi construit pour ses clients PME. Pour H'appi : se différencier sur l'intégration verticale (workflows métier spécifiques, support, conformité RGPD locale) plutôt que sur l'infrastructure d'agent brute, qui devient une commodité.
- **1 million de services IA exposés scannés : un argument commercial fort sur la sécurité des chatbots H'appi** — The Hacker News documente des credentials et logiques métier de chatbots accessibles publiquement (ex. instances Flowise mal configurées). Pour H'appi : intégrer un audit de sécurité (durcissement des endpoints, gestion des secrets) comme livrable standard de tout déploiement chatbot, et s'en servir comme argument différenciant face aux solutions no-code mal sécurisées.
- **ElevenLabs à 500M$ d'ARR : la Voice AI confirme sa traction commerciale, fenêtre d'opportunité pour une offre packagée H'appi** — La croissance d'ElevenLabs et l'extension omnicanal de Retell montrent que le marché Voice AI/centres d'appels est en forte expansion. Pour H'appi : packager une offre "Voice AI omnicanal" (téléphonie + chat + email) pour les PME, en s'appuyant sur des frameworks open-source comme livekit/agents pour réduire les coûts de développement.

---

## 📰 Veille Tech — 2026-06-20
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Suspension mondiale de Claude Fable 5 et Mythos 5 sur ordre d'export-control du gouvernement américain (3 jours après leur lancement)](https://www.anthropic.com/news/fable-mythos-access) | Anthropic Newsroom | #Claude #Anthropic |
| [Anthropic désactive Fable 5 et Mythos 5 sur AWS Bedrock, Google Cloud et l'API Claude directe pour tous les utilisateurs non-américains](https://www.marktechpost.com/2026/06/13/anthropic-disables-claude-fable-5-and-mythos-5-after-us-government-order/) | MarkTechPost | #Claude #Anthropic #RGPD |
| [Claude peut désormais générer des graphiques et visualisations interactives directement dans la conversation (bêta tous plans)](https://thenewstack.io/anthropics-claude-interactive-visualizations/) | The New Stack | #Claude #chatbot |
| [Claude Managed Agents : Anthropic veut héberger et faire tourner vos agents IA pour vous (cron, secrets, navigateur sécurisé)](https://thenewstack.io/with-claude-managed-agents-anthropic-wants-to-run-your-ai-agents-for-you/) | The New Stack | #Claude #agents #SaaS |
| [AI Act : la mise à jour "omnibus" de juin 2026 allège les obligations de transparence pour les IA déjà conformes CE](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonneesPersonnelles.fr | #RGPD #AIAct |
| [Bland (Voice AI) boucle une Series C de 50M$ menée par Dell Technologies Capital après avoir été refusé par 180 investisseurs](https://fortune.com/2026/06/16/voice-ai-bland-50-million-after-being-rejected-by-180-investors/) | Fortune | #VoiceAI #SaaS |
| [VoiceRun lève 5,5M$ en seed pour une plateforme Voice AI "code-first" destinée aux entreprises](https://techfundingnews.com/voicerun-bags-5-5m-for-code-first-voice-ai-platform/) | Tech Funding News | #VoiceAI #SaaS |
| [chopratejas/headroom — outil open-source de compression réduisant de 60 à 95% la consommation de tokens des prompts LLM](https://github.com/chopratejas/headroom) | GitHub Trending 🐍 | #LLM #chatbot |
| [fastapi/fastapi toujours en tête du trending Python — confirmation de FastAPI comme socle standard des backends IA](https://github.com/fastapi/fastapi) | GitHub Trending 🐍 | #FastAPI |
| [vercel/workflow — SDK Vercel pour construire des apps et agents IA durables et observables en TypeScript](https://github.com/vercel/workflow) | GitHub Trending TS | #Vercel #agents #LLM |
| [BuilderIO/agent-native — framework pour construire des applications "agent-native" pensées pour être pilotées par des agents IA](https://github.com/BuilderIO/agent-native) | GitHub Trending TS | #agents #LLM |
| [FastAPI for AI Engineers : pourquoi FastAPI devient le choix par défaut pour les backends IA en 2026](https://dev.to/zeroshotanu/fastapi-for-ai-engineers-part-1-why-every-ai-backend-is-moving-toward-fastapi-45fg) | DEV.to | #FastAPI #LLM #SaaS |
| [Designing a Production-Grade AI Chat Service with FastAPI : structurer un service de chat IA scalable](https://dev.to/masteringbackend/designing-a-production-grade-ai-chat-service-with-fastapi-8o2) | DEV.to | #chatbot #FastAPI |

### 💡 Insights clés
- **Suspension brutale de Fable 5/Mythos 5 par directive gouvernementale américaine : un risque de dépendance critique à isoler dans les contrats clients** — Trois jours après leur lancement, ces modèles ont été désactivés mondialement par ordre d'export-control, affectant AWS Bedrock, Google Cloud et l'API directe, sans préavis. Pour H'appi : ne jamais committer un client sur un modèle Anthropic "frontier" unique sans clause de repli (fallback Sonnet 4.6/Opus 4.8 ou multi-provider) — cet épisode démontre qu'un accès modèle peut disparaître en quelques heures pour des raisons hors du contrôle d'Anthropic.
- **AI Act "omnibus" de juin 2026 : les obligations de transparence s'allègent pour les IA déjà conformes CE — à intégrer dans le discours commercial H'appi** — La mise à jour réduit la charge réglementaire pour les systèmes IA industriels déjà certifiés. Pour H'appi : mettre à jour l'argumentaire de conformité pour ne pas sur-vendre la complexité réglementaire aux PME, tout en gardant l'obligation de signalement du caractère artificiel (Article 50, deadline 2 août) comme livrable non négociable de tout chatbot.
- **Claude Managed Agents + visualisations interactives : Anthropic grignote la couche d'orchestration que H'appi facture aujourd'hui** — L'hébergement natif d'agents (cron, secrets, navigateur) et la génération de graphiques à la volée rapprochent l'offre native Anthropic des livrables sur-mesure de H'appi. Pour H'appi : accélérer la différenciation sur l'intégration métier verticale (CRM, ERP, conformité RGPD locale) plutôt que sur l'infrastructure d'agent, qui devient une commodité gérée directement par Anthropic.
- **headroom (compression de tokens 60-95%) confirme une tendance forte : l'optimisation des coûts LLM devient un produit à part entière** — Ce projet GitHub Trending illustre la demande croissante pour réduire la facture API des chatbots à fort volume. Pour H'appi : évaluer l'intégration d'une couche de compression de contexte dans les chatbots clients à fort trafic, argument de différenciation "coût maîtrisé" face aux solutions no-code qui ne l'optimisent pas.
- **Bland (50M$) et VoiceRun (5,5M$) : la Voice AI enterprise continue d'attirer des financements importants malgré un contexte de levées plus sélectif** — Deux levées coup sur coup en juin confirment que le marché Voice AI B2B reste en forte traction, avec un accent sur le déploiement à l'échelle pour Voice Run et l'expansion vers les secteurs régulés pour Bland. Pour H'appi : prioriser une offre Voice AI packagée pour les secteurs réglementés (santé, RH, juridique) où la demande de fiabilité à l'échelle est la plus forte.

---

## 📰 Veille Tech — 2026-06-21
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic devient la startup IA la plus valorisée, dépassant OpenAI](https://news.ycombinator.com/item?id=48336233) | HackerNews | #Claude #Anthropic |
| [Anthropic annonce des partenariats avec TCS et DXC pour déployer Claude dans les secteurs régulés (banques, compagnies aériennes)](https://www.anthropic.com/news) | Anthropic Newsroom | #Claude #SaaS #RGPD |
| [Workload Identity Federation (WIF) : Anthropic remplace les clés API statiques par des identifiants temporaires pour les comptes Enterprise](https://www.anthropic.com/news) | Anthropic Newsroom | #Claude #SaaS |
| [Vercel lance "eve", un framework open-source qui traite les agents IA comme de simples répertoires de fichiers](https://thenewstack.io/) | The New Stack | #Vercel #agents |
| [Next.js tourne désormais dans ChatGPT : Vercel apporte le web dynamique au chat IA](https://thenewstack.io/next-js-in-chatgpt-vercel-brings-the-dynamic-web-to-ai-chat/) | The New Stack | #Vercel #chatbot |
| [Vapi atteint 500M$ de valorisation après avoir été choisi par Amazon Ring face à 40 concurrents Voice AI](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI #SaaS |
| [AethexAI lève 3M$ en pre-seed pour une Voice AI multilingue (anglais, français, arabe) construite sur un modèle et une couche d'orchestration propriétaires](https://techcrunch.com/2026/06/03/these-two-founders-left-goldman-and-meta-to-build-voice-ai-for-markets-everyone-else-overlooked/) | TechCrunch | #VoiceAI |
| [La Commission européenne ouvre une consultation publique jusqu'au 23 juin 2026 sur la classification des IA à haut risque (Article 6 de l'AI Act)](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonneesPersonnelles.fr | #RGPD #AIAct |
| [La CNIL publie de nouvelles fiches IA précisant l'application du RGPD aux modèles et les conditions d'annotation des données d'entraînement](https://www.cnil.fr/fr/ia-et-rgpd-la-cnil-publie-ses-nouvelles-recommandations-pour-accompagner-une-innovation-responsable) | CNIL | #RGPD |
| [onyx-dot-app/onyx — plateforme de chat IA open-source compatible avec plusieurs modèles de langage](https://github.com/onyx-dot-app/onyx) | GitHub Trending 🐍 | #chatbot #LLM |
| [jamiepine/voicebox — studio vocal IA open-source pour cloner, dicter et créer de la voix](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [twentyhq/twenty — alternative open-source à Salesforce conçue dès le départ pour l'IA](https://github.com/twentyhq/twenty) | GitHub Trending TS | #SaaS |
| [Building a Full-Stack AI Chatbot with FastAPI (Backend) and React (Frontend)](https://dev.to/vipascal99/building-a-full-stack-ai-chatbot-with-fastapi-backend-and-react-frontend-51ph) | DEV.to | #chatbot #FastAPI |

### 💡 Insights clés
- **Anthropic dépasse OpenAI en valorisation tout en multipliant les partenariats sectoriels (TCS, DXC) vers les banques et compagnies aériennes** — Le mouvement confirme la stratégie d'Anthropic de pénétrer les secteurs très régulés via des intégrateurs, exactement le terrain où H'appi positionne ses chatbots sur-mesure RGPD. Pour H'appi : capitaliser sur la crédibilité accrue de Claude auprès des grandes entreprises régulées pour vendre des déploiements "powered by Claude" aux PME du même secteur, sans attendre une offre packagée directe d'Anthropic sur ce segment.
- **Workload Identity Federation : Anthropic pousse les clients Enterprise à abandonner les clés API statiques pour des identifiants temporaires** — Cette évolution réduit le risque de fuite de credentials mais impose une mise à jour de l'intégration technique. Pour H'appi : anticiper la migration vers WIF dans les futurs contrats Enterprise et en faire un argument de sécurité différenciant face aux solutions concurrentes qui utilisent encore des clés API statiques.
- **AethexAI (Voice AI multilingue FR/EN/AR) confirme la demande pour des assistants vocaux capables de gérer dialectes et marchés locaux mal desservis** — Cette levée pre-seed cible précisément les marchés francophones et arabophones que les géants Voice AI américains négligent. Pour H'appi : c'est un signal direct de marché pour une offre Voice AI française/multilingue adaptée aux PME, créneau encore peu disputé par les leaders (Bland, Vapi, ElevenLabs) focalisés sur l'anglophone.
- **Vapi choisi par Amazon Ring face à 40 concurrents : la Voice AI enterprise se consolide autour de quelques plateformes dominantes** — La sélection par un acteur grand public de l'envergure d'Amazon Ring valide la maturité du marché Voice AI mais accélère aussi la concentration. Pour H'appi : se différencier sur l'intégration verticale et le support local plutôt que de concurrencer frontalement ces plateformes sur l'infrastructure brute.
- **Consultation européenne sur la classification des IA à haut risque (deadline 23 juin) + nouvelles fiches CNIL sur l'annotation des données d'entraînement** — Ces deux chantiers réglementaires parallèles vont préciser concrètement quelles obligations s'appliquent aux chatbots IA selon leur usage. Pour H'appi : suivre l'issue de la consultation pour ajuster le discours de conformité client, et utiliser les nouvelles fiches CNIL comme référence directe dans la documentation RGPD livrée aux clients.

---

## 📰 Veille Tech — 2026-06-22
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic's Claude Platform arrive en disponibilité générale sur AWS, avec accès direct aux mêmes API que via Anthropic](https://thenewstack.io/anthropics-claude-platform-comes-to-aws/) | The New Stack | #Claude #Anthropic |
| [Cursor, Claude Code et Codex fusionnent vers une même pile d'outils de codage IA, sans plan coordonné entre éditeurs](https://thenewstack.io/ai-coding-tool-stack/) | The New Stack | #Claude #LLM |
| [Retell AI lance "Retell Guardrails" : une couche programmable qui bloque des sujets sensibles et détecte/rédige les PII en temps réel dans les logs vocaux](https://www.retellai.com/blog/best-voice-ai-providers) | Retell AI (Voice AI) | #VoiceAI #RGPD |
| [bytedance/deer-flow — harness "SuperAgent" long-horizon capable de chercher, coder et créer de façon autonome](https://github.com/bytedance/deer-flow) | GitHub Trending 🐍 | #agents #LLM |
| [topoteretes/cognee — plateforme open-source de mémoire IA donnant aux agents une mémoire persistante long-terme](https://github.com/topoteretes/cognee) | GitHub Trending 🐍 | #LLM #chatbot |
| [mukul975/Anthropic-Cybersecurity-Skills — compétences cybersécurité structurées pour agents IA, mappées aux frameworks de sécurité majeurs](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) | GitHub Trending 🐍 | #Claude #Anthropic |
| [FlowiseAI/Flowise — outil low-code pour construire des agents IA visuellement, toujours en forte traction sur le trending TypeScript](https://github.com/FlowiseAI/Flowise) | GitHub Trending TS | #chatbot #LLM |
| [firecrawl/firecrawl — API de scraping web à grande échelle pensée pour alimenter des agents IA en données](https://github.com/firecrawl/firecrawl) | GitHub Trending TS | #LLM |
| [tashfeenahmed/freellmapi — proxy compatible OpenAI combinant les quotas gratuits de plusieurs fournisseurs LLM avec routage et failover intelligents](https://github.com/tashfeenahmed/freellmapi) | GitHub Trending TS | #LLM #SaaS |
| [FastAPI + Next.js 15 : la stack full-stack que personne ne construit encore, malgré ses avantages pour les apps IA](https://dev.to/alexmayhewdev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV.to | #FastAPI #chatbot |
| [Comment j'ai construit un SaaS IA avec Next.js, FastAPI et Dokploy](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #SaaS #FastAPI |
| [Streamer les réponses IA dans Next.js : Claude, OpenAI et le Vercel AI SDK](https://dev.to/whoffagents/streaming-ai-responses-in-nextjs-claude-openai-and-the-vercel-ai-sdk-1gm3) | DEV.to | #Claude #chatbot |
| [J'ai construit une app Next.js prête pour la production avec Claude Code — leçons apprises](https://dev.to/julykk/i-built-a-production-ready-nextjs-app-using-claude-code-heres-what-i-learned-3e0c) | DEV.to | #Claude #chatbot |

### 💡 Insights clés
- **Retell Guardrails (détection et rédaction PII en temps réel dans les logs vocaux) : la conformité RGPD devient une fonctionnalité produit attendue, pas un service à part** — Retell intègre nativement le blocage de sujets sensibles et la rédaction de données personnelles dans son infrastructure Voice AI. Pour H'appi : packager une couche équivalente de filtrage/rédaction PII dans les chatbots texte et vocaux livrés aux clients français, comme standard non négociable plutôt que comme option payante — c'est désormais l'attendu du marché.
- **Claude Platform en GA sur AWS : Anthropic multiplie les points d'accès (direct, Bedrock, AWS) pour capter les clients Enterprise déjà sur AWS** — Cette disponibilité élargie facilite l'intégration de Claude pour les clients H'appi déjà hébergés chez AWS, en plus des options Scaleway/Hetzner. Pour H'appi : conserver la flexibilité multi-hébergeur dans l'architecture (Claude via API directe, Bedrock ou AWS selon la contrainte de souveraineté du client) sans verrouiller un seul canal d'accès.
- **La fusion de facto entre Cursor, Claude Code et Codex en une seule pile d'outils de codage IA confirme la consolidation de la couche "agent de développement"** — Les frontières entre éditeurs IA et agents de code s'effacent, ce qui accélère la productivité de développement mais banalise l'outillage. Pour H'appi : continuer à différencier sur le produit final livré au client (chatbot métier intégré) plutôt que sur la rapidité de développement interne, qui devient un avantage de moins en moins défendable face à la concurrence outillée de la même façon.
- **deer-flow (SuperAgent long-horizon) et cognee (mémoire persistante pour agents) : la mémoire long-terme et l'autonomie multi-étapes deviennent les briques open-source à surveiller pour les chatbots H'appi de nouvelle génération** — Ces deux projets trending confirment que la prochaine vague de différenciation chatbot porte sur la persistance de contexte et l'autonomie d'exécution, pas seulement la génération de réponses. Pour H'appi : évaluer cognee comme brique de mémoire long-terme pour les chatbots SAV/secrétariat nécessitant un suivi client dans la durée (au-delà d'une session).
- **freellmapi (proxy multi-fournisseurs LLM avec failover) renforce l'argument de robustesse multi-provider après l'épisode de suspension Fable 5/Mythos 5** — Ce projet open-source illustre une tendance à se prémunir contre la dépendance à un seul fournisseur LLM en routant intelligemment entre quotas gratuits et fournisseurs. Pour H'appi : s'inspirer de ce pattern de failover pour la clause de repli multi-provider déjà identifiée comme nécessaire dans les contrats Enterprise.

---
## 📰 Veille Tech — 2026-06-23
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [jamiepine/voicebox — studio vocal IA open-source : cloner une voix, dicter, créer du contenu audio](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [vectorize-io/hindsight — "Agent Memory That Learns", brique de mémoire agentique qui s'améliore avec l'usage](https://github.com/vectorize-io/hindsight) | GitHub Trending 🐍 | #LLM #chatbot |
| [unclecode/crawl4ai — scraper web open-source pensé pour nourrir des LLM en données structurées](https://github.com/unclecode/crawl4ai) | GitHub Trending 🐍 | #LLM |
| [twentyhq/twenty — alternative open-source à Salesforce conçue nativement pour l'IA, toujours en tête du trending TypeScript](https://github.com/twentyhq/twenty) | GitHub Trending TS | #SaaS #chatbot |
| [Micron et Anthropic annoncent un accord stratégique sur l'infrastructure mémoire/stockage pour l'IA, avec investissement de Micron dans la Series H d'Anthropic](https://investors.micron.com/news-releases/news-release-details/micron-and-anthropic-announce-strategic-agreement-scale-next) | Micron Investor News | #Claude #Anthropic |
| [Anthropic dépose un dossier confidentiel d'introduction en bourse (IPO), avec une valorisation visée et $47Md de revenu annualisé porté par les abonnements Claude](https://www.cbsnews.com/news/anthropic-ipo-confidential-filing-claude-ai/) | CBS News | #Claude #Anthropic |
| [Anthropic scinde les abonnements Claude : ce qui change pour les indie hackers à partir du 15 juin](https://devtoolpicks.com/blog/anthropic-splits-claude-subscriptions-agent-sdk-credit-june-2026) | DevToolPicks | #Claude #SaaS |
| [La CNIL publie de nouvelles recommandations IA/RGPD pour accompagner une innovation responsable](https://www.cnil.fr/fr/ia-et-rgpd-la-cnil-publie-ses-nouvelles-recommandations-pour-accompagner-une-innovation-responsable) | CNIL | #RGPD |
| [AI Act 2026 : le paquet omnibus numérique allège les obligations pour la majorité des entreprises, application complète prévue le 2 août 2026](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonnéesPersonnelles.fr | #RGPD |
| [Railway vs Vercel en 2026 : pattern dominant — frontend Next.js sur Vercel, backend + base de données sur Railway pour le coût et la DX](https://docs.railway.com/platform/compare-to-vercel) | Railway Docs | #Vercel #Railway #SaaS |
| [Designing a Production-Grade AI Chat Service with FastAPI : garder un chatbot rapide, scalable et facile à étendre](https://dev.to/masteringbackend/designing-a-production-grade-ai-chat-service-with-fastapi-8o2) | DEV.to | #FastAPI #chatbot |
| [Building a Full-Stack AI Chatbot with FastAPI (Backend) and React (Frontend)](https://dev.to/vipascal99/building-a-full-stack-ai-chatbot-with-fastapi-backend-and-react-frontend-51ph) | DEV.to | #FastAPI #chatbot |

### 💡 Insights clés
- **Micron investit dans la Series H d'Anthropic et l'IPO confidentielle se confirme : Anthropic consolide son assise financière (47 Md$ de revenu annualisé) pendant que les abonnements Claude se segmentent (split du 15 juin pour les indie hackers)** — Pour H'appi : anticiper une possible évolution tarifaire ou de quotas côté API Claude liée à cette restructuration commerciale, et vérifier régulièrement les conditions des crédits Agent SDK utilisés en interne.
- **hindsight (mémoire d'agent qui apprend) confirme, après cognee hier, que la mémoire long-terme agentique est désormais une catégorie à part entière de l'écosystème open-source** — Deux briques mémoire trending en deux jours signalent une consolidation rapide de ce segment. Pour H'appi : comparer cognee et hindsight avant de choisir une brique de mémoire persistante pour les chatbots SAV/secrétariat à suivi client dans la durée, plutôt que d'en adopter une par défaut.
- **voicebox (studio vocal IA open-source) illustre la démocratisation des outils de clonage/dictée vocale, un signal direct pour l'offre Voice AI d'H'appi** — Ce type d'outil grand public abaisse la barrière technique pour des concurrents low-cost sur le vocal. Pour H'appi : continuer à différencier sur l'intégration métier (SAV, secrétariat) et la conformité RGPD plutôt que sur la brique de synthèse/clonage vocal elle-même, qui devient commoditisée.
- **Le paquet omnibus numérique de l'AI Act allège les obligations pour la majorité des entreprises, avec application complète au 2 août 2026 et la CNIL qui publie de nouvelles recommandations IA/RGPD** — Cet allègement réglementaire ne dispense pas les chatbots du RGPD dès qu'une donnée personnelle transite par un prompt. Pour H'appi : utiliser cette clarification CNIL comme argument commercial rassurant auprès des clients PME, tout en maintenant le niveau d'exigence RGPD déjà en place (rédaction PII, hébergement souverain).
- **Le pattern "Vercel pour le frontend Next.js + Railway pour le backend/DB" se confirme comme standard 2026 pour les stacks SaaS légères** — Cette répartition coût/performance correspond exactement à l'architecture déjà recommandée pour les petits clients H'appi. Pour H'appi : formaliser ce pattern comme option de déploiement par défaut dans les devis clients SaaS, en complément des offres Scaleway/Hetzner pour les clients à contrainte de souveraineté forte.

---
## 📰 Veille Tech — 2026-06-24
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic fait sortir Claude Cowork de la preview et l'amène directement en disponibilité générale Enterprise](https://thenewstack.io/anthropic-takes-claude-cowork-out-of-preview-and-straight-into-the-enterprise/) | The New Stack | #Claude #SaaS |
| [Anthropic double gratuitement les limites d'usage de Claude Cowork (5h) du 5 juin au 5 juillet 2026](https://thenewstack.io/anthropic-claude-cowork-promotion/) | The New Stack | #Claude #SaaS |
| [Anthropic va laisser ses "managed agents" rêver — orchestration multi-agents axée résultats avec pilotage minimal](https://thenewstack.io/anthropic-managed-agents-dreaming-outcomes/) | The New Stack | #Claude #LLM |
| [Claude atteint 10,3% de part de marché des assistants IA, ChatGPT tombe sous 50% pour la première fois face à Gemini et Claude](https://www.buildfastwithai.com/blogs/ai-news-today-june-22-2026) | BuildFastWithAI | #Claude #LLM |
| [Sesame (startup conversationnelle fondée par des ex-Oculus) lance son app iOS publique avec 4 agents vocaux à personnalité et mémoire propres](https://techcrunch.com/2026/05/28/sesame-the-conversational-ai-startup-from-oculus-founders-launches-its-ios-app/) | TechCrunch | #VoiceAI #chatbot |
| [AethexAI lève 3M$ en pré-seed pour combler le manque de Voice AI en Afrique/Moyen-Orient, déjà 17 000 appels/jour traités](https://techcrunch.com/2026/06/03/these-two-founders-left-goldman-and-meta-to-build-voice-ai-for-markets-everyone-else-overlooked/) | TechCrunch | #VoiceAI #SaaS |
| [La CNIL publie ses nouvelles fiches IA précisant l'application du RGPD aux modèles, les impératifs de sécurité et l'annotation des données d'entraînement](https://www.cnil.fr/fr/ia-finalisation-recommandations-developpement-des-systemes-ia) | CNIL | #RGPD |
| [La CNIL se prépare à devenir autorité de surveillance de marché au titre de l'AI Act, en plus de son rôle de protection des données](https://www.cnil.fr/fr/developpement-des-systemes-dia-les-recommandations-de-la-cnil-pour-respecter-le-rgpd) | CNIL | #RGPD |
| [anthropics/claude-plugins-official — répertoire officiel et géré par Anthropic de plugins Claude Code de haute qualité](https://github.com/anthropics/claude-plugins-official) | GitHub Trending 🐍 | #Claude |
| [aws/agent-toolkit-for-aws — serveurs MCP, skills et plugins officiels AWS pour construire des agents IA sur AWS](https://github.com/aws/agent-toolkit-for-aws) | GitHub Trending 🐍 | #LLM |
| [ZhuLinsen/daily_stock_analysis — analyse boursière multi-marché pilotée par LLM avec dashboards de décision et notifications automatiques](https://github.com/ZhuLinsen/daily_stock_analysis) | GitHub Trending 🐍 | #LLM |
| [garrytan/gstack — setup Claude Code complet de Garry Tan : 23 outils jouant les rôles CEO, Designer, Eng Manager, Release Manager, QA](https://github.com/garrytan/gstack) | GitHub Trending TS | #Claude |
| [Railway vs Vercel (2026) : quand migrer son frontend, et ce que Vercel ne peut pas remplacer (pas de conteneurs Docker en prod)](https://dev.to/thedevopsguy/railway-vs-vercel-when-to-migrate-your-frontend-4bo6) | DEV.to | #Vercel #Railway #Docker |

### 💡 Insights clés
- **Claude Cowork passe en disponibilité générale Enterprise avec des limites doublées gratuitement jusqu'au 5 juillet : Anthropic pousse fort sur l'adoption no-code en entreprise** — Pour H'appi, c'est un signal que les clients Enterprise vont s'habituer à déléguer des tâches à des agents Claude sans coder, ce qui peut ouvrir une porte d'entrée commerciale (proposer des chatbots H'appi comme extension métier de Cowork) plutôt qu'une menace de désintermédiation.
- **Claude franchit 10,3% de part de marché des assistants IA pendant que ChatGPT tombe sous 50% pour la première fois : la bascule vers un paysage multi-modèles s'accélère** — Pour H'appi : l'argument "agnostique LLM avec Claude par défaut" reste pertinent commercialement, la diversification du marché renforçant la légitimité de proposer plusieurs fournisseurs selon le client plutôt qu'un choix unique.
- **Sesame (4 agents vocaux à mémoire et personnalité propres) et AethexAI (Voice AI pour marchés sous-desservis, 17k appels/jour) confirment que la Voice AI conversationnelle à forte personnalité/mémoire devient un standard d'expérience attendu, pas un gadget** — Pour H'appi : enrichir l'offre Voice AI (SAV, secrétariat) avec une mémoire de conversation persistante et une personnalité de marque cohérente plutôt qu'une voix générique, pour rester compétitif face à ces nouveaux entrants spécialisés.
- **La CNIL publie ses fiches IA définitives sur l'application du RGPD aux modèles (sécurité, annotation des données d'entraînement) et se prépare à devenir autorité de surveillance de marché au titre de l'AI Act, cumulant les deux casquettes** — Pour H'appi : ces fiches CNIL deviennent la référence à citer explicitement dans la documentation de conformité fournie aux clients, et anticiper un contrôle combiné RGPD + AI Act par le même régulateur français à moyen terme.
- **L'article Railway vs Vercel confirme que Vercel doit rester une cible frontend pure (pas de conteneurs Docker en prod) tandis que Railway gère nativement PostgreSQL/Redis et les workers** — Cela valide la recommandation déjà formulée par H'appi (Next.js sur Vercel + backend/DB sur Railway) et donne un argument technique précis (absence de support Docker en prod côté Vercel) à utiliser dans les devis pour justifier l'architecture hybride auprès des clients techniques.

---
## 📰 Veille Tech — 2026-06-25
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic accuse Alibaba d'avoir "illicitement" accédé à ses modèles Claude via des milliers de comptes frauduleux ciblant le code et le raisonnement agentique](https://www.bloomberg.com/news/articles/2026-06-24/anthropic-accuses-alibaba-of-illicitly-accessing-its-ai-models) | Bloomberg | #Claude #Anthropic |
| [Anthropic lance Claude Tag : un coéquipier IA persistant et partagé dans Slack, qui mémorise le contexte des canaux et agit de façon autonome](https://thenewstack.io/anthropic-claude-tag-slack/) | The New Stack | #Claude #chatbot #SaaS |
| [Claude Tag remplace l'app "Claude in Slack" — fenêtre de migration de 30 jours pour les admins, bascule complète au 3 août 2026](https://venturebeat.com/technology/anthropic-launches-claude-tag-replacing-its-slack-app-with-a-persistent-ai-teammate-that-learns-monitors-and-works-autonomously) | VentureBeat | #Claude #chatbot |
| [La CNIL publie ses recommandations sur la base légale de l'intérêt légitime pour le développement de systèmes d'IA](https://www.cnil.fr/fr/recommandations-developpement-ia-interet-legitime) | CNIL | #RGPD |
| [tashfeenahmed/freellmapi reste en tête du trending TypeScript : proxy compatible OpenAI qui cumule les quotas gratuits de plusieurs fournisseurs LLM avec routage et failover](https://github.com/tashfeenahmed/freellmapi) | GitHub Trending TS | #LLM |
| [nocodb/nocodb — alternative open-source et auto-hébergeable à Airtable, toujours en tête du trending TypeScript](https://github.com/nocodb/nocodb) | GitHub Trending TS | #SaaS |
| [BerriAI/litellm — SDK/proxy Python unifié pour 100+ API LLM avec cost tracking et load-balancing, de retour dans le trending Python](https://github.com/BerriAI/litellm) | GitHub Trending 🐍 | #LLM #FastAPI |

### 💡 Insights clés
- **Anthropic accuse Alibaba (lab Qwen) d'avoir orchestré un accès frauduleux massif à Claude pour cibler ses capacités de code et de raisonnement agentique** — Pour H'appi : ce type d'incident renforce l'argument de sécurité/conformité dans les propositions commerciales (traçabilité des accès API, clés scoped/rotatives) et confirme que la robustesse anti-abus des fournisseurs LLM devient un critère de choix à part entière, pas seulement la qualité du modèle.
- **Claude Tag transforme Claude en coéquipier persistant dans Slack (mémoire de canal, action autonome, migration forcée avant le 3 août 2026)** — Ce pattern "assistant qui accumule du contexte métier au fil du temps sans être resollicité à chaque fois" est exactement la promesse différenciante que doivent porter les chatbots H'appi (SAV, secrétariat) face aux bots stateless. À citer comme référence produit Anthropic dans les pitchs : "même logique que Claude Tag, appliquée à votre métier."
- **La CNIL clarifie l'intérêt légitime comme base légale possible pour entraîner/développer des systèmes d'IA sur données personnelles** — Pour H'appi : documenter explicitement la base légale retenue (consentement vs intérêt légitime) dans chaque projet chatbot traitant des données clients, et ajouter cette clarification CNIL aux argumentaires de conformité déjà fournis aux clients PME.
- **freellmapi (anti-dépendance multi-LLM) et litellm (gateway unifié 100+ LLM) cohabitent en haut du trending : la résilience multi-fournisseur s'installe comme standard d'architecture, pas comme exception post-incident** — Pour H'appi : formaliser un pattern de gateway LLM par défaut (Claude en primaire, fallback configurable) dans l'architecture de référence proposée aux clients Enterprise, plutôt que de le traiter au cas par cas après un incident fournisseur.
- **nocodb (alternative open-source à Airtable) confirme la demande pour des couches de données no-code self-hostables** — Pour H'appi : option intéressante comme back-office léger pour les clients PME qui veulent gérer eux-mêmes le contenu de leur chatbot (FAQ, base de connaissance) sans dépendre d'un outil SaaS tiers payant à chaque utilisateur additionnel.

---
## 📰 Veille Tech — 2026-06-26
> Mis à jour automatiquement par Happi Brain Agent
> ⚠️ HackerNews, DEV.to et The New Stack RSS étaient bloqués par la politique réseau de l'environnement (403 sur le proxy de sortie) — veille basée uniquement sur GitHub Trending aujourd'hui.

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic-Cybersecurity-Skills — skills de cybersécurité structurés mappés aux frameworks majeurs pour agents IA](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) | GitHub Trending 🐍 | #Claude #Anthropic |
| [MinerU — transforme PDF et documents Office complexes en markdown/JSON prêt pour LLM](https://github.com/opendatalab/MinerU) | GitHub Trending 🐍 | #LLM |
| [free-llm-api-resources — compilation de ressources d'inférence LLM gratuites accessibles via API](https://github.com/cheahjs/free-llm-api-resources) | GitHub Trending 🐍 | #LLM |
| [NVIDIA-NeMo/Speech — framework IA générative scalable pour LLM, multimodal et Voice AI](https://github.com/NVIDIA-NeMo/Speech) | GitHub Trending 🐍 | #LLM #VoiceAI |
| [llama_index — plateforme leader d'agents documentaires et d'OCR pour applications LLM](https://github.com/run-llama/llama_index) | GitHub Trending 🐍 | #LLM |
| [open-seo (every-app) — alternative open-source à Semrush et Ahrefs](https://github.com/every-app/open-seo) | GitHub Trending TS | #SaaS |
| [gstack (garrytan) — setup Claude Code avec 23 outils opinionés (CEO, Designer, Engineering Manager, QA...)](https://github.com/garrytan/gstack) | GitHub Trending TS | #Claude #chatbot |
| [voicebox (jamiepine) — studio vocal IA open-source : clonage, dictée, création](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [mulmoclaude (receptron) — client Claude Code multi-modal](https://github.com/receptron/mulmoclaude) | GitHub Trending TS | #Claude |
| [Claude-Code-Agent-Monitor (hoangsonww) — dashboard de monitoring temps réel pour Claude Code avec analytics de session](https://github.com/hoangsonww/Claude-Code-Agent-Monitor) | GitHub Trending TS | #Claude |
| [compound-engineering-plugin (EveryInc) — plugin officiel "Compound Engineering" pour Claude Code, Codex, Cursor et autres](https://github.com/EveryInc/compound-engineering-plugin) | GitHub Trending TS | #Claude |

### 💡 Insights clés
- **L'écosystème d'outils tiers construits autour de Claude Code explose (gstack, mulmoclaude, Claude-Code-Agent-Monitor, compound-engineering-plugin tous dans le top trending TypeScript du jour)** — Pour H'appi : signal fort que Claude Code devient une plateforme à part entière avec son propre écosystème de plugins/monitoring, ce qui légitime de proposer du tooling Claude Code packagé (monitoring, plugins métier) comme service complémentaire aux chatbots livrés aux clients.
- **MinerU et llama_index confirment que la conversion de documents (PDF, Office) en contenu "LLM-ready" et l'indexation documentaire restent un besoin central des applications LLM** — Pour H'appi : ce pattern correspond directement aux chatbots de base de connaissance (FAQ, documentation interne) vendus aux clients PME — vérifier que le pipeline d'ingestion documentaire actuel s'appuie sur des briques équivalentes ou à défaut évaluer MinerU pour les documents PDF complexes.
- **voicebox (studio vocal IA open-source) et NVIDIA-NeMo/Speech (framework Voice AI scalable) confirment la dynamique d'outillage open-source autour de la Voice AI, en complément des entrants spécialisés (Sesame, AethexAI) déjà identifiés** — Pour H'appi : surveiller ces briques open-source comme alternative de coût pour les futurs projets Voice AI plutôt que de dépendre uniquement de fournisseurs propriétaires.
- **free-llm-api-resources reste en tête du trending Python, dans la continuité de freellmapi/litellm déjà identifiés hier** — confirme que la résilience multi-fournisseur LLM (fallback, quotas gratuits cumulés) est une tendance de fond et non un pic ponctuel ; à conserver dans l'architecture de référence H'appi.
- **Coupure réseau partielle des sources de veille (HackerNews, DEV.to, The New Stack bloqués par la politique d'environnement)** — à signaler : si ces blocages persistent demain, envisager une source de repli (ex. flux RSS via un proxy autorisé ou agrégateur alternatif) pour ne pas dépendre uniquement de GitHub Trending.

---
## 📰 Veille Tech — 2026-06-27
> Mis à jour automatiquement par Happi Brain Agent
> ⚠️ Pour le 2e jour consécutif, HackerNews, DEV.to et The New Stack RSS sont bloqués par la politique réseau de l'environnement (403 sur le proxy de sortie, y compris sur les endpoints de repli HN Algolia et thenewstack.io en direct) — veille basée uniquement sur GitHub Trending aujourd'hui.

| Article | Source | Tag |
|---------|--------|-----|
| [opendatalab/MinerU — reste en tête du trending Python : conversion PDF/Office complexes en markdown/JSON prêt pour workflows agentiques](https://github.com/opendatalab/MinerU) | GitHub Trending 🐍 | #LLM |
| [aws/agent-toolkit-for-aws — serveurs MCP, skills et plugins officiels AWS pour construire des agents IA sur l'infra AWS](https://github.com/aws/agent-toolkit-for-aws) | GitHub Trending 🐍 | #LLM #SaaS |
| [vllm-project/vllm — moteur d'inférence et de serving LLM à haut débit et économe en mémoire, de retour dans le trending Python](https://github.com/vllm-project/vllm) | GitHub Trending 🐍 | #LLM |
| [Panniantong/Agent-Reach — donne aux agents IA des capacités de navigation web pour rechercher et analyser Twitter, Reddit, YouTube, GitHub](https://github.com/Panniantong/Agent-Reach) | GitHub Trending 🐍 | #LLM #chatbot |
| [ZhuLinsen/daily_stock_analysis — système d'analyse boursière piloté par LLM avec données multi-sources et notifications automatisées](https://github.com/ZhuLinsen/daily_stock_analysis) | GitHub Trending 🐍 | #LLM #SaaS |
| [garrytan/gstack — setup Claude Code avec 23 outils opinionés, toujours en tête du trending TypeScript](https://github.com/garrytan/gstack) | GitHub Trending TS | #Claude #chatbot |
| [every-app/open-seo — alternative open-source aux plateformes SEO commerciales (Semrush, Ahrefs), toujours en tête du trending TypeScript](https://github.com/every-app/open-seo) | GitHub Trending TS | #SaaS |
| [stablyai/orca — environnement de développement d'agents pour exécuter des agents de code en parallèle sur desktop et mobile](https://github.com/stablyai/orca) | GitHub Trending TS | #LLM #chatbot |
| [anomalyco/opencode — agent de codage open-source](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #chatbot |

### 💡 Insights clés
- **MinerU et vllm dominent à nouveau le trending Python (3e jour pour MinerU, retour de vllm)** — Pour H'appi : confirme que l'ingestion documentaire LLM-ready (PDF/Office → markdown) et l'inférence LLM auto-hébergée à fort débit restent des briques d'infrastructure de référence ; vllm est à évaluer si H'appi envisage un jour de self-host un modèle open-weight en complément de Claude pour réduire les coûts d'inférence à fort volume.
- **aws/agent-toolkit-for-aws (serveurs MCP officiels AWS) signale que les grands clouders standardisent désormais l'agentic AI via MCP côté infrastructure, pas seulement côté IDE** — Pour H'appi : argument supplémentaire pour positionner les chatbots livrés comme compatibles MCP nativement, facilitant leur intégration future dans l'écosystème agentique des clients qui migrent vers ces toolkits cloud.
- **gstack et opencode confirment, pour le 2e jour, que l'écosystème d'outillage autour des agents de code (Claude Code et alternatives open-source) continue de s'étoffer** — Pour H'appi : tendance stable à suivre plutôt qu'un pic isolé ; pas d'action immédiate mais à recroiser avec une éventuelle offre de tooling packagé pour clients développeurs.
- **Agent-Reach et orca illustrent la montée des agents IA "actifs" (navigation web autonome, exécution parallèle de tâches) au-delà du simple chat conversationnel** — Pour H'appi : ce pattern d'agent qui exécute des actions multi-étapes de façon autonome est directement transposable aux chatbots SAV/secrétariat (ex. recherche d'info client en autonomie avant de répondre), à garder comme axe de différenciation produit.
- **Blocage réseau persistant pour le 2e jour consécutif (HackerNews, DEV.to, The New Stack, y compris les endpoints de repli testés) — recommandation : vérifier/ajuster la politique réseau de l'environnement de veille pour débloquer ces domaines, sinon la veille restera structurellement limitée à GitHub Trending.**

---
## 📰 Veille Tech — 2026-06-28
> Mis à jour automatiquement par Happi Brain Agent
> ⚠️ Pour le 3e jour consécutif, HackerNews, DEV.to et The New Stack RSS sont bloqués par la politique réseau de l'environnement (403, y compris sur les endpoints de repli HN Algolia et dev.to sans paramètre `per_page`) — veille basée uniquement sur GitHub Trending aujourd'hui.

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/skills — dépôt officiel Anthropic pour les Agent Skills, fait son entrée dans le trending Python](https://github.com/anthropics/skills) | GitHub Trending 🐍 | #Claude #LLM |
| [topoteretes/cognee — plateforme de mémoire IA open-source pour agents avec graphe de connaissances persistant](https://github.com/topoteretes/cognee) | GitHub Trending 🐍 | #LLM #chatbot |
| [moorcheh-ai/memanto — système de mémoire dédié aux agents IA](https://github.com/moorcheh-ai/memanto) | GitHub Trending 🐍 | #LLM #chatbot |
| [comet-ml/opik — plateforme de debug, évaluation et monitoring pour applications LLM et workflows agentiques](https://github.com/comet-ml/opik) | GitHub Trending 🐍 | #LLM #SaaS |
| [luongnv89/claude-howto — guide visuel de Claude Code, des fondamentaux au développement d'agents avancés](https://github.com/luongnv89/claude-howto) | GitHub Trending 🐍 | #Claude |
| [opendatalab/MinerU — toujours en tête du trending Python (4e jour), conversion PDF/Office en markdown/JSON prêt pour workflows agentiques](https://github.com/opendatalab/MinerU) | GitHub Trending 🐍 | #LLM |
| [aws/agent-toolkit-for-aws — serveurs MCP et skills officiels AWS, toujours présent (3e jour)](https://github.com/aws/agent-toolkit-for-aws) | GitHub Trending 🐍 | #LLM #SaaS |
| [CherryHQ/cherry-studio — studio de productivité IA avec chat intelligent et agents autonomes connectés aux LLM frontier](https://github.com/CherryHQ/cherry-studio) | GitHub Trending TS | #chatbot #LLM |
| [logto-io/logto — infrastructure d'authentification et d'autorisation pour SaaS et apps IA, basée sur OIDC/OAuth](https://github.com/logto-io/logto) | GitHub Trending TS | #SaaS |
| [TencentCloud/TencentDB-Agent-Memory — mémoire long-terme entièrement locale pour agents IA](https://github.com/TencentCloud/TencentDB-Agent-Memory) | GitHub Trending TS | #LLM #chatbot |
| [alibaba/page-agent — agent GUI in-page pilotant des interfaces web en langage naturel](https://github.com/alibaba/page-agent) | GitHub Trending TS | #LLM #chatbot |
| [garrytan/gstack — setup Claude Code avec 23 outils opinionés, toujours en tête du trending TypeScript (3e jour)](https://github.com/garrytan/gstack) | GitHub Trending TS | #Claude #chatbot |
| [anomalyco/opencode — agent de codage open-source, toujours présent (3e jour)](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM #chatbot |
| [tashfeenahmed/freellmapi — proxy compatible OpenAI mutualisant les quotas gratuits de 16 fournisseurs LLM](https://github.com/tashfeenahmed/freellmapi) | GitHub Trending TS | #LLM |

### 💡 Insights clés
- **Vague inédite de projets de "mémoire d'agent" persistante (cognee, memanto, TencentDB-Agent-Memory, et MemPalace hier) apparus simultanément dans le trending** — Pour H'appi : signal fort que la mémoire long-terme (contexte client, historique multi-session) devient une brique d'infrastructure standardisée pour les agents IA ; à évaluer comme amélioration produit pour les chatbots SAV/secrétariat qui doivent se souvenir des clients récurrents sans tout repasser par le prompt à chaque session.
- **anthropics/skills entre directement dans le trending Python — Anthropic structure officiellement le concept d'"Agent Skills"** — Pour H'appi : à surveiller en priorité puisque les chatbots H'appi sont construits sur Claude ; les Skills pourraient devenir un format standard pour packager des compétences métier réutilisables (ex. un "skill" de prise de RDV ou de FAQ produit) plutôt que des prompts ad hoc.
- **comet-ml/opik (observabilité/évaluation LLM) confirme la maturation de l'outillage LLMOps autour du monitoring qualité** — Pour H'appi : pertinent pour suivre en production la qualité des réponses des chatbots livrés aux clients (dérive de réponse, hallucinations) ; à évaluer comme brique de monitoring interne.
- **logto-io/logto positionne l'auth comme infrastructure partagée SaaS + IA (OIDC/OAuth)** — Pour H'appi : à garder en tête pour la partie back-office/auth des futurs chatbots SaaS multi-clients nécessitant une gestion d'identité robuste.
- **MinerU (4e jour), aws/agent-toolkit-for-aws, gstack et opencode (3e jour) confirment des tendances de fond plutôt que des pics isolés** — pas d'action immédiate, mais à recroiser avec la roadmap produit (ingestion documentaire, compatibilité MCP, tooling Claude Code).
- **Blocage réseau persistant pour le 3e jour consécutif (HackerNews, DEV.to, The New Stack) — la veille reste structurellement limitée à GitHub Trending ; recommandation maintenue de débloquer ces domaines dans la politique réseau de l'environnement.**

---
---

---
## 📰 Veille Tech — 2026-07-01
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Tag : Anthropic intègre Claude dans Slack comme coéquipier permanent — Karpathy y voit "la 3e révolution UX des LLM"](https://quasa.io/media/claude-tag-anthropic-turns-ai-into-a-persistent-teammate-in-slack-and-andrej-karpathy-calls-it-the-third-major-llm-ux-revolution) | Web | #Claude #chatbot |
| [Nouvelle Constitution de Claude publiée par Anthropic — valeurs et comportements fondamentaux documentés](https://www.anthropic.com/news/claude-new-constitution) | Anthropic | #Claude #LLM |
| [Californie × Anthropic : Claude disponible aux agences d'État à -50%, formation gratuite des agents publics](https://www.bloomberg.com/news/articles/2026-05-07/anthropic-is-making-claude-chatbot-more-appealing-to-consumers) | Bloomberg | #Claude #SaaS |
| [FastAPI vs Next.js : quel backend pour un AI SaaS en 2026 ? — comparaison de référence](https://hassanr.com/blogs/fastapi-vs-nextjs-ai-saas-backend-2026.html) | hassanr.com | #FastAPI #Next.js #SaaS |
| [J'ai construit un AI SaaS avec Next.js, FastAPI et Dokploy — retour d'expérience production](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #Next.js #SaaS |
| [TypeScript devient le langage n°1 sur GitHub — l'IA en est le moteur principal](https://github.blog/news-insights/octoverse/octoverse-a-new-developer-joins-github-every-second-as-ai-leads-typescript-to-1/) | GitHub Blog | #LLM #SaaS |
| [SpaceXAI Voice APIs désormais dans Vercel AI Gateway — latence sub-seconde via WebSocket](https://www.basenor.com/blogs/news/spacexai-voice-apis-now-in-vercel-ai-gateway-7-things-to-know) | basenor.com | #VoiceAI #Vercel |
| [Construire un chatbot IA en 15 min avec Vercel AI SDK [2026] — guide Next.js streaming](https://tech-insider.org/vercel-ai-sdk-tutorial-chatbot-nextjs-2026/) | tech-insider.org | #chatbot #Vercel #Next.js |
| [Docker + Vercel AI SDK : déployer des agents Chat UI en containers production-ready](https://www.docker.com/blog/launch-chat-ui-agent-docker-vercel-ai-sdk/) | Docker Blog | #Docker #chatbot |
| [Déployer un AI Chatbot avec streaming SSE sur Railway — guide officiel](https://docs.railway.com/guides/ai-chatbot-streaming) | Railway Docs | #Railway #chatbot |
| [Railway vs Vercel : comparaison technique 2026 et guide de migration](https://docs.railway.com/platform/compare-to-vercel) | Railway Docs | #Railway #Vercel |
| [AI Act : application complète le 2 août 2026 — sanctions jusqu'à 20M€ ou 4% CA mondial](https://www.leto.legal/guides/ai-act-conformite) | leto.legal | #RGPD |
| [Chatbot IA et RGPD : Guide de Conformité 2026 — obligations CNIL pour chatbots](https://heeya.fr/blog/chatbot-rgpd-guide-conformite-cnil) | Heeya | #chatbot #RGPD |
| [awesome-ai-agents-2026 : 300+ agents IA, frameworks et outils recensés](https://github.com/ARUNAGIRINATHAN-K/awesome-ai-agents-2026) | GitHub | #LLM #chatbot |

### 💡 Insights clés
- **Claude Tag fait entrer Claude dans les workflows d'équipe asynchrones (Slack) en tant que membre permanent avec mémoire org-wide** — Pour H'appi : signal fort que Claude devient une infrastructure d'équipe, pas seulement un chatbot client. À positionner comme argument commercial pour les offres de secrétariat IA et chatbot interne, où l'intégration Slack est une attente croissante des PME françaises.
- **L'AI Act entre en application complète le 2 août 2026 — fenêtre de 32 jours pour se mettre en conformité** — Pour H'appi : les chatbots livrés aux clients doivent afficher explicitement l'interaction avec une IA (message d'accueil) et avoir une DPA signée. Avantage concurrentiel majeur si H'appi propose une checklist de conformité AI Act + RGPD clé en main en tant qu'argument commercial différenciant.
- **L'architecture FastAPI + Next.js est confirmée comme le standard de référence pour l'AI SaaS production en 2026** — Pour H'appi : la stack de référence H'appi est parfaitement alignée avec les meilleures pratiques du marché. L'émergence de Dokploy (alternatif à Railway/Vercel) mérite une évaluation rapide pour réduire les coûts d'hébergement client.
- **Voice AI sub-seconde intégrée directement dans Vercel AI Gateway via WebSocket** — Pour H'appi : la stack voix Vapi.ai/ElevenLabs/Deepgram existante pourrait être concurrencée par des solutions natives Next.js/Vercel d'ici 6-12 mois. À suivre pour simplifier potentiellement la stack voix et réduire le nombre de fournisseurs tiers.
- **TypeScript dépasse Python comme langage n°1 sur GitHub, porté par l'explosion des projets IA** — Tendance de fond qui confirme le bon choix de Next.js/TypeScript côté frontend et renforce la pertinence de la stack hybride Python (FastAPI) + TypeScript (Next.js) adoptée par H'appi.

---
## 📰 Veille Tech — 2026-07-02
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 5 lancé — modèle le plus agentique, contexte 1M tokens, default sur Claude Code, tarif promo $2/$10/Mtok jusqu'au 31 août](https://releasebot.io/updates/anthropic/claude) | Anthropic | #Claude #LLM |
| [Trump Administration lève les restrictions sur Claude Fable 5 & Mythos 5 — accès élargi aux modèles frontier Anthropic](https://www.washingtonpost.com/business/2026/07/01/anthropic-fable-mythos-trump-claude/466d3a52-755c-11f1-b665-5f8be87f3787_story.html) | Washington Post | #Claude |
| [Claude disponible sur Microsoft Azure Foundry — accès enterprise natif avec data residency US et gouvernance Azure](https://aiweekly.co/ai-news-today/anthropic-news) | AI Weekly | #Claude #SaaS |
| [State of AI Agents (LangChain) : 57% des équipes ont des agents en production, observabilité à 89%, EU AI Act cité comme risque n°1](https://www.langchain.com/state-of-agent-engineering) | LangChain | #LLM #SaaS |
| [Deepgram — Top Voice AI Agents Buyer's Guide 2026 : 11 plateformes comparées (Vapi, ElevenLabs, Retell AI...)](https://deepgram.com/learn/best-voice-ai-agents-2026-buyers-guide) | Deepgram | #VoiceAI |
| [Vapi vs ElevenLabs 2026 — quelle plateforme Voice AI pour construire des agents vocaux en production ?](https://www.retellai.com/blog/vapi-vs-elevenlabs) | Retell AI | #VoiceAI |
| [OmniRoute — gateway IA gratuit unifiant 231+ providers (50+ gratuits), connecte Claude Code, Cursor, Cline sur un seul endpoint OpenAI-compatible](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #chatbot |
| [langchain-ai/deepagents — harness d'agents IA "batteries-included" (25k+ stars, trending Python)](https://github.com/langchain-ai/deepagents) | GitHub Trending 🐍 | #LLM #chatbot |
| [google/agents-cli — CLI officiel Google Cloud pour créer, évaluer et déployer des agents IA sur Google Cloud](https://github.com/google/agents-cli) | GitHub Trending 🐍 | #LLM |
| [vstorm-co/full-stack-ai-agent-template — template FastAPI + Next.js avec RAG, streaming, auth et 20+ intégrations prêt production](https://github.com/vstorm-co/full-stack-ai-agent-template) | GitHub | #FastAPI #Next.js #LLM |
| [Railway — les meilleures plateformes pour déployer des apps IA en 2026 : Redis + Postgres intégrés, timeouts longs pour inference](https://blog.railway.com/p/best-platforms-deploy-ai-apps-2026) | Railway Blog | #Railway #chatbot |
| [Northflank : Railway vs Cloudflare vs Vercel 2026 — quel cloud pour quelle stack IA en production ?](https://northflank.com/blog/railway-vs-cloudflare-vs-vercel) | Northflank | #Railway #Vercel |
| [AI Act : application complète le 2 août 2026 — sanctions jusqu'à 35M€ ou 7% CA pour IA interdites, 7,5M€ pour manquements de transparence](https://www.leto.legal/guides/ai-act-conformite) | leto.legal | #RGPD |
| [CNIL : recommandations officielles pour développer des systèmes IA conformes RGPD — checklist pratique](https://www.cnil.fr/fr/developpement-des-systemes-dia-les-recommandations-de-la-cnil-pour-respecter-le-rgpd) | CNIL | #RGPD |

### 💡 Insights clés
- **Claude Sonnet 5 devient le modèle agentique de référence avec contexte 1M tokens à 40-60% moins cher qu'Opus 4.8** — Pour H'appi : migration recommandée pour les chatbots en production ; le contexte 1M tokens permet d'ingérer de larges bases documentaires clients sans découpage RAG complexe, réduisant latence et complexité d'implémentation.
- **URGENCE — AI Act en application complète dans 31 jours (2 août 2026)** — Pour H'appi : fenêtre critique pour s'assurer que chaque chatbot livré affiche explicitement l'interaction avec une IA dès l'accueil, que les DPA clients sont signées et que la politique de rétention des données est documentée. Argument commercial fort : proposer une checklist conformité AI Act + RGPD clé en main différencie H'appi face aux agences qui ignorent ces obligations.
- **57% des entreprises ont des agents IA en production (LangChain) — l'observabilité adoptée par 89% devient une attente standard** — Pour H'appi : les clients matures vont demander des dashboards de monitoring qualité des réponses. À anticiper avec comet-ml/opik ou une brique LLMOps légère dans les prochains projets.
- **OmniRoute unifie 231+ providers LLM derrière un endpoint OpenAI-compatible** — Pour H'appi : solution de résilience pour les chatbots critiques — permet de basculer Claude → GPT → Gemini en cas de panne ou dépassement de quota sans refactoring backend. À évaluer comme couche de routing dans la stack de référence.
- **Vapi reste le choix n°1 pour l'orchestration voix full-stack en 2026, avec Claude désormais supporté comme LLM swappable dans le pipeline** — Confirmation que la stack H'appi (Vapi + Claude + ElevenLabs/Deepgram) est parfaitement alignée avec le marché. ElevenLabs Flash v2.5 atteint une latence sub-100ms — à tester pour améliorer la fluidité des chatbots vocaux existants.
- **Railway recommandé sur Vercel pour les apps IA avec inference longue** — Pour H'appi : les timeouts serverless Vercel (max 300s) sont incompatibles avec les agents multi-steps ou les inférences lentes. Railway avec Postgres + Redis intégrés reste le meilleur choix pour les chatbots avec historique de conversation persistant en production.
- **Blocage réseau persistant (HackerNews, DEV.to, The New Stack) — 4e jour consécutif** — La veille reste structurellement limitée à GitHub Trending + WebSearch. Recommandation maintenue de débloquer ces domaines dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-03
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Science lancé — workbench IA pour chercheurs avec 60+ connecteurs (génomique, protéomique, cheminformatique), beta Claude Pro/Team/Enterprise](https://www.anthropic.com/news/claude-science-ai-workbench) | Anthropic | #Claude #LLM |
| [Fable 5 de retour globalement — export controls levées le 1er juillet, disponible sur Claude.ai, Claude Code et Claude Cowork](https://9to5google.com/2026/07/01/anthropic-fable-5-returns-to-claude/) | 9to5Google | #Claude |
| [Claude Apps Gateway pour Amazon Bedrock & Google Cloud — SSO entreprise, RBAC, cost tracking et spend caps pour Claude Code](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude #SaaS |
| [AI Act Article 50 — deadline Code of Practice 22 juillet passée, amendes jusqu'à 15M€ ou 3% CA mondiale actives dès le 2 août](https://www.techtimes.com/articles/318822/20260622/eu-ai-act-chatbot-disclosure-deepfake-labeling-july-22-signatory-deadline.htm) | TechTimes | #RGPD |
| [EU AI Act & Chatbots : Guide de Conformité 2026 — obligation disclosure Article 50, marquage AI-Generated Content reporté au 2 décembre (Digital Omnibus)](https://heeya.fr/en/blog/eu-ai-act-chatbot-compliance-2026) | Heeya | #chatbot #RGPD |
| [Vapi vs ElevenLabs 2026 — Vapi traite 62M appels/mois (SLA 99.99%), ElevenLabs ajoute full conversational avec 96 langues et latence sub-300ms](https://www.retellai.com/blog/vapi-vs-elevenlabs) | Retell AI | #VoiceAI |
| [Vercel Sandbox peut désormais exécuter des containers Docker — agents buildent des images sans toucher l'hôte](https://vercel.com/changelog/run-docker-containers-inside-vercel-sandbox) | Vercel | #Docker #Vercel |
| [Railway — Deploy Next.js + AI SDK : template streaming + scale-to-zero + Postgres managé en réseau privé](https://railway.com/deploy/nextjs-ai-sdk) | Railway | #Railway #Next.js |
| [MLflow — Building Production-Ready AI Agents in 2026 : patterns d'architecture, evals, observabilité](https://mlflow.org/articles/building-production-ready-ai-agents-in-2026/) | MLflow | #LLM |
| [O'Reilly — The AI Agents Stack 2026 Edition : MCP comme standard de protocole, 57% des équipes en production](https://www.oreilly.com/radar/the-ai-agents-stack-2026-edition/) | O'Reilly | #LLM #chatbot |
| [browser-use/video-use (🔥 +554 stars) — éditer des vidéos avec des coding agents Python](https://github.com/browser-use/video-use) | GitHub Trending 🐍 | #LLM |
| [usestrix/strix (🔥 +2137 stars) — outil open-source de pen-testing IA pour détecter les vulnérabilités applicatives](https://github.com/usestrix/strix) | GitHub Trending 🐍 | #LLM |
| [logto-io/logto (🔥 +361 stars) — auth & authorization open-source pour apps SaaS et IA, multi-tenant](https://github.com/logto-io/logto) | GitHub Trending TS | #SaaS |
| [firecrawl (🔥 +535 stars) — API pour search, scrape et interaction web à grande échelle pour agents IA](https://github.com/firecrawl/firecrawl) | GitHub Trending TS | #LLM #chatbot |

### 💡 Insights clés
- **Claude Science inaugure le modèle "workbench vertical spécialisé" — IA pré-configurée par domaine métier avec des connecteurs sectoriels** — Pour H'appi : ce pattern est directement transposable aux PME françaises. Prochaine opportunité commerciale : chatbots "métier pré-connectés" (RH, juridique, supply chain) avec des intégrations sectorielles pré-configurées (Sage, Cegid, SAP B1) comme argument différenciant face aux chatbots génériques.
- **URGENCE AI Act J-30 — Article 50 actif le 2 août, marquage contenu IA reporté au 2 décembre (Digital Omnibus)** — Pour H'appi : action immédiate requise — chaque chatbot livré doit afficher dès la première interaction "Vous interagissez avec une IA". La bonne nouvelle : le marquage AI-generated content (deepfakes, textes synthétiques) est reporté à décembre, réduisant la charge de conformité immédiate. Priorité : mettre à jour les templates d'onboarding de tous les bots en production.
- **Fable 5 accessible globalement sans restriction depuis le 1er juillet** — Pour H'appi : le modèle frontier Anthropic le plus puissant est maintenant proposable aux clients Enterprise français pour des cas d'usage de raisonnement complexe, d'analyse de contrats ou de traitement de grandes bases documentaires (contexte 2M tokens).
- **Vercel Sandbox + Docker : les agents peuvent maintenant builder et tester des containers sans infra dédiée** — Pour H'appi : simplification du workflow de démonstration client. Les prototypes de chatbots conteneurisés peuvent être buildés et testés directement dans l'environnement de staging Vercel, sans besoin d'un VPS Railway dédié pour les phases de démo.
- **Vapi (62M appels/mois) + ElevenLabs sub-300ms conversationnel confirment la maturité de la stack voix H'appi** — ElevenLabs Conversational AI devient une alternative sérieuse à la stack 3 couches actuelle (Vapi + ElevenLabs + Deepgram) pour les cas d'usage simples : 1 seul provider, 96 langues, clonage vocal 30 secondes. À évaluer pour les prochains mandats voice AI afin de réduire les coûts d'intégration.

---
## 📰 Veille Tech — 2026-07-04
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 5 lancé — modèle le plus agentique d'Anthropic, contexte 1M tokens, $2/$10/Mtok promo jusqu'au 31 août](https://techcrunch.com/2026/06/30/anthropic-launches-claude-sonnet-5-as-a-cheaper-way-to-run-agents/) | TechCrunch | #Claude #LLM |
| [Claude reçoit une nouvelle Constitution — Anthropic publie sa charte de valeurs et principes directeurs du modèle](https://www.anthropic.com/news/claude-new-constitution) | Anthropic | #Claude |
| [langflow-ai/langflow (🔥 +531 stars) — outil low-code pour builder et déployer des agents IA et workflows en production](https://github.com/langflow-ai/langflow) | GitHub Trending 🐍 | #LLM #chatbot |
| [huggingface/speech-to-speech (🔥 +162 stars) — framework open-source pour agents vocaux locaux avec modèles open-source](https://github.com/huggingface/speech-to-speech) | GitHub Trending 🐍 | #VoiceAI |
| [alibaba/page-agent (🔥 +1110 stars) — GUI agent JavaScript pour contrôler des interfaces web en langage naturel](https://github.com/alibaba/page-agent) | GitHub Trending TS | #LLM |
| [stablyai/orca (🔥 +703 stars) — ADE (Agent Development Environment) pour orchestrer une flotte d'agents parallèles](https://github.com/stablyai/orca) | GitHub Trending TS | #LLM |
| [facebook/astryx (🔥 +885 stars) — design system open-source entièrement personnalisable et "agent-ready"](https://github.com/facebook/astryx) | GitHub Trending TS | #chatbot #LLM |
| [DEV.to — How I built an AI SaaS with Next.js, FastAPI and Dokploy — retour d'expérience complet en production](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #Next.js #SaaS |
| [DEV.to — FastAPI + Next.js 15 : The Full-Stack Nobody's Building — guide architecture pour IA SaaS scalable](https://dev.to/alexmayhew-dev/fastapi-nextjs-15-the-full-stack-nobodys-building-1hl9) | DEV.to | #FastAPI #Next.js |
| [Vapi valorisé $500M après avoir remporté Amazon Ring face à 40 concurrents — validation marché Voice AI](https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/) | TechCrunch | #VoiceAI |
| [ElevenLabs 2026 : de générateur TTS à stack audio complète — création, conversation, enterprise controls](https://blog.mean.ceo/elevenlabs-news-july-2026/) | Mean CEO Blog | #VoiceAI |
| [Chatbot IA et RGPD 2026 — Guide de conformité CNIL : obligations Article 50 AI Act, checklist pratique](https://heeya.fr/blog/chatbot-rgpd-guide-conformite-cnil) | Heeya | #chatbot #RGPD |
| [Railway vs Vercel pour apps IA 2026 — Railway recommandé pour backends IA (timeouts longs, Postgres/Redis privés)](https://docs.railway.com/platform/compare-to-vercel) | Railway Docs | #Railway #Vercel |

### 💡 Insights clés
- **URGENT — Claude Sonnet 5 à $2/$10/Mtok promo jusqu'au 31 août, puis $3/$15** — Pour H'appi : migrer les chatbots en production depuis Sonnet 4.6 maintenant = économies immédiates + meilleure performance agentique. Le contexte 1M tokens supprime le besoin de chunking RAG complexe pour la plupart des bases documentaires clients (manuels, FAQs, catalogues). Deadline promo : 27 jours.
- **La guerre IA bascule du chat vers les agents** (TechCrunch/TechRadar) — les 3 leaders (OpenAI, Google, Anthropic) positionnent tous leurs modèles sur l'agentique autonome. Pour H'appi : mettre à jour les pitchs commerciaux de "chatbot intelligent" vers "agent IA autonome" — les prospects PME comprennent mieux la valeur quand on parle d'automatisation d'actions vs simple Q&A.
- **Vapi $500M après Amazon Ring — validation marché Voice AI irréfutable** — Pour H'appi : argument commercial fort pour les prospects hésitants sur le Voice AI. Si Amazon Ring (millions d'utilisateurs) a choisi Vapi face à 40 alternatives, la plateforme est enterprise-ready. Réutiliser cette référence dans les devis Voice AI.
- **AI Act J-29 — Article 50 actif le 2 août, deadline critique** — Pour H'appi : chaque chatbot livré ou en cours doit afficher "Vous interagissez avec une IA" dès la première interaction. La checklist Heeya/CNIL est un outil concret pour auditer rapidement les bots en production. Transformer cette contrainte en argument commercial : proposer un audit conformité AI Act + RGPD inclus dans chaque livraison.
- **alibaba/page-agent (+1110 stars/jour) : les GUI agents browser-native explosent** — Pour H'appi : signal fort que les prochains mandats incluront des agents capables de naviguer des interfaces web métier (ERP, CRM legacy) sans API dédiée. À intégrer dans la roadmap produit pour proposer des automatisations "browser-native" complémentaires aux chatbots conversationnels.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 5e jour consécutif** — Veille limitée à GitHub Trending + WebSearch. Recommandation maintenue de débloquer ces domaines dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-05
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Science Beta — workbench multi-agents pour scientifiques : coordinating agent → sub-agents spécialisés → reviewer agent](https://www.anthropic.com/news/claude-science-ai-workbench) | Anthropic | #Claude #LLM |
| [Claude Fable 5 restauré mondialement au 1er juillet + framework industrie de scoring jailbreak (Anthropic/Amazon/Microsoft/Google)](https://releasebot.io/updates/anthropic/claude) | Releasebot | #Claude |
| [Claude Enterprise — spend alerts, model-level entitlements, analytics admin avancées](https://blog.mean.ceo/anthropic-claude-news-july-2026/) | Mean CEO Blog | #Claude #SaaS |
| [AI Act application COMPLÈTE le 2 août 2026 — chatbots = risque limité, obligation de transparence totale (Article 50)](https://www.leto.legal/guides/ai-act-conformite) | Leto Legal | #chatbot #RGPD |
| [ElevenLabs juillet 2026 — sendMultimodalMessage (images pendant les calls), audio_duration_secs, recording_quality](https://releasebot.io/updates/eleven-labs) | Releasebot | #VoiceAI |
| [Vapi — 62M appels/mois, 99,99% SLA, $0.05/min orchestration + 14 providers](https://www.retellai.com/blog/vapi-vs-elevenlabs) | Retell AI | #VoiceAI |
| [Railway PostgreSQL 18 HA Cluster AI-ready — pgvector natif, pg_cron, PostGIS, failover auto](https://railway.com/deploy/postgresql-18-ha-cluster-ai-and-gis-read) | Railway | #Railway #PostgreSQL |
| [FastAPI vs Next.js pour AI SaaS 2026 — FastAPI gagne sur les pipelines IA longs, Next.js sur le DX full-stack](https://hassanr.com/blogs/fastapi-vs-nextjs-ai-saas-backend-2026.html) | Hassan Raza | #FastAPI #Next.js #SaaS |
| [Vercel AI SDK 6.0 — couche API unifiée pour 25+ providers IA (switch en 2 lignes)](https://tech-insider.org/vercel-ai-sdk-tutorial-chatbot-nextjs-2026/) | Tech Insider | #Vercel #chatbot |
| [anthropics/claude-code (🔥 +357 stars) — outil agentique de coding en terminal, comprend le codebase](https://github.com/anthropics/claude-code) | GitHub Trending 🐍 | #Claude |
| [google/adk-python — toolkit Python code-first pour builder, évaluer et déployer des agents IA sophistiqués](https://github.com/google/adk-python) | GitHub Trending 🐍 | #LLM |
| [huggingface/speech-to-speech (🔥 +118 stars) — framework local pour agents vocaux open-source](https://github.com/huggingface/speech-to-speech) | GitHub Trending 🐍 | #VoiceAI |
| [alibaba/page-agent (🔥 +742 stars) — GUI agent JavaScript, contrôle d'interfaces web en langage naturel](https://github.com/alibaba/page-agent) | GitHub Trending TS | #LLM #chatbot |
| [ruvnet/ruflo (🔥 +145 stars) — swarms multi-agents avec mémoire adaptative et intégration RAG](https://github.com/ruvnet/ruflo) | GitHub Trending TS | #LLM |
| [facebook/astryx (🔥 +903 stars) — design system "agent-ready" open-source entièrement personnalisable](https://github.com/facebook/astryx) | GitHub Trending TS | #chatbot #LLM |

### 💡 Insights clés
- **Claude Science = architecture multi-agents de référence pour H'appi** — La structure coordinating agent → domain sub-agents spécialisés → reviewer agent (lancée par Anthropic le 1er juillet) est exactement le pattern à adopter pour les chatbots complexes multi-domaines (ex : bot support avec modules facturation, technique, commercial). Documenter ce pattern dans les best practices H'appi et le proposer comme upgrade aux clients existants.
- **AI Act J-28 : application TOTALE le 2 août — deadline non-négociable** — Contrairement aux phases précédentes, l'Article 50 oblige désormais TOUT chatbot (même à risque limité) à déclarer explicitement "Vous interagissez avec une IA" dès la première interaction. Sanctions jusqu'à 7,5M€ / 1% CA pour manquement de transparence. Pour H'appi : auditer en urgence tous les bots en production, transformer l'obligation en argument commercial ("conformité AI Act + RGPD incluse dans chaque livraison H'appi").
- **ElevenLabs multimodal : les agents vocaux deviennent visuels** — Le nouveau hook sendMultimodalMessage permet d'envoyer des images pendant un appel conversationnel. Pour H'appi : anticiper les mandats "voice + vision" dès maintenant (ex : agent support client qui analyse une photo du produit défectueux pendant l'appel vocal). Avantage concurrentiel fort sur les agences qui proposent encore du voice-only.
- **Railway PostgreSQL 18 + pgvector natif = stack RAG simplifiée** — Plus besoin d'un vector store séparé (Pinecone, Weaviate) pour les projets RAG déployés sur Railway. pgvector + pg_cron pour les refresh d'embeddings + failover HA = production-ready. Pour H'appi : adopter Railway PostgreSQL 18 comme stack par défaut pour tous les nouveaux projets chatbot avec RAG.
- **alibaba/page-agent +742 stars/jour (2e jour consécutif en trending TS)** — Les GUI agents browser-native s'imposent comme la prochaine vague après les chatbots. Signal fort pour H'appi : positionner une offre "automatisation d'interface métier" (ERP, CRM legacy sans API) en tier supérieur des mandats. Différenciation vs simple chatbot Q&A.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 6e jour consécutif** — Veille limitée à GitHub Trending + WebSearch. Recommandation maintenue de débloquer ces domaines dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-06
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [bradautomates/claude-video (🔥 +368 stars) — Claude peut regarder n'importe quelle vidéo : extraction de frames + transcription](https://github.com/bradautomates/claude-video) | GitHub Trending 🐍 | #Claude #LLM |
| [alirezarezvani/claude-skills (🔥 +392 stars) — 330+ skills et 30+ agents prêts à l'emploi pour Claude Code](https://github.com/alirezarezvani/claude-skills) | GitHub Trending 🐍 | #Claude |
| [anthropics/claude-code (🔥 +156 stars) — outil agentique de coding en terminal, comprend le codebase complet](https://github.com/anthropics/claude-code) | GitHub Trending 🐍 | #Claude |
| [hesreallyhim/awesome-claude-code (🔥 +148 stars) — collection curatée de ressources, skills et plugins pour Claude Code](https://github.com/hesreallyhim/awesome-claude-code) | GitHub Trending 🐍 | #Claude |
| [usestrix/strix (🔥 +1 114 stars) — outil open-source de pentest IA pour trouver et corriger les vulnérabilités app](https://github.com/usestrix/strix) | GitHub Trending 🐍 | #SaaS #LLM |
| [TauricResearch/TradingAgents (🔥 +257 stars) — framework multi-agents LLM pour le trading financier autonome](https://github.com/TauricResearch/TradingAgents) | GitHub Trending 🐍 | #LLM |
| [huggingface/speech-to-speech (🔥 +78 stars) — agents vocaux locaux open-source avec modèles HuggingFace](https://github.com/huggingface/speech-to-speech) | GitHub Trending 🐍 | #VoiceAI |
| [alibaba/page-agent (🔥 +805 stars — 3e jour consécutif) — GUI agent JavaScript, contrôle d'interfaces web en langage naturel](https://github.com/alibaba/page-agent) | GitHub Trending TS | #LLM #chatbot |
| [diegosouzapw/OmniRoute (🔥 +475 stars) — AI gateway multi-provider LLM avec token optimization et smart fallback](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #SaaS |
| [ChromeDevTools/chrome-devtools-mcp (🔥 +252 stars) — Chrome DevTools exposé comme outil MCP pour les coding agents](https://github.com/ChromeDevTools/chrome-devtools-mcp) | GitHub Trending TS | #LLM |
| [can1357/oh-my-pi (🔥 +155 stars) — agent IA coding terminal : edits hash-anchorés, LSP, Python, browser, subagents](https://github.com/can1357/oh-my-pi) | GitHub Trending TS | #LLM |

### 💡 Insights clés
- **bradautomates/claude-video : Claude "regarde" désormais les vidéos** — Extraction de frames + transcription ouvre un segment inédit pour H'appi : bots support qui analysent une vidéo de panne envoyée par l'utilisateur, bots formation qui répondent à partir de tutoriels vidéo clients, agents QA visuel. À intégrer dans la roadmap comme use-case premium multimodal.
- **alirezarezvani/claude-skills +392 stars : bibliothèque de 330+ skills Claude standardisée** — Source directe de composants réutilisables pour accélérer les développements H'appi. Plus besoin de coder from scratch les skills courants (recherche web, reformatting, génération de rapports). À auditer et intégrer dans le kit de développement interne.
- **alibaba/page-agent 3e jour consécutif trending (+805 stars/jour)** — La tendance GUI agents se confirme définitivement. Pour H'appi : le pitch "agent IA qui navigue vos outils métier (ERP, CRM legacy) sans API" est maintenant validé par le marché. À positionner comme offre premium distincte du chatbot conversationnel. Préparer une démo-concept pour les prochains pitchs.
- **diegosouzapw/OmniRoute +475 stars : AI gateway multi-LLM avec smart fallback** — Pour H'appi : adopter une couche de routing IA sur les projets clients = fallback automatique si Anthropic/Claude est indisponible + optimisation des coûts (modèle léger pour classification, modèle puissant pour génération). Infrastructure de résilience à intégrer dans l'architecture standard.
- **usestrix/strix +1 114 stars : pentest IA automatisé open-source** — Signal fort : la sécurité des apps IA devient mainstream. Pour H'appi : utiliser cet outil pour auditer les chatbots avant livraison et en faire un argument commercial : "chatbot H'appi audité par outils de sécurité IA spécialisés — conformité AI Act + RGPD garantie".
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack, Anthropic, Vercel, Railway) — 7e jour consécutif** — Veille limitée à GitHub Trending uniquement. Recommandation maintenue de débloquer ces domaines dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-07
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 5 lancé — modèle le plus agentique, proche d'Opus 4.8, prix réduit jusqu'au 31/08](https://www.anthropic.com/news) | Anthropic | #Claude #LLM |
| [Claude Tag — Claude intégré dans Slack comme coéquipier persistant (Karpathy : "3e révolution LLM UX")](https://quasa.io/media/claude-tag-anthropic-turns-ai-into-a-persistent-teammate-in-slack-and-andrej-karpathy-calls-it-the-third-major-llm-ux-revolution) | WebSearch | #Claude #chatbot |
| [Anthropic dépasse OpenAI : devient la startup IA la plus valorisée au monde](https://news.ycombinator.com/item?id=48336233) | HackerNews | #Claude #LLM |
| [AI Act Art. 50 : obligation légale de déclarer l'IA aux utilisateurs dès le 2 août 2026](https://www.levanteapp.com/blog/chatbots-rgpd-2026) | WebSearch | #RGPD |
| [Voice AI 2026 : latence < 300ms atteinte, 42 % des entreprises déploient des agents vocaux](https://flowful.ai/blog/voice-agents-2026/) | WebSearch | #VoiceAI |
| [Guide GDPR Voice Agents B2B 2026 : conformité des agents vocaux IA (DACH)](https://ainora.lt/blog/ai-voice-agent-gdpr-compliance-guide) | WebSearch | #VoiceAI #RGPD |
| [How I built an AI SaaS with Next.js, FastAPI, and Dokploy (alternative open-source à Railway/Heroku)](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #Next.js #SaaS #Docker |
| [Micro-SaaS Hosting 2026 : Vercel vs Railway vs Render vs Fly.io — comparatif complet](https://f3fundit.com/micro-saas-hosting-infrastructure-vercel-vs-railway-vs-render-vs-fly-io-2026/) | WebSearch | #SaaS #Vercel #Railway |
| [firecrawl/firecrawl (🔥 +867 stars) — API de scraping web at scale pour alimenter les LLMs](https://github.com/firecrawl/firecrawl) | GitHub Trending TS | #LLM #SaaS |
| [diegosouzapw/OmniRoute (🔥 +749 stars) — AI gateway 231+ providers, token compression, smart fallback](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #SaaS |
| [karakeep-app/karakeep (🔥 +199 stars) — bookmark app self-hostable avec auto-tagging IA](https://github.com/karakeep-app/karakeep) | GitHub Trending TS | #SaaS #LLM |
| [mvanhorn/last30days-skill — outil IA de recherche cross-platform : Reddit, X, YouTube, HN](https://github.com/mvanhorn/last30days-skill) | GitHub Trending 🐍 | #LLM #chatbot |
| [CVE-2026-42271 : RCE non authentifié dans LiteLLM AI Gateway via endpoints MCP (CISA KEV)](https://thehackernews.com/2026/05/we-scanned-1-million-exposed-ai.html) | The Hacker News | #LLM |

### 💡 Insights clés
- **Claude Sonnet 5 — migration immédiate recommandée pour H'appi** — Lancé le 30 juin, le modèle est agentique au niveau Opus 4.8 précédent, avec tarif réduit jusqu'au 31/08. À adopter comme modèle par défaut sur tous les projets. Tester les capacités autonomes (planification, outils, navigation) pour les mandats complexes — c'est le standard que les clients vont comparer.
- **Claude Tag Slack : nouvel angle commercial pour les offres Enterprise H'appi** — Anthropic positionne Claude comme coéquipier async persistant dans les flux Slack d'équipe. Pour H'appi : développer une offre "chatbot d'équipe Slack natif" en tier Enterprise. Karpathy appelle ça la "3e révolution UX des LLMs" — les DSI corporate vont le demander dans les 3 mois.
- **AI Act Art. 50 applicable le 2 août 2026 — action urgente** — Tous les chatbots H'appi doivent afficher une mention claire "Vous interagissez avec une IA" avant cette date. Fines réelles constatées : 30K€ (telecom) et 80K€ (clinique). Action immédiate : ajouter ce disclaimer dans le kit de déploiement standard et l'argument "conformité AI Act certifiée" dans les pitchs commerciaux.
- **firecrawl/firecrawl +867 stars : signal fort pour les projets RAG H'appi** — L'API de scraping web à grande échelle pour alimenter les LLMs est en explosion. À intégrer dans les chatbots RAG nécessitant des données web temps réel (veille produits, FAQ dynamiques, données concurrentielles). Remplace des solutions ad-hoc et ouvre un segment "chatbot veille automatique" pour les clients.
- **Voice AI 2026 : la parité humaine est atteinte, accélérer le positionnement** — Latence < 300ms, 42% des entreprises déploient des agents vocaux, 70% des appels entrants routiniers gérés par IA. Pour H'appi : mettre à jour tous les pitchs et landing pages avec ces chiffres 2026. L'argument "indiscernable d'un humain" est désormais crédible et vendable aux PME françaises.
- **WebSearch débloqué — veille multi-sources restaurée après 7 jours** — Accès WebSearch fonctionnel pour la première fois depuis le début de la veille. HackerNews, DEV.to et The New Stack restent inaccessibles directement. Recommandation : maintenir WebSearch comme source principale ; demander le déblocage réseau des autres domaines pour une couverture complète.

---
## 📰 Veille Tech — 2026-07-08
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Cowork s'étend au mobile et web — start on desk, finish on phone, MS365 write tools intégrés](https://techcrunch.com/2026/07/07/the-coding-agent-wars-are-spilling-into-the-rest-of-the-office-claude-cowork/) | TechCrunch | #Claude #chatbot |
| [Claude Science — workbench IA pour chercheurs, workflows end-to-end, accès HPC via NVIDIA BioNeMo](https://www.anthropic.com/news/claude-science-ai-workbench) | Anthropic | #Claude #LLM |
| [Alibaba interdit Anthropic à ses employés suite à "distillation attack" — géopolitique IA](https://www.cnbc.com/2026/07/06/alibaba-anthropic-ai-ban-claude-china.html) | CNBC | #Claude #LLM |
| [Anthropic : Claude utilise un espace interne pour "penser sans mots" — recherche conscience IA](https://www.axios.com/2026/07/06/anthropic-claude-ai-conscious) | Axios | #Claude #LLM |
| [CNIL publie nouvelles recommandations IA & RGPD — innovation responsable, obligations AIPD](https://www.cnil.fr/fr/ia-et-rgpd-la-cnil-publie-ses-nouvelles-recommandations-pour-accompagner-une-innovation-responsable) | CNIL | #RGPD |
| [Chatbot RGPD 2026 : obligations légales, registre traitements, sanctions jusqu'à 20M€](https://www.webotit.ai/blog/ia-conversationnelle/generalites/chatbot-et-rgpd-respectez-les-droits-des-personnes-avec-les-conseils-de-la-cnil) | Webotit.ai | #RGPD #chatbot |
| [Vapi lève 50M$ Série B — revenus x10, clients Amazon/Intuit/NY Life — voice AI devenu mainstream](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI |
| [xAI lance Voice Agent Builder beta — no-code, agent vocal en < 2 min, téléphonie + MCPs intégrés](https://x.ai/news/grok-voice-agent-builder) | xAI | #VoiceAI |
| [Voice AI : marché 18,39B$ en 2025 → 61,71B$ en 2031 (CAGR 22,38%) — 87,5% des builders actifs](https://www.assemblyai.com/blog/voice-ai-in-2026-series-1) | AssemblyAI | #VoiceAI |
| [FastAPI vs Node.js pour backends IA 2026 — FastAPI + Python 3.13 + pgvector recommandés pour RAG](https://www.marsdevs.com/compare/fastapi-vs-nodejs-for-ai-backends) | MarsDevs | #FastAPI |
| [kyutai-labs/pocket-tts (🔥 trending) — TTS qui tourne sur CPU, idéal pour déploiements edge/offline](https://github.com/kyutai-labs/pocket-tts) | GitHub Trending 🐍 | #VoiceAI |
| [langbot-app/LangBot (🔥 trending) — plateforme bot multi-plateforme : Discord, Slack, Telegram, WeChat](https://github.com/langbot-app/LangBot) | GitHub Trending 🐍 | #chatbot |
| [TencentCloud/TencentDB-Agent-Memory (🔥 +610 stars) — mémoire long-terme locale pour agents IA sans API externe](https://github.com/TencentCloud/TencentDB-Agent-Memory) | GitHub Trending TS | #LLM #chatbot |
| [diegosouzapw/OmniRoute (🔥 +640 stars — 4e jour consécutif) — AI gateway 231+ providers, smart fallback](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #SaaS |
| [n8n-io/n8n (195k stars) — workflow automation open-source avec capacités IA natives intégrées](https://github.com/n8n-io/n8n) | GitHub Trending TS | #SaaS |

### 💡 Insights clés
- **Claude Cowork mobile/web + MS365 : nouvel argument commercial enterprise H'appi** — Claude Cowork est disponible depuis mobile et web avec écriture d'emails, gestion calendriers et fichiers OneDrive/SharePoint. Pour H'appi : pitcher "assistant IA d'équipe disponible partout" auprès des DSI. L'intégration MS365 ouvre la porte des PME françaises déjà sur Office 365 — à intégrer dans le tier Enterprise.
- **Vapi $50M Série B + revenus x10 : le Voice AI B2B explose** — Vapi, partenaire clé de la stack H'appi (téléphonie), lève 50M$ avec des clients Amazon, Intuit, NY Life. Pour H'appi : argument commercial direct — "infrastructure identique aux géants". Marché Voice AI à 61,71B$ en 2031 valide l'investissement dans cette offre. Mettre à jour les pitchs avec ces chiffres immédiatement.
- **CNIL nouvelles recommandations + sanctions jusqu'à 20M€ : action immédiate** — La CNIL impose une AIPD pour les usages IA à risque élevé. Pour H'appi : intégrer systématiquement "registre des traitements" et "AIPD" dans chaque livraison client. C'est un argument commercial différenciant fort — les concurrents génériques ne font pas ce travail. Mettre à jour le kit de déploiement standard.
- **xAI Voice Agent Builder no-code : surveiller la commoditisation** — Grok permet de créer un agent vocal sans code en < 2 minutes. Pour H'appi : notre valeur ajoutée reste l'intégration profonde (PostgreSQL, CRM, webhooks) et la conformité RGPD. Articuler clairement "chatbot H'appi ≠ no-code" dans les pitchs pour se différencier et justifier le prix premium.
- **TencentDB-Agent-Memory +610 stars : mémoire agent locale sans cloud = argument RGPD** — Mémoire long-terme pour agents IA sans dépendance API externe. Pour H'appi : à tester pour les chatbots qui retiennent le contexte client multi-sessions sans cloud (données hébergées France). Réduit les coûts dev sur les projets avec mémoire persistante et renforce l'argument RGPD souverain.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack, Anthropic.com) — 8e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. WebSearch reste fonctionnel et couvre l'essentiel des actualités pertinentes. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-09
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 5 — nouveau modèle par défaut Free & Pro, contexte 1M tokens, pricing intro $2/$10/Mtok jusqu'au 31 août](https://releasebot.io/updates/anthropic/claude) | Anthropic / Releasebot | #Claude #LLM |
| [Claude Cowork mobile & web + MS365 — email, calendrier, OneDrive/SharePoint depuis app/browser](https://9to5mac.com/2026/07/07/anthropic-expanding-claude-cowork-to-mobile-and-web-details-here/) | 9to5Mac | #Claude |
| [Claude for Government disponible en beta — déploiements secteur public officiellement lancés](https://www.anthropic.com/news) | Anthropic | #Claude #SaaS |
| [Vercel Services — Docker + multi-backend (FastAPI, Go, Rails…) dans un seul projet, annonce semaine du 6 juillet](https://community.vercel.com/t/vercel-weekly-2026-07-06/45111) | Vercel Community | #Vercel #Docker #FastAPI |
| [Railway starter Next.js + FastAPI + PostgreSQL + Redis — monorepo production prêt à l'emploi](https://railway.com/deploy/nextjs-fastapi-full-stack-starter) | Railway | #FastAPI #Railway #PostgreSQL |
| [ElevenLabs en pourparlers pour valorisation à 22B$ — leader TTS vocal en pleine expansion](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI |
| [SoundHound acquiert LivePerson pour accélérer sa présence enterprise en Voice AI](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI |
| [AI Act août 2026 — obligations systèmes IA haut risque applicables dans ~6 semaines](https://www.leto.legal/guides/ai-act-conformite) | Leto.legal | #RGPD |
| [Guide conformité chatbot RGPD 2026 — AIPD, base légale, droits utilisateurs, CNIL](https://heeya.fr/blog/chatbot-rgpd-guide-conformite-cnil) | Heeya.fr | #RGPD #chatbot |
| [bradautomates/claude-video (🔥 +951 stars) — Claude analyse des vidéos : extraction frames + transcription](https://github.com/bradautomates/claude-video) | GitHub Trending 🐍 | #Claude #LLM |
| [kyutai-labs/pocket-tts (🔥 +655 stars) — TTS qui tourne sur CPU, idéal déploiement edge/offline](https://github.com/kyutai-labs/pocket-tts) | GitHub Trending 🐍 | #VoiceAI |
| [TencentCloud/TencentDB-Agent-Memory (🔥 trending) — mémoire long-terme locale pour agents IA, zéro dépendance API externe](https://github.com/TencentCloud/TencentDB-Agent-Memory) | GitHub Trending TS | #LLM #chatbot |
| [wonderwhy-er/DesktopCommanderMCP (6.4k⭐) — MCP server : contrôle terminal + filesystem + diff editing pour Claude](https://github.com/wonderwhy-er/DesktopCommanderMCP) | GitHub Trending TS | #Claude |
| [prisma/prisma (46.6k⭐) — ORM PostgreSQL/MySQL/MongoDB next-gen pour Node.js & TypeScript, en trending](https://github.com/prisma/prisma) | GitHub Trending TS | #PostgreSQL |

### 💡 Insights clés
- **Claude Sonnet 5 = nouveau standard API + pricing agressif jusqu'au 31 août** — Claude Sonnet 5 est le modèle par défaut depuis le 1er juillet (fenêtre 1M tokens, pricing $2/$10 par Mtok en promo). Pour H'appi : migrer les projets clients de Sonnet 4.6 vers Sonnet 5 en priorité pour réduire les coûts d'API et gagner en performance. Deadline budgétaire : avant fin août pour profiter du pricing intro.
- **AI Act haut risque applicable en août 2026 : alerte commerciale et opérationnelle** — Dans ~6 semaines, les obligations sur les systèmes IA à haut risque deviennent contraignantes. Pour H'appi : vérifier si les chatbots déployés tombent dans les catégories haut risque (RH, crédit, sécurité). Préparer les dossiers de conformité AI Act dès maintenant — argument commercial différenciant fort pour les clients en compliance.
- **ElevenLabs 22B$ + SoundHound/LivePerson : consolidation Voice AI enterprise** — Le marché vocal se consolide autour de quelques acteurs valorisés à des niveaux extrêmes. Pour H'appi : l'intégration Vapi (stack actuelle) reste un choix solide. Surveiller les évolutions tarifaires si ElevenLabs entre en bourse — prévoir alternatives open-source (pocket-tts) pour les clients cost-sensitive.
- **Vercel Services + Docker multi-backend : stack H'appi nativisée** — Vercel supporte maintenant Docker + FastAPI + Next.js dans un seul projet. Pour H'appi : la stack Next.js/FastAPI/PostgreSQL peut être déployée entièrement sur Vercel (simplifie DevOps) ou Railway (starter prêt à l'emploi avec Redis). Tester le template Railway pour les nouvelles livraisons clients.
- **claude-video trending +951 stars : ingestion vidéo pour Claude** — Extraction de frames + transcription pour analyser des vidéos avec Claude. Pour H'appi : cas d'usage chatbot formation/e-learning (analyser des tutos vidéo) et support client (analyser des screen recordings). À proposer en module add-on aux clients des secteurs éducation et RH.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 9e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-10
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Opus 4.8 — modèle le plus puissant d'Anthropic, contexte 1M tokens natif, dispo API/Bedrock/Vertex](https://releasebot.io/updates/anthropic/claude) | Anthropic / Releasebot | #Claude #LLM |
| [Anthropic découvre le "J-Space" chez Claude : espace interne de réflexion sans mots — similitudes avec conscience humaine](https://www.technologyreview.com/2026/07/09/1140293/anthropic-found-a-hidden-space-where-claude-puzzles-over-concepts/) | MIT Technology Review | #Claude #LLM |
| [Claude Cowork passe au cloud & mobile — sessions à distance, fichiers synchronisés, disponible hors-ligne](https://www.nbcnews.com/tech/tech-news/anthropic-will-make-claude-cowork-available-users-cloud-rcna353218) | NBC News | #Claude #SaaS |
| [Claude : 9,2% de part de marché chatbot mondial en mai 2026, +855% sur un an — 2e croissance la plus rapide](https://firstpagesage.com/reports/top-generative-ai-chatbots/) | First Page Sage | #Claude #LLM |
| [OpenAI lance GPT-Live — voix full-duplex (parole + écoute simultanées), remplace Advanced Voice Mode](https://openai.com/index/introducing-gpt-live/) | OpenAI | #VoiceAI |
| [ElevenLabs en négociation pour valorisation à 22B$ — doublement de valeur en quelques mois](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI |
| [jamiepine/voicebox (🔥 +1146 stars) — studio vocal IA open-source : clonage de voix, dictée, création audio](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [Graphify-Labs/graphify (🔥 +909 stars) — convertit un repo en knowledge graph queryable pour assistants IA](https://github.com/Graphify-Labs/graphify) | GitHub Trending 🐍 | #LLM |
| [TencentCloud/TencentDB-Agent-Memory (🔥 +581 stars) — mémoire long-terme locale 4 niveaux pour agents IA, zéro API externe](https://github.com/TencentCloud/TencentDB-Agent-Memory) | GitHub Trending TS | #LLM #chatbot |
| [microsoft/SkillOpt (🔥 +276 stars) — optimise des skills LLM réutilisables par trajectory-driven edits sur agents gelés](https://github.com/microsoft/SkillOpt) | GitHub Trending 🐍 | #LLM |
| [unclecode/crawl4ai (🔥 +215 stars) — web crawler open-source optimisé pour LLMs, scraping structuré](https://github.com/unclecode/crawl4ai) | GitHub Trending 🐍 | #LLM |
| [langfuse/langfuse (🔥 +94 stars) — plateforme open-source LLM engineering : observabilité, evals, prompt management](https://github.com/langfuse/langfuse) | GitHub Trending TS | #LLM #SaaS |
| [Vercel Services — Docker + FastAPI/Go/Rails dans un seul projet Vercel, annonce semaine du 6 juillet](https://community.vercel.com/t/vercel-weekly-2026-07-06/45111) | Vercel Community | #Vercel #Docker #FastAPI |
| [RGPD + AI Act double conformité 2026 — guide complet obligations chatbot IA pour entreprises françaises](https://ayinedjimi-consultants.fr/articles/rgpd-ai-act-double-conformite-guide) | Ayi Nedjimi Consultants | #RGPD #chatbot |
| [Chatbot RGPD France 2026 — DPA, base légale, AIPD, droits utilisateurs, obligations CNIL à jour](https://www.agentsia.fr/chatbot-rgpd-france-2026/) | Agentsia.fr | #RGPD #chatbot |

### 💡 Insights clés
- **Claude Opus 4.8 + J-Space : nouveau levier commercial et R&D pour H'appi** — Anthropic lance Opus 4.8 (1M tokens natif) et publie une recherche sur le "J-Space", espace interne de raisonnement chez Claude. Pour H'appi : Opus 4.8 ouvre des cas d'usage très longs (analyse de contrats, knowledge bases larges) — à intégrer dans le tier Enterprise. La recherche J-Space est un argument de crédibilité scientifique dans les pitchs.
- **OpenAI GPT-Live full-duplex : la référence Voice AI change — surveiller de près** — GPT-Live (parole + écoute simultanées) est maintenant le standard par défaut pour les voix ChatGPT. Pour H'appi : notre stack Vapi reste solide pour la téléphonie B2B, mais GPT-Live fixe un nouveau standard d'expérience utilisateur. Anticiper des demandes clients pour ce type de fluidité dans les agents vocaux — évaluer l'intégration GPT-Live-1 mini (tier free) comme alternative future.
- **Claude part de marché +855% YoY : argument commercial fort pour l'écosystème Anthropic** — Claude est le chatbot à la croissance la plus rapide en 2026 (9,2% marché, 952M visites mensuelles). Pour H'appi : "nous bâtissons sur la plateforme à la croissance la plus forte du marché" est un argument de crédibilité auprès des investisseurs et DSI. À intégrer dans les decks commerciaux.
- **voicebox +1146 stars : studio vocal IA open-source à surveiller** — Clone de voix + dictée open-source en TypeScript. Pour H'appi : alternative open-source à ElevenLabs pour les clients cost-sensitive ou RGPD-strict (hébergement local). Tester sur un projet pilote avant de s'engager sur ElevenLabs à $22B de valorisation.
- **graphify +909 stars : knowledge graph de code pour IA = productivité dev H'appi** — Convertit un repo en graphe queryable pour assistants IA. Pour H'appi : accélérer onboarding des chatbots clients (graphify le code legacy du client → l'IA comprend la base de code plus vite). Tester en interne sur les projets les plus complexes.
- **Double conformité RGPD + AI Act : argument commercial différenciant clé en juillet 2026** — Les obligations AI Act haut risque entrent en vigueur imminemment. Pour H'appi : packager systématiquement "conformité RGPD + AI Act" dans chaque livraison — DPA, AIPD, registre des traitements. C'est un différenciateur fort face aux solutions génériques. Mettre à jour les CGV et contrats clients avant fin juillet.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 10e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-11
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [MCP 2026-07-28 RC — plus grande révision depuis le lancement : cœur stateless HTTP, Tasks extension, MCP Apps UI](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/) | MCP Blog | #LLM |
| [5 000+ serveurs MCP dispo : GitHub, Slack, PostgreSQL, Docker, Stripe, Figma — devenu standard industrie IA](https://explore.n1n.ai/blog/mcp-tools-2026-model-context-protocol-guide-2026-05-12) | n1n.ai | #LLM #chatbot |
| [huggingface/speech-to-speech (🔥 trending) — build local voice agents with open-source models, Python](https://github.com/huggingface/speech-to-speech) | GitHub Trending 🐍 | #VoiceAI |
| [microsoft/agent-governance-toolkit (🔥 trending) — policy enforcement, zero-trust identity, sandboxing pour agents IA autonomes](https://github.com/microsoft/agent-governance-toolkit) | GitHub Trending 🐍 | #LLM #SaaS |
| [LMCache/LMCache (🔥 trending) — couche KV Cache ultra-rapide pour LLM : réduit latence et coût d'inférence](https://github.com/LMCache/LMCache) | GitHub Trending 🐍 | #LLM |
| [microsoft/graphrag (🔥 trending) — système RAG modulaire basé sur graphes de connaissances](https://github.com/microsoft/graphrag) | GitHub Trending 🐍 | #LLM |
| [xerrors/Yuxi (🔥 trending) — Agent Harness multi-tenant avec knowledge base + knowledge graphs intégrés](https://github.com/xerrors/Yuxi) | GitHub Trending 🐍 | #chatbot #LLM |
| [davila7/claude-code-templates (🔥 trending) — CLI pour configurer et monitorer Claude Code](https://github.com/davila7/claude-code-templates) | GitHub Trending 🐍 | #Claude |
| [EveryInc/compound-engineering-plugin (+127 stars) — plugin officiel pour Claude Code, Codex, Cursor, Windsurf](https://github.com/EveryInc/compound-engineering-plugin) | GitHub Trending TS | #Claude |
| [pipecat-ai/pipecat — framework Python open-source : agents conversationnels voix + multimodal temps réel](https://github.com/pipecat-ai/pipecat) | GitHub / AssemblyAI | #VoiceAI #chatbot |
| [syncable-dev/memtrace-public (🔥 trending) — mémoire structurelle pour agents IA par bi-temporal graphs](https://github.com/syncable-dev/memtrace-public) | GitHub Trending 🐍 | #LLM #chatbot |
| [DEV.to : "How I built an AI SaaS with Next.js, FastAPI, and Dokploy" — retour d'expérience stack complète + déploiement](https://dev.to/julykk/how-i-built-an-ai-saas-with-nextjs-fastapi-and-dokploy-52eo) | DEV.to | #FastAPI #Next.js #SaaS |
| [CNIL publie ses nouvelles recommandations IA 2026 — chatbot : base légale, minimisation, AIPD, droits utilisateurs](https://www.cnil.fr/fr/ia-et-rgpd-la-cnil-publie-ses-nouvelles-recommandations-pour-accompagner-une-innovation-responsable) | CNIL | #RGPD #chatbot |

### 💡 Insights clés
- **MCP atteint la maturité production (5 000+ serveurs, spec RC juillet) — à intégrer systématiquement** — MCP est devenu le standard de facto pour connecter les agents IA aux outils externes. La spec 2026-07-28 RC apporte un cœur stateless scalable sur HTTP standard + extensions Tasks et MCP Apps (UI server-rendered). Pour H'appi : packager des MCP servers dans chaque chatbot client (PostgreSQL, Slack, GitHub) — c'est désormais un attendu de production, pas une option.
- **microsoft/agent-governance-toolkit : gouvernance IA enterprise à packager dans l'offre H'appi** — Policy enforcement, zero-trust identity et sandboxing d'exécution pour agents autonomes. Pour H'appi : ce toolkit peut devenir la colonne vertébrale d'un module "Chatbot Enterprise Sécurisé" — différenciateur fort auprès des grands comptes (banque, santé, RH) qui exigent des garanties de gouvernance IA.
- **huggingface/speech-to-speech trending : Voice AI locale = réponse au blocage RGPD des APIs tierces** — Framework Python pour construire des agents vocaux entièrement en local, zéro appel API externe. Pour H'appi : argument commercial clé auprès des clients RGPD-strict qui refusent d'envoyer de l'audio à ElevenLabs ou OpenAI. Benchmarker contre la stack Vapi actuelle pour identifier les cas d'usage où le local gagne.
- **LMCache + graphRAG trending : optimisation LLM et RAG deviennent commodités open-source** — LMCache réduit le coût d'inférence via KV cache ; graphRAG structure la connaissance en graphes pour un meilleur retrieval. Pour H'appi : intégrer LMCache pour les chatbots à fort volume de requêtes répétées (FAQ, support client) — réduction de coût directe. GraphRAG pour les bases de connaissance clients complexes (documentation technique, légal).
- **Stack Next.js + FastAPI + Dokploy : alternative PaaS souveraine à Railway/Vercel** — Dokploy est un PaaS self-hosted open-source déployable sur VPS à coût fixe (vs Railway à la consommation). Pour H'appi : évaluer Dokploy pour les projets avec hébergement souverain français requis (secteur public, santé, finance RGPD strict). Benchmark Railway vs Dokploy sur le prochain projet.
- **CNIL recommandations IA 2026 publiées : mettre à jour le template livrable conformité H'appi** — Nouvelle guidance CNIL spécifique IA : base légale obligatoire, minimisation des données, AIPD pour les traitements à risque, gestion des sous-traitants IA, durée de conservation. Pour H'appi : créer et livrer systématiquement un "Dossier Conformité RGPD + AI Act" avec chaque déploiement chatbot — différenciateur commercial clé, protège le client et H'appi en cas de contrôle CNIL.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 11e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-12
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 5 — le plus agentique à ce jour, proche d'Opus 4.8, tarif réduit jusqu'au 31 août](https://www.anthropic.com/news) | Anthropic | #LLM #Claude |
| [Claude Cowork migre vers le cloud — exécution en arrière-plan multi-appareils, beta Max](https://www.nbcnews.com/tech/tech-news/anthropic-will-make-claude-cowork-available-users-cloud-rcna353218) | NBC / Anthropic | #Claude #SaaS |
| [wonderwhy-er/DesktopCommanderMCP — MCP server terminal + FS pour Claude (+909 stars/jour)](https://github.com/wonderwhy-er/DesktopCommanderMCP) | GitHub Trending TS | #LLM |
| [pydantic/pydantic-ai — AI Agent Framework by Pydantic (trending Python)](https://github.com/pydantic/pydantic-ai) | GitHub Trending 🐍 | #LLM #chatbot |
| [Shubhamsaboo/awesome-llm-apps — 100+ apps LLM & RAG à cloner et déployer](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot |
| [HuggingFace smolagents v1.26.0 — agents qui écrivent et exécutent du Python directement](https://huggingface.co/docs/smolagents/en/index) | HuggingFace | #LLM |
| [ICML 2026 Séoul — record 23 918 soumissions, 60 workshops agentic AI](https://alicelabs.ai/en/insights/best-ai-agent-frameworks-2026) | ICML / AliceLabs | #LLM |
| [Pipecat — Voice AI open-source, sub-250ms latency, 70+ langues, WebRTC](https://www.assemblyai.com/blog/orchestration-tools-ai-voice-agents) | AssemblyAI | #VoiceAI #chatbot |
| [FastAPI vs Next.js : quel backend pour un AI SaaS en 2026 ?](https://hassanr.com/blogs/fastapi-vs-nextjs-ai-saas-backend-2026.html) | hassanr.com | #FastAPI #Next.js #SaaS |
| [Déployer FastAPI + Next.js sur Vercel — guide 2026](https://nemanjamitic.com/blog/2026-02-22-vercel-deploy-fastapi-nextjs/) | nemanjamitic.com | #FastAPI #Next.js #Vercel |
| [louislam/dockge — gestionnaire Docker Compose self-hosted réactif (+17 stars/jour)](https://github.com/louislam/dockge) | GitHub Trending TS | #Docker |
| [Chatbot IA & RGPD 2026 : DPA obligatoire, AIPD, AI Act — guide conformité CNIL](https://heeya.fr/blog/chatbot-rgpd-guide-conformite-cnil) | heeya.fr | #RGPD #chatbot |
| [MervinPraison/PraisonAI — agents IA autonomes auto-améliorants en 5 lignes, mémoire + RAG](https://github.com/MervinPraison/PraisonAI) | GitHub Trending 🐍 | #LLM #chatbot |
| [Infisical — secrets & certificats open-source, +40 stars/jour, alternative à HashiCorp Vault](https://github.com/Infisical/infisical) | GitHub Trending TS | #SaaS #Docker |
| [gitroomhq/postiz-app — scheduling social media agentique open-source (+76 stars/jour)](https://github.com/gitroomhq/postiz-app) | GitHub Trending TS | #SaaS |

### 💡 Insights clés
- **Claude Sonnet 5 disponible : migrer nos intégrations Anthropic dès maintenant** — Lancé le 30 juin, Sonnet 5 est le défaut pour tous les utilisateurs Claude depuis le 1er juillet. Il surpasse Sonnet 4.6 sur les tâches agentiques, approche Opus 4.8, et est à tarif réduit jusqu'au 31 août. Pour H'appi : remplacer claude-sonnet-4-6 par claude-sonnet-5 dans nos chatbots clients — gain de performance immédiat, coût similaire ou inférieur pendant la période promo.
- **Claude Cowork cloud = shift vers les agents en arrière-plan — nouveau cas d'usage H'appi** — Anthropic déplace Cowork vers le cloud : les agents tournent même quand l'appareil est éteint. C'est le signal que les agents autonomes longue durée deviennent mainstream. Pour H'appi : proposer des "chatbots backgroundés" capables de surveiller des flux, d'envoyer des rapports, de monitorer des données — package "Agent Veille Automatisée" à ajouter à notre catalogue.
- **DesktopCommanderMCP +909 stars/jour : l'outillage MCP terminal explose** — Ce MCP server donne à Claude le contrôle du terminal et du filesystem — meilleur score journalier de la semaine sur GitHub TS. Pour H'appi : intégrer des MCP servers spécialisés dans nos chatbots enterprise (terminal, BDD, CRM) pour passer du chatbot passif à l'agent actif — argument commercial décisif en démo client.
- **Pipecat sub-250ms : Voice AI production-ready, open-source, souverain** — Framework Python, sub-250ms end-to-end, WebRTC natif, 70+ langues, auto-hébergeable. Rival direct de Vapi mais sans API tiers. Pour H'appi : benchmarker Pipecat vs Vapi sur un projet pilote — si latence OK, Pipecat devient notre stack Voice AI RGPD-compliant pour clients santé et secteur public.
- **RGPD + AI Act 2026 : DPA désormais obligatoire pour TOUT chatbot IA** — Les dernières directives juridiques d'avril 2026 rendent le DPA obligatoire pour toute intégration IA conversationnelle, même en B2B. Sanctions jusqu'à 20M€ ou 4% du CA mondial. Pour H'appi : ajouter le DPA en annexe standard de chaque contrat client chatbot + livrer systématiquement un template AIPD — protège H'appi et valorise notre expertise conformité face aux concurrents.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 12e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-13
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Anthropic J-Space : Claude a un espace de raisonnement interne silencieux (J-lens)](https://www.anthropic.com/research/global-workspace) | Anthropic Research | #LLM #Claude |
| [Claude Cowork cloud & mobile : agents actifs même appareil éteint](https://www.fingerlakes1.com/2026/07/09/claude-cowork-ai-agent-launches-as-anthropic-expands-ai-assistant-to-cloud-and-mobile/) | Fingerlakes1 / Anthropic | #Claude #SaaS |
| [Anthropic vaut plus qu'OpenAI — Claude à 17% du marché mobile chatbot US](https://fatjoe.com/blog/claude-ai-stats/) | FatJoe | #Claude #LLM |
| [EU AI Act Art. 50 : disclosure chatbot obligatoire dès le 2 août 2026](https://www.techtimes.com/articles/320101/20260710/eu-ai-act-enforcement-here-chatbot-rules-live-high-risk-ai-delay-now-binding-law.htm) | TechTimes | #RGPD #chatbot |
| [Chatbot & AI Act : guide conformité 2026 pour opérateurs](https://heeya.fr/en/blog/eu-ai-act-chatbot-compliance-2026) | Heeya.fr | #RGPD #chatbot |
| [Next.js 16.3 : Turbopack persistent cache, Rust React Compiler, import.meta.glob](https://releasebot.io/updates/vercel/next-js) | Releasebot / Vercel | #Next.js #Vercel |
| [Vercel Services : FastAPI + Docker dans un projet full-stack unique](https://community.vercel.com/t/vercel-weekly-2026-07-06/45111) | Vercel Community | #Vercel #FastAPI #Docker |
| [Railway $41/mo vs Vercel $1 010/mo — benchmark Next.js 2026](https://www.13labs.au/compare/railway-vs-vercel) | 13labs.au | #Railway #Vercel #Next.js |
| [ElevenLabs vise $22B de valorisation — Voice AI devient mainstream](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI |
| [xAI lance Grok Voice Builder pour créer des agents vocaux](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI #chatbot |
| [davila7/claude-code-templates — CLI Claude Code trending (+274 étoiles/jour)](https://github.com/davila7/claude-code-templates) | GitHub Trending 🐍 | #Claude #LLM |
| [wonderwhy-er/DesktopCommanderMCP — MCP terminal + FS pour Claude (8K stars)](https://github.com/wonderwhy-er/DesktopCommanderMCP) | GitHub Trending TS | #LLM #Claude |
| [ColeMurray/background-agents — agents IA en arrière-plan open-source](https://github.com/ColeMurray/background-agents) | GitHub Trending TS | #LLM #SaaS |
| [heygen-com/hyperframes — écrire du HTML pour produire de la vidéo, conçu pour les agents](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #LLM #SaaS |
| [Shubhamsaboo/awesome-llm-apps — 100+ apps LLM & RAG à déployer (+408 étoiles/jour)](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot |

### 💡 Insights clés
- **J-Space : Anthropic peut lire les "pensées" silencieuses de Claude — game changer en transparence IA** — Le J-lens révèle les raisonnements internes de Claude sans qu'il les exprime. Implication double : (1) sécurité IA renforcée (détecter un plan nuisible avant exécution) ; (2) transparence commerciale (montrer aux clients enterprise comment leur chatbot raisonne). Pour H'appi : positionner l'argument "interprétabilité Claude" dans nos démos — différenciateur fort face aux solutions black-box.
- **AI Act Article 50 applicable le 2 août 2026 — J-20 jours, action urgente sur tous les chatbots clients** — Obligation légale : informer l'utilisateur en début de conversation qu'il interagit avec une IA. Sanction jusqu'à 4% du CA mondial en cas de non-conformité. Pour H'appi : patcher IMMÉDIATEMENT tous les chatbots déployés avec un message d'accueil "Vous interagissez avec un assistant IA". Priorité absolue avant toute autre feature.
- **Vercel Services = FastAPI + Docker + Next.js dans un seul projet — full-stack unifié** — Vercel brise son silos frontend : déploiement d'une app full-stack (Next.js + FastAPI + Docker) dans un projet unique. Pour H'appi : tester Vercel Services sur le prochain projet avant de valider Railway comme défaut. Si l'expérience DX est bonne, Vercel devient notre plateforme unique.
- **Railway $41/mo vs Vercel $1 010/mo pour la même Next.js app — benchmark choc** — Pour les projets clients à fort trafic, Railway est 25× moins cher que Vercel. Pour H'appi : avoir ce chiffre prêt en démo pour les clients sensibles au coût d'hosting. Positionnement : Vercel pour early-stage (DX, vitesse), Railway pour maturité (coût, Docker natif).
- **ElevenLabs $22B + Grok Voice Builder : Voice AI entre dans la phase mainstream** — En quelques jours : ElevenLabs devient l'une des 10 startups IA les mieux valorisées, xAI lance un constructeur d'agents vocaux grand public. Pour H'appi : l'offre Voice AI n'est plus optionnelle — les clients vont la demander par défaut. Structurer un module Voice AI (Pipecat ou Vapi) dans notre catalogue standard.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 13e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-14
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude for Government — Anthropic ouvre Claude aux collectivités (Californie -50%, formation gratuite, portail SIT)](https://www.anthropic.com/news) | Anthropic | #LLM #Claude #SaaS |
| [Vercel AI SDK v6.0 — API unifiée 25+ providers IA, changer de modèle en 2 lignes de code](https://tech-insider.org/vercel-ai-sdk-tutorial-chatbot-nextjs-2026/) | Tech-Insider | #Next.js #Vercel #chatbot |
| [Building a Hybrid AI Chatbot with Next.js 16 — Partial Prerendering + AI SDK (GitNation)](https://gitnation.com/contents/building-a-hybrid-ai-chatbot-with-nextjs-16) | GitNation | #Next.js #chatbot |
| [How to Add an AI Chatbot to Your React Native App (FastAPI Backend) — guide production Simplico](https://simplico.net/2026/06/21/ai-chatbot-react-native-fastapi/) | Simplico | #chatbot #FastAPI |
| [LiveKit Agents — Voice AI open-source WebRTC natif, auto-hébergeable, zéro lock-in tiers](https://livekit.com/) | LiveKit | #VoiceAI #chatbot |
| [bolna-ai/bolna — framework end-to-end open-source pour agents vocaux LLM production-ready](https://github.com/bolna-ai/bolna) | GitHub | #VoiceAI #chatbot |
| [AI Act : application intégrale le 2 août 2026 — J-19, sanctions jusqu'à €35M ou 7% du CA](https://www.donneespersonnelles.fr/actualite-ia-2026) | DonnéesPersonnelles.fr | #RGPD #chatbot |
| [AI Act obligations 2026 : calendrier complet, amendes, European AI Registry — guide Leto Legal](https://www.leto.legal/guides/ai-act-conformite) | Leto Legal | #RGPD |
| [Docker vs Vercel pour le déploiement SaaS en 2026 — guide StarterPick](https://starterpick.com/guides/docker-vs-vercel-deployment-strategies-2026) | StarterPick | #Docker #Vercel #SaaS |
| [Railway : déploiement PostgreSQL en un clic, SSL natif, backups managés](https://docs.railway.com/databases/postgresql) | Railway Docs | #PostgreSQL #Railway |
| [ARUNAGIRINATHAN-K/awesome-ai-agents-2026 — 300+ agents IA : Voice, Enterprise, Research, Frameworks](https://github.com/ARUNAGIRINATHAN-K/awesome-ai-agents-2026) | GitHub | #LLM #chatbot |
| [ruvnet/ruflo (🔥 trending TS) — agent meta-harness multi-player, mémoire adaptative + RAG intégrés](https://github.com/ruvnet/ruflo) | GitHub Trending TS | #LLM #SaaS |
| [Graphify-Labs/graphify (🔥 trending 🐍) — transformer code + schemas + docs en graphe queryable pour Claude](https://github.com/Graphify-Labs/graphify) | GitHub Trending 🐍 | #LLM #Claude |
| [YishenTu/claudian (🔥 trending TS) — plugin Obsidian intégrant Claude AI comme collaborateur dans le vault](https://github.com/YishenTu/claudian) | GitHub Trending TS | #Claude #SaaS |

### 💡 Insights clés
- **Claude for Government = nouveau marché B2G pour H'appi** — Anthropic déploie Claude dans les collectivités publiques (Californie en beta, -50% + formation gratuite). Signal fort que le secteur public va accélérer l'adoption de chatbots IA. Pour H'appi : préparer une offre "Chatbot Secteur Public" spécifique (souveraineté hébergement, conformité RGPD & AI Act, accessibilité RGAA) — positionner auprès des mairies, établissements de santé, services RH publics.
- **Vercel AI SDK v6.0 — portabilité fournisseur LLM en 2 lignes : à adopter dans tous nos projets** — Le SDK unifie 25+ providers (Claude, GPT, Gemini, Mistral…) derrière une API identique. Pour H'appi : intégrer Vercel AI SDK dans nos projets Next.js dès maintenant — on peut switcher de Claude à GPT-4o en modifiant 2 lignes, argument clé face aux clients qui veulent éviter le vendor lock-in Anthropic.
- **LiveKit + Bolna : 3 frameworks Voice AI open-source production-ready — souveraineté totale** — Pipecat (sub-250ms, WebRTC), LiveKit (WebRTC natif, self-hosted), Bolna (end-to-end LLM voice). Pour H'appi : la souveraineté Voice AI est désormais accessible — construire un comparatif Vapi vs Pipecat vs LiveKit sur latence, coût, conformité RGPD avant le prochain projet vocal.
- **AI Act J-19 — €35M de sanctions au 2 août : audit chatbot urgent** — Les sanctions ont été confirmées : jusqu'à €35M ou 7% du CA mondial pour les systèmes interdits, €7,5M pour non-respect de transparence. L'European AI Registry est maintenant exigible pour certains systèmes. Pour H'appi : (1) vérifier le message "vous interagissez avec une IA" sur TOUS les chatbots déployés, (2) vérifier l'éligibilité à l'enregistrement dans l'AI Registry, (3) livrer un rapport de conformité AI Act aux clients à risque avant le 1er août.
- **Graphify trending : rendre le code legacy d'un client queryable par Claude — onboarding 10× plus rapide** — Graphify convertit un repo entier (code + schemas + docs) en graphe de connaissance queryable par une IA. Pour H'appi : utiliser Graphify lors de l'onboarding des chatbots clients sur des bases de code complexes (ERP, legacy Java/PHP). Réduction drastique du temps de contextualisation de Claude sur le domaine client.
- **Ruflo meta-harness + Claudian : l'écosystème TS autour de Claude s'industrialise** — Ruflo orchestre des swarms d'agents avec mémoire adaptative ; Claudian intègre Claude comme collaborateur dans Obsidian. Pour H'appi : l'outillage multi-agent TS est mature — structurer un module "agent workflow" dans nos projets basé sur Ruflo pour les clients qui ont des processus métier complexes à automatiser.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 14e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-15
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Fable 5 restauré — le Commerce Dept US lève l'export control après 18 jours hors-ligne](https://www.anthropic.com/news/redeploying-fable-5) | Anthropic | #LLM #Claude |
| [Claude for Teachers — accès premium gratuit aux enseignants K-12 US, données FERPA-protégées](https://www.anthropic.com/news) | Anthropic | #LLM #Claude #SaaS |
| [Intervo.ai — plateforme open source tout-en-un agents vocaux & chatbots pour entreprises](https://intervo.ai/) | Intervo | #VoiceAI #chatbot #SaaS |
| [Vexa-ai/vexa — API transcription réunion open-source (Google Meet, Teams, Zoom) + MCP server pour agents IA](https://github.com/Vexa-ai/vexa) | GitHub Trending 🐍 | #VoiceAI #chatbot #LLM |
| [moeru-ai/airi — AI companion self-hosted avec voice chat et gaming, open source (42k stars)](https://github.com/moeru-ai/airi) | GitHub Trending TS | #VoiceAI #chatbot |
| [stripe/ai — SDK officiel Stripe pour construire des produits IA monétisés (paiements natifs)](https://github.com/stripe/ai) | GitHub Trending TS | #SaaS #LLM |
| [earendil-works/pi — Toolkit agent IA : API LLM unifiée, agent loop, TUI, CLI (71k stars)](https://github.com/earendil-works/pi) | GitHub Trending TS | #LLM #chatbot |
| [openclaw/openclaw — Personal AI assistant open source, multi-OS, multi-plateforme (382k stars)](https://github.com/openclaw/openclaw) | GitHub Trending TS | #LLM #chatbot |
| [millionco/react-doctor — Agent qui détecte et corrige le mauvais code React écrit par IA](https://github.com/millionco/react-doctor) | GitHub Trending TS | #Next.js #LLM |
| [google/skills — Agent Skills officielles Google pour produits et technologies Google](https://github.com/google/skills) | GitHub Trending 🐍 | #LLM |
| [RGPD + AI Act : guide double conformité 2026 — obligations simultanées pour chatbots et IA](https://ayinedjimi-consultants.fr/articles/rgpd-ai-act-double-conformite-guide) | Ayi Nedjimi Consultants | #RGPD #chatbot |
| [Vercel vs Railway vs Hetzner — quand utiliser quoi pour un SaaS solo en 2026](https://devtoolpicks.com/blog/when-to-use-vercel-vs-railway-vs-hetzner-solo-saas-2026) | DevToolPicks | #Vercel #Railway #SaaS |
| [Railway vs Vercel 2026 — calcul de coût réel + cas d'usage gagnants](https://justinmckelvey.com/blog/railway-vs-vercel) | Justin McKelvey | #Railway #Vercel #SaaS |
| [The Open-Source Voice AI Stack Every Developer Should Know in 2026](https://dev.to/dograh/the-open-source-voice-ai-stack-every-developer-should-know-in-2026-4363) | DEV.to | #VoiceAI #chatbot |
| [Google AI Overviews — 55% des recherches, taux zéro-clic à 69% : impact SEO massif](https://dentro.de/ai/news/) | Dentro.de | #LLM #SaaS |

### 💡 Insights clés
- **Claude Fable 5 de retour — benchmarker vs Sonnet 5 pour choisir le modèle H'appi** — Après 18 jours de blocage lié aux export controls US, Fable 5 est à nouveau accessible sur Claude.ai, l'API et Claude Code. C'est le modèle le plus puissant d'Anthropic, il a compressé une migration de 50M de lignes de code (2 mois d'équipe) en une seule journée lors des tests. Pour H'appi : lancer un benchmark rapide Fable 5 vs Sonnet 5 sur nos cas d'usage chatbot clients — si le gain de qualité justifie le surcoût, l'utiliser sur les comptes enterprise à forte valeur.
- **Intervo.ai + Vexa : deux nouveaux outils open source qui complètent notre stack Voice AI** — Intervo.ai est une plateforme tout-en-un (voice + chat) open source pour entreprises ; Vexa auto-rejoint les réunions (Meet, Teams, Zoom) et transcrit en temps réel via WebSocket avec un MCP server intégré pour les agents IA. Pour H'appi : Vexa est un cas d'usage immédiat — proposer un "Chatbot Assistant Réunion" qui rejoint les calls clients, transcrit, et génère un compte-rendu + actions automatiques. Différenciateur fort, RGPD-compliant car auto-hébergeable.
- **stripe/ai SDK officiel : monétisation IA native prête à l'emploi — intégrer dans notre boilerplate SaaS** — Stripe lance un SDK dédié pour construire des produits IA avec paiements natifs (abonnements, usage-based billing, pay-per-message). Pour H'appi : ajouter stripe/ai à notre boilerplate Next.js + FastAPI pour proposer du billing usage-based aux clients SaaS — facturation à la conversation ou au token, pas seulement au forfait mensuel.
- **AI Act J-18 — double conformité RGPD + AI Act obligatoire dès le 2 août : audit final maintenant** — Les chatbots sont classés "risque limité" mais ont des obligations de transparence contraignantes (disclosure IA obligatoire). Le RGPD et l'AI Act s'appliquent simultanément pour tout chatbot traitant des données personnelles. Pour H'appi : (1) checklist finale : message "vous interagissez avec une IA" sur 100% des chatbots déployés, (2) DPA en annexe de chaque contrat, (3) proposer un audit de conformité RGPD+AI Act comme prestation payante aux clients — J-18, urgence maximale.
- **Vercel vs Railway vs Hetzner 2026 — la règle d'or confirmée pour H'appi** — Consensus des analyses 2026 : Vercel pour le frontend Next.js (edge, DX), Railway pour le backend FastAPI + PostgreSQL (flexibilité, coût), Hetzner pour les charges à fort volume (bare metal, autonomie totale). Pour H'appi : standardiser cette architecture tri-layer pour nos projets SaaS clients à partir de maintenant — clarté pour les devis et les handoff ops.
- **Google AI Overviews à 55% des recherches — le SEO classique est mort, place au SEO conversationnel** — 69% des recherches Google se terminent sans un clic sur un site. Les chatbots IA capturent l'intention là où le site web ne peut plus. Pour H'appi : intégrer l'argument "votre chatbot IA remplace votre trafic organique perdu" dans les démos commerciales — c'est désormais une réalité mesurable, pas une projection.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 15e jour consécutif** — Veille appuyée sur GitHub Trending + WebSearch. Recommandation maintenue : débloquer les domaines API directs dans la politique réseau de l'environnement remote.

---
## 📰 Veille Tech — 2026-07-16
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Shubhamsaboo/awesome-llm-apps — 100+ AI Agent & RAG apps clonables et déployables (1 236 ⭐ aujourd'hui)](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot |
| [HKUDS/nanobot — Agent IA léger open-source pour outils, chats et workflows](https://github.com/HKUDS/nanobot) | GitHub Trending 🐍 | #chatbot #LLM |
| [HKUDS/Vibe-Trading — Personal Trading AI Agent (915 ⭐ aujourd'hui)](https://github.com/HKUDS/Vibe-Trading) | GitHub Trending 🐍 | #LLM |
| [vllm-project/vllm — Moteur d'inférence LLM haute performance + memory-efficient (104 ⭐ aujourd'hui)](https://github.com/vllm-project/vllm) | GitHub Trending 🐍 | #LLM |
| [moeru-ai/airi — AI companion self-hosted avec voice chat intégré (42 653 ⭐)](https://github.com/moeru-ai/airi) | GitHub Trending TS | #VoiceAI #chatbot |
| [earendil-works/pi — Toolkit agent IA : API LLM unifiée, agent loop, TUI, CLI coding agent (71 576 ⭐)](https://github.com/earendil-works/pi) | GitHub Trending TS | #LLM #chatbot |
| [heygen-com/hyperframes — Write HTML. Render video. Built for agents. (35 527 ⭐)](https://github.com/heygen-com/hyperframes) | GitHub Trending TS | #LLM #SaaS |
| [browseros-ai/BrowserOS — Navigateur agentique alternatif à ChatGPT Atlas (12 233 ⭐)](https://github.com/browseros-ai/BrowserOS) | GitHub Trending TS | #LLM #chatbot |
| [PeterH0323/Streamer-Sales — LLM + TTS + ASR + FastAPI + Docker-compose (3 734 ⭐, màj 16/07)](https://github.com/PeterH0323/Streamer-Sales) | GitHub Search | #VoiceAI #FastAPI #Docker |
| [AleksNeStu/ai-real-estate-assistant — FastAPI + Next.js + ChromaDB + RAG (279 ⭐, màj 14/07)](https://github.com/AleksNeStu/ai-real-estate-assistant) | GitHub Search | #FastAPI #Next.js #chatbot |
| [adrianhajdin/saas-app — SaaS LMS Next.js 15 + Vapi AI voice agent + Stripe (431 ⭐)](https://github.com/adrianhajdin/saas-app) | GitHub Search | #VoiceAI #SaaS #Next.js |
| [Anil-matcha/AI-Voice-Agent — Self-hosted AI voice agent (Next.js + TTS, 158 ⭐)](https://github.com/Anil-matcha/AI-Voice-Agent) | GitHub Search | #VoiceAI #Next.js |
| [paulpierre/RasaGPT — LLM chatbot headless FastAPI + Langchain + pgvector (2 464 ⭐)](https://github.com/paulpierre/RasaGPT) | GitHub Search | #chatbot #FastAPI #PostgreSQL |

### 💡 Insights clés
- **awesome-llm-apps — 1 236 ⭐ en une journée : la bibliothèque de référence RAG + agents à intégrer dans notre onboarding** — Ce repo concentre 100+ applications AI Agent et RAG clonables et immédiatement déployables. Il est devenu la ressource communautaire de référence pour les patterns LLM. Pour H'appi : indexer ce repo dans notre base de patterns. Quand un client demande un use case (chatbot doc, agent CRM, assistant vocal), aller y chercher le template le plus proche plutôt que de repartir de zéro — économise 2-3 jours de setup.
- **Hyperframes "Write HTML. Render video. Built for agents" — la prochaine génération de chatbots génère du contenu vidéo interactif** — HeyGen lance un framework TypeScript où les agents écrivent du HTML qui est ensuite rendu en vidéo. Cela signale une transition : les chatbots vont au-delà du texte vers des livrables visuels automatisés (présentations, démos produit, tutoriels générés). Pour H'appi : explorer un cas d'usage "chatbot qui génère une vidéo de présentation produit" pour les clients e-commerce — différenciateur fort à prix premium.
- **airi + AI-Voice-Agent + saas-app Vapi : le Voice AI self-hosted est devenu un pattern mature** — Trois projets GitHub indépendants convergent vers le même stack : Next.js + Vapi.ai + TTS + self-hosting. Ce n'est plus expérimental — c'est un pattern reproductible. Pour H'appi : notre intégration Vapi.ai dans le boilerplate est alignée avec la communauté. Accélérer la documentation du pattern "Voice Agent self-hosted RGPD-compliant" pour le proposer comme prestation packagée.
- **RasaGPT + pgvector — notre choix FastAPI + PostgreSQL + pgvector est validé par 2 464 ⭐** — RasaGPT utilise exactement notre stack (FastAPI + Langchain + pgvector + ngrok) pour un chatbot LLM headless. C'est une validation communautaire forte. Pour H'appi : lire le code de RasaGPT pour s'en inspirer sur la gestion des sessions de dialogue et l'architecture headless — il peut aussi servir de référence technique dans les pitchs clients.
- **vllm — inférence LLM haute performance : pertinent pour les clients enterprise à fort volume** — vllm est le moteur d'inférence le plus utilisé pour déployer des LLM open-source à grande échelle. Pour H'appi : pour les clients qui demandent du LLM on-premise (données sensibles, RGPD strict), vllm + Hetzner est la réponse. À mentionner dans les devis enterprise comme option "full souveraineté des données".
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack, Anthropic.com) — 16e jour consécutif** — Veille appuyée exclusivement sur GitHub Trending + GitHub Search API. Recommandation maintenue : débloquer les domaines dans la politique réseau de l'environnement remote pour diversifier les sources.

---
## 📰 Veille Tech — 2026-07-17
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [anthropics/knowledge-work-plugins — plugins open-source pour travailleurs du savoir dans Claude (Claude Code, Cowork)](https://github.com/anthropics/knowledge-work-plugins) | GitHub Trending 🐍 | #Claude |
| [Graphify-Labs/graphify (🔥 +1 107 stars) — convertit code + schemas + docs en knowledge graph queryable pour IA](https://github.com/Graphify-Labs/graphify) | GitHub Trending 🐍 | #LLM |
| [Shubhamsaboo/awesome-llm-apps (🔥 +923 stars) — 100+ apps AI Agent & RAG clonables et déployables](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot |
| [NousResearch/hermes-agent (🔥 +588 stars) — plateforme d'agents adaptatifs open-source](https://github.com/NousResearch/hermes-agent) | GitHub Trending 🐍 | #LLM |
| [microsoft/markitdown (🔥 +363 stars) — outil Python pour convertir fichiers et docs Office en Markdown pour LLMs](https://github.com/microsoft/markitdown) | GitHub Trending 🐍 | #LLM |
| [HKUDS/DeepTutor (🔥 +656 stars) — plateforme de tutoring IA personnalisé lifelong](https://github.com/HKUDS/DeepTutor) | GitHub Trending 🐍 | #chatbot #LLM |
| [HKUDS/nanobot (🔥 +85 stars) — agent IA léger open-source pour outils, chats et workflows](https://github.com/HKUDS/nanobot) | GitHub Trending 🐍 | #chatbot #LLM |
| [PostHog/posthog (🔥 +77 stars) — plateforme SaaS avec AI observabilité, analytics et session replay](https://github.com/PostHog/posthog) | GitHub Trending 🐍 | #SaaS |
| [moeru-ai/airi (🔥 +402 stars) — AI companion self-hosted avec voice chat et gaming intégrés](https://github.com/moeru-ai/airi) | GitHub Trending TS | #VoiceAI #chatbot |
| [anomalyco/opencode (🔥 +404 stars) — agent de coding open-source](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM |
| [browseros-ai/BrowserOS (🔥 +63 stars) — navigateur agentique open-source, alternative à ChatGPT Atlas](https://github.com/browseros-ai/BrowserOS) | GitHub Trending TS | #LLM #chatbot |
| [EKKOLearnAI/hermes-studio (🔥 +48 stars) — dashboard web pour Hermes Agent avec chat et analytics](https://github.com/EKKOLearnAI/hermes-studio) | GitHub Trending TS | #chatbot #LLM |
| [callstack/agent-device (🔥 +38 stars) — CLI pour contrôler des appareils iOS/Android via agents IA](https://github.com/callstack/agent-device) | GitHub Trending TS | #ReactNative |

### 💡 Insights clés
- **anthropics/knowledge-work-plugins : Anthropic ouvre ses outils internes Claude — mine de composants pour H'appi** — Anthropic publie en open-source ses plugins pour travailleurs du savoir (compatible Claude Code, Cowork). Pour H'appi : auditer immédiatement ce repo — ces plugins représentent les patterns officiels d'intégration Claude que l'on peut réutiliser dans nos chatbots clients. Avantage : validé par les ingénieurs Anthropic eux-mêmes, excellent argument de crédibilité en démo.
- **Graphify trending 3e fois en 10 jours (+1 107 stars) : knowledge graphs = infrastructure RAG de nouvelle génération** — graphify convertit un repo complet en graphe queryable pour IA. Le signal de trending répété valide que ce pattern remplace le RAG vectoriel classique pour les bases de code complexes. Pour H'appi : tester graphify sur le prochain projet avec une base de code legacy client — si l'onboarding est 2× plus rapide, l'intégrer dans notre kit standard.
- **NousResearch/hermes-agent + hermes-studio : écosystème agent complet en open-source** — Hermes Agent (backend) + Hermes Studio (dashboard web analytics) forment une stack agent autonome production-ready. Pour H'appi : hermes-studio est un modèle de tableau de bord pour monitorer nos chatbots clients — inspirer le design de notre futur dashboard H'appi avec les métriques clés (sessions, coût, intents).
- **moeru-ai/airi (42k stars, 3e journée trending) : le Voice AI self-hosted multimodal s'impose** — airi est un compagnon IA avec voice chat + gaming, auto-hébergeable. Apparaît pour la 3e fois consécutive en trending. Pour H'appi : ce niveau de trending valide un marché pour des expériences voice IA immersives en self-hosting. À explorer comme base pour un module "Voice Agent Personnalisé" RGPD-compliant sans dépendance ElevenLabs/Vapi.
- **callstack/agent-device : les agents IA arrivent sur mobile natif iOS/Android** — CLI de Callstack (experts React Native) pour contrôler des apps mobiles via agents IA. Pour H'appi : signal fort que les prochains mandats incluront des agents capables d'interagir avec des apps mobiles sans API. À surveiller pour l'intégration React Native des chatbots clients.
- **microsoft/markitdown trending : préparation de documents pour LLMs devenue commodité** — Outil de conversion Office → Markdown pour alimenter les LLMs, signé Microsoft. Pour H'appi : intégrer markitdown dans nos pipelines RAG pour les chatbots documentaires clients (PDF, Word, Excel → embedding). Économise le développement d'un parseur custom et bénéficie du support Microsoft.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack, Anthropic.com) — 17e jour consécutif** — Veille appuyée exclusivement sur GitHub Trending. Recommandation maintenue : débloquer les domaines dans la politique réseau de l'environnement remote pour diversifier les sources.

---
## 📰 Veille Tech — 2026-07-18
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Shubhamsaboo/awesome-llm-apps (🔥 +951 stars, 4e jour) — 100+ AI Agent & RAG apps clonables et déployables](https://github.com/Shubhamsaboo/awesome-llm-apps) | GitHub Trending 🐍 | #LLM #chatbot |
| [Graphify-Labs/graphify (🔥 +1 360 stars, 4e jour) — transformer code + schemas + docs en knowledge graph queryable pour IA](https://github.com/Graphify-Labs/graphify) | GitHub Trending 🐍 | #LLM #Claude |
| [HKUDS/DeepTutor (🔥 +531 stars) — plateforme de tutoring IA personnalisé lifelong](https://github.com/HKUDS/DeepTutor) | GitHub Trending 🐍 | #chatbot #LLM |
| [PostHog/posthog (🔥 +438 stars) — AI observability, analytics, session replay, feature flags, error tracking](https://github.com/PostHog/posthog) | GitHub Trending 🐍 | #SaaS |
| [tirth8205/code-review-graph (🔥 trending 🐍) — Local-first code intelligence graph pour MCP et CLI IA](https://github.com/tirth8205/code-review-graph) | GitHub Trending 🐍 | #LLM |
| [aws/agent-toolkit-for-aws — SDK officiel AWS pour construire des agents IA sur l'infrastructure Amazon](https://github.com/aws/agent-toolkit-for-aws) | GitHub Trending 🐍 | #LLM |
| [lobehub/lobehub (🔥 +409 stars) — Chief Agent Operator : organise des flottes d'agents IA en opérations 7×24](https://github.com/lobehub/lobehub) | GitHub Trending TS | #chatbot #LLM #SaaS |
| [anomalyco/opencode (🔥 +401 stars) — agent de coding open-source, 187k stars](https://github.com/anomalyco/opencode) | GitHub Trending TS | #LLM |
| [OpenCut-app/OpenCut (🔥 +1 074 stars) — alternative open-source à CapCut, full TypeScript](https://github.com/OpenCut-app/OpenCut) | GitHub Trending TS | #SaaS |
| [n8n-io/n8n (🔥 +160 stars) — plateforme d'automatisation workflow avec IA native, 400+ intégrations, self-hostable](https://github.com/n8n-io/n8n) | GitHub Trending TS | #SaaS #LLM #Docker |
| [firecrawl/open-lovable (🔥 +326 stars) — cloner et recréer n'importe quel site en app React moderne en quelques secondes](https://github.com/firecrawl/open-lovable) | GitHub Trending TS | #Next.js #SaaS |

### 💡 Insights clés
- **awesome-llm-apps 4e jour consécutif trending (+951 ⭐) : la bibliothèque RAG+Agent devient l'index de référence absolu** — Pour la 4e fois de suite, ce repo cumule les stars à grande vitesse. 100+ patterns IA clonables couvrent maintenant des cas d'usage verticaux (healthcare, finance, legal, e-commerce). Pour H'appi : institutionnaliser ce repo comme point d'entrée de chaque nouveau projet client — avant de coder, chercher si un pattern existe déjà. Cible : réduire le temps de setup initial de 50%.
- **graphify trending 4e fois (+1 360 ⭐ aujourd'hui, record) : les knowledge graphs s'imposent comme alternative au RAG vectoriel** — Le record de stars journalières sur graphify confirme que la communauté adopte massivement le pattern "code → knowledge graph → query IA". Pour H'appi : mettre graphify en production sur le prochain projet d'onboarding chatbot client avec base de code legacy. Objectif : démontrer une réduction du temps de contextualisation LLM, et packager ce service en prestation "Audit Base de Connaissance IA".
- **LobeHub "Chief Agent Operator" — l'orchestration d'agents 7×24 est un nouveau produit viable** — LobeHub positionne la gestion de flottes d'agents IA comme une couche opérationnelle à part entière (scheduling, reporting, supervision). Pour H'appi : ce paradigme "agent fleet ops" est la prochaine étape après les chatbots — commencer à construire un argumentaire commercial "Multi-Agent Ops" pour les clients enterprise qui ont plusieurs processus à automatiser en parallèle.
- **n8n 196k stars + IA native + Docker self-hostable : le workflow automation devient un composant clé des chatbots enterprise** — n8n combine 400+ intégrations avec des capacités IA natives et s'auto-héberge en Docker. Pour H'appi : n8n peut remplacer des développements custom d'intégration CRM/ERP dans nos chatbots clients (Salesforce, HubSpot, Notion, Slack, etc.). Proposer n8n comme middleware d'intégration dans nos offres enterprise réduit les coûts de développement tout en gardant la souveraineté des données (RGPD-compliant via self-hosting).
- **open-lovable — "clone n'importe quel site en React en secondes" : la génération de frontend IA s'accélère** — Firecrawl lance un outil qui scrape un site, le comprend, et génère une app React moderne. Pour H'appi : cet outil peut accélérer les maquettes de chatbot pour les clients en clonant leur site existant comme base de l'interface. Gain de temps en phase de design : 1-2 jours → quelques heures.
- **aws/agent-toolkit : AWS entre officiellement dans la course aux SDK agents** — Après Stripe et Google, AWS publie un toolkit officiel pour agents IA sur son infrastructure. Pour H'appi : surveiller ce toolkit pour les clients avec infrastructure AWS existante — intégration native avec S3, Lambda, Bedrock (Claude on AWS). Argument clé pour les gros comptes qui ne veulent pas quitter AWS.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack, Anthropic.com) — 18e jour consécutif** — Veille appuyée exclusivement sur GitHub Trending. Recommandation maintenue : débloquer les domaines dans la politique réseau de l'environnement remote pour diversifier les sources.

---
## 📰 Veille Tech — 2026-07-19
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [Claude Sonnet 5 désormais modèle par défaut pour tous les utilisateurs Free et Pro](https://releasebot.io/updates/anthropic/claude) | Anthropic News | #Claude #LLM |
| [Anthropic découvre le "J-space" : espace caché où Claude raisonne avant de répondre](https://www.technologyreview.com/2026/07/09/1140293/anthropic-found-a-hidden-space-where-claude-puzzles-over-concepts/) | MIT Technology Review | #Claude #LLM |
| [OpenAI GPT-Live : modèles voix full-duplex (écoute + parole simultanés) pour conversations naturelles](https://openai.com/index/introducing-gpt-live/) | OpenAI | #VoiceAI |
| [xAI Voice Agent Builder (beta) : plateforme no-code pour créer agents vocaux et call centers IA](https://www.aiapps.com/blog/july-ai-mega-update-major-breakthroughs-launches/) | AIapps | #VoiceAI #SaaS |
| [ElevenLabs en discussion pour une valorisation à 22 milliards de dollars](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI #SaaS |
| [Retell AI lance Conductor : interface graph-native pour tester et améliorer les agents vocaux en production](https://www.voiceaispace.com/news/voice-ai-news-2026-07-06) | VoiceAISpace | #VoiceAI |
| [Vercel Services : Docker + FastAPI + Next.js déployables ensemble en full-stack avec preview environments](https://community.vercel.com/t/vercel-weekly-2026-07-06/45111) | Vercel Community | #Vercel #FastAPI #Next.js #Docker |
| [Vercel AI SDK 7 : toolkit pour agents IA multi-turns, téléchargé 16M fois/semaine](https://vercel.com/blog/vercel-ship-2026-recap) | Vercel Blog | #Vercel #LLM |
| [AI Act : pleine application le 2 août 2026 — systèmes IA à haut risque sous obligation, amendes jusqu'à 35M€](https://www.donneespersonnelles.fr/actualite-ia-2026) | donneespersonnelles.fr | #RGPD |
| [Five Eyes : alerte conjointe sur l'intensification des cyberattaques exploitant l'IA](https://www.ayinedjimi-consultants.fr/articles/conformite/rgpd-comprendre-reglement-ia-ria.html) | Ayi Nedjimi Consultants | #RGPD |
| [SigNoz/signoz (🔥 +432 ⭐) — Observabilité OpenTelemetry-native avec APM, traces et logs pour apps IA](https://github.com/SigNoz/signoz) | GitHub Trending TS | #SaaS #Docker |
| [upstash/context7 (🔥 +69 ⭐, 59k stars) — Documentation de code always-up-to-date pour LLMs et AI code editors](https://github.com/upstash/context7) | GitHub Trending TS | #LLM |
| [agentscope-ai/agentscope — Framework Python pour construire des agents IA transparents et auditables](https://github.com/agentscope-ai/agentscope) | GitHub Trending 🐍 | #LLM |
| [fastapi/fastapi (🔥 trending) — FastAPI framework haute performance, prêt pour la production](https://github.com/fastapi/fastapi) | GitHub Trending 🐍 | #FastAPI |

### 💡 Insights clés
- **Claude Sonnet 5 = nouveau modèle par défaut depuis le 1er juillet : migration à planifier avant fin août** — Sonnet 5 tourne quasi au niveau d'Opus 4.8 sur de nombreuses tâches, à tarif réduit jusqu'au 31 août. Pour H'appi : évaluer les chatbots clients encore sur Sonnet 4.6 — un upgrade peut améliorer les résultats sans surcoût jusqu'à fin août. Opportunité commerciale : proposer une "mise à niveau IA gratuite" aux clients existants pour démontrer notre proactivité.
- **AI Act pleine application le 2 août 2026 — J-14 : audit de conformité urgent pour les chatbots clients à haut risque** — Santé, RH, éducation, juridique entrent dans le périmètre obligatoire dans 14 jours. Pour H'appi : identifier quels chatbots clients tombent en catégorie "haut risque", documenter les bases légales RGPD + exigences AI Act (transparence, supervision humaine, logs d'audit). Ne pas agir maintenant expose nos clients à 35M€ ou 7% de leur CA.
- **Voice AI en consolidation massive : OpenAI GPT-Live + xAI Voice Builder + ElevenLabs 22 milliards** — Trois signaux simultanés confirment que le Voice AI entre dans sa phase de commoditisation. Pour H'appi : formaliser une offre "Voice Chatbot RGPD-compliant" maintenant, avant saturation du marché — les early movers capteront les meilleurs contrats enterprise. Retell AI Conductor est une référence d'évaluation à intégrer dans notre pipeline QA.
- **Vercel Services = la stack H'appi (FastAPI + Next.js + Docker) native sur Vercel** — Vercel permet désormais de déployer FastAPI, Next.js et Docker dans un seul projet avec preview environments. Pour H'appi : migrer les nouvelles démos et prototypes clients vers Vercel Services — setup en quelques heures, preview URLs partageables avec les clients pour validation rapide, et Vercel AI SDK 7 pour les composants agents IA.
- **SigNoz trending fort (+432 ⭐) : l'observabilité IA est la prochaine attente des clients enterprise** — SigNoz est une alternative open-source self-hostable à Datadog/New Relic, orientée OpenTelemetry. Pour H'appi : proposer SigNoz dans notre offre chatbots enterprise comme dashboard d'observabilité (latences, erreurs, coûts tokens, volume sessions) — différenciant fort vs. concurrents sans monitoring structuré.
- **Anthropic J-space : l'explicabilité LLM progresse, argument commercial pour les secteurs réglementés** — La découverte d'un espace de raisonnement interne dans Claude ouvre la voie à une meilleure auditabilité. Pour H'appi : utiliser cette recherche comme argument client — "nos chatbots Claude sont les plus auditables du marché" — particulièrement pour santé, finance et juridique où l'explicabilité est une exigence AI Act.
- **WebSearch débloqué (1er jour) — sources enrichies : Anthropic, OpenAI, Vercel, RGPD, VoiceAI** — Première veille avec accès WebSearch en complément de GitHub Trending. HackerNews, DEV.to API et The New Stack restent bloqués. Recommandation : débloquer ces domaines pour une couverture maximale.

## 🩺 Happi Brain Health Check — 2026-07-20

### 1. Fichiers absents de l'index
Aucun problème détecté

### 2. Liens cassés
- memory/MEMORY_global.md:3 -> happi_brain.md (résolu en `memory/happi_brain.md`, inexistant — le fichier existe seulement à la racine, le lien devrait être `../happi_brain.md`)
- memory/MEMORY_quality_tracking.md:67 -> audit-details.md (résolu en `memory/audit-details.md`, fichier introuvable dans tout le repo)
- memory/MEMORY_quality_tracking.md:73 -> happi_brain.md (résolu en `memory/happi_brain.md`, inexistant — même problème que ci-dessus, devrait être `../happi_brain.md`)

### 3. Doublons / quasi-doublons potentiels
- `memory/project_microsoft_sales_app.md` vs `projects/microsoft-sales-app.md` : les deux fichiers ont été créés dans le même commit (0ab3dd9), mais seul `projects/microsoft-sales-app.md` a été mis à jour depuis (commit 96cffb6, ajout de l'inventaire complet des agents). Le fichier `memory/` renvoie d'ailleurs explicitement vers `projects/microsoft-sales-app.md` pour "les détails techniques complets" — probable snapshot devenu partiellement obsolète par rapport à la version curée dans `projects/`.

### 4. Fichiers potentiellement obsolètes (non modifiés depuis 60+ jours)
Aucun problème détecté

---
## 📰 Veille Tech — 2026-07-20
> Mis à jour automatiquement par Happi Brain Agent

| Article | Source | Tag |
|---------|--------|-----|
| [bojieli/ai-agent-book (🔥 +1 734 stars) — Guide open-source "深入理解 AI Agent" : comprendre les agents IA en profondeur](https://github.com/bojieli/ai-agent-book) | GitHub Trending 🐍 | #LLM |
| [rohitg00/ai-engineering-from-scratch (🔥 +501 stars) — Ressource complète d'ingénierie IA de zéro à la production](https://github.com/rohitg00/ai-engineering-from-scratch) | GitHub Trending 🐍 | #LLM |
| [MoonshotAI/kimi-cli (🔥 +410 stars) — Outil CLI agent IA par MoonshotAI](https://github.com/MoonshotAI/kimi-cli) | GitHub Trending 🐍 | #LLM |
| [PostHog/posthog (🔥 +411 stars) — Plateforme SaaS AI observabilité, analytics et session replay](https://github.com/PostHog/posthog) | GitHub Trending 🐍 | #SaaS #LLM |
| [tirth8205/code-review-graph (🔥 +663 stars) — Code intelligence graph local-first pour MCP et CLI IA](https://github.com/tirth8205/code-review-graph) | GitHub Trending 🐍 | #LLM #Claude |
| [kvcache-ai/ktransformers (🔥 +360 stars) — Framework flexible pour optimisation d'inférence et fine-tuning LLM](https://github.com/kvcache-ai/ktransformers) | GitHub Trending 🐍 | #LLM |
| [topoteretes/cognee (🔥 +303 stars) — Plateforme de mémoire IA open-source pour agents, avec PostgreSQL natif](https://github.com/topoteretes/cognee) | GitHub Trending 🐍 | #LLM #chatbot #PostgreSQL |
| [AstrBotDevs/AstrBot (🔥 +83 stars) — Agent IA multi-plateforme : WhatsApp, Telegram, WeChat, Discord, 200+ LLMs](https://github.com/AstrBotDevs/AstrBot) | GitHub Trending 🐍 | #chatbot #LLM #Docker |
| [Canner/WrenAI (🔥 +121 stars) — Plateforme GenBI text-to-SQL open-source](https://github.com/Canner/WrenAI) | GitHub Trending 🐍 | #LLM #SaaS |
| [diegosouzapw/OmniRoute (🔥 +1 343 stars) — AI gateway MIT gratuit : 268+ providers, 500+ modèles](https://github.com/diegosouzapw/OmniRoute) | GitHub Trending TS | #LLM #SaaS |
| [jamiepine/voicebox (🔥 +610 stars) — Studio vocal IA open-source : clonage de voix, dictée, création audio](https://github.com/jamiepine/voicebox) | GitHub Trending TS | #VoiceAI |
| [KnockOutEZ/wigolo (🔥 +595 stars) — Interface web pour agents de coding IA avec recherche local-first](https://github.com/KnockOutEZ/wigolo) | GitHub Trending TS | #LLM |
| [garrytan/gstack (🔥 +330 stars) — Setup exact de Claude Code par Garry Tan (Y Combinator) : 23 outils configurés](https://github.com/garrytan/gstack) | GitHub Trending TS | #Claude #Anthropic |
| [SigNoz/signoz (🔥 +345 stars) — Observabilité OpenTelemetry-native pour agents IA : APM, traces, logs](https://github.com/SigNoz/signoz) | GitHub Trending TS | #LLM #SaaS |
| [firecrawl/open-lovable (🔥 +34 stars) — Cloner n'importe quel site en app React moderne en quelques secondes](https://github.com/firecrawl/open-lovable) | GitHub Trending TS | #Next.js #SaaS |

### 💡 Insights clés
- **OmniRoute atteint +1 343 stars/jour — record du jour sur GitHub TS** — OmniRoute unifie 268+ providers (500+ modèles) derrière un endpoint OpenAI-compatible, MIT et gratuit. Il revient en tête du trending TS. Pour H'appi : l'adopter comme couche de résilience dans la stack de référence — fallback automatique Claude → GPT → Gemini si quota ou panne, sans refactoring backend. La progression de stars confirme que le multi-provider routing devient un standard de production en 2026.
- **topoteretes/cognee : mémoire IA native PostgreSQL — alignement parfait avec la stack H'appi** — Cognee est une plateforme de mémoire IA open-source pour agents avec PostgreSQL comme store natif (pgvector + knowledge graph). Pour H'appi : à intégrer dans les chatbots clients nécessitant une mémoire multi-sessions persistante — Cognee gère automatiquement les couches de mémoire (épisodique, sémantique, procédurale) sans développement custom. Alignment direct avec notre stack Railway + PostgreSQL + pgvector.
- **garrytan/gstack : le setup Claude Code de Garry Tan (Y Combinator) publié en open-source** — Le patron de Y Combinator publie ses 23 outils et configurations Claude Code. Pour H'appi : auditer ce setup pour identifier les outils manquants dans notre propre workflow Claude Code — les pratiques YC sont des indicateurs avancés des standards d'ingénierie qui vont devenir mainstream dans les 6-12 prochains mois.
- **jamiepine/voicebox +610 stars : studio vocal IA open-source complet — 2e apparition en veille** — Voicebox couvre le clonage de voix, la dictée et la création audio en TypeScript. Pour H'appi : alternative open-source gratuite à ElevenLabs pour les clients RGPD-strict ou cost-sensitive. À benchmarker sur la qualité vocale et la latence avant de le proposer comme option souveraine dans les mandats voice AI (surtout pertinent post-valorisation $22B ElevenLabs).
- **AstrBot multi-plateforme (WhatsApp, Telegram, Discord, WeChat, 200+ LLMs) — un seul agent, tous les canaux** — AstrBot est le framework le plus complet pour les chatbots multi-canal avec Docker natif. Pour H'appi : à évaluer pour les clients qui veulent un chatbot présent sur plusieurs canaux sans multiplier les déploiements. Architecture RGPD-compliant avec hébergement souverain possible.
- **Blocage réseau persistant (HackerNews, DEV.to API, The New Stack) — 19e jour consécutif** — Veille appuyée exclusivement sur GitHub Trending. Recommandation maintenue : débloquer les domaines dans la politique réseau de l'environnement remote pour diversifier les sources.

---
