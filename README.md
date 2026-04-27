# Hi, I'm Vaibhav Singhal

Senior Software Engineer at Workday, focused on building scalable backend systems, clean APIs, and ambitious AI-driven products.

## About Me

- Backend-focused engineer with a strong interest in system design and architecture
- Work primarily with Python (FastAPI, Flask, Django), Java (Micronaut), TypeScript (NestJS), PostgreSQL, AWS/GCP, and Docker
- Interested in LLM systems, developer tooling, and production-grade full-stack products

## Featured Work

### Prism - Reusable AI Microservices Layer

Shared AI platform powering the products below. Prism exposes Pulse, Cortex, and Synthesizer behind one gateway, with stable routes like `/pulse/v1`, `/cortex/v1`, and `/synthesizer/v1`.

```mermaid
flowchart LR
    Client["Consumer Product<br/>(Axiom, ZitherAi, ...)"]
    Gateway["Prism Gateway<br/>nginx<br/>/pulse/v1<br/>/cortex/v1<br/>/synthesizer/v1"]
    Pulse["Prism-pulse<br/>Input Service<br/>Normalize / Parse"]
    Cortex["Prism-cortex<br/>LLM Gateway<br/>OpenAI / Anthropic / Gemini"]
    Synthesizer["Prism-synthesizer<br/>Output Service<br/>Text / TTS / Files"]

    Client --> Gateway
    Gateway --> Pulse
    Gateway --> Cortex
    Gateway --> Synthesizer
    Pulse -. parse (optional) .-> Cortex
    Synthesizer -. compose (optional) .-> Cortex
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`Prism-pulse`](https://github.com/vsinghal3737/Prism-pulse) | FastAPI / stateless | Input service: text normalization, document parsing, optional model-backed transforms |
| [`Prism-cortex`](https://github.com/vsinghal3737/Prism-cortex) | FastAPI / stateless | LLM executor: multi-provider OpenAI, Anthropic, Gemini, circuit breakers, fallback |
| [`Prism-synthesizer`](https://github.com/vsinghal3737/Prism-synthesizer) | FastAPI / stateless | Output service: text, TTS, file generation, optional model-backed composition |
| [`Prism-orchestration`](https://github.com/vsinghal3737/Prism-orchestration) | Docker Compose / nginx / Make | Independent Prism stack with gateway routing and external `prism-network` for consumer products |

### Axiom - AI-Powered Markdown Notes Platform

Full-stack markdown notes platform with a domain-driven FastAPI backend, Next.js editor, streaming LLM gateway, Docker orchestration, e2e tests, and CI guardrails.

```mermaid
flowchart LR
    subgraph Axiom
        UI["Axiom UI<br/>Next.js 14 / TypeScript<br/>Tailwind / TanStack Query"]
        API["Axiom API<br/>FastAPI / SQLModel<br/>Supabase Auth / Alembic"]
        Nexus["Axiom Nexus<br/>LLM Gateway / SSE Streaming<br/>Job Queue / Prompt Cache"]
        PG[("PostgreSQL<br/>pgvector")]
    end

    subgraph Prism["Prism AI Platform"]
        Gateway["Prism Gateway"]
        Pulse["Prism-pulse"]
        Cortex["Prism-cortex"]
        Synthesizer["Prism-synthesizer"]
    end

    subgraph Infra["Infrastructure"]
        Orch["Axiom Orchestration<br/>Docker Compose / nginx<br/>e2e / CI Guardrails"]
    end

    UI --> API
    UI --> Nexus
    Nexus --> Gateway
    Gateway --> Pulse & Cortex & Synthesizer
    API --> PG
    Nexus --> PG
    Orch -.- UI & API & Nexus
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`Axiom-api`](https://github.com/vsinghal3737/Axiom-api) | FastAPI / SQLModel / PostgreSQL | Backend API: notes, workspaces, queue recovery |
| [`Axiom-ui`](https://github.com/vsinghal3737/Axiom-ui) | Next.js 14 / TypeScript / Tailwind | Frontend: TanStack Query, Zustand, BlockNote editor |
| [`Axiom-nexus`](https://github.com/vsinghal3737/Axiom-nexus) | FastAPI / SSE / pgvector | LLM gateway: jobs, RAG, streaming, cost tracking |
| [`Axiom-orchestration`](https://github.com/vsinghal3737/Axiom-orchestration) | Docker Compose / nginx / Make | Local stack, e2e testing, Prism network wiring |
| [`my-notes`](https://github.com/vsinghal3737/my-notes) | Monorepo | V1 migration reference |

### ZitherAi - AI Music Brain and Playlist Copilot

AI music brain and playlist copilot with provider adapters, taste modeling, playlist ranking, sequencing, and Prism-backed AI operations.

```mermaid
flowchart LR
    subgraph ZitherAi
        ZUI["ZitherAi UI<br/>Next.js / TypeScript"]
        ZAPI["ZitherAi API<br/>FastAPI / SQLModel"]
        ZNexus["ZitherAi Nexus<br/>Music Brain"]
        ZBridge["ZitherAi Bridge<br/>Provider Adapters"]
        PG[("PostgreSQL<br/>pgvector")]
    end

    subgraph Providers["Music Providers"]

        YouTube["YouTube"]
        Spotify["Spotify"]
        Apple["Apple Music"]
    end

    subgraph Prism["Prism AI Platform"]
        Gateway["Prism Gateway"]
        Pulse["Prism-pulse"]
        Cortex["Prism-cortex"]
        Synthesizer["Prism-synthesizer"]
    end

    subgraph Infra["Infrastructure"]
        ZOrch["ZitherAi Orchestration<br/>Docker Compose / nginx"]
    end

    ZUI --> ZAPI
    ZUI --> ZNexus
    ZAPI --> PG
    ZNexus --> PG
    ZNexus --> ZBridge
    ZBridge --> YouTube
    ZBridge --> Spotify
    ZBridge --> Apple
    ZNexus --> Gateway
    Gateway --> Pulse
    Gateway --> Cortex
    Gateway --> Synthesizer
    ZOrch -.- ZUI
    ZOrch -.- ZAPI
    ZOrch -.- ZNexus
    ZOrch -.- ZBridge

    style Providers fill:#262626,stroke:#525252,color:#e5e5e5,stroke-dasharray: 4 4
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`ZitherAi-api`](https://github.com/vsinghal3737/ZitherAi-api) | FastAPI / SQLModel / PostgreSQL | Backend API: users, taste profiles, playlists |
| [`ZitherAi-ui`](https://github.com/vsinghal3737/ZitherAi-ui) | Next.js 14 / TypeScript / Tailwind | Frontend: conversational playlist generation |
| [`ZitherAi-nexus`](https://github.com/vsinghal3737/ZitherAi-nexus) | FastAPI / SSE / pgvector | Music brain: recommendations, ranking, embeddings |
| [`ZitherAi-bridge`](https://github.com/vsinghal3737/ZitherAi-bridge) | FastAPI / stateless | Provider adapters: YouTube, Spotify, Apple Music |
| [`ZitherAi-orchestration`](https://github.com/vsinghal3737/ZitherAi-orchestration) | Docker Compose / nginx / Make | Local stack, gateway routing, Prism network wiring |

### Other Projects

- **SmartKart** - AI-powered meal-kit ordering platform with event-driven conversational ordering
  - [`SmartKart-api`](https://github.com/vsinghal3737/SmartKart-api) - FastAPI / SQLModel / PostgreSQL / RabbitMQ
- **Portfolio** - [Repo](https://github.com/vsinghal3737/Vaibhav-Singhal-Portfolio) | [Live](https://www.vaibhavsinghal.dev/)
- **Monitoring Service**

---

*Building useful, scalable systems without unnecessary complexity.*
