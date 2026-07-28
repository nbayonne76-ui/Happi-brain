# 📣 Veille Marketing & Croissance

> Alimenté automatiquement chaque semaine par l'agent Happi Brain — Marketing Director.
> Revue hebdomadaire : cohérence des messages du site vs le playbook commercial, pipeline
> de contenu blog, veille concurrentielle, note SEO technique, et stratégie de croissance
> & visibilité (section principale). Chaque semaine reprend et fait avancer les idées
> encore ouvertes de la semaine précédente plutôt que de repartir de zéro.

---
## 📣 Revue hebdomadaire — 2026-07-28
> Première revue — pas d'historique antérieur à vérifier ou à faire avancer.

### 1. Audit de cohérence des messages

Le site public contient **plusieurs incohérences internes**, pas seulement des écarts
avec le playbook — certaines contredisent le playbook ET se contredisent entre elles
sur la même page. À trancher par un humain, aucune valeur n'a été choisie arbitrairement.

**Délai de livraison — 5 chiffres différents en circulation sur le site**
| Valeur | Emplacement |
|--------|-------------|
| "14 jours" | `h-appi-website/components/ui/ExitIntentPopup.tsx:69`, `components/Testimonials.tsx:22`, `components/about/ValuesSection.tsx:24`, `app/[locale]/a-propos/page.tsx:57` |
| "3 semaines" | `messages/fr.json` (`hero.subtitle`/`hero.stats.adoption`, via `components/Hero.tsx:57,63`), `app/[locale]/opengraph-image.tsx:105-106,118` |
| "2 semaines" | `components/ui/Ticker.tsx:10`, `components/quiz/SolutionQuiz.tsx:154-156` |
| "2 à 3 semaines" | `components/HowItWorks.tsx:24`, `components/ComparisonTable.tsx:22` |
| "3 à 4 semaines" | `app/[locale]/atelier/page.tsx:140` |
| "14 jours en moyenne" / "1 à 2 semaines" | `Happi-brain/PLAYBOOK-COMMERCIAL.md:48` (ch.0) et `:246` (ch.5.2) |

**Économie de coût — un "4x moins cher" fixe vs des fourchettes ailleurs**
- "4x moins cher" (= 75% fixe) → `messages/fr.json` (`hero.stats.cost`, via `components/Hero.tsx:71-72`), `app/[locale]/opengraph-image.tsx:105-106`
- "-50% à -75%" → `components/about/PricingStrategy.tsx:38` (correspond au playbook `:42`)
- "50 à 70%" → `components/about/ValuesSection.tsx:25`
- Playbook : "50 à 75%" global (ch.0) mais "-50 à -65%" spécifique chatbot (ch.7.3, `:364-367`) — aucune fourchette du playbook ne devient jamais un "4x" fixe.

**Happi CRM — nombre d'outils IA**
- Site : "4 Fonctionnalités IA" → `app/[locale]/crm/CrmContent.tsx:13,138`
- Playbook : "9 outils IA" (AI Intelligence Suite, ch.9) → `PLAYBOOK-COMMERCIAL.md:520`

**Mobilier de France — un "-80% de litiges" que le playbook n'a jamais dit**
- Site : "−80% de litiges" → `app/[locale]/blog/[slug]/page.tsx:979,1112,1178`, `components/quiz/SolutionQuiz.tsx:167,169`
- Playbook ch.3 (`:120-171`) ne donne que "0 litige non documenté" pour Mobilier de France — le "-80%" existe dans le playbook mais pour un **autre secteur/métrique** : Notariat, "-80% d'appels non qualifiés" (`:116`). Le site semble avoir réutilisé ce chiffre sur le mauvais cas client.

**Nombre de clients — le site se contredit lui-même**
- "2 Clients actifs" (liste affichée : Mobilier de France + INnatural seulement) → `app/[locale]/a-propos/page.tsx:56,50-51`
- "17+ projets livrés · 11 secteurs" → `components/about/JoinSection.tsx:97,196`
- Playbook ch.2.1 (`:86-100`) liste ~17 clients nommés sur 11 secteurs — cohérent avec le "17+", pas avec le "2".

