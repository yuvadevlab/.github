# Yuva DevLab Central Organization Repository (`.github`)

**Author & Maintainer:** `yuva.devlab@gmail.com`  
**Organization:** [yuvadevlab](https://github.com/yuvadevlab)

---

## Overview

This repository serves as the centralized configuration, shared CI/CD workflows, composite actions, and standardized issue/PR templates for the entire **Yuva DevLab** GitHub organization.

GitHub automatically surfaces templates, community health files, and workflows defined in this repository to all repositories under `yuvadevlab` (unless overridden at the repository level).

---

## Contents & Architecture

```
.github/
├── .agents/                        # Agent rules and core invariants
│   ├── AGENTS.md
│   └── rules/00-core-invariants.md
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.yml          # Structured bug reporting form with ecosystem app picker
│   │   ├── feature_request.yml     # Structured RFC / feature proposal form
│   │   └── config.yml              # Issue template chooser configuration & security redirects
│   ├── actions/
│   │   └── setup-devlab-env/       # Composite action for Node 22, pnpm 12.5.1, uv & Turbo cache
│   ├── workflows/
│   │   ├── reusable-ci.yml         # Shared callable CI workflow for monorepos and microservices
│   │   ├── reusable-docker.yml     # Shared callable Docker build verification workflow
│   │   ├── reusable-pr-lint.yml    # Shared branch naming & conventional commits linting
│   │   └── validate.yml            # Self-validation CI checking YAML syntax & action integrity
│   ├── dependabot.yml              # Weekly automated updates for GitHub Actions
│   └── pull_request_template.md    # Universal polyglot PR template with verification checklists
├── profile/
│   └── README.md                   # Public organization profile landing page for yuvadevlab
├── AGENTS.md                       # Master instructions and invariants for AI agents
├── CODE_OF_CONDUCT.md              # Contributor Covenant 2.1 code of conduct
├── CONTRIBUTING.md                 # Universal development standards and commit policies
├── LICENSE                         # MIT License
├── README.md                       # This repository documentation
└── SECURITY.md                     # Organization-wide vulnerability disclosure policy
```

---

## How Repositories Consume Shared Assets

### 1. Reusable CI Workflow (`reusable-ci.yml`)

Repositories can call the central CI workflow via `workflow_call`:

```yaml
name: CI

on:
  push:
    branches: [main, dev]
  pull_request:
    branches: [main, dev]

jobs:
  ci:
    uses: yuvadevlab/.github/.github/workflows/reusable-ci.yml@main
    with:
      node-version: "22"
      pnpm-version: "12.5.1"
      python-version: "3.12"
      install-python: false
      run-tests: true
      run-lint: true
      run-typecheck: true
      run-build: true
```

### 2. Composite Environment Action (`setup-devlab-env`)

For custom workflows that need standardized tooling:

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: yuvadevlab/.github/.github/actions/setup-devlab-env@main
    with:
      node-version: "22"
      pnpm-version: "12.5.1"
      install-python: "true"
      python-version: "3.12"
```

### 3. Reusable Docker Workflow (`reusable-docker.yml`)

```yaml
jobs:
  docker:
    uses: yuvadevlab/.github/.github/workflows/reusable-docker.yml@main
    with:
      dockerfile: "Dockerfile"
      context: "."
      image-name: "devlab-portal"
      push: false
```

### 4. Reusable PR & Branch Linter (`reusable-pr-lint.yml`)

Ensures branch names and commit messages follow ecosystem standards on PRs:

```yaml
jobs:
  lint-pr:
    uses: yuvadevlab/.github/.github/workflows/reusable-pr-lint.yml@main
```

---

## Centralized Community Health Defaults

The following files are automatically inherited across all `yuvadevlab` repositories:

- **PR Template:** Standardized PR description, checklist, and testing verification.
- **Issue Templates:** Consistent bug reports and feature requests.
- **Security Policy:** Default vulnerability reporting instructions.
- **Code of Conduct & Contributing:** Uniform open-source standards.

---

## Development & Maintenance

### Validating Changes

Run YAML validation locally before committing:

```bash
python3 -c "
import yaml, glob
for f in glob.glob('.github/**/*.yml', recursive=True):
    yaml.safe_load(open(f))
    print(f'✓ {f}')
"
```

The repository's `.github/workflows/validate.yml` will also verify all workflow files automatically on push and pull request.
