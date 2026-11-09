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
