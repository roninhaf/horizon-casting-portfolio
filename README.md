# Horizon Casting Portfolio

**Public Architecture & Technical Documentation**

**Horizon Casting by Ombre & Pixel**  
Bilingual SaaS platform for artists, actors (including child actors and voice actors), and creatives to build rich, discoverable profiles for casting directors, productions, and photographers.

**OpenClaw** — Self-hosted persistent AI agent infrastructure with multi-role orchestration and compound learning loops.

This repository provides a transparent, detailed view of the architecture, compliance posture, technical decisions, and agentic development systems behind the private production codebase. It is prepared specifically to demonstrate end-to-end full-stack engineering, production-grade deployment, privacy-first design, and real-world agentic systems building in the context of an application for the **Full Stack Engineer** role at **Nous Research**.

---

## Why This Work Aligns with Nous Research

Nous Research builds open-source, humanistic AI with a focus on powerful agents (Hermes) that feature self-improving learning loops, persistent memory, skill creation from experience, and seamless local/cloud model routing. The Full Stack Engineer role owns software end-to-end — from managed inference and platform infrastructure to agent UX and developer APIs — while shipping user-facing products like Nous Portal and Hermes Agent.

My work directly parallels and operationalizes these priorities:

- **Agentic Systems & Tool-Calling Loops**: OpenClaw is a production daily-driver persistent agent system with explicit role-based orchestration (Chief Orchestrator, Coding Architect, etc.), long-term memory, and structured compound engineering loops. This mirrors Hermes Agent's core architecture of self-improvement, persistence, and multi-provider intelligence.
- **End-to-End Full-Stack Ownership**: Complete ownership of a production SaaS platform including frontend (Next.js), backend services, media pipelines, payments, deployment infrastructure, security, and compliance — exactly the broad-scope, high-leverage responsibility described in the role.
- **Privacy & Security by Design**: Handling highly sensitive personal visual and identity data (photos, videos, profiles of actors including minors) under Quebec Law 25 (full PIA + Transfer Impact Assessment), PIPEDA, and GDPR. This is the exact posture required for trustworthy AI products that process user data.
- **High-Agency Execution & AI-Augmented Velocity**: Solo development of a complex, regulated MVP with intense output through structured multi-model AI workflows (millions of tokens across frontier models) while maintaining architectural integrity and shipping real users.
- **Production Infrastructure**: Self-hosting on consumer GPU hardware (RTX 5070), Dockerized agents, Coolify PaaS, Hetzner EU hosting for data residency, Cloudflare — practical experience with the managed inference and platform layers central to Nous products.

I bring not just code, but lived experience building the class of systems Nous is productizing at scale.

---

## Project Overview: Horizon Casting (Ombre & Pixel)

Horizon Casting enables creative professionals to create compelling, searchable profiles that connect them with opportunities. Key capabilities include rich media support (photos, videos, voice), semantic discovery features for casting directors, tiered subscriptions, and a privacy-respecting architecture suitable for sensitive personal data including that of child actors.

**Status**: MVP live in production with initial users; active iteration toward 500–1000 users. Bilingual (English/French) UX prioritized from the start.

---

## High-Level Architecture

```mermaid
graph TD
    subgraph "User-Facing Layer"
        Users[Casting Directors / Productions / Photographers]
        Actors[Artists & Actors \n(incl. child actors, voice actors)]
    end

    subgraph "Frontend"
        NextJS[Next.js Frontend\nTypeScript, Responsive, Bilingual UX]
    end

    subgraph "Backend & Services"
        Laravel[Laravel Backend\nPHP, APIs, Auth, Business Logic]
        Postgres[(PostgreSQL)]
        Cloudinary[Cloudinary\nSigned uploads, transformations, delivery]
        Stripe[Stripe\nSubscriptions + Tax]
        Resend[Resend\nTransactional Email]
    end

    subgraph "Agentic Infrastructure"
        OpenClaw[OpenClaw Persistent Agent\nDocker on RTX 5070\nMulti-Role Orchestration]
        MultiLLM[Multi-Provider Routing\nOpenRouter + Local Models]
    end

    subgraph "Deployment & Platform"
        Coolify[Coolify Self-Hosted PaaS]
        Hetzner[Hetzner Helsinki\nEU Data Residency]
        Cloudflare[Cloudflare CDN & Security]
    end

    Actors -->|Profile Creation & Media Upload| NextJS
    Users -->|Search & Discovery| NextJS
    NextJS -->|REST/GraphQL APIs| Laravel
    Laravel -->|Data| Postgres
    Laravel -->|Media Pipeline| Cloudinary
    Laravel -->|Billing Webhooks| Stripe
    Laravel -->|Notifications| Resend
    OpenClaw -->|Development Acceleration & Tool Calls| MultiLLM
    Coolify -->|Hosts & Orchestrates| Laravel
    Coolify -->|Hosts| OpenClaw
    Hetzner & Cloudflare -->|Infrastructure| Coolify
```

**Data Flow Highlights**:
- Sensitive media and profile data flows through encrypted, signed channels with strict access controls.
- Compliance boundaries enforced at every layer (minimization, consent, residency, auditability).
- Agentic layer operates orthogonally for development velocity while production systems remain deterministic and auditable.

---

## Compliance & Privacy Architecture (Quebec Law 25, PIPEDA, GDPR)

