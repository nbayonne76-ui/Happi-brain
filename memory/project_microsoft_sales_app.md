---
name: Microsoft Sales App — pattern SaaS réutilisable
description: L'architecture agents autonomes + KB-grounding + multi-tenant construite dans microsoft-sales-app est un pattern généralisable pour un futur produit de sales intelligence — mais ce n'est pas un CDP type Dynamics 365 Customer Insights
type: project
---

Microsoft Sales App a été construit comme outil interne (Partner Account Manager Microsoft),
mais l'architecture qui en résulte est un **pattern SaaS réutilisable** pour de futurs clients :
watchlist de comptes cibles → recherche externe (Tavily/DDG) → scoring par règles → synthèse
GPT ancrée dans une knowledge base → persistance par utilisateur (multi-tenant) → digest
périodique. Voir détails techniques complets : [projects/microsoft-sales-app.md](../projects/microsoft-sales-app.md).

**Précision importante donnée à Nicolas (14-18/07/2026)** : ce n'est PAS l'équivalent de
Dynamics 365 Customer Insights. D365 CI est une vraie CDP (Customer Data Platform) — elle
unifie des données de première partie sur des CLIENTS EXISTANTS à l'échelle (résolution
d'identité, profils unifiés, scale entreprise). Ce qu'on a construit surveille des PROSPECTS
via des signaux publics tiers (actualités, recrutement, appels d'offres) — catégorie plus
proche de ZoomInfo/Cognism (intent data) ou Klue/Crayon (competitive intelligence), combinée à
un générateur de contenu IA ancré KB. Pas de profils clients unifiés, pas de scale CDP.

**Why (pourquoi c'est important pour Happi Brain)** : si un futur client H'appi a besoin d'un
outil de sales/marketing intelligence (pas un CDP), ce pattern est directement réutilisable en
remplaçant la KB (prix/produits Microsoft → catalogue du client) et les règles de scoring
(secteur Microsoft → secteur du client). Le garde-fou "fix structurel = auto-commit, fix
contenu/prix = PR humaine" (dans l'agent de correction d'articles) est aussi un pattern
générique à réutiliser pour tout agent de correction de contenu généré par IA.

**How to apply** : avant de proposer "on peut construire un CDP" ou "équivalent Customer
Insights" à un client, vérifier qu'il parle bien de sales intelligence sur des prospects (bon
fit pour ce pattern) et non d'unification de données clients existants à l'échelle (mauvais
fit — nécessiterait une vraie architecture CDP, pas ce pattern agents+KB).
