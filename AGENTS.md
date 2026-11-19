# Yuva DevLab Organization Agent Guidelines

Master instructions and ecosystem invariants for AI agents (Antigravity, Claude Code, GitHub Copilot, Cursor) working within the **Yuva DevLab (`yuvadevlab`)** organization.

---

## 1. Core Invariants (Zero Exceptions)

1. **Zero Commits Without Explicit Instruction (CRITICAL)**:
   - NEVER execute `git commit`, `git push`, or open pull requests in ANY repository unless the user explicitly commands it in the current turn (e.g. "commit these changes", "commit and push").
   - Directives like "start", "proceed", "fix this", "implement", "build", or "test" authorize implementation, building, and running tests ONLY.
   - Always leave changes staged or in the working tree, present verification results, and wait for confirmation.

2. **Standardized Attribution**:
   - All git commit author and committer metadata, documentation, and PR attribution must use `yuva.devlab@gmail.com`.

3. **Strict Prohibition on Legacy Utility CSS**:
   - Do NOT mention, recommend, or use the legacy utility-first CSS framework anywhere in code, comments, documentation, commit messages, or responses.
   - All styling across the ecosystem is built using pure platform CSS, W3C Cascade Layers (`@layer dl-*`), and `@yuva-devlab/tokens`.

4. **Hard 250-Line Code Modularity**:
   - No source file across any package, app, or service may exceed 250 lines of code.
   - Deconstruct into focused submodules early when approaching 200 lines.

5. **Polyglot & Future-Proof Engineering**:
   - The Yuva DevLab ecosystem is polyglot and designed to accommodate any language or runtime (TypeScript, Python, Go, Rust, etc.).
   - Organization-wide templates, rules, and workflows must remain language-agnostic, focusing on universal engineering invariants (clean compilation, zero warnings, modularity, full documentation) rather than binding to specific language tooling.

6. **Standardized Branch Naming**:
   - Branches created by agents or contributors must strictly match:
     `^(feat|fix|refactor|perf|chore|docs|test|ci|hotfix)/[a-z0-9-]+$`
   - Examples: `feat/supervisor-process-engine`, `fix/port-collision-detection`.

7. **Conventional Commits Invariant**:
   - When authorized to commit, messages must strictly adhere to Conventional Commits v1.0.0:
     `<type>(<optional-scope>): <imperative summary>`
   - Allowed types: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `ci`, `chore`, `revert`.
   - Imperative mood, lowercase first letter, no period at end, under 72 characters.

8. **Enums Over Raw Unions & Centralized Keys**:
   - Prefer TypeScript `enum`s or `as const` object dictionaries with mapped types over raw string literal unions (`"dev" | "prod"`).
   - Never hardcode raw URL search parameters, route paths, HTTP headers, or storage keys; declare them centrally and construct URLs with `URLSearchParams`.

9. **Shared NPM Packages Environment Isolation**:
   - Shared NPM packages (`@yuva-devlab/*`) must NEVER read `process.env` directly. Consumers pass parameters explicitly.

10. **Semantic Component Architecture & 90/10 Hybrid Styling Standard**:
   - UI components must declare purpose-revealing semantic classes (`.dl-card`, `.app-card`, `.dl-table`) in domain-scoped modular stylesheets (`< 200 lines`, strictly `< 250 lines`) under `@layer dl-components`.
   - Multi-class utility soup in JSX (`className="class-1 class-2 class-3..."`) is strictly prohibited; utilities are reserved exclusively for macro layout orchestration (10% glue).
   - Variations and themes must be parameterized via CSS variables mapped to `@yuva-devlab/tokens`.

---

## 2. Organization Repositories Reference

| Repository                                                     | Primary Stack                                  | Scope                                 |
| -------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------- |
| [`devlab-portal`](https://github.com/yuvadevlab/devlab-portal) | TypeScript (Next.js 15, NestJS 11, Prisma)     | Control Plane & Process Orchestration |
| [`devlab-shared`](https://github.com/yuvadevlab/devlab-shared) | TypeScript (Design System, Tokens, Supervisor) | Core Shared Libraries & Packages      |
| [`fin-ai`](https://github.com/yuvadevlab/fin-ai)                 | TypeScript (Next.js, NestJS, Prisma)           | Financial Intelligence & Analytics    |
| [`orchestr-ai`](https://github.com/yuvadevlab/orchestr-ai)       | TypeScript (Next.js, Fastify, gRPC)            | Multi-Agent Orchestration Swarm       |
| [`devlab-logs`](https://github.com/yuvadevlab/devlab-logs)     | TypeScript (Next.js, Express, pgvector)        | Centralized Telemetry & Observability |
| [`knowledg-ai`](https://github.com/yuvadevlab/knowledg-ai)     | TypeScript + Python (FastAPI) (Planned)        | Enterprise Knowledge & Semantic RAG   |
| [`devlab-guard`](https://github.com/yuvadevlab/devlab-guard)   | Python (FastAPI, Tree-sitter)                  | AI Security Guardrails                |
| [`incident-ai`](https://github.com/yuvadevlab/incident-ai)       | TypeScript (FSM, Docker Sandboxing)            | Automated SRE Incident Triage         |
| [`devlab-ops`](https://github.com/yuvadevlab/devlab-ops)       | Go / Shell / Docker                            | Production Host & Worktree CLI        |
| [`.github`](https://github.com/yuvadevlab/.github)             | GitHub Actions, YAML, Markdown                 | Org Defaults, Workflows & Templates   |

---

## 3. Working in This Repository (`.github`)

When modifying `.github`:

- **Local Validation**: Always test YAML files before presenting changes:
  ```bash
  python3 -c "import yaml, glob; [yaml.safe_load(open(f)) for f in glob.glob('.github/**/*.yml', recursive=True)]"
  ```
- **Single `main` Branch**: Changes are integrated directly into `main` because workflows and templates are consumed directly from `@main`.
- **Targeted Action Triggers**: Workflows must use `pull_request` on all PRs + `push` strictly scoped to `[main, dev]` with `cancel-in-progress: true`.