This is one of the most critical aspects of the system and directly relevant to building trustworthy AI products.

- **Privacy Impact Assessment (PIA)** conducted for Quebec Law 25, including Transfer Impact Assessment for any cross-border elements.
- Data minimization by design: only essential fields collected; media handling prioritizes external links where possible, with Cloudinary upsell for premium rich media.
- Explicit consent flows, granular permissions, and clear data subject rights implementation.
- EU hosting (Hetzner Helsinki) chosen for strong data residency alignment.
- Encryption in transit and at rest; secure signed URLs for media delivery.
- Audit logging and access controls suitable for sensitive personal data including that of minors.
- Bilingual consent and privacy policy language.

This experience gives me practical, production-level understanding of the regulatory and architectural requirements for any system handling personal media or identity data at scale — a foundation for responsible AI tooling.

---

## OpenClaw: Persistent Self-Hosted AI Agent Infrastructure

OpenClaw is my daily-driver implementation of a persistent, self-improving agent system running locally on consumer hardware (Pop!_OS 24.04 + RTX 5070 12GB).

**Core Capabilities**:
- **Multi-Role Orchestration**: Explicit agent roles including Chief Orchestrator and Coding Architect that delegate, review, and iterate on complex tasks.
- **Persistent Memory & Context**: Cross-session recall, project memory, and user modeling patterns.
- **Compound Engineering Loops**: Structured iterative workflows combining frontier models (GPT-5.5 class, Claude, DeepSeek, GLM, Kimi, etc.) with tool-calling and verification steps. This has enabled burning millions of tokens while shipping high-quality production features in compressed timeframes.
- **Tool Integration**: Deep integration with coding environments (KiloCode, Cursor), Discord for notifications/collaboration, and local inference where beneficial.
- **Multi-Provider Routing**: Patterns consistent with OpenRouter and Nous-style ecosystems — choosing the right model for cost, speed, capability, and privacy.

**Relevance to Hermes Agent**: OpenClaw embodies the same principles Nous has productized — persistent agents that learn, maintain memory, create and refine capabilities over time, and operate reliably as infrastructure rather than one-off sessions. Running it daily on real work gives me intimate, practical insight into the UX, reliability, and orchestration challenges of such systems.

---

## Development Methodology & Velocity

The intense development of Horizon Casting (major activity May 2026 onward, MVP shipped with users live) was accelerated by treating AI as a force multiplier through compound loops and agent swarms rather than simple prompting. This meta-layer of agentic development is itself a core skill for building the next generation of AI products.

Outcomes include rapid iteration on complex features (media pipelines, compliance architecture, billing, semantic matching) while maintaining clean architecture and shipping to real users under regulatory constraints.

---

## Technical Decisions & Tradeoffs

- **Why Next.js + Laravel?** Next.js for modern, type-safe, performant frontend with excellent developer experience and SEO/UX capabilities. Laravel chosen for rapid, secure backend development with mature ecosystem for auth, queues, APIs, and business logic — pragmatic choice enabling solo velocity on a regulated product. Equivalent patterns transfer directly to Python/Node/Rust stacks.
- **Media Strategy**: Hybrid approach — prioritize verifiable external links (YouTube, Vimeo) for core profiles to control costs and complexity; Cloudinary for premium rich media (photos, videos, voice). Signed uploads and transformations ensure security and performance.
- **Deployment**: Coolify on Hetzner provides self-hosted PaaS control and EU residency without vendor lock-in. Cloudflare adds global CDN, DDoS protection, and caching.
- **Compliance-First Design**: Regulatory requirements shaped data models, hosting choices, consent UX, and logging from day one rather than bolted on later.

---

## Production Status & Metrics

- MVP fully deployed and live (horizoncasting.studio)
- Initial paying/ active users achieved; clear growth path to hundreds of profiles
- Complete compliance implementation (PIA artifacts, policies, technical controls)
- Production observability, automated backups, security hardening in place
- Bilingual experience delivered end-to-end

---

## Repository Purpose & Future Content

This public repository serves as a living portfolio. Current content focuses on architecture and rationale. Future additions (as non-sensitive elements are extracted) may include:
- Detailed decision records (ADRs)
- Sanitized architecture diagrams and data flow maps
- Compliance implementation notes (high-level)
- Screenshots and walkthroughs of key UX flows
- OpenClaw configuration patterns and orchestration examples (where shareable)

Screenshots and visuals to be added by owner.

---

## Contact & Next Steps

The core production codebase remains private for IP and operational reasons. I am fully prepared to provide secure walkthroughs, code reviews, architecture deep-dives, or live demonstrations of OpenClaw patterns and compliance flows during any interview or diligence process.

This body of work demonstrates precisely the combination of skills Nous Research seeks in a Full Stack Engineer: broad end-to-end ownership, practical agentic systems experience, production deployment under real constraints, privacy/security rigor, and the high-agency execution needed to ship important products.

**GitHub**: https://github.com/roninhaf  
**Primary Private Repo**: solid-happiness (Horizon Casting production)  
**Live Product**: horizoncasting.studio (upon request)

Thank you for reviewing this portfolio. I look forward to contributing to Nous Portal, Hermes Agent, and the broader mission of democratizing world-class intelligence.

— Hafid Feghouli  
Montréal, Québec  
June 2026
