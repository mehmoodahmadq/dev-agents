# dev-agents

**Production-ready AI agent definitions for every dev workflow.**

Each file in this repo *is* the agent — a complete, self-contained system prompt you drop into your project and use immediately. No runtime, no framework, no setup. Just markdown.

---

## Why this exists

Most "AI agents" repositories are catalogs: they list use cases, describe what an agent *could* do, and link off to demos. This one is different.

- **Every file is a working agent.** Copy it, use it.
- **Opinionated, not exhaustive.** Each agent takes a clear stance on the right way to do things in its domain. No "you could also consider..." hedging.
- **Security-aware by default.** Every language agent has a dedicated Security section covering injection, crypto, secrets, deserialization, and supply chain — not an afterthought.
- **Current tooling only.** No legacy patterns, no dated advice. Python uses `uv` and Ruff. TypeScript uses Zod and `satisfies`. Swift uses Swift Concurrency. Kotlin uses coroutines and Compose.
- **Tool-agnostic.** Written for Claude Code's sub-agent system, but the body of every file is a plain system prompt — drop it into ChatGPT, Cursor, Windsurf, or any API call.

---

## Quick start

### With Claude Code

```bash
# From the root of your project
mkdir -p .claude/agents
cp /path/to/dev-agents/agents/languages/typescript.md .claude/agents/
```

Then invoke in Claude Code:

```
/typescript refactor this service to use Zod validation
```

Claude Code auto-routes to the right agent based on the `description` field in the frontmatter.

### With any other AI tool

Everything below the `---` frontmatter block is a plain system prompt. Copy it into ChatGPT's "custom GPT" instructions, Cursor rules, Windsurf workflows, or an API call's `system` parameter.

```python
import anthropic

with open("agents/languages/python.md") as f:
    content = f.read()
    system_prompt = content.split("---", 2)[2].strip()

client = anthropic.Anthropic()
client.messages.create(
    model="claude-opus-5",
    system=system_prompt,
    messages=[...],
)
```

---

## Available agents

### Languages

| Agent | Focus | Highlights |
|-------|-------|------------|
| [typescript](agents/languages/typescript.md) | Type-safe TypeScript | Strict mode, Zod, discriminated unions, `satisfies`, no `any` |
| [javascript](agents/languages/javascript.md) | Modern JavaScript | ES2020+, async/await, Web APIs, zero-dep mindset |
| [python](agents/languages/python.md) | Idiomatic Python | Type hints, Pydantic, asyncio, Ruff, mypy strict |
| [go](agents/languages/go.md) | Production Go | Explicit errors, small interfaces, errgroup, context propagation |
| [rust](agents/languages/rust.md) | Systems Rust | Ownership, `thiserror`/`anyhow`, Tokio, zero-cost abstractions |
| [java](agents/languages/java.md) | Modern Java 21 | Records, sealed classes, Spring Boot, constructor injection |
| [csharp](agents/languages/csharp.md) | C# 12 / .NET 8 | Nullable safety, ASP.NET Core, EF Core, async end-to-end |
| [ruby](agents/languages/ruby.md) | Idiomatic Ruby / Rails | Service objects, thin controllers, RSpec, security-first Rails |
| [swift](agents/languages/swift.md) | Modern Swift | SwiftUI, Swift Concurrency, `Actor`, value semantics |
| [kotlin](agents/languages/kotlin.md) | Modern Kotlin | Coroutines, Flow, Compose, MVVM, null safety |
| [php](agents/languages/php.md) | Modern PHP 8.3+ | `strict_types`, readonly classes, enums, PHPStan max, Symfony/Laravel |
| [erlang](agents/languages/erlang.md) | Erlang / OTP | Supervision trees, gen_server, Dialyzer, let-it-crash, rebar3 |

### Security

| Agent | Focus | Highlights |
|-------|-------|------------|
| [owasp-reviewer](agents/security/owasp-reviewer.md) | OWASP Top 10 (2021) audit | Language-agnostic, severity-ranked findings with concrete fixes |
| [threat-modeler](agents/security/threat-modeler.md) | STRIDE threat modeling | Trust boundaries, ranked threats, mitigations tied to owners |
| [secure-code-reviewer](agents/security/secure-code-reviewer.md) | PR-level secure review | Secrets, crypto, authn/authz, validation, logging/PII |
| [dependency-auditor](agents/security/dependency-auditor.md) | Supply-chain audit | CVEs, typosquats, install scripts, lockfile & SBOM hygiene |
| [secrets-scanner](agents/security/secrets-scanner.md) | Credential leak detection | Source, git history, Docker layers, CI logs; rotation-first remediation |
| [authn-authz-reviewer](agents/security/authn-authz-reviewer.md) | Identity & access control | Login, MFA, sessions, OAuth/OIDC, JWT, IDOR/BOLA, multi-tenant isolation |
| [crypto-reviewer](agents/security/crypto-reviewer.md) | Cryptographic review | Algorithms, AEAD, KDFs, PRNGs, key management, TLS, protocol composition |
| [iac-security-reviewer](agents/security/iac-security-reviewer.md) | IaC misconfiguration | Terraform, CloudFormation, K8s, Dockerfiles, CI/CD pipelines |
| [api-security-reviewer](agents/security/api-security-reviewer.md) | OWASP API Top 10 (2023) | BOLA, BOPLA, function-level authz, resource consumption, GraphQL/gRPC |
| [privacy-reviewer](agents/security/privacy-reviewer.md) | Privacy & data protection | GDPR/CCPA, retention, DSAR, consent, PII in logs/analytics, sub-processors |

