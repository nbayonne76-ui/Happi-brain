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
