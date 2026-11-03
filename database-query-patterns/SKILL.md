---
name: database-query-patterns
description: >-
  Learn, assess, implement, and verify database query patterns in an existing or new
  project. Use for N+1 queries, slow reads, pagination, indexing, query shape,
  projections, joins, ORM loading behavior, transactions, and data access changes.
  Inspect the project's database engine, ORM, schema, conventions, constraints,
  and actual query evidence before recommending or changing anything.
---

# Database Query Patterns — Project-First

## Purpose

Improve query **correctness, predictability, and measured performance** without imposing a new ORM, database engine, architecture, or query convention. Be a focused database-query specialist inside the developer's existing debugging, planning, testing, and review workflows; do **not** duplicate generic development orchestration.

## Non-negotiable rules

1. **Inspect before prescribing.** Identify engine/version, ORM/query builder/version, relevant schema/indexes, query path, data size, existing data-access conventions and observable contracts. Never assume SQL Server, PostgreSQL, MySQL, SQLite, MongoDB, or a particular ORM.
2. **Preserve semantics.** Filters, tenant/authorization scoping, null behavior, collations, ordering, deduplication, time boundaries, transaction boundaries, isolation, and result shape are requirements—not incidental query details.
3. **No unmeasured speed claims.** An index, join, projection, or eager-load is a *hypothesis* until a representative plan/trace/benchmark supports it. Do not invent plans, timings, row counts, or test results.
4. **Do not rewrite an existing abstraction by default.** Reuse established repository/query patterns and database capabilities unless evidence justifies divergence.
5. **Watch cardinality.** Joins can multiply rows; eager loads can explode result sets; LIMIT without deterministic ordering can produce unstable pages; batching can change ordering and errors.
6. **Safety first.** Use parameterized queries and least-privilege access. Do not remove access-control filters or log secrets/PII to make a query faster. Never execute destructive DDL, broad data updates, or production migrations without authorization and a rollback plan.
7. **Discover dialect semantics.** Syntax, execution plans, index behavior, isolation levels, NULL ordering, collations, date operations, and JSON features vary. Mark unfamiliar behavior as unknown until verified.
8. **Risk-based effort.** A single-line query change may alter business meaning or expose private data. Escalate analysis based on impact and uncertainty, not line count.
9. **No invented inspection.** If repository, DB, profiler, or tests are unavailable, say what was not inspected and provide conditional guidance instead of pretending to have verified the project.
10. **Company-independent.** All public examples and evaluation fixtures must use fictional generic entities; never publish proprietary code, schemas, data, or credentials.

## Modes

- **Learn:** Explain a query concept through a small example, show when it helps and when it hurts, then give a practice question. Keep database-/language-specific behavior clearly labeled.
- **Apply:** Investigate a concrete project issue or requested change, implement the *smallest semantics-preserving* solution, and verify. Inspect before editing.
- **Verify:** Review a query/PR/optimization against the baseline contract, explain plan and regressions, and report checks actually performed.

## Adaptive depth

- **Lightweight:** Local query with well-understood contract, stable access patterns, no migration or security impact. Inspect relevant caller/query and focused tests.
- **Standard:** N+1, filtering/projection, pagination, joins, or ORM loading. Trace generated SQL or database commands, constraints, data distributions, and regression tests; compare alternatives if needed.
- **Deep:** Schema/index migrations, high-volume hot paths, cross-tenant queries, concurrency/locking, transaction changes, read/write consistency, production performance, or uncertain scope. Establish baseline, plan rollback, assess concurrency and operational impact, and explicitly report unknowns.

## Workflow

### 1. Define the contract and symptom

Clarify the requested outcome: correct data, lower latency, fewer queries, less memory, stable paging, or safe concurrency. Record expected rows, ordering, page semantics, filters, authorized scope, supported environments, and success criteria. If the goal is unclear, avoid changing behavior speculatively.

### 2. Discover the project's data-access conventions

Use [project-discovery](references/project-discovery.md). Inspect relevant schema and migrations, existing indexes, query definitions and callers, ORM loading/tracking settings, database compatibility, tests, and available query logs/plans. Read what is relevant; avoid blind repository-wide rewrites. Record **evidence vs assumptions**.

### 3. Trace the actual query behavior

Map `request → application filters → ORM/query builder → generated query/commands → database plan → materialization → response` where accessible. For N+1, establish queries per item rather than guessing. For slowness, distinguish DB time, network, hydration, and downstream processing. For correctness, build a small reproducible fixture.

### 4. Choose the narrowest appropriate pattern

Use [pattern decisions](references/pattern-decisions.md). Options include preserving the current query, selecting fewer columns, batching, prefetching, a filtered join, keyset pagination, an appropriate index, a transaction, or no change. Explain why rejected options are unsuitable for this project. Do not use an index or cache as a generic default.

### 5. Implement with operational safety

Respect access-control predicates, parameterization, engine semantics, existing transaction/isolation strategy, migration conventions, and backwards compatibility. For schema/index changes, assess write overhead, maintenance, lock/online build capability, deployment sequencing, and rollback. Avoid production query/DDL execution without explicit authorization.

### 6. Verify both semantics and performance

Follow [verification matrix](references/verification-matrix.md). Test rows, duplicates, boundaries, authorization filters, empty data, null semantics, stable ordering, concurrency where applicable, and query counts/plans/latency where measurable. Compare representative workloads, not isolated tiny fixtures. Explain observed data and limitations. Never call a refactor faster based on aesthetics alone.

### 7. Report concisely

```text
Scope: <component/query and environment>
Contract: <filters, ordering, access scope, result semantics>
Evidence: <files, generated SQL, plan, metrics, tests or unavailable>
Finding: <specific issue; observed vs suspected>
Options: <simple alternatives and trade-offs, if needed>
Decision: <minimal compatible action or no change>
Changes: <what was modified; migration/rollback if applicable>
Verification: <actual checks and results; unverified aspects>
```

## Quick anti-pattern checks

- Query inside loop / per-record lazy loading → investigate N+1 before prescribing join or eager loading.
- Materialize early then filter/sort in application → verify whether server-side operations preserve semantics and are supported by provider.
- `SELECT *` or entity hydration when only a few fields are required → consider projection, including needed identity/tracking behavior.
- Offset pagination with non-unique order → add deterministic tie-breaker; for large pages consider keyset with explicit trade-offs.
- Broad join with one-to-many → inspect duplicated parent rows and aggregate correctness.
- Index suggestions without predicates, cardinality or explain plan → treat as hypothesis; assess maintenance and write costs.
- ORM tracking on read-only queries → consider no-tracking only when identity/change-tracking semantics permit.
- Blind retries around writes or transactions → analyze duplicate effects, idempotency and isolation separately.

## Supporting material

- [Project discovery](references/project-discovery.md)
- [Pattern decision guide](references/pattern-decisions.md)
- [Engine and ORM portability](references/portability.md)
- [Verification matrix](references/verification-matrix.md)
- [SQL examples](examples/sql.md)
- [ORM examples](examples/orm.md)
- [Evaluation cases](evals/cases.json)
- [Evaluation rubric](evals/rubric.md)
