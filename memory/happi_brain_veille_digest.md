# 📊 Synthèse Hebdo Veille — Happi Brain

> Ce fichier compile chaque semaine, de façon automatique, les signaux les plus significatifs des 7 derniers jours de veille quotidienne (Veille Tech dans `happi_brain.md` et Veille Architecture dans `memory/happi_brain_architecture.md`). Lecture seule sur ces deux fichiers sources — la synthèse ci-dessous est une compression à valeur ajoutée, pas une republication de leur contenu.

---
## 📊 Synthèse Hebdo Veille — semaine du 2026-07-20
> Généré automatiquement à partir des entrées Veille Tech (happi_brain.md) et Veille Architecture (memory/happi_brain_architecture.md) des 7 derniers jours.

- **AI gateway multi-provider (OmniRoute)** — En trending TypeScript 7 jours consécutifs sur la semaine, seul repo à ce niveau de constance. Le signal est assez fort pour dépasser le stade "à surveiller" : évaluer une intégration comme couche de fallback Claude → GPT → Gemini dans le backend FastAPI, pour les chatbots à SLA élevé.
- **Orchestration multi-agents** — signal le plus fort de la semaine, confirmé à la fois par la tendance marché (OmniRoute, stablyai/orca, n8n tous en trending la même semaine) et par la pratique de référence (voir croisement ci-dessous). Action : auditer chaque brique de l'AI Intelligence Suite du CRM et de H'appi Automate pour choisir workflow orchestré vs agent autonome, au lieu de généraliser un pattern agentique partout par défaut.
- **Écosystème Claude Skills (awesome-claude-skills)** — revient 3 fois dans la semaine (07-20, 07-23, 07-25/26) avec une base d'étoiles qui continue de grossir. Action : intégrer un inventaire des Skills disponibles à la phase de cadrage de chaque nouveau projet chatbot — gain de vitesse de livraison direct, pas juste une curiosité à suivre.
- **Migration Claude Sonnet 5 avant le 1er septembre** — tarif intro $2/M input tokens expirant le 31 août (puis $3/M). Action concrète et datée : planifier la bascule des chatbots clients vers `claude-sonnet-5` avant la fin août pour capter le tarif réduit.
- **Marché Voice AI en surchauffe** (Rime $24M Series A, Pipecat comme référence open-source, chiffres Vapi/ElevenLabs) — le segment PME reste ouvert pendant que les gros acteurs US ciblent l'enterprise. Action : accélérer les propositions voice pour PME françaises tant que ce créneau est dégagé, plutôt que de laisser mûrir.
- **RLS PostgreSQL (`FORCE ROW LEVEL SECURITY`) en défense en profondeur multi-tenant** — pattern documenté par ClickHouse, directement applicable au Happi CRM, à la Quality Tracking App et au Microsoft Sales App (tous multi-tenant sur PostgreSQL). Action : évaluer l'ajout à court terme, en complément du filtrage applicatif par tenant_id déjà en place.

### 🔗 Croisement tendance × architecture
L'orchestration multi-agents est confirmée des deux côtés la même semaine : côté tendance, OmniRoute (gateway multi-provider), stablyai/orca (ADE pour flottes d'agents) et n8n (automation + IA native) dominent le trending ; côté architecture, Anthropic ("Building Effective Agents" — workflows vs agents autonomes) et Azure ("AI Agent Orchestration Patterns" — Handoff, Supervisor) posent le cadre de référence. Le marché et la pratique établie pointent dans la même direction : c'est le signal le plus solide pour investir sur H'appi Automate.
