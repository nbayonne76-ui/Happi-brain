# 🏛️ Veille Architecture & Blueprints

> Alimenté automatiquement chaque jour par l'agent Happi Brain — Architecture & Blueprints.
> Contrairement aux sections "Veille Tech" de happi_brain.md (repos/news tendance), ce fichier capture des architectures de référence, blueprints et design patterns issus de sources fiables (cloud providers, engineering blogs reconnus, auteurs établis), avec leur applicabilité concrète aux projets H'appi.

---
## 🏛️ Veille Architecture — 2026-07-26
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**Building Effective AI Agents (workflows vs agents)** — [lien](https://www.anthropic.com/engineering/building-effective-agents)
*Source* : Anthropic, engineering blog (Erik Schluntz & Barry Zhang), publication de référence toujours citée comme canonique en 2026
*Le pattern* : distingue les **workflows** (LLM + outils orchestrés par un chemin de code prédéfini — prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer) des **agents** autonomes (le LLM décide lui-même des étapes en boucle). Recommandation centrale : commencer par le pattern le plus simple possible (appels API directs, sans framework), et n'augmenter la complexité que si le besoin le justifie réellement.
*Pourquoi cette source est fiable* : documentation officielle d'Anthropic issue de retours d'expérience directs avec des dizaines d'équipes ayant déployé des agents Claude en production.
*Applicabilité H'appi* : directement transposable à l'AI Intelligence Suite du CRM (predict-win, next-action, research…) — chaque outil devrait être audité pour savoir s'il a vraiment besoin d'un agent autonome ou si un simple workflow orchestrator-workers (moins cher, plus prévisible, plus facile à debugger) suffit.

**AI Agent Orchestration Patterns** — [lien](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns)
*Source* : Azure Architecture Center, Microsoft Learn (documentation officielle cloud provider)
*Le pattern* : catalogue de patterns de coordination multi-agents — Sequential (chaîne linéaire d'agents), Concurrent (agents en parallèle sur la même tâche), Group Chat / Supervisor (un agent superviseur distribue le travail), Handoff (transfert de contrôle entre agents spécialisés), et Magentic (planification dynamique par un orchestrateur qui adapte le plan en cours de route).
*Pourquoi cette source est fiable* : documentation d'architecture officielle d'un cloud provider majeur, maintenue et mise à jour en continu.
*Applicabilité H'appi* : pertinent pour H'appi Automate (orchestrateur type Azure Logic Apps) — le pattern Handoff correspond bien à un futur besoin de router une tâche entre plusieurs nodes/agents spécialisés (ex: node Claude → node CRM → node Email) sans tout faire porter à un seul agent générique.

**Ralph Loop (agent pattern)** — [lien](https://www.thoughtworks.com/radar/techniques/agents-md)
*Source* : ThoughtWorks Technology Radar, volume 34 (2026), publication technique établie de référence dans l'industrie
*Le pattern* : plutôt qu'un essaim de plusieurs agents coordonnés, un agent unique tourne en boucle infinie sur une tâche longue, chaque itération démarrant avec un **contexte frais** (au lieu d'accumuler l'historique complet) pour éviter la dégradation de qualité observée sur les longues sessions d'agents autonomes.
*Pourquoi cette source est fiable* : le Technology Radar de ThoughtWorks est une synthèse biannuelle des retours d'expérience terrain de leurs consultants sur des dizaines de missions clients, avec une réputation établie de rigueur depuis plus de 10 ans.
*Applicabilité H'appi* : ce pattern est déjà partiellement présent dans le scraper self-healing (healer.py, ERP Scraper UK) — le formaliser explicitement (reset de contexte entre itérations plutôt qu'accumulation) pourrait aussi bénéficier aux futurs workers longue durée de H'appi Automate.

**Architecture multi-tenant SaaS sur Postgres (RLS)** — [lien](https://clickhouse.com/resources/engineering/multi-tenant-saas-postgres-architecture)
*Source* : ClickHouse, ressources engineering (organisation reconnue dans l'écosystème bases de données), mis à jour juin 2026
*Le pattern* : compare 4 architectures — shared schema + tenant_id (défaut recommandé pour ~80% des SaaS B2B), schema-per-tenant (rarement rentable à l'échelle), database-per-tenant (adapté aux workloads régulés/white-label), et hybrid tiering. Insiste sur PostgreSQL Row-Level Security avec `FORCE ROW LEVEL SECURITY` comme filet de sécurité au niveau base de données (ne dépend pas de chaque développeur qui filtre correctement par tenant_id dans chaque requête), complété par des statement timeouts pour éviter le bruit inter-tenant.
*Pourquoi cette source est fiable* : organisation reconnue de l'écosystème data/Postgres, contenu technique daté et vérifiable (paramètres concrets : timeouts 30s standard / 5min entreprise).
*Applicabilité H'appi* : s'applique directement au Happi CRM, à la Quality Tracking App et au Microsoft Sales App — tous multi-tenant sur PostgreSQL/SQLAlchemy. Le RLS avec FORCE ROW LEVEL SECURITY est un filet de sécurité peu coûteux à ajouter en défense en profondeur, au-dessus du filtrage applicatif par tenant_id déjà probablement en place.

**Options et architectures RAG sur AWS** — [lien](https://docs.aws.amazon.com/prescriptive-guidance/latest/retrieval-augmented-generation-options/introduction.html)
*Source* : AWS Prescriptive Guidance, documentation officielle AWS
*Le pattern* : découpe une architecture RAG en 5 étapes (ingestion, chunking, embedding, retrieval, génération) et détaille les arbitrages à chaque étape — notamment le choix entre un service managé clé-en-main (type Bedrock Knowledge Bases) et une pipeline RAG custom (contrôle fin du chunking, du vector store, du re-ranking) selon le niveau d'exigence métier.
*Pourquoi cette source est fiable* : documentation officielle d'un cloud provider majeur, orientée arbitrages concrets plutôt que promotion produit.
*Applicabilité H'appi* : grille de lecture utile pour tout futur chatbot SAV/e-commerce nécessitant du RAG sur la base de connaissance client — même si H'appi héberge en France/Europe (pas AWS Bedrock), la décomposition en étapes et les critères d'arbitrage (chunking, vector store, latence vs pertinence) restent transposables à une stack pgvector + Claude.

### 🔧 À creuser en priorité
Activer PostgreSQL RLS (`FORCE ROW LEVEL SECURITY`) comme défense en profondeur sur Happi CRM et Microsoft Sales App est une action concrète et peu coûteuse à évaluer court-terme, en complément du filtrage applicatif par tenant_id existant.

---
## 🏛️ Veille Architecture — 2026-07-27
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**Effective Context Engineering for AI Agents** — [lien](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
*Source* : Anthropic, engineering blog, publié le 29 septembre 2025, toujours cité comme référence canonique en 2026
*Le pattern* : traite la fenêtre de contexte comme une ressource finie et précieuse plutôt qu'un espace à remplir. Recommande la récupération "just-in-time" (charger les outils/documents seulement quand nécessaire plutôt que tout pré-charger), la compaction (résumer/élaguer l'historique de conversation à l'approche des limites), la prise de notes structurée (mémoire externalisée hors contexte) et l'isolation de sous-agents pour cloisonner un contexte spécialisé.
*Pourquoi cette source est fiable* : documentation officielle d'Anthropic, issue de retours d'expérience directs sur des agents Claude en production à grande échelle.
*Applicabilité H'appi* : directement actionnable sur l'AI Intelligence Suite du CRM (9 outils) et les futurs nodes de H'appi Automate (20+ nodes) — charger les définitions d'outils à la demande plutôt qu'au démarrage de chaque appel Claude, et appliquer une compaction sur les longues conversations SAV/secrétariat vocal pour éviter la dégradation de qualité et l'explosion de coût token.

**How Stripe uses graph search and state machines to auto-remediate a global database fleet** — [lien](https://stripe.dev/blog/how-stripe-uses-graph-search-and-state-machines-to-auto-remediate-a-global-database-fleet)
*Source* : Stripe, Stripe Dot Dev Blog (Pragya Mehta & Sai Samant), publié le 16 juillet 2026
*Le pattern* : modélise l'infrastructure de base de données (flotte MongoDB) comme un graphe traversable où chaque état (sain/dégradé) est un nœud et chaque action de remédiation une arête. En cas d'incident, un algorithme de pathfinding calcule dynamiquement la séquence d'actions la plus courte pour revenir à un état sain, exécutée via une state machine — plutôt qu'un arbre de décision codé en dur par type de panne.
*Pourquoi cette source est fiable* : retour d'expérience direct et chiffré d'une équipe d'ingénierie ayant déployé le système en production (−30% de pages d'astreinte, −12 jours de shards dégradés/an).
*Applicabilité H'appi* : formalisation intéressante pour le système self-healing du ERP Scraper UK (healer.py) — remplacer/compléter la logique de remédiation cas par cas par un graphe d'états + pathfinding généraliserait la capacité à gérer de nouveaux modes de panne sans code spécifique ; le même principe est transposable aux futurs nodes de reprise sur erreur de H'appi Automate.

**Sequential Pipeline Architecture for Voice Agents** — [lien](https://livekit.com/blog/sequential-pipeline-architecture-voice-agents)
*Source* : LiveKit, engineering blog (infrastructure temps réel voix/vidéo de référence du secteur), publié le 23 mars 2026
*Le pattern* : détaille l'architecture cascadée STT → LLM → TTS qui équipe la majorité des voice agents en production, avec chaque étage remplaçable indépendamment, et la distingue des modèles speech-to-speech natifs (audio-in/audio-out direct, plus rapides mais moins débogables). Donne des budgets de latence concrets par étage et des cibles de production 2026 (p50 < 400ms stack standard, p95 < 800ms).
*Pourquoi cette source est fiable* : LiveKit est l'infrastructure WebRTC temps réel utilisée par une large part de l'écosystème voice AI (dont des déploiements OpenAI Realtime) ; retour d'expérience direct sur des pipelines en production.
*Applicabilité H'appi* : correspond exactement à l'architecture du produit Secrétariat IA vocal (Vapi) — grille de lecture utile pour arbitrer cascadé (transparence, débogage, adapté aux secteurs réglementés) vs speech-to-speech (latence minimale), et benchmarks de latence pour auditer le pipeline vocal existant.

**RAG reference architectures (catalogue)** — [lien](https://docs.cloud.google.com/architecture/rag-reference-architectures)
*Source* : Google Cloud Architecture Center, documentation officielle, maintenue en continu (dernières mises à jour mars 2026)
*Le pattern* : catalogue de variantes d'architecture RAG selon le niveau de contrôle voulu — plateforme managée clé-en-main, pipeline custom avec vector store dédié (dont une variante AlloyDB for PostgreSQL + pgvector), et GraphRAG combinant recherche vectorielle et graphe de connaissances pour les requêtes multi-hop où la seule similarité vectorielle perd le contexte relationnel.
*Pourquoi cette source est fiable* : documentation d'architecture officielle d'un cloud provider majeur, orientée arbitrages techniques plutôt que promotion produit.
*Applicabilité H'appi* : la variante pgvector est le pendant direct de la stack PostgreSQL de H'appi (hors GCP, transposable à Railway) pour le RAG des chatbots SAV/e-commerce sur base de connaissance client ; la variante GraphRAG mérite d'être évaluée pour le CRM, où les données sont fortement relationnelles (contacts/deals/interactions) et pas seulement documentaires.

### 🔧 À creuser en priorité
Évaluer une formalisation du healer.py (ERP Scraper UK) en graphe d'états + pathfinding façon Stripe serait le gain le plus concret à court terme : cela généraliserait le self-healing existant à de nouveaux modes de panne sans code spécifique par cas.

---
## 🏛️ Veille Architecture — 2026-07-28
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**Building Reliable Agentic AI Systems (retour d'expérience Bayer/PRINCE)** — [lien](https://martinfowler.com/articles/reliable-llm-bayer.html)
*Source* : martinfowler.com, article co-écrit par les équipes Bayer AG et Thoughtworks, publié le 16 juin 2026
*Le pattern* : retour d'expérience complet sur PRINCE, une plateforme d'agentic RAG + Text-to-SQL en production pharma, qui détaille les briques nécessaires pour passer d'un prototype à un système fiable : gestion d'erreurs robuste, persistance d'état, fallbacks LLM en cascade, citations granulaires pour l'explicabilité, et évaluation/monitoring continu de la qualité des réponses.
*Pourquoi cette source est fiable* : retour d'expérience direct et documenté d'une équipe (Bayer + Thoughtworks) ayant conçu et exploité le système en production sur un cas d'usage réglementé, publié sur martinfowler.com, référence reconnue en architecture logicielle.
*Applicabilité H'appi* : grille de lecture concrète pour tout chatbot SAV/e-commerce en agentic RAG — en particulier la nécessité de citations granulaires (traçabilité des réponses vers les sources) et de fallbacks LLM en cascade, deux points souvent négligés en V1 mais critiques dès que le chatbot touche à des réponses engageantes (SAV, facturation).

**How we built our multi-agent research system** — [lien](https://www.anthropic.com/engineering/built-multi-agent-research-system)
*Source* : Anthropic, engineering blog, publié le 13 juin 2025, toujours cité comme référence canonique du pattern orchestrator-workers en 2026
*Le pattern* : architecture où un agent "lead" décompose une requête complexe en sous-tâches et déploie des subagents spécialisés en parallèle, chacun avec un objectif précis, un format de sortie attendu, et des limites de périmètre explicites. L'article détaille aussi les pièges rencontrés en production (subagents qui explorent 50 pistes pour une requête simple, agents qui se distraient mutuellement à force de mises à jour, coût en tokens ~15x un simple appel de chat) et comment les corriger par un prompting plus strict des rôles.
*Pourquoi cette source est fiable* : documentation officielle d'Anthropic issue de l'exploitation réelle de ce système de recherche multi-agent en production, avec des chiffres concrets sur les échecs rencontrés et leurs correctifs.
*Applicabilité H'appi* : complète le pattern orchestrator-workers déjà noté (Azure, 2026-07-26) avec des garde-fous concrets à appliquer sur l'AI Intelligence Suite du CRM ou un futur node "recherche" de H'appi Automate : borner explicitement le nombre de subagents et leur périmètre pour éviter l'explosion de coût token observée par Anthropic elle-même.

**Scaling PostgreSQL to power 800 million ChatGPT users** — [lien](https://openai.com/index/scaling-postgresql/)
*Source* : OpenAI, blog officiel, publié le 22 janvier 2026 par Bohan Zhang (Member of Technical Staff)
*Le pattern* : ChatGPT tourne sur une seule instance PostgreSQL primaire (écritures) épaulée par près de 50 réplicas de lecture répartis par région, avec PgBouncer devant chaque réplica (temps de connexion divisé par 10) et une couche de cache qui absorbe la majorité du trafic de lecture avant même d'atteindre un réplica. OpenAI a délibérément évité le sharding (coût de migration applicatif trop élevé) et a plutôt minimisé la charge sur le primaire en déportant écritures et lectures non critiques.
*Pourquoi cette source est fiable* : retour d'expérience direct et chiffré (p99 en dizaines de ms, cinq neuf de disponibilité, charge x10 en un an) publié sur le blog officiel d'OpenAI par l'ingénieur ayant conduit le projet.
*Applicabilité H'appi* : preuve qu'on peut repousser très loin les limites d'un PostgreSQL "classique" (Happi CRM, Quality Tracking App, Microsoft Sales App) avant d'envisager du sharding — la priorité concrète reste PgBouncer devant les réplicas et une couche de cache applicative, bien avant toute réécriture d'architecture.

**Durable execution pour agents IA (pattern human-in-the-loop)** — [lien](https://docs.temporal.io/ai-cookbook/human-in-the-loop-python)
*Source* : documentation officielle Temporal (plateforme de durable execution/orchestration de référence du secteur, levée de 300M$ en février 2026)
*Le pattern* : les workflows d'agents IA sont modélisés comme des séquences d'étapes dont l'état complet est journalisé — en cas de crash, l'exécution reprend à l'étape exacte où elle s'est arrêtée plutôt que de repartir de zéro. Le pattern human-in-the-loop est natif : un workflow peut se mettre en pause (attente d'une validation humaine) pendant des heures ou des jours sans consommer de ressources, et reprendre exactement là où il s'était arrêté au signal reçu.
*Pourquoi cette source est fiable* : documentation officielle d'un éditeur spécialisé et reconnu en orchestration de workflows durables, avec des intégrations actives citées avec LangGraph et OpenAI Agents SDK.
*Applicabilité H'appi* : correspond précisément au besoin de H'appi Automate (orchestrateur type Azure Logic Apps) pour les nodes longue durée ou nécessitant une validation humaine (ex: un node CRM qui attend l'approbation d'un commercial avant d'envoyer un email) — le pattern signal/pause/reprise évite de devoir réinventer une machine à états maison pour ce cas.

### 🔧 À creuser en priorité
Sur Happi CRM et Microsoft Sales App, vérifier si PgBouncer est déjà en place devant PostgreSQL — sinon, c'est l'action la plus simple et la moins chère à évaluer avant toute question de sharding, avec un signal clair d'OpenAI que ça encaisse une charge x10.

---
## 🏛️ Veille Architecture — 2026-07-29
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**Ask DoorDash — assistant shopping conversationnel multi-agent** — [lien](https://www.infoq.com/news/2026/07/doordash-ai-ask-assistant/)
*Source* : InfoQ, reportage sur l'équipe engineering DoorDash, juillet 2026
*Le pattern* : "Ask DoorDash" n'est pas un simple wrapper autour d'un LLM mais un système multi-agent construit sur Google Agent Development Kit, avec trois couches de mémoire persistante (court terme, préférences, historique), un ancrage temps réel sur le catalogue produit via des outils MCP, et un framework d'évaluation LLM-as-judge tournant sur plus de 2000 évaluations automatisées par jour.
*Pourquoi cette source est fiable* : retour d'expérience chiffré d'une équipe produit en production (+24% de conversion panier, +17% de panier moyen, -35% de latence après migration de modèle validée par les évals).
*Applicabilité H'appi* : blueprint quasi directement transposable aux chatbots SAV/e-commerce H'appi — la mémoire à plusieurs couches et l'ancrage catalogue via MCP correspondent exactement au besoin d'un chatbot qui doit se souvenir du client et rester factuellement exact sur un catalogue produit qui change.

**Skipper — moteur de workflow embarqué chez Airbnb** — [lien](https://medium.com/airbnb-engineering/skipper-building-airbnbs-embedded-workflow-engine-f6c34552146f)
*Source* : Airbnb Engineering & Data Science, blog officiel, avril 2026
*Le pattern* : plutôt que de dépendre d'un cluster d'orchestration externe (type Temporal) pour les services critiques (Tier-0), Airbnb a construit une bibliothèque de durable execution embarquable directement dans chaque service — sans nouvelle dépendance d'infrastructure critique — au prix d'un compromis explicite sur les garanties exactly-once par rapport à un moteur externe dédié.
*Pourquoi cette source est fiable* : retour d'expérience direct d'une équipe ayant conçu et déployé le système en production sur plusieurs domaines (assurance, paiements, traitement média, automatisation infra).
*Applicabilité H'appi* : point de comparaison concret pour H'appi Automate face au pattern Temporal déjà noté (2026-07-28) — si l'infra Railway de H'appi doit rester légère, une librairie de workflow embarquée (plutôt qu'un cluster d'orchestration externe supplémentaire à opérer) peut être le bon compromis pour les nodes longue durée qui n'exigent pas des garanties exactly-once strictes.

**Design a Secure Multitenant RAG Inferencing Solution** — [lien](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/secure-multitenant-rag)
*Source* : Azure Architecture Center, Microsoft Learn, documentation officielle, révision 2026
*Le pattern* : guide dédié à l'intersection RAG + multi-tenant — arbitrage entre index vectoriels dédiés par tenant et index partagé avec filtres tenant par requête, avec l'exigence que la couche de retrieval ne renvoie jamais un document qu'un tenant n'est pas autorisé à voir, et que l'orchestration route vers le bon store de données avant même de construire le prompt.
*Pourquoi cette source est fiable* : documentation d'architecture officielle d'un cloud provider majeur, focalisée sur les arbitrages sécurité plutôt que la promotion produit.
*Applicabilité H'appi* : angle plus précis et plus actionnable que le catalogue RAG général déjà noté (Google Cloud, 2026-07-27) — directement pertinent pour les chatbots SAV/e-commerce multi-clients de H'appi, où une fuite de contexte RAG entre deux clients (ex: base de connaissance d'un client visible par un autre) serait une faille RGPD critique à éliminer par construction, pas seulement par filtrage applicatif.

**Cart Assistant — agent de shopping agentique chez Uber Eats** — [lien](https://www.uber.com/us/en/blog/uber-cart-assistant/)
*Source* : Uber Engineering, blog officiel, 16 juin 2026
*Le pattern* : même problème que DoorDash (agent conversationnel de shopping) mais résolu avec une architecture différente — un state-graph explicite plutôt qu'un système multi-agent, choisi délibérément pour la contrôlabilité et l'inspectabilité — associé à un flux d'évaluation qui compare baseline vs candidat et inspecte les traces étape par étape, à la fois avant mise en prod et en continu sur trafic réel.
*Pourquoi cette source est fiable* : retour d'expérience direct d'une équipe d'ingénierie ayant conçu et exploité le système en production.
*Applicabilité H'appi* : à lire en contraste avec DoorDash ci-dessus — pour un chatbot SAV/e-commerce H'appi, le choix entre "state-graph explicite" (plus simple à déboguer et à auditer, bon défaut pour un premier produit réglementé) et "multi-agent avec mémoire" (plus flexible mais plus coûteux à maintenir) est un arbitrage concret à trancher projet par projet plutôt qu'un choix universel.

**Multi-Provider Generative AI Gateway (architecture de référence)** — [lien](https://aws.amazon.com/blogs/machine-learning/streamline-ai-operations-with-the-multi-provider-generative-ai-gateway-reference-architecture/)
*Source* : AWS Machine Learning Blog / AWS Solutions Library, architecture de référence, 2026
*Le pattern* : passerelle centralisée (construite sur LiteLLM) placée devant tous les appels vers des providers LLM, avec gestion centralisée du rate limiting, de l'authentification, de l'observabilité (logs/coûts par produit) et de la bascule entre providers, plutôt que chaque produit qui appelle son LLM directement en dur.
*Pourquoi cette source est fiable* : architecture de référence documentée officiellement par un cloud provider majeur, orientée gouvernance/coût plutôt que promotion produit.
*Applicabilité H'appi* : H'appi opère plusieurs produits IA (chatbots, secrétariat vocal, CRM, sales intelligence) qui appellent tous l'API Claude indépendamment — une gateway interne légère (même auto-hébergée sur Railway plutôt que sur AWS) permettrait de centraliser le rate limiting, l'attribution des coûts par produit/client et un futur fallback multi-provider, sans dupliquer cette logique dans chaque codebase.

### 🔧 À creuser en priorité
Le pattern "Secure Multitenant RAG" (Azure) mérite un audit court-terme sur les chatbots SAV/e-commerce H'appi existants : vérifier que l'isolation tenant au niveau du retrieval RAG est garantie par construction (index/filtre obligatoire) et pas seulement par un filtrage applicatif optionnel.

---
## 🏛️ Veille Architecture — 2026-07-30
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**We replaced Redis with MySQL for inventory reservations — and it scaled** — [lien](https://shopify.engineering/scaling-inventory-reservations)
*Source* : Shopify Engineering, blog officiel, publié le 12 mai 2026
*Le pattern* : plutôt qu'une colonne quantité par article, Shopify modélise chaque unité vendable comme une ligne SQL distincte (10 unités en stock = 10 lignes) et utilise `SELECT ... FOR UPDATE SKIP LOCKED` pour réserver des lignes disponibles sans bloquer sur celles déjà verrouillées par une transaction concurrente, avec un pool borné (max 1000 lignes par article/localisation) pour éviter la dégradation de perf à grande échelle.
*Pourquoi cette source est fiable* : retour d'expérience direct et chiffré d'une équipe ayant migré un système critique en production, validé sous la charge réelle du Black Friday 2025 ($5,1M de ventes/minute) — -50% de lectures, -33% de transactions, zéro survente.
*Applicabilité H'appi* : `SKIP LOCKED` existe nativement en PostgreSQL (donc directement utilisable, pas seulement en MySQL) — pattern concret pour tout futur système de réservation/allocation de ressources sous contention dans le CRM ou un chatbot e-commerce (ex: gestion de stock, créneaux de rendez-vous secrétariat vocal), en évitant d'ajouter une dépendance Redis supplémentaire pour un problème que PostgreSQL seul sait résoudre proprement.

**Logic Apps Automation** — [lien](https://www.infoq.com/news/2026/06/azure-logic-apps-automation/)
*Source* : InfoQ, couverture de l'annonce Microsoft Build 2026, juin 2026 (documentation complémentaire sur techcommunity.microsoft.com)
*Le pattern* : nouvelle offre Azure packageant workflows, agents IA et accès modèles dans un SaaS managé — agents intégrés via orchestration en boucle et sandbox managée, RAG entièrement managé ("Knowledge as a Service"), et surtout un serveur MCP qui expose chaque workflow Logic Apps existant comme un outil découvrable et invocable par un agent.
*Pourquoi cette source est fiable* : annonce produit officielle relayée et contextualisée par InfoQ, publication technique établie, avec documentation officielle Microsoft en complément.
*Applicabilité H'appi* : concurrent direct positionné exactement sur le créneau de H'appi Automate (orchestrateur "type Azure Logic Apps") — le choix d'exposer chaque workflow comme outil MCP plutôt que via une API propriétaire est un signal de marché fort à répliquer : les futurs nodes de H'appi Automate gagneraient à être nativement invocables par un agent Claude via MCP, pas seulement déclenchables par une UI de workflow.

**How We Contain Claude Across Products** — [lien](https://www.infoq.com/news/2026/07/anthropic-claude-containment/)
*Source* : Anthropic, article technique du 28 mai 2026 (Max McGuinness, Mikaela Grace, Jiri De Jonghe, Jake Eaton, Abel Ribbink), relayé par InfoQ en juillet 2026
*Le pattern* : la sécurité d'un agent doit reposer sur des limites déterministes au niveau du système de fichiers, du réseau et de l'environnement d'exécution (containment à la frontière), et non sur des prompts de permission ou des garde-fous côté modèle. Trois implémentations différentes selon le produit : conteneurs gVisor éphémères pour claude.ai, sandboxing OS (Seatbelt/bubblewrap) pour Claude Code, isolation VM complète pour Claude Cowork — le niveau d'isolation est choisi selon le blast radius acceptable, pas uniformément.
*Pourquoi cette source est fiable* : documentation technique directe d'Anthropic sur ses propres systèmes en production, incluant un exercice de red-team interne chiffré (phishing réussi 24 fois sur 25 tentatives) qui illustre concrètement pourquoi le containment prime sur la confiance dans le comportement du modèle.
*Applicabilité H'appi* : principe directement actionnable pour tout produit H'appi qui donne à un agent Claude un accès outils (scraper self-healing, futurs nodes H'appi Automate avec exécution de code, secrétariat vocal avec accès CRM) — isoler par défaut (sandbox/conteneur dédié, accès réseau et filesystem minimal) plutôt que de compter sur le prompt système pour empêcher les actions dangereuses, en particulier vu l'exigence RGPD/hébergement Europe de H'appi.

**Keep the Terminal Relevant: Patterns for AI Agent Driven CLIs** — [lien](https://www.infoq.com/articles/ai-agent-cli/)
*Source* : InfoQ, article de Sachin Joglekar, 2026
*Le pattern* : tout outil qui produit une sortie structurée destinée à être consommée par un agent publie de fait un contrat d'API — les formats de sortie doivent donc être versionnés sémantiquement et validés par schéma à chaque changement, avec des codes de sortie sémantiques et des flags dédiés à l'automatisation. Recommandation centrale : adopter le protocole MCP pour l'intégration d'agents dès la conception plutôt qu'en couche ajoutée après coup.
*Pourquoi cette source est fiable* : publication technique établie (InfoQ), auteur signé, alignée avec la donation de MCP par Anthropic à la Linux Foundation (Agentic AI Foundation) en décembre 2025 qui en fait un standard de facto.
*Applicabilité H'appi* : directement pertinent pour tout outil interne H'appi exposé à un agent Claude (scrapers, endpoints CRM, nodes d'Automate) — traiter chaque sortie JSON d'API/CLI comme un contrat versionné évite de casser silencieusement un agent en production lors d'une évolution de schéma, un risque concret vu le nombre d'outils déjà connectés à l'AI Intelligence Suite du CRM.

### 🔧 À creuser en priorité
Logic Apps Automation (Microsoft) valide un choix d'architecture à trancher tôt pour H'appi Automate : exposer chaque node comme outil MCP dès la conception plutôt qu'après coup, en cohérence avec le pattern InfoQ sur les contrats d'API/CLI ci-dessus.

---
## 🏛️ Veille Architecture — 2026-07-31
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**The new rules of context engineering for Claude 5 generation models** — [lien](https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models)
*Source* : Anthropic, blog officiel (Thariq Shihipar, Member of Technical Staff), publié le 24 juillet 2026
*Le pattern* : l'équipe Claude Code a supprimé plus de 80% du system prompt de Claude Code pour les modèles Claude 5 (Opus 5, Fable 5) sans perte mesurable sur les évaluations de code. Les règles défensives accumulées pour contenir les faiblesses des générations de modèles précédentes deviennent une taxe sur les modèles récents : des instructions contradictoires font perdre des tokens de raisonnement au modèle pour arbitrer entre elles. Anthropic recommande de réauditer régulièrement system prompts, Skills et fichiers de mémoire/contexte à chaque nouvelle génération de modèle plutôt que d'empiler les garde-fous au fil du temps.
*Pourquoi cette source est fiable* : retour d'expérience direct de l'équipe Anthropic ayant conçu et mesuré ce changement sur Claude Code en production, publié sur le blog officiel.
*Applicabilité H'appi* : actionnable immédiatement sur tous les prompts système des produits IA H'appi (chatbots SAV/e-commerce, secrétariat vocal, AI Intelligence Suite du CRM) — à chaque montée de version de Claude, auditer et alléger les instructions défensives héritées plutôt que les accumuler, ce qui réduit à la fois la latence et le coût token sans dégrader la qualité.

**Agentic AI Architecture Framework for Enterprises** — [lien](https://www.infoq.com/minibooks/agentic-ai-architecture/)
*Source* : InfoQ, minibook (Subash Natarajan & Ahilan Ponnusamy), 2026
*Le pattern* : structure la maturité d'un système agentique en 3 paliers progressifs — Foundation Tier (confiance et gouvernance : orchestration d'outils, transparence du raisonnement, cycle de vie des données), Workflow Tier (automatisation via 5 patterns : prompt chaining, routing, parallelization, evaluator-optimizer, orchestrator-workers) et Autonomous Tier (planification orientée objectif). L'argument central : la confiance et la gouvernance doivent précéder l'autonomie, pas l'inverse.
*Pourquoi cette source est fiable* : publication technique établie (InfoQ), minibook signé par des auteurs identifiés, synthétisant des patterns déjà documentés individuellement par les cloud providers (dont Azure, déjà noté le 2026-07-26).
*Applicabilité H'appi* : grille utile pour situer où en est chaque produit IA H'appi sur cette échelle de maturité — le CRM et les chatbots SAV sont probablement au Workflow Tier (patterns type routing/orchestrator-workers), tandis qu'un futur node autonome de H'appi Automate (ex: résolution de ticket SAV de bout en bout sans validation humaine) basculerait vers l'Autonomous Tier et exigerait de solidifier d'abord la gouvernance du Foundation Tier (traçabilité, permissions, cycle de vie des données) avant d'y aller.

**How API changes flow into Stripe's developer products** — [lien](https://stripe.dev/blog/how-api-changes-flow-into-stripes-developer-products)
*Source* : Stripe, Stripe Dot Dev Blog, blog d'ingénierie officiel, 2026
*Le pattern* : Stripe ne conçoit pas son API directement via OpenAPI, mais génère automatiquement à partir des changements d'API tous les artefacts dérivés — SDKs, mock servers, collection Postman, documentation — pour éviter que ces produits développeurs dérivent de l'API réelle. Chaque changement passe par une revue croisée (API Review) avant merge, puis un pipeline automatisé propage le changement à l'ensemble des surfaces développeur.
*Pourquoi cette source est fiable* : retour d'expérience direct de l'équipe plateforme développeur de Stripe, référence reconnue en design d'API, publié sur son blog d'ingénierie officiel.
*Applicabilité H'appi* : pertinent pour l'API FastAPI backend de H'appi dès qu'elle sert plusieurs consommateurs (CRM, widgets chatbot embarqués chez les clients, futurs SDKs H'appi Automate) — générer la doc et les schémas clients depuis l'OpenAPI de FastAPI (déjà natif) plutôt que de les maintenir à la main, et faire passer les changements de contrat par une revue explicite avant merge, réduirait le risque de rupture silencieuse pour les intégrations clients.

**How Outtake built a cyber investigator on Claude** — [lien](https://claude.com/blog/how-outtake-built-a-cyber-investigator-on-claude)
*Source* : Anthropic, blog officiel, publié le 22 juillet 2026, en co-publication avec Outtake (client)
*Le pattern* : Outtake a construit un agent autonome longue durée ("Recon Agent") sur Claude Code et l'Agent SDK, capable de partir d'un seul indicateur de menace et de remonter, en quelques minutes et sans supervision continue, tout le réseau adverse associé (faux profils, sites clonés, apps frauduleuses). L'architecture repose sur une exécution longue et autonome plutôt qu'un enchaînement de prompts courts, avec l'agent qui pilote lui-même ses outils d'investigation successifs jusqu'à un objectif final plutôt qu'une tâche unitaire.
*Pourquoi cette source est fiable* : retour d'expérience direct co-publié par Anthropic et l'équipe produit d'Outtake sur un système déployé en production pour des clients (labs IA, hedge funds, agences fédérales).
*Applicabilité H'appi* : blueprint concret pour tout agent H'appi qui doit exécuter une investigation ou une tâche longue sans intervention humaine à chaque étape — pertinent pour un futur mode "autonome" du scraper self-healing (diagnostiquer et corriger une panne de bout en bout) ou pour un node de monitoring de H'appi Automate qui doit creuser une anomalie sur plusieurs étapes avant de conclure, plutôt que de se limiter à des appels Claude ponctuels et isolés.

### 🔧 À creuser en priorité
Réauditer les system prompts des produits IA H'appi (chatbots, secrétariat vocal, CRM) à chaque montée de version de Claude, en s'inspirant directement du retour d'expérience Anthropic sur Claude Code : alléger les garde-fous hérités plutôt que les empiler réduit latence et coût token sans perte de qualité.

---
## 🏛️ Veille Architecture — 2026-08-01
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**Introducing advanced tool use on the Claude Developer Platform** — [lien](https://www.anthropic.com/engineering/advanced-tool-use)
*Source* : Anthropic, engineering blog officiel, 2026
*Le pattern* : trois capacités combinées pour des agents à large catalogue d'outils — le Tool Search Tool (découverte et chargement des définitions d'outils à la demande plutôt qu'au démarrage), le Programmatic Tool Calling (Claude écrit du code Python d'orchestration qui appelle les outils depuis un sandbox d'exécution, au lieu d'un aller-retour API par appel d'outil), et les Tool Use Examples (exemples d'usage concrets qui améliorent la précision au-delà de la seule définition de l'outil). Sur un benchmark interne à 75 outils, le Programmatic Tool Calling réduit les tokens d'entrée facturés d'environ 38% sans perte de précision, en parallélisant par exemple 20 appels d'outils indépendants en une seule passe de code plutôt que 20 aller-retours séquentiels.
*Pourquoi cette source est fiable* : documentation officielle d'Anthropic avec chiffres internes vérifiables, disponible sur Claude API, Claude Platform AWS et Microsoft Foundry.
*Applicabilité H'appi* : concrétise et prolonge le pattern de "récupération just-in-time" déjà noté (Anthropic, 2026-07-27) — directement actionnable sur l'AI Intelligence Suite du CRM (9 outils) : le Programmatic Tool Calling est le bon candidat pour tout outil qui doit interroger plusieurs enregistrements CRM en parallèle (ex: scorer 20 deals d'un coup) plutôt que d'enchaîner les appels un par un, avec un gain de coût token direct et mesurable.

**Developer's guide to multi-agent patterns in ADK** — [lien](https://developers.googleblog.com/developers-guide-to-multi-agent-patterns-in-adk/)
*Source* : Google Developers Blog (Sergio De Simone), 2026
*Le pattern* : catalogue de 8 patterns d'orchestration multi-agents avec pseudocode concret sur l'Agent Development Kit — notamment Sequential (chaîne déterministe et facile à déboguer, ex: Parser → Extractor → Summarizer), Parallel (plusieurs agents spécialisés analysent la même entrée simultanément puis un Synthesizer fusionne leurs sorties, ex: relecture de code par un auditeur sécurité + un vérificateur de style + un analyste perf en parallèle), et Loop (un agent répète une séquence de sous-agents jusqu'à une condition de sortie évaluée par une logique prédéfinie, sans consulter le modèle pour l'orchestration elle-même).
*Pourquoi cette source est fiable* : publication officielle de l'équipe Google Developers, avec pseudocode et exemples d'implémentation vérifiables sur un framework agent en production (ADK).
*Applicabilité H'appi* : complète les catalogues Azure et InfoQ déjà notés (2026-07-26, 2026-07-31) avec un niveau plus concret — le pattern Parallel + Synthesizer est directement transposable à un futur node de relecture/scoring dans H'appi Automate ou l'AI Intelligence Suite (ex: 3 outils qui évaluent un lead sous des angles différents, fusionnés par un agent de synthèse), et le pattern Loop à condition de sortie déterministe (pas de décision modèle à chaque itération) réduit le coût par rapport à une boucle agentique complète pour des tâches répétitives bornées.

**Agentic AI Lens — AWS Well-Architected Framework** — [lien](https://docs.aws.amazon.com/wellarchitected/latest/agentic-ai-lens/agentic-ai-lens.html)
*Source* : AWS Well-Architected Framework, documentation officielle, publiée le 10 juin 2026
*Le pattern* : étend le Well-Architected Framework aux systèmes agentiques — infrastructure de calcul et de mémoire pour agents, patterns d'orchestration multi-agents, et pratiques opérationnelles de fiabilité/sécurité/coût. Point clé : les agents qui invoquent des outils et modifient des données de façon autonome (sans instruction humaine explicite à chaque étape) exigent des contrôles de sécurité et des frontières de permission conçus spécifiquement pour l'autonomie, distincts des contrôles classiques d'une API request-response.
*Pourquoi cette source est fiable* : documentation d'architecture officielle d'un cloud provider majeur, extension formelle d'un framework déjà établi et éprouvé (Well-Architected) plutôt qu'un contenu promotionnel isolé.
*Applicabilité H'appi* : grille d'audit directement utilisable pour tout produit H'appi où un agent Claude agit de façon autonome sur des données réelles (scraper self-healing avec ré-écriture de sélecteurs, futurs nodes H'appi Automate qui déclenchent des actions CRM/email sans validation humaine) — poser explicitement des frontières de permission par outil/action plutôt que de laisser le prompt système seul porter la sécurité, en cohérence avec le pattern de containment Anthropic déjà noté (2026-07-30).

**Scaling beyond one: comment Airbnb a fait évoluer son architecture de données pour un monde multi-produits** — [lien](https://medium.com/airbnb-engineering/scaling-beyond-one-how-airbnb-evolved-its-data-architecture-for-a-multi-product-world-6125645d470c)
*Source* : Airbnb Tech Blog (Patrick Lam, Staff Analytics Engineer), juin 2026
*Le pattern* : au moment de lancer deux nouvelles lignes de produits (Experiences, Services) à côté du produit historique (Homes), les modèles de données transverses (messagerie, paiements) sont restés délibérément monolithiques plutôt que fragmentés par produit — un fil de conversation ou une transaction peut couvrir plusieurs types de produits, donc les modéliser séparément aurait cassé les analyses transverses. Seules les couches spécifiques à un produit (inventaire, disponibilité) sont fragmentées ; tout ce qui est intrinsèquement partagé reste un modèle unique.
*Pourquoi cette source est fiable* : retour d'expérience direct et signé d'une ingénieure senior d'Airbnb ayant conduit cette évolution d'architecture en production, publié sur le blog technique officiel de l'entreprise.
*Applicabilité H'appi* : question directement transposable à H'appi, qui opère déjà plusieurs produits (chatbots SAV, secrétariat vocal, CRM, sales intelligence, scraper, futur orchestrateur) — au moment de faire évoluer le schéma PostgreSQL/SQLAlchemy partagé, garder un modèle unique pour ce qui est intrinsèquement transverse à un client (identité, facturation, conversations si elles traversent plusieurs produits) et ne fragmenter par produit que ce qui l'est réellement (ex: configuration spécifique à un chatbot), plutôt que de dupliquer prématurément par produit.

### 🔧 À creuser en priorité
Évaluer le Programmatic Tool Calling (Anthropic) sur les outils de l'AI Intelligence Suite du CRM qui font des appels répétés/parallélisables (ex: scoring de plusieurs deals) est l'action la plus concrète et la moins coûteuse à tester court-terme, avec un gain de coût token déjà chiffré par Anthropic (~38%).

---
## 🏛️ Veille Architecture — 2026-08-04
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**Jump Start Solution: Generative AI RAG with Cloud SQL** — [lien](https://docs.cloud.google.com/architecture/ai-ml/generative-ai-rag)
*Source* : Google Cloud Architecture Center, documentation officielle
*Le pattern* : architecture de référence pour un RAG complet bâti entièrement sur PostgreSQL — les documents sources sont chargés dans une base Cloud SQL for PostgreSQL, les embeddings sont générés puis stockés comme vecteurs dans cette même base via l'extension `pgvector`, et une recherche de similarité s'exécute directement en SQL avant l'appel au LLM (Cloud Run en frontend/backend, pas de vector DB dédiée séparée).
*Pourquoi cette source est fiable* : architecture de référence officielle d'un cloud provider majeur, pensée explicitement comme point de départ "coût réduit" plutôt que comme démonstration marketing.
*Applicabilité H'appi* : directement transposable au stack H'appi (PostgreSQL + SQLAlchemy déjà en place) — activer `pgvector` sur la base Postgres existante (Railway) pour tout futur besoin RAG (ex: base de connaissances d'un chatbot SAV, mémoire longue du secrétariat vocal) évite d'introduire une vector DB séparée (Pinecone, Weaviate) et le coût opérationnel/RGPD associé à un service tiers hors Europe.

**Row Level Security for Tenants in Postgres** — [lien](https://www.crunchydata.com/blog/row-level-security-for-tenants-in-postgres)
*Source* : Crunchy Data, blog d'ingénierie officiel (éditeur PostgreSQL entreprise reconnu)
*Le pattern* : plutôt que de créer un rôle Postgres par client (coûteux à gérer et incompatible avec le pooling de connexions), la base garde un seul rôle applicatif et une policy RLS compare une colonne `tenant_id`/`org_id` à une variable de session (`current_setting('rls.org_id')`) positionnée à chaque connexion — la base filtre alors automatiquement toutes les requêtes (SELECT/INSERT/UPDATE/DELETE) sans dépendre d'un `WHERE tenant_id = ...` ajouté manuellement côté application.
*Pourquoi cette source est fiable* : éditeur PostgreSQL entreprise établi, contenu technique orienté implémentation (avec tutoriel interactif associé) plutôt que promotionnel.
*Applicabilité H'appi* : filet de sécurité pertinent pour tout produit H'appi multi-clients sur base partagée (CRM, chatbots SAV) — la RLS garantit l'isolation des données au niveau base même si un bug applicatif SQLAlchemy oublie un filtre tenant, un risque concret vu le nombre de produits/clients servis sur une infra commune ; attention documentée au piège du pooling en mode transaction, qui exige de repositionner la variable de session à chaque transaction (`set_config(..., true)`) plutôt qu'à la connexion.

**Context engineering (Technology Radar Vol. 34)** — [lien](https://www.thoughtworks.com/radar/techniques/context-engineering)
*Source* : ThoughtWorks, Technology Radar Vol. 34, publié en avril 2026
*Le pattern* : le context engineering devient une préoccupation architecturale à part entière plutôt qu'une optimisation de prompt — le contexte fourni à un agent est traité comme une surface de conception à part entière. Pour éviter le "context rot" (dégradation du raisonnement quand on charge tout en avance), le pattern recommandé est la divulgation progressive du contexte : l'agent démarre avec un index léger de ce qui est disponible et ne charge que ce dont il a besoin à l'étape en cours, plutôt qu'un prompt monolithique statique contenant tout par avance.
*Pourquoi cette source est fiable* : publication de référence en architecture logicielle établie depuis 2010, radar collégial issu de l'expérience terrain de centaines de consultants ThoughtWorks sur des missions clients réelles.
*Applicabilité H'appi* : rejoint directement le Tool Search Tool d'Anthropic déjà noté (2026-08-01) — principe applicable à la conception des prompts système et de la mémoire des agents H'appi (AI Intelligence Suite du CRM, secrétariat vocal) : structurer les fichiers de contexte/mémoire en index léger + chargement à la demande plutôt qu'en un unique gros fichier system prompt, pour limiter la dégradation de raisonnement à mesure que le nombre d'outils et de produits H'appi augmente.

**Sequential Pipeline Architecture for Voice Agents** — [lien](https://livekit.com/blog/sequential-pipeline-architecture-voice-agents)
*Source* : LiveKit, blog d'ingénierie officiel (infrastructure temps réel/WebRTC utilisée en production par de nombreux produits voice AI)
*Le pattern* : pipeline séquentiel STT → LLM → TTS pour un agent vocal, avec une gestion explicite du barge-in (interruption) : un détecteur d'activité vocale (VAD) qui capte la voix de l'utilisateur pendant que l'agent parle déclenche l'arrêt immédiat de la lecture TTS, le vidage de l'audio en file d'attente, et le redémarrage du pipeline depuis le STT — avec des cas limites documentés (faux déclenchements par écho/bruit de fond, interruption en plein milieu d'un appel d'outil par le LLM).
*Pourquoi cette source est fiable* : blog d'ingénierie officiel d'une entreprise d'infrastructure temps réel spécialisée, contenu technique détaillé sur des cas limites réels plutôt qu'un tutoriel générique.
*Applicabilité H'appi* : directement actionnable pour le produit de secrétariat vocal IA de H'appi — le pipeline séquentiel STT→LLM→TTS (plutôt qu'un modèle speech-to-speech intégré) reste le choix par défaut en production pour la transparence et la capacité à remplacer un composant (ex: changer de provider TTS) sans toucher au reste ; la gestion du barge-in et des interruptions pendant un appel d'outil (ex: création de rendez-vous en cours) est un cas limite concret à couvrir explicitement dans la conception de l'agent vocal H'appi.

### 🔧 À creuser en priorité
Activer `pgvector` sur la base PostgreSQL existante (Railway) plutôt que d'introduire une vector DB tierce est l'option la plus directement testable pour tout futur besoin RAG H'appi (base de connaissances chatbot SAV, mémoire secrétariat vocal), en cohérence avec le stack et les contraintes RGPD/Europe déjà en place.

---
## 🏛️ Veille Architecture — 2026-08-05
> Mis à jour automatiquement par Happi Brain Agent (Architecture & Blueprints)

**An Evolutionary Architecture Pattern for Managing AI's Pace of Change** — [lien](https://www.infoq.com/articles/evolutionary-architecture-pattern/)
*Source* : InfoQ, article signé (Joe Price, Branimir Đurek, Pavlos Migkiros, Trevor Dearham), publié le 27 juillet 2026
*Le pattern* : les API gateways classiques supposent des services déterministes et des schémas simples — deux hypothèses que l'IA agentique casse. L'article propose l'AI Gateway comme "seam" d'architecture évolutive : un plan de contrôle unique qui concentre les éléments qui changent vite (routage de modèle, identité de l'agent, politique d'action, garde-fous de contenu, audit sémantique) pour que le reste du système reste stable pendant que les modèles/protocoles évoluent en continu. L'article note explicitement que ce n'est pas gratuit (latence, centralisation, coût opérationnel) et n'est pas justifié pour un cas d'usage mono-équipe/mono-LLM avec des garde-fous applicatifs suffisants.
*Pourquoi cette source est fiable* : publication technique établie (InfoQ), article signé par plusieurs auteurs identifiés, qui formalise et nomme un pattern déjà esquissé par l'architecture de référence AWS Multi-Provider Generative AI Gateway déjà notée (2026-08-01) sous un angle gouvernance/évolutivité plutôt que routage technique.
*Applicabilité H'appi* : pertinent au moment où H'appi Automate (orchestrateur type Logic Apps) et le CRM AI Intelligence Suite connectent de plus en plus d'outils/modèles à travers plusieurs produits — plutôt que d'éparpiller identité d'agent, politique d'action et audit dans chaque produit, centraliser ces contrôles dans une couche gateway commune devant l'API Claude évite de dupliquer la gouvernance à chaque nouveau chatbot/CRM client ; à évaluer seulement une fois plusieurs produits partagent effectivement les mêmes appels Claude, pas avant.

**Teaching Sidekick to say no: automated data curation with LLM judge consensus** — [lien](https://shopify.engineering/sidekick-curation)
*Source* : Shopify Engineering, blog officiel, publié le 15 juin 2026
*Le pattern* : pour apprendre à un modèle spécialisé (Sidekick, l'assistant marchand agentique de Shopify) à refuser les requêtes hors de sa portée — un cas que les données de production ne couvrent pas, puisqu'elles ne capturent que les requêtes réussies — l'équipe fait tourner un panel de LLMs frontière calibrés par few-shot sur un jeu de référence, puis utilise ce panel comme arbitre de conflit sur l'ensemble du corpus d'entraînement : quand les sources de labels divergent sur une requête, le consensus du panel tranche par rapport à la distribution de référence plutôt que par vote majoritaire brut.
*Pourquoi cette source est fiable* : retour d'expérience direct de l'équipe Sidekick de Shopify sur un pipeline de curation utilisé en production, publié sur le blog d'ingénierie officiel de l'entreprise.
*Applicabilité H'appi* : pattern directement transposable à l'AI Intelligence Suite du CRM et aux chatbots SAV — pour apprendre à un agent H'appi à dire "je ne sais pas"/"j'escalade vers un humain" plutôt que d'halluciner une réponse, la même logique de panel de juges LLM calibrés s'applique pour curer et étiqueter les transcripts de conversations réelles, un axe direct d'amélioration de la fiabilité perçue par les clients finaux des chatbots SAV.

**Equipping agents for the real world with Agent Skills** — [lien](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
*Source* : Anthropic, engineering blog officiel, publié le 16 octobre 2025 (standard ouvert annoncé le 18 décembre 2025)
*Le pattern* : les Agent Skills structurent l'expertise métier comme des dossiers portables (instructions, scripts, ressources) chargés dynamiquement par l'agent plutôt qu'embarqués dans un system prompt monolithique. Seul le frontmatter YAML (nom + description) est chargé par défaut ; le contenu complet du SKILL.md n'est lu que lorsque l'agent juge la compétence pertinente pour la tâche en cours — un principe de "divulgation progressive" qui permet à un agent généraliste de rester léger tout en ayant accès à un grand catalogue de compétences spécialisées et partageables entre équipes/produits.
*Pourquoi cette source est fiable* : documentation officielle d'Anthropic sur un standard ouvert qu'elle a conçu et publié, avec adoption cross-plateforme déjà engagée.
*Applicabilité H'appi* : prolonge directement le pattern de context engineering/divulgation progressive déjà noté (ThoughtWorks, 2026-08-04) avec un mécanisme concret d'implémentation — packager les playbooks métier récurrents de H'appi (procédures SAV par secteur client, scripts de qualification pour le secrétariat vocal, logique de scoring CRM) en Skills réutilisables plutôt qu'en instructions dupliquées dans chaque prompt système produit, ce qui permettrait de partager et versionner cette expertise entre les différents chatbots clients sans tout réécrire à chaque nouveau projet.

### 🔧 À creuser en priorité
Packager un premier playbook SAV récurrent (ex: procédure de remboursement/réclamation e-commerce) en Agent Skill plutôt qu'en instructions system prompt dupliquées est le test le plus rapide à mener pour valider si ce pattern réduit la duplication entre les chatbots SAV de plusieurs clients H'appi.