**Chiffres du playbook absents du site (à noter, pas forcément un bug)**
- NPS "+38 points" et "2,5 jours → 4 heures" / "÷15" (Mobilier de France, ch.3)
- Stat marché "85% des interactions automatisées en France en 2025" (ch.5.3) — le site n'a qu'un "85%" sans rapport (stat Gartner ROI IA, `blog/[slug]/page.tsx:1192`)
- Répartition "51%/36%/9%" humain vs IA (ch.5.3)
- Détail hébergement Scaleway/Hetzner, HDS, SecNumCloud, SOC 2 — les clés `messages/fr.json` (`securitePage.hostingTitle/certsTitle/...`) existent mais **ne sont pas rendues** par `app/[locale]/securite/page.tsx` ; la page live n'affiche qu'un badge générique "ISO 27001".
- Les grilles tarifaires CRM et support (`components/pricing/BillingToggle.tsx`) correspondent exactement au playbook — aucun écart là-dessus.

---

### 2. Pipeline de contenu blog

**12 articles déjà en ligne** (thèmes couverts, pour référence) : Mobilier de France -65%,
Happi Secretary 24h/24, qualification 3 phases +34%, Claude vs GPT-4o 2026, ROI chatbot
SAV, méthode 14 jours démo→prod, RGPD + AI Act 2026, coût d'une livraison ratée, SAV
ameublement, personnalisation ≠ prénom, sur-mesure vs standard, 5 tendances chatbot 2026.

**3 sujets neufs proposés** (aucun encore traité) :

1. **"Agent IA vs chatbot classique : le vrai changement de 2026"** — différence
   agent (exécute des actions : booking, remboursement, CRM) vs chatbot (répond
   seulement) · 3 exemples concrets PME · comment évaluer si son chatbot actuel est
   "agentic-ready" · pourquoi ça redéfinit le ROI attendu.
   *Pourquoi maintenant* : HubSpot/Salesforce positionnent 2026 comme la bascule
   "copilot → agentic" ; H'appi ne l'a pas encore nommée alors que c'est exactement
   ce que fait Happi CRM/Secretary.

2. **"Le vrai coût des appels manqués (et pourquoi votre standard vous coûte des
   clients)"** — chiffre choc appels manqués jamais rappelés · coût caché client
   perdu vs secrétaire humain (2000-3500€/mois) vs secrétariat IA · mini cas d'usage
   artisanat/services · lien direct Happi-Secretary.
   *Pourquoi maintenant* : angle complémentaire au post existant sur les livraisons
   ratées, mais rien sur les appels/RDV manqués — sujet chaud chez les concurrents
   télécom-IA français.

3. **"WhatsApp Business + IA : le canal que les PME françaises ignorent encore"** —
   contexte Meta Business Agent (juin 2026) · taux d'ouverture WhatsApp 98% vs email
   pro 21% · cas d'usage PME (FAQ, catalogue, RDV) · positionnement H'appi vs offres
   génériques (Meta, Botnation).
   *Pourquoi maintenant* : aucun article H'appi sur la messagerie sociale, alors que
   le sujet accélère fortement pour les PME françaises en 2026.

---

### 3. Veille concurrentielle (7 derniers jours)

**Rien de majeur daté précisément du 21 au 28 juillet 2026** chez les concurrents
directs (chatbot, CRM IA, secrétariat/téléphonie IA) — pas de nouvelle tarification,
pas de nouveau client phare, pas de levée de fonds dans la fenêtre exacte. Deux
signaux un peu plus anciens restent utiles pour le positionnement :

- **Tarification à la performance chez les gros CRM** — Salesforce Agentforce
  (Help Agent / Customer Service Portal, ~2$/résolution par blocs de 1000+) et
  HubSpot Breeze (0,50$/conversation résolue), tous deux passés en usage-based
  pricing courant juillet 2026. Argument à exploiter : H'appi reste en tarif fixe
  et prévisible (chapitre 7 du playbook) — un vrai contraste pour des PME françaises
  méfiantes du "pay-per-use" imprévisible.
