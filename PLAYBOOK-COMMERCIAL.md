---
name: playbook-commercial
description: Playbook de vente H'appi — document unique à donner à un commercial pour prospecter et présenter la société, sans rien inventer : uniquement des chiffres et faits réels tirés des projets livrés.
metadata:
  type: sales-enablement
  audience: commercial / prospection
  last_updated: 2026-07-27
---

# 🧭 Playbook Commercial H'appi

> **À qui s'adresse ce document** : à toute personne qui doit présenter H'appi à un
> prospect — appel de découverte, rendez-vous, réponse à un appel d'offres. Tout ce
> qui est écrit ici est vérifiable dans les repos et les projets livrés — aucun chiffre
> inventé. Là où une donnée est une estimation ou un exemple fictif, c'est indiqué
> explicitement.

## Sommaire

0. [L'elevator pitch](#0-lelevator-pitch)
1. [Ce qu'on fait — 10 capacités IA](#1-ce-quon-fait--10-capacités-ia)
2. [Qui on aide — secteurs et vrais clients](#2-qui-on-aide--secteurs-et-vrais-clients)
3. [La preuve — cas client Mobilier de France](#3-la-preuve--cas-client-mobilier-de-france)
4. [Comment c'est construit — architecture](#4-comment-cest-construit--architecture)
5. [Le produit en détail — stack IA & comparatif concurrentiel](#5-le-produit-en-détail--stack-ia--comparatif-concurrentiel)
6. [Sécurité & conformité](#6-sécurité--conformité)
7. [Le modèle économique — pourquoi c'est moins cher](#7-le-modèle-économique--pourquoi-cest-moins-cher)
8. [Zoom produit — Happi-Secretary](#8-zoom-produit--happi-secretary)
9. [Zoom produit — Happi CRM](#9-zoom-produit--happi-crm)
10. [Zoom produit — DropOS](#10-zoom-produit--dropos)
11. [Calculateur ROI — méthodologie](#11-calculateur-roi--méthodologie)
12. [Objections fréquentes & réponses](#12-objections-fréquentes--réponses)
13. [Preuves sociales — 18 démos clients par secteur](#13-preuves-sociales--18-démos-clients-par-secteur)
14. [Checklist premier rendez-vous prospect](#14-checklist-premier-rendez-vous-prospect)

---

## 0. L'elevator pitch

> **H'appi est une startup franco-égyptienne (lancée début 2026) qui construit des
> chatbots IA et des outils digitals 100% sur-mesure pour les entreprises françaises —
> à 50 à 75% sous les prix du marché — parce qu'on facture le développement, pas la
> bureaucratie.**

Trois phrases à retenir pour ouvrir un appel :

1. *"On ne vend pas un template — on construit exactement l'outil dont le client a
   besoin, en 14 jours en moyenne."*
2. *"Chez Mobilier de France, notre premier client phare, ça a fait tomber les appels
   SAV de 65% et divisé le temps de traitement d'un litige par 15."*
3. *"Tout est hébergé en France/Europe, conforme RGPD, et le client reste propriétaire
   à 100% de son code — zéro vendor lock-in."*

**Positionnement** : CX (expérience client) + Supply Chain + Secrétariat IA.
**Philosophie** : "Qualité avant quantité" — personnalisation radicale, pas de solution
générique.

---

## 1. Ce qu'on fait — 10 capacités IA

Toutes nos solutions piochent dans les mêmes 10 briques technologiques, assemblées
différemment selon le client :

| # | Capacité | Ce que ça fait concrètement | Techno |
|---|----------|------------------------------|--------|
| 1 | Compréhension métier NLP | Claude analyse la terminologie sectorielle du client et s'adapte à ses process sans formation manuelle | Claude |
| 2 | Voix IA 24h/24 | Répond aux appels, prend RDV, transmet les messages — voix naturelle, latence < 500ms | Vapi · ElevenLabs · Deepgram |
| 3 | Vision & analyse photo | Analyse automatique de photos de défauts produit, résolution SAV sans intervention humaine | Claude Vision |
| 4 | Multilingue natif | FR, EN, AR, IT, DE et plus — détection automatique, réponse dans la langue du client | Claude |
| 5 | Détection de sentiment | Repère les clients VIP, les urgences, l'insatisfaction avant l'escalade — routage intelligent | Claude |
| 6 | Analytics & prédictif | KPIs temps réel, insights prédictifs pour anticiper les besoins clients | Claude |
| 7 | Intégration CRM/ERP | HubSpot, Salesforce, SAP, Shopify, ServiceNow via webhooks et API — zéro double saisie | API · Webhooks |
| 8 | Ticketing intelligent P0-P3 | Tickets créés, priorisés et assignés automatiquement, escalade auto des cas critiques | Claude |
| 9 | Qualification leads 3 phases | Identification → Qualification → Conversion, en conversation naturelle, direct vers le CRM | Claude |
| 10 | RGPD & souveraineté IA | Hébergement France/Europe, conformité ISO 27001, les données ne quittent jamais le périmètre client | Made in France |

**Argument à utiliser** : *"On n'a pas 10 produits différents — on a 10 briques, et on
construit la combinaison exacte dont vous avez besoin. C'est pour ça qu'on est plus
rapides ET moins chers qu'une agence qui repart de zéro à chaque projet."*

---

## 2. Qui on aide — secteurs et vrais clients

### 2.1 Les 11 secteurs couverts (clients réels, projets livrés)

| Secteur | Clients réels | Cas d'usage chatbot |
|---------|---------------|----------------------|
| Meuble / Déco | **Mobilier de France** ⭐, Monsieur Meuble | SAV, recommandations produits, suivi livraison |
| Hôtellerie | Lavorel Hotels | Réservation, concierge, FAQ |
| Agroalimentaire | Labeyrie, Saint-Jean, Mademoiselle Desserts | Support produits, recettes, SAV |
| BTP / Construction | Charier | Devis, planning, support technique |
| Industrie | Plastivaloire, Icelec | Support technique, commandes |
| Transport / Logistique | Groupe Trouillet | Suivi, dispatch, SAV |
| Notariat / Juridique | Groupe Monassier, Cabinet Arc | FAQ, RDV, information juridique |
| Finance / Audit | Audit Expert | FAQ, onboarding client |
| Sport | L'Olympique Lyonnais (L'OL) | Fan engagement, billetterie, infos |
| E-commerce | **INnatural** (cosmétiques naturels), KingKong, Top Tier Collection | Recommandations produits, suivi commande, support |
| KYC / Identité digitale | Uqudo | Onboarding, vérification, support |

> **Argument à utiliser** : *"On n'a pas de secteur de prédilection unique — on a
> onze secteurs couverts avec des clients réels et nommés. Si votre secteur n'est pas
> dans la liste, ce n'est pas qu'on ne sait pas faire, c'est qu'on n'y est pas encore
> allé."*

### 2.2 Le pitch par problème (à utiliser en fonction du secteur du prospect)

| Secteur | Douleur du prospect | Résultat mesuré / promesse | Solution vendue |
|---------|----------------------|------------------------------|------------------|
| SAV & Meuble | 300 appels/mois traités manuellement, 1 litige sur 4 sans preuve | **-65% d'appels SAV** *(chiffre réel Mobilier de France)* | Bot SAV + App Traçabilité livraisons avec signature numérique et photos |
| Hôtellerie | Réception saturée, questions répétitives, réservations manquées hors horaires | 24h/7j de disponibilité concierge | Concierge IA vocal + chatbot multilingue pour FAQ, réservations et upsell |
| Secrétariat (PME & cabinets) | Appels manqués, agendas non tenus, pas de secrétaire la nuit | < 500ms de latence vocale, jamais indisponible | Secrétaire IA vocale 24h/24 : RDV, FAQ, résumé email + SMS post-appel |
| E-commerce | Support débordé, recommandations manuelles, panier abandonné | **+34% de taux de conversion** *(chiffre réel INnatural)* | Bot recommandation produits + qualification leads en 3 phases + support 24h |
| Transport & Logistique | Suivi de flotte manuel, dispatch inefficace, clients sans visibilité | -40% de coûts de dispatch | Bot suivi livraison + dispatch IA + alertes automatiques temps réel |
| Notariat & Juridique | Standard saturé, clients mal informés, RDV mal qualifiés | -80% d'appels non qualifiés | Bot FAQ juridique + prise de RDV qualifiée + routage intelligent |

---

## 3. La preuve — cas client Mobilier de France ⭐

Notre projet le plus complet et le plus avancé techniquement. **Toujours commencer
une démo ou une réponse à appel d'offres par ce cas** — c'est le seul avec des
chiffres de production vérifiables sur plusieurs mois.

### Fiche client
- **Enseigne** : Mobilier de France (national, meuble/ameublement)
- **Repo** : `SAV-BOT-Meuble-de-france`
- **Produit livré** : Bot SAV après-vente + ticketing + App Traçabilité livraisons (mobile)
- **Statut** : en production

### Stack technique réelle
```
Backend   → FastAPI (Python 3.13) + PostgreSQL + Redis + Alembic
Frontend  → React 18.2
IA        → OpenAI GPT (intégration Claude possible)
Deploy    → Docker + docker-compose + Railway
CI/CD     → GitHub Actions + Codecov
Tests     → 351+ tests — couverture backend 62%, frontend 53%
```

### Fonctionnalités livrées
- Dialogue naturel multilingue : FR, EN, AR, IT, DE
- Recommandations produits intelligentes (AI-powered)
- Upload photo + analyse automatique des défauts visuels
- Ticketing automatique avec système de priorité P0-P3
- Support vocal (reconnaissance + synthèse)
- Détection d'émotion sur les messages vocaux (améliore la priorisation)
- Monitoring santé + métriques
- Sécurité : JWT auth, rate limiting, CORS

### Système de tickets (à montrer en démo — très visuel)
| Priorité | Cas | Délai de traitement |
|----------|-----|----------------------|
| P0 | Urgence sécurité | Immédiat |
| P1 | Produit inutilisable | < 4h |
| P2 | Problème fonctionnel | < 24h |
| P3 | Cosmétique / information | < 72h |

### Timeline de déploiement (le déroulé à raconter à un prospect)
| Période | Ce qui se passe |
|---------|--------------------|
| Semaine 1 | Bot SAV configuré et formé sur les processus Mobilier de France · App Traçabilité installée sur tous les terminaux livreurs · connexion bot ↔ app opérationnelle dès J+1 |
| Mois 1 | **-65% d'appels entrants** dès la 4ème semaine · 0 litige non documenté grâce à la preuve numérique · traitement après-vente passé de 2,5 jours à 4 heures |
| Mois 3 | +38 points de NPS mesurés sur les clients livrés · détection d'anomalies de tournée activée · SAV prédictif sur les modèles à risque élevé |

### Notre philosophie sur ce projet
*"Pas de modèle standard. On apprend la réalité du client et on construit en
conséquence — ici, un bot SAV et une app de traçabilité interconnectés dès le
premier jour."*

---

## 4. Comment c'est construit — architecture

On explique aux prospects que la plateforme H'appi tient sur **3 couches**, toujours
les mêmes, quel que soit le client :

1. **Couche conversationnelle** — le bot (texte ou voix) qui parle au client final,
   branché sur la base de connaissance du client (produits, FAQ, procédures).
2. **Couche métier** — les règles spécifiques au client : système de tickets P0-P3,
   qualification 3 phases, routage, escalade, intégrations CRM/ERP.
3. **Couche plateforme** — ce qui se réveille après 2-3 mois d'usage : les données
   collectées deviennent des recommandations, puis des modules SaaS activables à la
   carte (voir chapitre 7 sur le modèle économique).

### Pattern architecture réutilisé sur tous les projets chatbot

```
Widget embeddable (site existant client)      Chatbot full-stack (projet complet)
widget/                                        frontend/  → React / Next.js
  chatbot.js  → logique                        backend/
  chatbot.css → styles                           app/
  embed.js    → 1 script tag à intégrer            main.py
backend/                                            routers/  → chat, auth, tickets, webhooks
  server.js → Express ou FastAPI                    models/   → DB models
  claudeService.js → intégration IA                 services/ → claude_service, email_service...
  productKnowledge.js → base de connaissance       alembic/  → migrations DB
config/                                          docker-compose.yml
  products.json / faqs.json / bot-personality.json (éditables par le client sans dev)
```

### Système de qualification en 3 phases — le différenciateur produit

Toutes nos solutions intègrent ce système, qui **augmente la conversion de 34% par
rapport à un chatbot générique** *(mesuré sur le projet INnatural)* :

```
Phase 1 — Identification : qui est l'utilisateur ? quel est son besoin précis ? quel canal utilise-t-il ?
Phase 2 — Qualification  : quel produit ou service correspond ? quel niveau de priorité (P0-P3) ?
Phase 3 — Conversion     : proposition sur-mesure, collecte du lead ou action directe (ticket, RDV, achat)
```

### Modèle IA utilisé — et pourquoi

- **Modèle de référence : Claude (Anthropic)** — supérieur pour l'analyse post-appel,
  la compréhension de contexte long et le français naturel.
- Sonnet 4.6 = usage par défaut sur un chatbot standard. Opus 4.6 pour l'analyse
  complexe. Haiku 4.5 pour les réponses rapides à faible coût.
- Certains projets historiques tournent encore sur OpenAI GPT (ex. SAV-Bot Mobilier
  de France, migration vers Claude possible) — à ne jamais présenter comme un point
  faible : c'est un choix technique par projet, pas une limitation de la plateforme.

---

## 5. Le produit en détail — stack IA & comparatif concurrentiel

### 5.1 La stack IA H'appi

| Techno | Rôle | Pourquoi |
|--------|------|----------|
| **Claude (Anthropic)** | NLP · Analyse · Génération | Modèle de référence pour la compréhension métier et la génération de réponses complexes |
| **Vapi.ai** | Téléphonie IA | Latence < 500ms — idéal pour secrétariat vocal et callbots |
| **ElevenLabs** | Synthèse vocale | Voix naturelles ultra-réalistes en FR, EN, AR + 29 autres langues |
| **Deepgram** | Reconnaissance vocale | Transcription temps réel, 99%+ de précision en conditions réelles |

### 5.2 H'appi vs solutions génériques (Zendesk Bot, Intercom IA, ChatGPT brut)

| Critère | H'appi | Solutions génériques |
|---------|--------|------------------------|
| Personnalisation métier | Sur-mesure complet | Templates fixes |
| Hébergement | France / Europe (RGPD) | USA (soumis au CLOUD Act) |
| Langues | FR, EN, AR, IT, DE... | Anglais principalement |
| Voix IA | Intégrée (Vapi + ElevenLabs) | Optionnelle / payante en plus |
| Ticketing | P0-P3 natif | Basique ou absent |
| Délai de déploiement | 1 à 2 semaines | 2 à 6 mois |
| Support | Équipe dédiée + SLA | Self-service |

### 5.3 Pourquoi H'appi — 3 arguments détaillés

**1. Personnalisation sectorielle unique.** Connaissance métier intégrée dès la
conception (terminologie CX, workflows supply chain). Templates sectoriels prêts à
l'emploi (e-commerce, services B2B, logistique), apprentissage continu du vocabulaire
métier du client. *Stat marché à citer : 85% des interactions de service client
seront automatisées en France en 2025.*

**2. Intégration avec l'écosystème existant.** Connexion CRM, ERP, messaging,
e-commerce via API, sur-mesure selon la stack du client. Pas de migration, pas de
double saisie — le client garde ses outils, on ajoute l'intelligence. Outils
connectables : Salesforce, HubSpot, SAP, Oracle, Shopify, WooCommerce, WhatsApp,
Messenger, Microsoft Teams, Slack, ServiceNow, API générique.

**3. L'approche hybride humain-IA.** H'appi renforce les équipes, ne les remplace
pas. Le bot gère le répétitif (jusqu'à 80% du volume), transfère le complexe avec
tout le contexte. *Stats marché à citer : 51% des clients veulent concilier humain
et technologie, 36% privilégient l'humain, seulement 9% misent tout sur la
technologie — l'argument "on ne remplace pas, on augmente" est un vrai argument de
vente, pas juste une posture.*

---

## 6. Sécurité & conformité

> Argument d'ouverture : *"On applique les mêmes standards de sécurité que Microsoft
> et Oracle — chiffrement, MFA, monitoring 24/7, audits réguliers — mais à des coûts
> optimisés grâce à nos partenaires cloud européens."*

### 6.1 Hébergement — deux partenaires selon le besoin client

| | **Scaleway** 🇫🇷 France | **Hetzner** 🇩🇪 Allemagne / 🇫🇮 Finlande |
|---|---|---|
| Positionnement | Recommandé secteurs sensibles | Meilleur rapport coût/performance |
| Certifications actives | ISO 27001, ISO 27017, ISO 27018, HDS | ISO 27001, GDPR/RGPD |
| En cours | SecNumCloud, SOC 2 Type II | — |
| Notes | Filiale du groupe Iliad (Free). Datacenters Paris, Amsterdam, Varsovie | Fondé en 1997. Datacenters Nuremberg, Falkenstein, Helsinki |

**Garantie à donner au client, quel que soit le choix d'infra** : les données restent
100% dans l'Union Européenne.

Pour les secteurs santé, finance ou public → toujours recommander **Scaleway**
(certifié HDS, seule infra autorisée en France pour les données de santé sensibles).

### 6.2 Les 4 niveaux de sécurité (à détailler si le prospect est technique)

| Niveau | Contenu |
|--------|---------|
| 01 — Infrastructure | Datacenters haute sécurité (accès biométrique, vidéosurveillance 24/7), redondance électrique et réseau (uptime 99,9%+), protection DDoS native, isolation réseau (VLANs, firewalls) |
| 02 — Applicatif | Chiffrement TLS 1.3 pour toutes les communications, chiffrement AES-256 des données au repos, pare-feu applicatif (WAF), protection contre injections SQL/XSS/CSRF |
| 03 — Données | Sauvegardes automatiques quotidiennes chiffrées, rétention 30 jours minimum, tests de restauration réguliers, stockage géo-redondant |
| 04 — Accès | Authentification multi-facteurs (MFA) obligatoire, principe du moindre privilège, journalisation complète des accès, révocation immédiate en fin de collaboration |

### 6.3 Engagements RGPD

- Hébergement UE exclusif — aucun transfert de données hors Union Européenne
- Accord de sous-traitance (DPA) signé avec chaque client, conforme Article 28 RGPD
- Chiffrement de bout en bout (transit et repos)
- Contrôle d'accès strict avec MFA
- Notification d'incident sous 48h en cas de violation de données
- Procédures claires d'accès, rectification, effacement
- Audits de conformité disponibles sur demande
- Suppression certifiée de toutes les données en fin de contrat

### 6.4 FAQ sécurité — réponses prêtes à l'emploi

**"Mes données sont-elles vraiment en sécurité ?"**
Oui. Mêmes standards que Microsoft et Oracle (chiffrement, MFA, monitoring 24/7,
audits réguliers), à des coûts optimisés grâce aux partenaires européens.

**"Que se passe-t-il si mon hébergeur a une panne ?"**
Sauvegardes géo-redondantes + plan de reprise d'activité. Objectif de reprise en
moins de 4h après une panne majeure.

**"Puis-je changer d'hébergeur après le déploiement ?"**
Oui, absolument — le client est propriétaire à 100% de son code et de ses données.
Migration possible vers tout hébergeur européen, sans engagement de notre côté.

**"Que se passe-t-il avec mes données en fin de contrat ?"**
Le client choisit : restitution complète en format lisible (CSV, JSON, SQL) ou
suppression sécurisée certifiée, avec attestation écrite dans les deux cas.

**"Mes données de santé sont-elles protégées ?"**
Si données de santé → Scaleway certifié HDS, seule infra autorisée en France pour ce
type de données sensibles.

---

## 7. Le modèle économique — pourquoi c'est moins cher

### 7.1 Le problème de l'industrie IT traditionnelle

Les agences et ESN traditionnelles facturent : infrastructures cloud surcotées
(AWS/Azure/GCP avec marges confortables), licences propriétaires (Oracle, Microsoft,
SAP — des milliers d'euros par mois), organisation lourde (commerciaux, chefs de
projet, consultants), processus bureaucratiques (semaines de réunions et
validations).

**Résultat chez une agence classique : seulement 30 à 40% du budget va au
développement réel.**

### 7.2 Les 4 piliers de la solution H'appi

| Pilier | Description | Économie |
|--------|-------------|----------|
| Infrastructures cloud nouvelle génération | Fournisseurs innovants (Scaleway, Hetzner, Railway) au lieu des tarifs premium des grands clouds, mêmes performances | **-60 à -80%** sur les coûts d'infrastructure |
| Stack open-source et moderne | PostgreSQL, Node.js, Python, React, Next.js — aucune licence, communauté active | **Élimination complète** des coûts de licences (20-30% du budget traditionnel) |
| Organisation lean | Pas de commercial à 20% de marge, pas de chef de projet sans valeur ajoutée directe | **-40 à -50%** sur les coûts de main d'œuvre |
| Automatisation et réutilisation | Composants réutilisables, CI/CD automatisé, templates sectoriels | **-20 à -30%** de temps de développement |

### 7.3 Résultat par type de prestation — grille à utiliser en négociation

| Type de prestation | Écart vs marché | Avantage client |
|----------------------|--------------------|--------------------|
| Site web sur-mesure | -50 à -70% | Investissement divisé par 2 à 3 |
| Chatbot intelligent personnalisé | -50 à -65% | Accessible aux PME |
| Application web métier | -55 à -70% | Budget libéré pour le marketing |
| Application mobile (iOS + Android) | -50 à -60% | ROI plus rapide |
| Modules SaaS (upsell mensuel) | -60 à -75% | Coûts récurrents maîtrisés |

*Argument de clôture : "Même qualité, voire supérieure, grâce à notre expertise
technique et nos choix technologiques modernes."*

### 7.4 Le modèle d'upsell en 4 phases — comment on transforme un bot en plateforme

C'est l'argument le plus fort pour rassurer un prospect qui a peur de "trop
s'engager" dès le départ :

```
Phase 1 — Création sur-mesure       → tarif optimisé (50-70% sous le marché), livraison rapide
Phase 2 — Collecte de données       → automatique, RGPD-compliant (consentement, anonymisation)
Phase 3 — Analyse & recommandations → GRATUIT, après 3 à 6 mois, rapport détaillé personnalisé
Phase 4 — Activation modules SaaS   → à la carte, sans engagement long terme, facturation mensuelle flexible
```

**Exemple fictif (à présenter comme un exemple, pas un cas réel) pour un
e-commerce** : sur 6 mois d'analyse — 2 000+ interactions bot, 70% de questions sur
le statut de commande, 15% sur les retours produits → on recommanderait d'activer
le module CX Tracking Intelligent pour automatiser ces réponses.

**Pourquoi ce modèle est gagnant-gagnant :**

| Pour le client | Pour H'appi |
|-----------------|--------------|
| Investissement initial réduit | Relation long terme avec les clients |
| Pas d'engagement sur les modules | Revenus récurrents pour investir dans l'innovation |
| Valeur prouvée sur SES données | Incités à créer de vrais outils utiles (pas du remplissage) |
| ROI mesurable pour chaque module | Expertise sectorielle renforcée à chaque projet |
| Évolution progressive à son rythme | |

### 7.5 Grille tarifaire de référence (maintenance/support — hors implémentation)

| Formule | Prix | Pour qui |
|---------|------|----------|
| Support Essentiel | Inclus avec l'implémentation | Indépendants, entreprises en démarrage |
| Support Professionnel | 100-500€/mois | Entreprises en croissance, volume plus important — *formule la plus populaire* |
| Support Enterprise | 500-2000€/mois | Grandes organisations, SLA personnalisé, infrastructure dédiée |

> Implémentation : toujours du devis personnalisé, jamais de prix générique affiché.
> Argument : *"Le tarif dépend de vos besoins réels — scénarios, intégrations,
> volume. On en discute plutôt que d'afficher un prix qui ne voudrait rien dire."*

---

## 8. Zoom produit — Happi-Secretary

**Positionnement** : secrétariat IA vocal 24h/24 pour PME, cabinets, hôtels,
cliniques — remplace ou complète un standard téléphonique humain.

### Stack technique
```
Backend     → FastAPI + PostgreSQL + SQLAlchemy async
IA          → Claude (Anthropic) — conversation + analyse post-appel
Téléphonie  → Vapi.ai — latence < 500ms
Voix        → ElevenLabs (TTS) + Deepgram (STT)
Calendrier  → Cal.com API — prise de RDV en direct pendant l'appel
Notifs      → Resend (email) + Twilio (SMS)
Dashboard   → Next.js 14 + Tailwind CSS
```

### Flow d'appel complet (à montrer en démo)
```
Appelant → Vapi.ai → webhook "assistant-request"
        → Claude construit la réponse avec la base de connaissance du client
        → ElevenLabs synthétise la voix
        → [book_appointment] → réservation Cal.com en temps réel
        → [transfer_call]    → transfert vers un humain
        → [take_message]     → email + SMS instantané

Fin d'appel → webhook "end-of-call-report"
           → Claude analyse : résumé + sentiment + intention
           → email transcript + SMS résumé envoyés
           → webhook CRM déclenché automatiquement
```

### Les 6 fonctionnalités clés à présenter
| Fonctionnalité | Description |
|-----------------|--------------|
| Gestion des appels | Identifie l'appelant, route vers la bonne personne ou prend le message |
| Prise de rendez-vous | Planification automatique selon le calendrier réel — zéro conflit, zéro oubli |
| Messages intelligents | Messages vocaux transcrits, résumés et priorisés automatiquement |
| Répondeur professionnel | Voix naturelle, ton adapté au secteur — indétectable |
| Disponibilité 24h/24 | Jamais de pause, jamais de congé — 7j/7, 365 jours par an |
| Intégration en 48h | Google Calendar, Outlook, CRM du client — opérationnel en 2 jours |

### L'argument avant/après (très efficace en rendez-vous)
| Avant Happi-Secretary | Avec Happi-Secretary |
|--------------------------|---------------------------|
| Appels manqués | 100% des appels traités |
| Messages oubliés | Tous les messages enregistrés |
| Rendez-vous en double | Planification sans erreurs |
| Personnel interrompu | Équipe focalisée sur l'essentiel |
| Service limité aux heures de bureau | Service client 24h/24, 7j/7 |
| Coûts administratifs élevés | Économies significatives |

### Chiffres clés à citer
- 100% des appels traités
- Disponibilité garantie 24/7
- -70% de tâches administratives

### Fonctionnalités additionnelles (catalogue complet)
Support niveau 1 avec auto-escalation, prise de commandes, détection de sentiment
(positif/négatif/urgent), reconnaissance des appelants VIP, analyse IA post-appel
(résumé/intention/résultat), dashboard analytique, webhook CRM (HubSpot, Pipedrive,
Zapier, Make), multilangue auto-detect (FR/EN/ES), enregistrement RGPD-compliant.

### FAQ prête à l'emploi
**"Les clients sauront-ils que c'est une IA ?"** Non — voix naturelle, conversation
fluide, distinction imperceptible.
**"Comment ça s'intègre à mon calendrier ?"** Synchronisation automatique Google
Calendar / Outlook / iCal, disponibilité vérifiée en temps réel à chaque appel.
**"Mes données sont-elles sécurisées ?"** Sécurité niveau bancaire, chiffrement bout
en bout, hébergement France/Europe, conforme RGPD.
**"Combien ça coûte ?"** Dépend du volume d'appels — devis personnalisé et gratuit.
**"Combien de temps pour la mise en place ?"** 24 à 48 heures.

### Cas d'usage par secteur (à adapter selon le prospect)
Cabinets médicaux/dentaires (RDV + rappels auto, -40% d'absences), PME (service
client pro sans ressource RH dédiée), cabinets juridiques (tri d'appels + RDV +
demandes prioritaires), hôtels/restaurants (réservations 24h/24), écoles/universités
(secrétariat virtuel), centres d'appels (plus de volume sans plus d'effectifs).

---

## 9. Zoom produit — Happi CRM

**Positionnement** : "le CRM IA conçu pour les équipes qui veulent gagner — tout ce
qu'il faut, sans le prix d'un HubSpot."

### État du projet (à ne PAS sous-vendre — c'est le produit le plus avancé après le SAV-Bot)
- **28+ sprints livrés**
- **130+ endpoints API**
- **16+ pages frontend**
- Repo : `github.com/nbayonne76-ui/Happi-CRM`

### Stack technique
```
Backend   → FastAPI 0.135+ + PostgreSQL 16 + SQLAlchemy 2 + Alembic
Frontend  → Next.js 16 + TypeScript + Tailwind CSS + shadcn/ui
IA        → Claude Sonnet 4.6 (Anthropic) + OpenAI GPT-4o en fallback
Cache     → Redis 7
Auth      → JWT (access + refresh)
Tests     → pytest, 37 tests
```

### Les 16 modules (à citer en bloc pour montrer l'exhaustivité)
Tableau de bord · Contacts · Entreprises · Pipeline de ventes · Leads qualifiés par
IA · Devis (PDF) · Catalogue produits · Emails & campagnes · Activités · Support
client · Analyses & rapports · Prévisions de ventes · Équipe · Intégrations ·
Assistant IA · Paramètres.

### L'AI Intelligence Suite — 9 outils IA (argument différenciant le plus fort face à HubSpot/Salesforce)

| Question du commercial | Ce que fait le CRM |
|---------------------------|------------------------|
| "Extrais le contact depuis ce texte" | Extrait automatiquement les infos d'un contact depuis un email ou une carte de visite |
| "Quel est le prochain pas sur ce deal ?" | Recommande la prochaine meilleure action (Next Best Action) |
| "Analyse notre pipeline" | Analyse IA complète du pipeline en cours |
| "Recherche des infos sur Acme Corp" | Recherche d'opportunité sur une entreprise donnée |
| "Probabilité de gagner ce deal ?" | Scoring IA de la probabilité de closing |
| "Résume cette réunion" | Résumé de réunion → liste d'actions à faire |
| "Quels deals sont bloqués ?" | Détecte les deals stagnants + recommandations |
| "Score ce lead" | Note un lead de 0 à 100 |
| "Rédige un email pour ce prospect" | Génère un email commercial prêt à envoyer |

*Argument à utiliser telle quelle : "Vous ne cliquez pas dans 15 menus pour avoir une
info — vous la demandez en langage naturel, comme à un collègue."*

### Intégrations
Slack, Gmail, Cal.com, Vapi (téléphonie — connexion directe avec Happi-Secretary),
SAP (ERP), Generix (ERP/WMS supply chain), webhooks entrants pour les chatbots H'appi
(un lead capté par le chatbot SAV atterrit direct dans le pipeline commercial).

### Grille tarifaire CRM
| Formule | Prix | Contenu |
|---------|------|---------|
| Starter | Devis personnalisé | Déploiement Docker + 1 mois de support |
| Pro | 300-800€/mois | Starter + intégrations avancées + mises à jour |
| Enterprise | 800-2000€/mois | Pro + SLA + personnalisations + formation |

### L'argument concurrentiel à retenir
**HubSpot Pro coûte 90€/utilisateur/mois + environ 15 000€ d'implémentation.**
Happi CRM inclut l'IA Claude nativement (pas un add-on payant), est hébergé en
France/Europe (RGPD), et le client reste propriétaire de son code et de ses données.

---

## 10. Zoom produit — DropOS

> Ce produit vise un marché différent (dropshippers e-commerce, souvent hors France)
> — à ne présenter que si le prospect correspond à ce profil précis. Statut actuel :
> phase de lancement "founding members" (100 places, 1 an gratuit contre feedback).

**Vision** : remplacer 6-7 outils payants fragmentés (analytics, fulfillment,
sourcing, marketing) par une seule plateforme.

- **Cible** : dropshippers à $10K-$200K de chiffre d'affaires mensuel, frustrés par
  des stacks à $400-$1000/mois d'outils
- **Pricing prévu** : $99-149/mois (remplace $400-1000/mois d'outils multiples)
- **Stack** : Next.js + FastAPI + PostgreSQL + JWT, intégration Shopify Partner API,
  tarifs douaniers US HTS / EU TARIC

### Ce qu'aucun autre outil SMB ne propose actuellement
1. Failover stock multi-fournisseurs en temps réel
2. Calcul du profit net réel (duties, chargebacks, fees, remboursements déduits)
3. Dashboard consolidé multi-boutiques
4. Scoring fournisseurs + routage automatique
5. Orchestration retours unifiée
6. Calculateur de landed cost avec données tarifaires live

### Roadmap produit
| Phase | Focus |
|-------|-------|
| Phase 1 (MVP) | Analytics — profit réel, landed cost, dashboard multi-boutiques |
| Phase 2 | Fulfillment — sync fournisseurs, failover stock, retours |
| Phase 3 | Sourcing — recherche produits, scoring fournisseurs, tendances |
| Phase 4 | Marketing — flows email, automation avis, tracking ads |

---

## 11. Calculateur ROI — méthodologie

Le calculateur ROI présenté aux prospects (ex. sur le site ou en démo live) répond à
la question : *"Combien H'appi vous fait économiser sur votre support après-vente ?"*

**Entrées demandées au prospect :**
1. Nombre d'appels/tickets après-vente par mois (tickets, emails, appels confondus)
2. Temps moyen passé par contact (en minutes)
3. Coût horaire chargé d'un agent (salaire + charges)

**Sortie calculée :**
- Coût actuel estimé (mensuel)
- Économies mensuelles avec H'appi (hypothèse : ~65% d'automatisation, basé sur le
  chiffre réel Mobilier de France)
- Heures libérées par mois
- Appels automatisés par mois
- Projection d'économies annuelles

**Sources citées pour la crédibilité de la méthodologie** : données Narvar, Gorgias
et Zendesk 2024 sur les benchmarks de coût de traitement d'un ticket SAV.

> **Règle d'usage** : ne jamais présenter le résultat du calculateur comme une
> garantie contractuelle — toujours le présenter comme une estimation basée sur des
> hypothèses réalistes, avec le vrai chiffre Mobilier de France (-65%) comme seule
> preuve dure.

---

## 12. Objections fréquentes & réponses

**"Pourquoi pas juste utiliser ChatGPT / un GPT personnalisé ?"**
ChatGPT brut n'a pas de mémoire métier persistante, pas de ticketing, pas
d'hébergement européen garanti, pas de qualification 3 phases, pas d'intégration
CRM/ERP native. H'appi construit l'infrastructure complète autour du modèle IA — le
modèle n'est qu'une des 10 briques (voir chapitre 1).

**"Comment être sûr que vous livrez vraiment en 14 jours ?"**
Chiffre issu du déploiement réel Mobilier de France (voir chapitre 3, timeline
semaine 1). C'est une moyenne, pas une promesse universelle — la fourchette dépend de
la complexité des intégrations demandées.

**"Vous êtes une petite structure, est-ce risqué ?"**
Arguments à opposer : hébergement chez les mêmes standards que Microsoft/Oracle
(chapitre 6), code 100% propriété du client dès la livraison (pas de dépendance à
H'appi pour continuer à faire tourner l'outil), pas de vendor lock-in.

**"Pourquoi moins cher, il y a un piège ?"**
Non — voir le détail complet chapitre 7 (pas de commercial à 20% de marge, stack
open-source à 0€ de licence, cloud nouvelle génération 40-60% moins cher que les
tarifs premium AWS/Azure). La structure de coût est structurellement différente,
pas un discount marketing.

**"On a déjà un CRM (HubSpot/Salesforce), pourquoi changer ?"**
Ne pas pousser à changer de CRM si le client en a déjà un qui fonctionne — proposer
plutôt le chatbot ou le secrétariat IA connecté à SON CRM existant via webhook
(voir chapitre 5.3, "intégration avec l'écosystème existant"). Le CRM Happi CRM ne
se vend en remplacement que si le client cherche explicitement une alternative moins
chère à HubSpot/Salesforce.

---

## 13. Preuves sociales — 18 démos clients par secteur

18 démos HTML statiques construites pour convaincre des prospects avant le
développement du vrai bot. **Argument à utiliser** : *"On peut vous montrer une
démo fonctionnelle de votre secteur en moins d'un jour, avant même de signer quoi
que ce soit."*

| Client | Secteur |
|--------|---------|
| Mobilier de France | Meuble |
| Monsieur Meuble | Meuble |
| Lavorel Hotels | Hôtellerie |
| Labeyrie Fine Foods | Agroalimentaire |
| Saint-Jean | Agroalimentaire |
| Mademoiselle Desserts | Agroalimentaire |
| Charier | BTP / Construction |
| Groupe Plastivaloire | Industrie / Plasturgie |
| Icelec | Électronique |
| Groupe Trouillet | Transport / Logistique |
| Groupe Monassier | Notariat |
| Cabinet Arc | Juridique |
| Audit Expert | Finance / Audit |
| King Kong | E-commerce |
| INnatural | E-commerce / Cosmétiques |
| Uqudo | Identité digitale / KYC |
| L'Olympique Lyonnais (L'OL) | Sport |
| Benta | Commerce |

*Leçon interne : ces démos statiques se livrent en moins d'un jour — c'est le
meilleur outil pour obtenir un accord de principe avant de démarrer le vrai
développement.*

---

## 14. Checklist premier rendez-vous prospect

- [ ] Ouvrir avec l'elevator pitch (chapitre 0)
- [ ] Identifier le secteur du prospect → sortir le bon pitch-problème (chapitre 2.2)
- [ ] Si le secteur a un client H'appi nommé (chapitre 2.1/13) → le citer explicitement
- [ ] Présenter le cas Mobilier de France si le prospect n'a pas encore de preuve concrète en tête (chapitre 3)
- [ ] Ne jamais annoncer de prix fixe — toujours "devis personnalisé sous 48h" (chapitre 7.5)
- [ ] Si objection sécurité/RGPD → chapitre 6, jamais improviser un chiffre
- [ ] Si objection prix → chapitre 7 (structure de coût), jamais dire "c'est juste moins cher"
- [ ] Terminer par le modèle d'upsell 4 phases (chapitre 7.4) pour rassurer sur l'engagement initial faible
- [ ] Proposer une démo sectorielle HTML sous 24-48h si le prospect hésite encore (chapitre 13)

---

*Document vivant — à mettre à jour à chaque nouveau client signé, nouveau chiffre de
production disponible, ou nouvelle objection rencontrée en rendez-vous. Toute
correction : dire "mets à jour le playbook commercial" à Claude Code dans ce repo.*