### Data

| Agent | Focus | Highlights |
|-------|-------|------------|
| [sql](agents/data/sql.md) | Production SQL | Postgres/MySQL/SQLite + OLAP; schema, indexes, plans, parameterization, RLS |
| [data-pipelines](agents/data/data-pipelines.md) | Batch & streaming pipelines | ELT, medallion, dbt, Airflow/Dagster, idempotency, backfills, observability |
| [ml-workflows](agents/data/ml-workflows.md) | Production ML | Reproducibility, eval, train/serve parity, deployment, drift monitoring, security |

### Frontend

| Agent | Focus | Highlights |
|-------|-------|------------|
| [react](agents/frontend/react.md) | React 18/19 | Composition API, hooks rules, RSC/Next App Router, TanStack Query, Suspense, Compiler-aware |
| [vue](agents/frontend/vue.md) | Vue 3 / Nuxt 3 | Composition API + `<script setup>`, runes-style reactivity, Pinia setup stores, server actions |
| [svelte](agents/frontend/svelte.md) | Svelte 5 / SvelteKit | Runes (`$state`/`$derived`/`$effect`), form actions, server vs universal load, env separation |
| [css](agents/frontend/css.md) | Modern CSS | `@layer`, container queries, design tokens, logical properties, `:has()`, motion preferences |
| [accessibility](agents/frontend/accessibility.md) | WCAG 2.2 AA | Semantic HTML, keyboard, focus management, ARIA patterns, screen-reader testing |

### Backend

| Agent | Focus | Highlights |
|-------|-------|------------|
| [express](agents/backend/express.md) | Node.js + Express 5 | Async error flow, middleware order, Zod validation, Drizzle/Prisma, helmet, structured logs |
| [fastapi](agents/backend/fastapi.md) | FastAPI + Pydantic v2 | Async SQLAlchemy 2.0, Depends DI, lifespan, OpenAPI-driven, async hygiene |
| [django](agents/backend/django.md) | Django 5 / DRF / Ninja | Settings split, custom user model, services + selectors, migrations, `manage.py check --deploy` |
| [nestjs](agents/backend/nestjs.md) | NestJS 10+ / Fastify | Modules + DI, guards/interceptors/pipes/filters, Prisma/TypeORM, BullMQ, microservices |
| [rest-api](agents/backend/rest-api.md) | Language-agnostic API design | Resources, status codes, RFC 7807 errors, cursor pagination, idempotency keys, ETags, versioning, OpenAPI 3.1 |

### DevOps

| Agent | Focus | Highlights |
|-------|-------|------------|
| [docker](agents/devops/docker.md) | OCI image authoring | Multi-stage, BuildKit cache/secret mounts, distroless, non-root, digest pinning, signals, SBOM/cosign |
| [kubernetes](agents/devops/kubernetes.md) | Production manifests | Deployments/StatefulSets, probes, requests/limits, HPA, PDB, NetworkPolicy, Helm/Kustomize, graceful shutdown |
| [terraform](agents/devops/terraform.md) | Terraform / OpenTofu 1.6+ | Modules, remote state with locking, provider pinning, `moved`/`removed`/`import`, OIDC CI, drift detection |
| [github-actions](agents/devops/github-actions.md) | CI/CD on GitHub | Least-privilege `GITHUB_TOKEN`, OIDC cloud auth, SHA-pinned actions, caching, matrix, reusable workflows |
| [observability](agents/devops/observability.md) | Logs / metrics / traces | OpenTelemetry SDK + Collector, RED/USE, cardinality discipline, SLO burn-rate alerts, tail sampling |
| [sre](agents/devops/sre.md) | Site reliability practice | SLOs + error budgets, incident roles, blameless postmortems, runbooks, on-call hygiene, progressive delivery |

### Testing

