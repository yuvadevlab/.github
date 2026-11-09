# Yuva DevLab Ecosystem

**Author & Maintainer:** `yuva.devlab@gmail.com`  
**Organization:** [yuvadevlab](https://github.com/yuvadevlab)

---

## Overview

**Yuva DevLab** is a unified, multi-application engineering ecosystem and autonomous intelligence platform. It consists of specialized enterprise applications powered by a centralized web control plane, a shared design system and SDK foundation, and dedicated operational tooling.

---

## Architectural Landscape

```
┌────────────────────────────────────────────────────────────────────────┐
│                        YUVA DEVLAB ARCHITECTURE                        │
├────────────────────────────────────────────────────────────────────────┤
│                                                                        │
│   CENTRAL CONTROL PLANE                                                │
│   ┌────────────────────────────────────────────────────────────────┐   │
│   │                      devlab-portal (:3000)                     │   │
│   │   • Unified Application Catalog & SSO Authentication           │   │
│   │   • Centralized Process & Lifecycle Orchestration              │   │
│   │   • Real-Time Socket.IO Streaming Logs & Health Telemetry      │   │
│   └────────────────────────────────┬───────────────────────────────┘   │
│                                    │                                   │
│   SPECIALIZED APPLICATIONS         │                                   │
│   ┌───────────────┬────────────────┴┬───────────────┬──────────────┐   │
│   │     FinAI     │   OrchestrAI    │  DevLab Logs  │   VitalAI    │   │
│   │ (:3001/:4001) │  (:3002/:4002)  │ (:3003/:4003) │(:3004/:4004) │   │
│   │ Finance &     │ Multi-Agent     │ Centralized   │ Health &     │   │
│   │ Analytics     │ Orchestration   │ Telemetry     │ Analytics    │   │
│   └───────────────┴─────────────────┴───────────────┴──────────────┘   │
│   ┌────────────────────────────────┬───────────────────────────────┐   │
│   │       devlab-guard (:8000)     │      incidentai (:8085)       │   │
│   │   Security Guardrails & AI Gate│   Automated Incident Triage   │   │
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
│   PRODUCTION HOST OPERATIONS       │                                   │
│   ┌────────────────────────────────┴───────────────────────────────┐   │
│   │                     devlab-ops (CLI Suite)                     │   │
│   │   • Production Worktrees       • Zero-Downtime Builds          │   │
│   │   • Database Backup & Sync     • System Health Diagnostics     │   │
│   └────────────────────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────────────────────┘
```

---

## Ecosystem Repositories

| Repository                                                     | Purpose                                           | Primary Technologies                            | Ports (Web / API) |
| -------------------------------------------------------------- | ------------------------------------------------- | ----------------------------------------------- | ----------------- |
| [`devlab-portal`](https://github.com/yuvadevlab/devlab-portal) | Central Control Plane & Process Orchestrator      | Next.js 15, NestJS 11, Prisma, Redis, Socket.IO | `:3000` / `:4000` |
| [`devlab-shared`](https://github.com/yuvadevlab/devlab-shared) | Core Design System, Tokens, Supervisor & SDKs     | TypeScript, pnpm, tsup, W3C Layers              | —                 |
| [`finai`](https://github.com/yuvadevlab/finai)                 | Intelligent Financial Analytics & Ledger Platform | Next.js, NestJS, Prisma, PostgreSQL             | `:3001` / `:4001` |
| [`orchestrai`](https://github.com/yuvadevlab/orchestrai)       | Multi-Agent Orchestration & Workflow Automation   | Next.js, NestJS, Temporal/Queues                | `:3002` / `:4002` |
| [`devlab-logs`](https://github.com/yuvadevlab/devlab-logs)     | Distributed Log Aggregation & Observability       | Next.js, NestJS, ClickHouse/PostgreSQL          | `:3003` / `:4003` |
| [`vitalai`](https://github.com/yuvadevlab/vitalai)             | Healthcare Telemetry & Predictive Analytics       | Next.js, FastAPI, Python, PostgreSQL            | `:3004` / `:4004` |
| [`devlab-guard`](https://github.com/yuvadevlab/devlab-guard)   | Security Guardrails & Policy Enforcement          | Python, FastAPI                                 | `:8000`           |
| [`incidentai`](https://github.com/yuvadevlab/incidentai)       | Automated Incident Response & Root Cause Analysis | Python, FastAPI                                 | `:8085`           |
| [`.github`](https://github.com/yuvadevlab/.github)             | Central Workflows, Reusable Actions & Templates   | GitHub Actions                                  | —                 |

---

## Engineering Standards

1. **Design System & Platform CSS:**  
   Styling across all applications is built exclusively on pure platform CSS, W3C Cascade Layers (`@layer dl-*`), and `@yuva-devlab/tokens`. Utility-first CSS frameworks are prohibited.
2. **Modularity & Clean Architecture:**  
   In `devlab-shared`, source files strictly adhere to a **250-line maximum**. Helper logic, subcomponents, and styles are decomposed early.
3. **Commit & Governance Invariant:**  
   Automated tools and agents operate under a strict approval policy: code authoring, linting, and testing are performed locally, but commits and pushes require explicit authorization.
4. **Attribution:**  
   All commits, author metadata, and governance attribution are standardized to `yuva.devlab@gmail.com`.
