# Software Development Axioms

High-level software development guidelines that cannot be enforced by linters. Particularly helpful for AI agents during automated code reviews. Use them during design, development, and code review as a shared mental model for how to build software.

## Categories

| Category | Scope |
| --- | --- |
| **0 - Meta & orchestration** | AI agents, tooling philosophy, automation |
| **1 - Tools & services** | CI, monitoring, infrastructure, dependencies |
| **2 - Code** | Naming, structure, patterns, architecture |
| **3 - Tests** | Test design, isolation, coverage philosophy |
| **4 - Content** | Typography, localization |
| **5 - Interfaces & accessibility** | CSS, interactivity, keyboard/focus, a11y |
| **6 - Performance** | Optimization, caching, indexing |
| **7 - Security & reliability** | Secrets, permissions, least privilege |
| **D - Database** | ORM, schema design, migrations |
| **I - Internet** | REST, URLs, HTML/JSON boundaries, deep linking |
| **P - Python** | EAFP, exception handling, type checking |
| **S - Swift** | Protocols, DI, factory pattern, access control |

## Usage

The full axioms document is in [`axioms.md`](axioms.md). It is self-contained so it can be synced to other repositories.

Each axiom has a short identifier (e.g., **X204**, **P001**, **S003**). Axioms with expanded explanations and code examples link to the [Axiom Details & Examples](axioms.md#axiom-details--examples) section at the bottom of the document.

## Syncing to other repositories

Add this repo as a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) in consuming repositories:

```bash
git submodule add https://github.com/chasefinch/axioms.git axioms
```

Then add the `gitsubmodule` ecosystem to the consuming repo's `.github/dependabot.yml` so Dependabot opens PRs when axioms are updated:

```yaml
version: 2
updates:
  - package-ecosystem: "gitsubmodule"
    directory: "/"
    schedule:
      interval: "weekly"
```

When cloning a repo that includes this submodule:

```bash
git clone --recurse-submodules <repo-url>

# Or, if already cloned:
git submodule update --init
```
