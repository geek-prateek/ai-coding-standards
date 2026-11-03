# Project discovery: evidence before query changes

## Discovery order (targeted, not exhaustive)

1. **Request contract:** operation, expected rows/shape, filters, scope/authorization, ordering, pagination, consistency, and backward-compatibility requirements.
2. **Stack:** database engine/version, provider/driver, ORM/query builder/version; identify read replicas and caches when they affect the path.
3. **Query path:** caller, repository/service, query expression/raw SQL, generated SQL/commands and materialization boundaries; note lazy/eager loading, tracking and relation shape.
4. **Schema:** table/collection structure, relevant keys, constraints, relationship cardinality, nullability, collations, indexes and applied migrations. Do not infer production schema from a single outdated model.
5. **Baseline evidence:** query count, request p50/p95 latency if available, plan (actual vs estimated), rows read/returned, duration, locks, memory, representative parameter values and data distributions. Never request live credentials or sensitive data in public artifacts.
6. **Tests and conventions:** existing query helpers, test fixtures, explicit API contracts, migration practices and performance test tooling.

## Evidence ledger

| Question | Evidence to record | If unknown |
| --- | --- | --- |
| Which query executes? | Generated SQL/DB command + call site | Mark unconfirmed; don't optimize guessed SQL |
| Where is time spent? | Trace/plan/profiler | Describe alternatives as hypotheses |
| What rows must be returned? | Tests/spec/caller | Avoid shape-changing optimization |
| What isolates records? | Auth/tenant filters | Do not weaken scope |
| What is the effective ordering? | Query + tests | Verify paging stability before change |
| What indexes exist? | Current schema/catalog | Do not assert missing index |
| What data distribution exists? | Aggregated counts/statistics | Note selectivity uncertainty |

## Questions that change the answer

- Does the query operate on thousands or tens of millions of rows? How skewed are filter values?
- Are consumers relying on duplicate rows, sort order, null semantics or materialization side effects?
- Is the application using repeatable reads, snapshots, optimistic concurrency, or custom retry behavior?
- Are the query and DB on different systems or are significant network round-trips involved?
- Is a query migration part of the task, or should the fix remain application-only?

If the user cannot supply a database or a profiler, explain the assumption and offer safe instrumentation or a minimal non-production reproduction; don't present an estimated plan as observed.
