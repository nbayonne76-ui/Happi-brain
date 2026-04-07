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
- **Type** : Application commerciale (ancienne)
- **Stack** : JavaScript

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

*Dernière mise à jour : 2026-04-07*
*Projets analysés : 28 repos GitHub (nbayonne76-ui)*

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
