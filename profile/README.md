# Yuva DevLab Ecosystem

A unified autonomous AI agent ecosystem, distributed microservices fleet, and engineering control plane.

---

## Overview

**Yuva DevLab** is a multi-application engineering ecosystem and autonomous intelligence platform. It consists of specialized enterprise applications powered by a centralized web control plane, a shared design system and SDK foundation, automated CI/CD engines, and dedicated infrastructure tooling.

---

## Architectural Landscape

```
┌────────────────────────────────────────────────────────────────────────┐
│                        YUVA DEVLAB ARCHITECTURE                        │
├────────────────────────────────────────────────────────────────────────┤
│                                                                        │
│   CONTROL PLANE & INFRASTRUCTURE                                       │
│   ┌───────────────────────────────┬────────────────────────────────┐   │
│   │     devlab-portal (:3000)     │      devlab-infra (Cloud)      │   │
│   │ • Central SSO & RBAC Hub      │ • Master Service Fleet Catalog │   │
│   │ • Process Supervisor & Logs   │ • Google Secret Manager (GSM)  │   │
│   │ • Real-Time Socket.IO Stream  │ • Ingress & Routing Topology   │   │
│   └───────────────┬───────────────┴────────────────┬───────────────┘   │
│                   │                                │                   │
│   SPECIALIZED AUTONOMOUS APPLICATIONS              │                   │
│   ┌───────────────┴────────────────┬───────────────┴───────────────┐   │
│   │             FinAI              │          OrchestrAI           │   │
│   │         (:3001 / :4001)        │    (:3002 / :4002 / :8082)    │   │
│   │ • Personal Financial Advisory  │ • Multi-Agent Swarm Coord     │   │
│   │ • Autonomous Ledger & Analytics│ • Realtime Streaming Agents   │   │
│   ├────────────────────────────────┼───────────────────────────────┤   │
│   │          DevLab Logs           │          KnowledgeAI          │   │
│   │    (:3003 / :4003 / :9003)     │        (:3008 / :4008)        │   │
│   │ • OpenTelemetry Collector      │ • Enterprise Knowledge Graph  │   │
│   │ • Trace Aggregation & Audits   │ • Vector RAG & Semantic Search│   │
│   ├────────────────────────────────┼───────────────────────────────┤   │
│   │          DevLab Guard          │          IncidentAI           │   │
│   │            (:8085)             │        (:3006 / :4006)        │   │
│   │ • SAIF Security Guardrails     │ • SRE Drill Simulator         │   │
│   │ • Vulnerability Scanner Daemon │ • Automated RCA & Post-Mortem │   │
│   └────────────────────────────────┴───────────────────────────────┘   │
│                                                                        │
│   SHARED FOUNDATION (devlab-shared)                                    │
│   ┌────────────────────────────────────────────────────────────────┐   │
│   │ • @yuva-devlab/ui         • @yuva-devlab/tokens                │   │
│   │ • @yuva-devlab/supervisor • @yuva-devlab/logger                │   │
│   │ • @yuva-devlab/auth-client• @yuva-devlab/auth-server (Node/Py) │   │
│   │ • @yuva-devlab/regex      • @yuva-devlab/resilience            │   │
│   └────────────────────────────────┬───────────────────────────────┘   │
│                                    │                                   │
│   CI/CD PIPELINE ENGINE (.github)  │                                   │
│   ┌────────────────────────────────┴───────────────────────────────┐   │
│   │ • Reusable CI & Testing        • Reusable Docker Buildx        │   │
│   │ • Conventional PR Linting      • Reusable Cloud Run Deployment │   │
│   └────────────────────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────────────────────┘
```

---

## Ecosystem Repositories

| Repository                                                     | Purpose                                           | Primary Technologies                             | Ports (Web / API)           |
| :------------------------------------------------------------- | :------------------------------------------------ | :----------------------------------------------- | :-------------------------- |
| [`devlab-portal`](https://github.com/yuvadevlab/devlab-portal) | Central Control Plane & Process Orchestrator      | Next.js 15, NestJS 11, Prisma, Redis, Socket.IO  | `:3000` / `:4000`           |
| [`devlab-infra`](https://github.com/yuvadevlab/devlab-infra)   | Infrastructure Control Plane, Fleet Catalog & GSM | Terraform, Cloud Run, Secret Manager, Python     | Control Plane               |
| [`devlab-shared`](https://github.com/yuvadevlab/devlab-shared) | Core Design System, Tokens, Supervisor & SDKs     | TypeScript, pnpm, tsup, W3C Layers               | Shared SDKs                 |
| [`.github`](https://github.com/yuvadevlab/.github)             | Central Workflows, Reusable Actions & Templates   | GitHub Actions, Docker Buildx, Artifact Registry | CI/CD Engine                |
| [`fin-ai`](https://github.com/yuvadevlab/fin-ai)               | Intelligent Financial Analytics & Ledger Platform | Next.js 15, NestJS 11, Prisma, PostgreSQL        | `:3001` / `:4001`           |
| [`orchestr-ai`](https://github.com/yuvadevlab/orchestr-ai)     | Multi-Agent Orchestration & Workflow Automation   | Next.js 15, Fastify, Python 3.12, Redis, BullMQ  | `:3002` / `:4002` / `:8082` |
| [`devlab-logs`](https://github.com/yuvadevlab/devlab-logs)     | Distributed Log Aggregation & Observability       | Next.js 15, NestJS 11, Go 1.23, PostgreSQL       | `:3003` / `:4003` / `:9003` |
| [`knowledg-ai`](https://github.com/yuvadevlab/knowledg-ai)     | Enterprise Semantic Knowledge & Realtime Sync     | Next.js 15, Node.js 24, Python 3.12, pgvector    | `:3008` / `:4008`           |
| [`devlab-guard`](https://github.com/yuvadevlab/devlab-guard)   | Security Guardrails & Policy Enforcement          | Python 3.12, FastAPI                             | `:8085`                     |
| [`incident-ai`](https://github.com/yuvadevlab/incident-ai)     | Automated Incident Response & Root Cause Analysis | Next.js 15, Node.js 22, Docker Sandboxing        | `:3006` / `:4006`           |
| [`quant-ai`](https://github.com/yuvadevlab/quant-ai)           | High-Frequency Backtesting & Signal Pipeline      | Next.js 15, Node.js 22, Python 3.12              | `:3007` / `:4007`           |

---

## Engineering Standards

1. **Design System & Platform CSS:**  
   Styling across all applications is built exclusively on pure platform CSS, W3C Cascade Layers (`@layer dl-*`), and `@yuva-devlab/tokens`.
2. **Modularity & Clean Architecture:**  
   In `devlab-shared`, source files strictly adhere to a **250-line maximum**. Helper logic, subcomponents, and styles are decomposed early.
3. **Commit & Governance Invariant:**  
   Automated tools and agents operate under a strict approval policy: code authoring, linting, and testing are performed locally, but commits and pushes require explicit authorization.
4. **Attribution:**  
   All commits and repository governance attribution are standardized to `yuva.devlab@gmail.com`.
