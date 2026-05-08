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