- **Gradium (spin-off Kyutai, Paris)** a étendu son tour de seed à plus de 100M$
  avec Nvidia comme investisseur (~3 semaines avant la fenêtre). Pas un concurrent
  direct (couche modèle vocal, pas produit SMB), mais un signal fort que l'IA vocale
  française attire de l'argent sérieux — utile pour renforcer le narratif "IA
  vocale souveraine/européenne" de Happi-Secretary.
- Rien de notable chez Crisp, Dydu, Zendesk AI, Intercom/Fin, Zaion, Calldesk, Yelda,
  Allo-Media, Golem.ai, Vapi ou Synthflow spécifiquement cette semaine.

---

### 4. Note SEO (portée limitée)

**Vérification technique impossible ce run** : `https://happi-bot.com/sitemap.xml`,
le homepage, `/tarifs` et `/robots.txt` renvoient tous **HTTP 403 Forbidden** — testé
à la fois via WebFetch et via une requête curl directe (User-Agent navigateur inclus),
même résultat. Cause probable : un WAF/CDN (type Cloudflare) bloque la signature de
requête de cet environnement cloud, pas nécessairement un problème réel pour de vrais
visiteurs ou Googlebot. **À revérifier depuis un navigateur normal ou un crawler
classique (Screaming Frog) — pas exploitable depuis cet environnement.**

**Rappel obligatoire** : les métriques Google Search Console (impressions, clics,
positions) ne sont **pas disponibles** dans cet environnement cloud — connectées
uniquement sur la machine locale du fondateur. Aucun chiffre de trafic n'a été
estimé ou inventé ici ; à vérifier séparément par le fondateur.

---

### 5. Croissance & visibilité

Toutes nouvelles cette semaine (première revue, rien à poursuivre). 4 initiatives,
classées par effort croissant — la dernière est volontairement moins évidente que
"poster plus sur LinkedIn".

**A. Se faire lister dans la cartographie Hub France IA** — répertoire officiel
(soutenu par la DGE) de 972 acteurs IA en France, **utilisé activement par le réseau
des CCI** dans le cadre de leur partenariat pour sensibiliser 20 000 TPE/PME à l'IA.
Gratuit, à candidater directement. Intérêt : c'est le répertoire que les CCI
recommandent concrètement à leurs adhérents PME — H'appi coche exactement la case
"solution IA souveraine pour PME" que ce partenariat cherche à mettre en avant.

**B. Candidater au Vapi Solutions Partner Program (partner directory)** — Vapi
propose un programme partenaire avec co-vente et un annuaire public de partenaires
(`vapi.ai/partnerships/directory`). H'appi construit déjà Happi-Secretary sur Vapi
(cf. playbook ch.8) — devenir partenaire listé capte de la découverte entrante de
prospects qui cherchent spécifiquement un intégrateur Vapi en France, sans travail
de contenu supplémentaire.

**C. Soumettre Happi-Secretary à l'App Store de Cal.com** — Happi-Secretary utilise
déjà Cal.com pour la prise de RDV en direct (playbook ch.8). Cal.com a un app store
tiers ouvert aux développeurs. Une fiche d'intégration exposerait H'appi à une base
d'utilisateurs déjà équipés de scheduling — un public adjacent à la cible PME/cabinets,
sans budget d'acquisition.

**D. [Angle original] Canal de recommandation via les experts-comptables** — au lieu
de viser directement les dirigeants de PME, construire une offre d'apporteur d'affaires
avec des cabinets d'expertise-comptable : ils voient en premier les PME qui perdent du
CA sur des appels/RDV manqués (chiffres clients), et sont un tiers de confiance que
les startups IA n'utilisent presque jamais comme canal. Proposer une commission de
recommandation simple + un pitch clé-en-main ("votre client rate des appels, voici
Happi-Secretary") que le comptable peut caser en 2 minutes lors d'un rendez-vous
bilan. Canal B2B2B non conventionnel, à fort niveau de confiance, quasi inexploité
par la concurrence IA vocale/CRM.

**À suivre la semaine prochaine** : vérifier si A/B/C ont été initiés, et creuser
un premier partenariat pilote (1 cabinet comptable, ou 1 CCI régionale) pour D plutôt
que de viser un déploiement national d'emblée.