| Agent | Focus | Highlights |
|-------|-------|------------|
| [unit-testing](agents/testing/unit-testing.md) | Language-agnostic unit testing | AAA, FIRST, fakes vs mocks, behavior-not-implementation, deterministic, mutation-driven coverage |
| [integration-testing](agents/testing/integration-testing.md) | Real-dependency integration | Testcontainers, ephemeral DBs/queues, migrations, transactional vs TRUNCATE isolation, MSW for HTTP boundaries |
| [e2e-playwright](agents/testing/e2e-playwright.md) | End-to-end browser flows | Playwright TS, role-based locators, web-first assertions, storage-state auth, traces, sharding |
| [client-testing](agents/testing/client-testing.md) | Frontend component testing | Vitest/Jest + Testing Library, user-event v14, MSW, role queries, no implementation-detail tests |
| [load-testing](agents/testing/load-testing.md) | Performance & capacity | k6 / Locust, smoke / load / stress / spike / soak / breakpoint, open-loop arrival rate, SLO-driven thresholds |
| [mutation-testing](agents/testing/mutation-testing.md) | Real test-quality measurement | Stryker / mutmut / PIT, operators, equivalent mutants, incremental + per-test coverage, ratcheting thresholds |

### Databases

| Agent | Focus | Highlights |
|-------|-------|------------|
| [postgres](agents/databases/postgres.md) | PostgreSQL 15+ in production | Schema & index design, plan reading, lock-safe migrations, vacuum/bloat, partitioning, PgBouncer, PITR, roles & RLS |
| [mongodb](agents/databases/mongodb.md) | MongoDB 7/8 | Embed vs reference, ESR index rule, aggregation pipelines, read/write concerns, shard keys, change streams, operator injection |
| [redis](agents/databases/redis.md) | Redis 7+ / Valkey | Structure selection, key schemas & TTLs, stampede control, Lua rate limits, streams over pub/sub, eviction, ACLs |
| [elasticsearch](agents/databases/elasticsearch.md) | Elasticsearch 8/9, OpenSearch | Strict mappings, text vs keyword, filter context, hybrid BM25 + kNN with RRF, ILM & data streams, shard sizing, reindex behind an alias |

### Mobile

| Agent | Focus | Highlights |
|-------|-------|------------|
| [react-native](agents/mobile/react-native.md) | React Native 0.76+ / Expo | New Architecture, Expo Router, FlashList & Reanimated 3, offline-first storage, EAS Build/Update, SecureStore, deep-link validation |

---

## Agent file format

Every agent follows the same structure:

```markdown
---
name: <slug>
description: <one-line description — used by Claude Code for auto-routing>
---

You are an expert <role>...

## Core principles
## <Domain sections — Type System, Error Handling, Concurrency, etc.>
## Tooling             # current, specific tools — "use a linter" is not tooling
## Security            # mandatory outside agents/security/ — see below
## What to avoid       # exactly one closing section, under this name
```

The `description` field matters: it's what Claude Code reads to decide which sub-agent to invoke for a given task. Keep it specific and action-oriented.

Two structural rules worth stating explicitly:

- **Agents in `agents/security/` carry no `## Security` section.** The whole file is a security document, so a nested section is noise. They carry `## Review procedure` and `## Output format` instead — a domain-appropriate name (`## Audit procedure`, `## How to run a threat model`) is fine.
- **Reviewer agents in other domains** carry `## Review procedure` and `## Output format` as well, alongside their `## Security` section.

---

## Quality bar

Every agent in this repo must be:

- **Opinionated** — one clear stance, not a survey of options.
- **Actionable** — code examples, not vague prose.
- **Current** — reflects the ecosystem *today*, not five years ago.
- **Self-contained** — usable without reading any other file.
- **Security-aware** — a dedicated `## Security` section is mandatory outside `agents/security/`, where the entire agent already is one.
- **Honest about trade-offs** — explains *why* a decision was made.

If a PR adds an agent that doesn't meet all six, it doesn't merge.

---

## Roadmap

Agents are organised by domain under `agents/`. Current layout:

```
agents/
  languages/     typescript, javascript, python, go, rust, java, csharp, ruby, swift, kotlin, php, erlang
  security/      owasp-reviewer, threat-modeler, secure-code-reviewer, dependency-auditor,
                 secrets-scanner, authn-authz-reviewer, crypto-reviewer,
                 iac-security-reviewer, api-security-reviewer, privacy-reviewer
  data/          sql, data-pipelines, ml-workflows
  frontend/      react, vue, svelte, css, accessibility
  backend/       express, fastapi, django, nestjs, rest-api
  devops/        docker, kubernetes, terraform, github-actions, observability, sre
  testing/       unit-testing, integration-testing, e2e-playwright, client-testing,
                 load-testing, mutation-testing
  databases/     postgres, mongodb, redis, elasticsearch
  mobile/        react-native (swift and kotlin may move here)
```

Planned domains:

```
agents/
  mobile/        flutter, ios-native, android-native
  databases/     dynamodb, clickhouse, cassandra
```

Naming: `<stack-or-tool>.md` — lowercase, hyphenated, no version numbers in filenames.

---

## Contributing

PRs welcome. Before opening one:

1. Read an existing agent to match the structure and tone.
2. Make sure your agent meets every point in the [Quality bar](#quality-bar).
3. Include a working code example in every major section.
4. Add a dedicated `## Security` section — no exceptions.

---

## License

MIT
