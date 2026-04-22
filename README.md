# Hi, I'm Vaibhav Singhal

Senior Software Engineer at Workday, focused on building scalable backend systems, clean APIs, and ambitious AI-driven products.

## About me

- Backend-focused engineer with a strong interest in system design and architecture
- Work primarily with Python (FastAPI, Flask, Django), Java (Micronaut), TypeScript (NestJS), PostgreSQL, AWS/GCP, and Docker
- Interested in LLM systems, developer tooling, and production-grade full-stack products

## Featured work

### Prism — Reusable AI microservices layer

Shared AI platform powering all AI-driven products below. Pulse, Cortex, and Synth are exposed as separate stateless HTTP services, so consumer projects call only the capabilities they need. Pulse and Synth can optionally delegate model-backed work to Cortex. Prism orchestration lives in its own repo and creates the external `prism-network`.

```mermaid
flowchart LR
    Client["Any Project<br/>(Axiom, ZitherAi, ...)"]
    Client --> Pulse["Pulse<br/>Input Service<br/>Normalize · Parse"]
    Client --> Cortex["Cortex<br/>LLM Gateway<br/>OpenAI · Anthropic · Gemini"]
    Client --> Synth["Synth<br/>Output Service<br/>Text · TTS · Files"]
    Pulse -. optional parse .-> Cortex
    Synth -. optional compose .-> Cortex
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`pulse`](https://github.com/vsinghal3737/pulse) | FastAPI · stateless | Input service — text normalization, document parsing, optional model-backed transforms |
| [`cortex`](https://github.com/vsinghal3737/cortex) | FastAPI · stateless | LLM executor — multi-provider (OpenAI, Anthropic, Gemini), circuit breakers, fallback |
| [`synth`](https://github.com/vsinghal3737/synth) | FastAPI · stateless | Output service — text, TTS, file generation, optional model-backed composition |
| [`prism-orchestration`](https://github.com/vsinghal3737/prism-orchestration) | Docker Compose · Make | Independent Prism stack — creates `prism-network` for consumer projects |

### Axiom — AI-powered markdown notes platform

Full-stack platform with 190+ PRs and 1,000+ tests. Domain-driven backend, streaming LLM gateway, and block-based editor — wired through its own Docker Compose stack with e2e testing and CI guardrails. Connects to [Prism](#prism--reusable-ai-microservices-layer) over the external `prism-network` for AI operations.

```mermaid
flowchart LR
    subgraph Axiom
        UI["Axiom UI<br/>Next.js 14 · TypeScript<br/>Tailwind · TanStack Query"]
        API["Axiom API<br/>FastAPI · SQLModel<br/>Supabase Auth · Alembic"]
        Nexus["Axiom Nexus<br/>LLM Gateway · SSE Streaming<br/>Job Queue · Prompt Cache"]
    end

    subgraph Prism["Prism — AI Platform"]
        Pulse["Pulse"]
        Cortex["Cortex"]
        Synth["Synth"]
    end

    subgraph Infra["Infrastructure"]
        Orch["Orchestration<br/>Docker Compose · nginx<br/>e2e · CI Guardrails"]
        PG[(PostgreSQL<br/>pgvector)]
    end

    UI --> API
    UI --> Nexus
    Nexus --> Pulse & Cortex & Synth
    API --> PG
    Nexus --> PG
    Orch -.- UI & API & Nexus
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`Axiom-api`](https://github.com/vsinghal3737/Axiom-api) | FastAPI · SQLModel · PostgreSQL | Backend API — domain-driven layers, 300+ tests |
| [`Axiom-ui`](https://github.com/vsinghal3737/Axiom-ui) | Next.js 14 · TypeScript · Tailwind | Frontend — TanStack Query, Zustand, BlockNote editor |
| [`Axiom-nexus`](https://github.com/vsinghal3737/Axiom-nexus) | FastAPI · SSE · pgvector | LLM gateway — job orchestration, RAG, streaming, cost tracking |
| [`Axiom-orchestration`](https://github.com/vsinghal3737/Axiom-orchestration) | Docker Compose · nginx · Make | Product orchestration only — local stack, e2e testing, joins external `prism-network` |
| [`my-notes`](https://github.com/vsinghal3737/my-notes) | Monorepo | V1 (deprecated) — 59 PRs, migration reference |

### ZitherAi — AI music brain and playlist copilot

AI-powered music recommendation engine that sits on top of provider ecosystems (YouTube, Apple Music). Provider-agnostic AI taste layer for intent understanding, mood/vibe parsing, candidate retrieval, ranking, sequencing, and optional original music generation. Connects to [Prism](#prism--reusable-ai-microservices-layer) over the external `prism-network` for AI operations.

```mermaid
flowchart LR
    subgraph ZitherAi
        ZUI["ZitherAi UI<br/>Next.js 14 · TypeScript<br/>Tailwind · TanStack Query"]
        ZAPI["ZitherAi API<br/>FastAPI · SQLModel<br/>Supabase Auth · Alembic"]
        ZNexus["ZitherAi Nexus<br/>Music Gateway<br/>Recommendation Brain"]
        ZBridge["ZitherAi Bridge<br/>Provider Adapters<br/>YouTube · Apple Music"]
    end

    subgraph Prism["Prism — AI Platform"]
        Pulse["Pulse"]
        Cortex["Cortex"]
        Synth["Synth"]
    end

    subgraph Infra["Infrastructure"]
        ZOrch["Orchestration<br/>Docker Compose<br/>Dev Environment"]
        PG[(PostgreSQL<br/>pgvector)]
    end

    ZUI --> ZAPI
    ZUI --> ZNexus
    ZNexus --> Pulse & Cortex & Synth
    ZNexus --> ZBridge
    ZAPI --> PG
    ZNexus --> PG
    ZOrch -.- ZUI & ZAPI & ZNexus & ZBridge
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`ZitherAi-api`](https://github.com/vsinghal3737/ZitherAi-api) | FastAPI · SQLModel · PostgreSQL | Backend API — users, taste profiles, playlists |
| [`ZitherAi-ui`](https://github.com/vsinghal3737/ZitherAi-ui) | Next.js 14 · TypeScript · Tailwind | Frontend — conversational playlist generation |
| [`ZitherAi-nexus`](https://github.com/vsinghal3737/ZitherAi-nexus) | FastAPI · SSE · pgvector | Music gateway — recommendation brain, ranking, sequencing, taste embeddings |
| [`ZitherAi-bridge`](https://github.com/vsinghal3737/ZitherAi-bridge) | FastAPI · stateless | Provider adapters — YouTube and Apple Music integration |
| [`ZitherAi-orchestration`](https://github.com/vsinghal3737/ZitherAi-orchestration) | Docker Compose · Make | Product orchestration only — local stack, joins external `prism-network` |

### Other projects

- **SmartKart** — AI-powered meal-kit ordering platform (event-driven, conversational ordering)
  - [`SmartKart-api`](https://github.com/vsinghal3737/SmartKart-api) — FastAPI · SQLModel · PostgreSQL · RabbitMQ
- **Portfolio** — [Repo](https://github.com/vsinghal3737/Vaibhav-Singhal-Portfolio) | [Live](https://www.vaibhavsinghal.dev/)
- **Monitoring Service**

---

*Building useful, scalable systems without unnecessary complexity.*
