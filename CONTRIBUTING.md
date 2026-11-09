# Contributing to the Yuva DevLab Ecosystem

**Author & Maintainer:** `yuva.devlab@gmail.com`  
**Organization:** [yuvadevlab](https://github.com/yuvadevlab)

---

## 1. Branch Naming Standards

To prevent random and inconsistent branch names across repositories, all branches must follow this strict pattern:

```
<type>/<short-description>
```

### Allowed Types

| Prefix      | Description                                  | Example                           |
| ----------- | -------------------------------------------- | --------------------------------- |
| `feat/`     | New feature or capability                    | `feat/supervisor-process-engine`  |
| `fix/`      | Bug fix or issue resolution                  | `fix/port-collision-detection`    |
| `refactor/` | Code restructuring without functional change | `refactor/runner-decomposition`   |
| `perf/`     | Performance optimization                     | `perf/socket-stream-buffering`    |
| `chore/`    | Tooling, dependencies, or maintenance        | `chore/upgrade-node-22`           |
| `docs/`     | Documentation or guide updates               | `docs/architecture-overview`      |
| `test/`     | Adding or updating tests                     | `test/port-prober-cases`          |
| `ci/`       | CI/CD pipelines and GitHub Actions           | `ci/reusable-pr-lint`             |
| `hotfix/`   | Urgent production patch                      | `hotfix/session-token-expiration` |

### Rules

- **Lowercase kebab-case only:** Use `[a-z0-9-]`. No uppercase letters, spaces, or underscores.
- **Concise & Descriptive:** Keep `<short-description>` between 2 and 5 words separated by hyphens.
- **Integration Branches:** `main` (production-ready) and `dev` (active integration) are protected branches.

---

## 2. Commit Message Standards

All commits across every repository must strictly adhere to the **Conventional Commits v1.0.0** specification:

```
<type>(<optional-scope>): <imperative summary>

[optional body]

[optional footer(s)]
```

### Commit Types

- `feat`: New user-facing feature or library capability.
- `fix`: Bug fix.
- `refactor`: Code restructuring without bug fix or feature addition.
- `perf`: Performance enhancement.
- `docs`: Documentation only.
- `test`: Adding or correcting tests.
- `ci`: Changes to CI/CD workflows or scripts.
- `chore`: Maintenance, dependencies, or tool configurations.
- `revert`: Reverting a previous commit.

### Format Rules

1. **Imperative Mood:** Use "add process supervisor", not "added" or "adds".
2. **Lowercase First Letter:** Write `feat(supervisor): implement runner`, not `feat(supervisor): Implement runner`.
3. **No Trailing Period:** Do not end the subject line with a `.`.
4. **Length Limit:** Keep the first line under 72 characters.
5. **Scope:** Lowercase module, package, or app name (e.g. `supervisor`, `portal`, `tokens`, `ui`).

---

## 3. Enforcement Mechanisms

These standards are enforced through three complementary layers:

1. **GitHub Organization Rulesets (Server-Side):**
   GitHub blocks any branch push or commit that does not conform to the regex before it reaches the remote.
2. **Reusable PR Lint Workflow (`reusable-pr-lint.yml`):**
   Validates PR branch names, PR titles, and all commit subjects on every pull request.
3. **AI Agent Guidelines (`AGENTS.md`):**
   Antigravity and all AI agents are required to adhere to these rules before staging changes.

---

## 4. Strict Ecosystem Invariants

1. **Commit & Push Authorization:**
   Automated tools and agents must **never** run `git commit` or `git push` without explicit user confirmation.
2. **Polyglot & Future-Proof Standards:**
   Zero compiler/type errors, zero linter warnings, and comprehensive documentation across any language.
3. **Pure Platform CSS:**
   Utility-first CSS frameworks are prohibited. All styling uses W3C Cascade Layers (`@layer dl-*`) and `@yuva-devlab/tokens`.
4. **Modularity & 250-Line Limit:**
   Every source file must remain strictly under 250 lines of code (decompose early at 200 lines).
5. **Attribution:**
   Standardize author and committer metadata to `yuva.devlab@gmail.com`.
