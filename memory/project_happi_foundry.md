---
name: H'appi Foundry Research & Roadmap
description: Deep research on Azure AI Foundry, competitors, and optimal architecture for H'appi Foundry
type: project
---

## What H'appi Foundry is
AI platform at `/home/v-nbayonne/ai-foundry/` — GitHub: github.com/nbayonne76-ui/Happi-Foundry
Stack: Next.js 14 + FastAPI + PostgreSQL. Currently on `main` branch.

## Key Finding: The Optimal Combination
H'appi Foundry should combine:
- **OpenRouter**: model breadth, unified API, zero-friction
- **Azure Foundry**: evaluation depth, guardrails
- **LangSmith**: developer-centric trace/experiment UX
- **Langfuse**: prompt management, open-source portability
- **Yupp.ai**: multi-model comparison, human preference collection

## P1 — Critical Features (Must Build)
1. Multi-Model Compare (3-10 models side by side on same prompt) — KEY differentiator
2. Unified API Gateway (OpenAI-compatible, one endpoint, any model, failover)
3. Full Tracing (every LLM call logged with input/output/tokens/latency/cost) — by DEFAULT
4. Prompt Registry (versioned, deploy from UI without code changes)
5. Projects/Workspaces (per-project API keys, models, traces)

## P2 — Important (90 days)
1. Evaluation engine (bring dataset, built-in evaluators, LLM-as-judge)
2. RAG/Knowledge bases (upload docs → vector index → use in playground/agent)
3. Agent Builder (no-code: instructions + tools)
4. Fine-tuning SFT (upload dataset → job → deploy)
5. Production monitoring (real-time tokens/cost/latency/quality)
6. Content safety guardrails (per deployment)

## P3 — Nice to have
- Scenario leaderboard (benchmark scores: MMLU, HumanEval, MATH)
- AI Red Teaming (adversarial attack simulation)
- Synthetic data generation
- Visual pipeline/workflow builder
- Human feedback collection (thumbs up/down → annotation queue)
- Pairwise evaluation (Yupp.ai style)
- CI/CD quality gates

## Architecture Recommendations
- **ClickHouse** for traces/evals (not PostgreSQL — won't scale)
- **pgvector** for RAG indexes (start simple)
- **Redis** for caching + Celery for async eval jobs
- **OpenAI-compatible API surface** for every deployment endpoint
- **Trace-first design** — traces are the backbone for eval, monitoring, fine-tuning
- `POST /v1/compare` as core primitive for multi-model comparison
- Evaluators as plug-in functions with standard interface

## Azure AI Foundry Key Differentiators to Copy
1. Evaluation at every lifecycle stage (pre-production, production monitoring, CI/CD)
2. Guardrails at input + tool call + tool response + output layers
3. Model leaderboard with quality/safety/performance/cost benchmarks
4. Agentic RAG with parallel subquery execution + citations

## Azure AI Foundry Weaknesses to Exploit
1. Too complex — no instant gratification
2. Azure lock-in — no open-source option
3. No native prompt registry
4. Poor developer UX vs LangSmith
5. Multi-model compare limited to 3 models, requires deploying each
6. Pricing opacity

**Why:** To guide H'appi Foundry development toward the right features and architecture.
**How to apply:** Use P1/P2/P3 ranking when the user asks what to build next.
