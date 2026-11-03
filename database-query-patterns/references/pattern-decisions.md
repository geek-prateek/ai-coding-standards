# Query pattern decision guide

Consider a change only after confirming actual constraints and query behavior.

| Symptom | Investigate | Candidate changes | Important counter-risk |
| --- | --- | --- | --- |
| N+1 reads | Query log, lazy loading, response cardinality | Batch IDs, filtered prefetch, projection, eager loading | Cartesian row explosion, extra unused data, parameter limits |
| Slow filtered lookup | Predicates, statistics, plan, selectivity | Adjust predicate, suitable index, projection | Writes/storage overhead, index not used, migration locks |
| Too much memory | Materialization, tracking, columns | Server-side filters/projections, streaming, no-tracking | Lifetime of connection, tracking/identity semantics |
| Duplicate parent rows | One-to-many join, grouping keys | EXISTS, grouping, separate query, dedupe if valid | Incorrect counts/totals and changed semantics |
| Unstable pages | Order uniqueness, concurrent inserts, offset | Stable composite order, keyset | Cursor compatibility, direction/tie-break handling |
| Incorrect totals | Join multiplicity, null handling, types | Aggregate before join, correct predicate, precision preservation | Altered aggregation semantics |
| Write race | Transaction boundaries, isolation, constraints | Unique constraint, optimistic concurrency, transaction | Deadlocks, serialization failures, throughput |
| Repeated expensive reads | Request rate, cache invalidation, freshness needs | Optimize query first; cache only if justified | Staleness, invalidation complexity, leakage |

## Ranking alternatives

1. **Correctness and data isolation** are hard gates.
2. **Compatibility**: preserve observable response, ordering, errors, isolation and transaction semantics unless change is authorized.
3. **Evidence**: use real query/plan data where accessible, not pattern popularity.
4. **Smallest sufficient change**: prefer existing project abstractions and query APIs.
5. **Operations**: assess deployment, schema migration, rollback, monitoring, read/write trade-offs.

## Non-decisions

- `JOIN` is not inherently faster or safer than multiple queries.
- An index may not help small tables, low-selectivity filters or functions that prevent efficient access.
- Keyset is not always appropriate: random page-number navigation can require offset or another approach.
- `COUNT(*)` may still be expensive; do not promise constant time.
- No-tracking may reduce overhead for read-only queries but can break callers requiring tracked entities.
- More parallel database queries may increase contention and latency rather than improve it.

## When to stop

If expected row semantics, authorization, or transactional correctness cannot be established, do not make a behavior-changing rewrite. Report the smallest missing fact and safe next measurement.
