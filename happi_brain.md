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
