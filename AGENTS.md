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

---

## 2. Organization Repositories Reference

| Repository                                                     | Primary Stack                                  | Scope                                 |
| -------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------- |
| [`devlab-portal`](https://github.com/yuvadevlab/devlab-portal) | TypeScript (Next.js 15, NestJS 11, Prisma)     | Control Plane & Process Orchestration |
| [`devlab-shared`](https://github.com/yuvadevlab/devlab-shared) | TypeScript (Design System, Tokens, Supervisor) | Core Shared Libraries & Packages      |
| [`finai`](https://github.com/yuvadevlab/finai)                 | TypeScript (Next.js, NestJS, Prisma)           | Financial Intelligence & Analytics    |
| [`orchestrai`](https://github.com/yuvadevlab/orchestrai)       | TypeScript (Next.js, NestJS, Temporal)         | Multi-Agent Orchestration             |
| [`devlab-logs`](https://github.com/yuvadevlab/devlab-logs)     | TypeScript (Next.js, NestJS, ClickHouse)       | Centralized Telemetry & Observability |
| [`vitalai`](https://github.com/yuvadevlab/vitalai)             | TypeScript + Python (FastAPI)                  | Healthcare Analytics & Telemetry      |
| [`devlab-guard`](https://github.com/yuvadevlab/devlab-guard)   | Python (FastAPI, LangChain)                    | AI Security Guardrails                |
| [`incidentai`](https://github.com/yuvadevlab/incidentai)       | Python (FastAPI)                               | Automated Incident Triage             |
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
