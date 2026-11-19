# Core Invariants & Agent Operating Rules

**Author & Owner:** `yuva.devlab@gmail.com`  
**Scope:** Organization-wide (`yuvadevlab`)

---

## Invariant 0: Zero Unapproved Commits & Pushe (Strict Policy)

- **NEVER** run `git commit`, `git push`, or create pull requests in ANY repository unless the user explicitly requests it in the current turn.
- Directives like "start", "proceed", "fix this", "implement", "build" or "test" authorize implementation, building, and running tests, but strictly do NOT authorize committing or pushing.
- Always leave changes staged or in the working tree, present verification results, and wait for confirmation.

---

## Invariant 1: Attribution Standard

- All documentation, commit messages, and git author/committer configs must use:
  - Name: `yuva-devlab`
  - Email: `yuva.devlab@gmail.com`

---

## Invariant 2: Polyglot & Future-Proof Standards

The Yuva DevLab ecosystem is polyglot by design and extensible to any language, runtime, or framework. Organization-wide templates, configurations, and workflows must never lock into a single language's tooling or syntax. Instead, they enforce universal engineering disciplines:

- **Clean Compilation & Type Safety**: Zero syntax, type, or compiler errors.
- **Strict Static Analysis**: Zero linter errors and zero linter warnings.
- **Automated Verification**: Comprehensive test coverage across all active modules.
- **Self-Documenting Code**: Public interfaces, APIs, and complex logic must be documented.

---

## Invariant 3: Hard 250-Line Limit & Early Decomposition

- No source file (`.ts`, `.tsx`, `.py`, `.go`, `.css`, `.yml`) may exceed 250 lines of code.
- Files reaching 200 lines must be proactively decomposed into focused submodules.

---

## Invariant 4: Pure Platform CSS & Design Tokens

- The legacy utility-first CSS framework is prohibited across all codebases.
- Styling is implemented exclusively with W3C Cascade Layers (`@layer dl-*`), pure platform CSS, and `@yuva-devlab/tokens`.

---

## Invariant 5: Standardized Branch Naming

- All branches must match: `^(feat|fix|refactor|perf|chore|docs|test|ci|hotfix)/[a-z0-9-]+$`
- Random, unformatted, or single-word branch names are prohibited.

---

## Invariant 6: Conventional Commits Standard

- All commits must conform to Conventional Commits v1.0.0:
  `<type>(<optional-scope>): <imperative summary>`
- Permitted types: `feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `ci`, `chore`, `revert`.
- Imperative tense, lowercase first letter, no trailing period, max 72 characters.

---

## Invariant 7: Enums Over Raw Unions & Centralized Route/Query Keys

- Avoid declaring types as raw string literal unions (`"dev" | "prod"`). Always declare TypeScript `enum`s or `as const` object dictionaries.
- Never hardcode raw URL query parameters, route paths, HTTP headers, or storage keys; declare them centrally and build URLs with `URLSearchParams`.

---

## Invariant 8: Shared NPM Packages Environment Isolation

- Shared NPM packages (`@yuva-devlab/*`) must NEVER read `process.env` directly. Consumers pass parameters explicitly.

---

## Invariant 9: Semantic Component Architecture & 90/10 Hybrid Styling Standard

- UI components must declare purpose-revealing semantic classes (`.dl-card`, `.app-card`, `.dl-table`) in domain-scoped modular stylesheets (`< 200 lines`, strictly `< 250 lines`) under `@layer dl-components`.
- Multi-class utility soup in JSX (`className="class-1 class-2 class-3..."`) is strictly prohibited; utilities are reserved exclusively for macro layout orchestration (10% glue).
- Variations and themes must be parameterized via CSS variables mapped to `@yuva-devlab/tokens`.
