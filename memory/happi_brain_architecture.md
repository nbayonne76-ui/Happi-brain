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
