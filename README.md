# Hi, I'm Vaibhav Singhal

Senior Software Engineer at Workday, focused on building scalable backend systems, clean APIs, and ambitious AI-driven products.

## About me

- Backend-focused engineer with a strong interest in system design and architecture
- Work primarily with Python (FastAPI, Flask, Django), Java (Micronaut), TypeScript (NestJS), PostgreSQL, AWS/GCP, and Docker
- Interested in LLM systems, developer tooling, and production-grade full-stack products

## Featured work

### Axiom — AI-powered markdown notes platform

Full-stack platform with 8 repos, 190+ PRs, and 1,000+ tests. Domain-driven backend, streaming LLM gateway, and a reusable AI microservices layer — all wired through Docker Compose with e2e testing and CI guardrails.

```mermaid
flowchart LR
    subgraph Application
        UI["Axiom UI\nNext.js 14 · TypeScript\nTailwind · TanStack Query"]
        API["Axiom API\nFastAPI · SQLModel\nSupabase Auth · Alembic"]
        Nexus["Axiom Nexus\nLLM Gateway · SSE Streaming\nJob Queue · Prompt Cache"]
    end

    subgraph AI["AI Platform"]
        Pulse["Pulse\nInput Normalizer\nChunking · Embeddings"]
        Cortex["Cortex\nLLM Executor\nOpenAI · Anthropic · Gemini"]
        Synth["Synth\nOutput Renderer\nText · TTS · Files"]
    end

    subgraph Infra["Infrastructure"]
        Orch["Orchestration\nDocker Compose · nginx\ne2e · CI Guardrails"]
        PG[(PostgreSQL\npgvector)]
    end

    UI --> API
    UI --> Nexus
    Nexus --> Pulse
    Nexus --> Cortex
    Nexus --> Synth
    API --> PG
    Nexus --> PG
    Orch -.- UI & API & Nexus & Pulse & Cortex & Synth
```

| Repo | Stack | What it does |
|------|-------|-------------|
| [`Axiom-api`](https://github.com/vsinghal3737/Axiom-api) | FastAPI · SQLModel · PostgreSQL | Backend API — domain-driven layers, 300+ tests |
| [`Axiom-ui`](https://github.com/vsinghal3737/Axiom-ui) | Next.js 14 · TypeScript · Tailwind | Frontend — TanStack Query, Zustand, BlockNote editor |
| [`Axiom-nexus`](https://github.com/vsinghal3737/Axiom-nexus) | FastAPI · SSE · pgvector | LLM gateway — job orchestration, RAG, streaming, cost tracking |
| [`Axiom-orchestration`](https://github.com/vsinghal3737/Axiom-orchestration) | Docker Compose · nginx · Make | 6-service stack, e2e testing, policy guardrails |
| [`pulse`](https://github.com/vsinghal3737/pulse) | FastAPI · stateless | Input normalizer — text chunking, embeddings, document parsing |
| [`cortex`](https://github.com/vsinghal3737/cortex) | FastAPI · stateless | LLM executor — multi-provider, circuit breakers, fallback |
| [`synth`](https://github.com/vsinghal3737/synth) | FastAPI · stateless | Output renderer — text, TTS, file generation |
| [`my-notes`](https://github.com/vsinghal3737/my-notes) | Monorepo | V1 (deprecated) — 59 PRs, migration reference |

### Other projects

- **SmartKart** — AI-powered meal-kit ordering platform (event-driven, conversational ordering)
  - [`SmartKart-api`](https://github.com/vsinghal3737/SmartKart-api) — FastAPI · SQLModel · PostgreSQL · RabbitMQ
- **Portfolio** — [Repo](https://github.com/vsinghal3737/Vaibhav-Singhal-Portfolio) | [Live](https://www.vaibhavsinghal.dev/)
- **Monitoring Service**

---

*Building useful, scalable systems without unnecessary complexity.*
