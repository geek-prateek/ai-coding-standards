# Verification matrix

Choose relevant checks according to risk; do not claim every row was executed.

| Dimension | Test cases / evidence |
| --- | --- |
| Filters | Matching, nonmatching, compound, empty list, boundary dates |
| Access control | Cross-user / cross-tenant records not returned or modified |
| Nulls and collations | Nullable fields, null ordering, case/collation behavior, Unicode |
| Relationship cardinality | Zero, one, many children; duplicates; deleted/orphaned references |
| Aggregates | Counts/totals match baseline including join fan-out and null data |
| Pagination | Stable unique ordering, ties, empty page, large offset, concurrent change |
| Write consistency | Conflicting updates, unique constraint, rollback, partial failures |
| Queries executed | ORM command count before/after using representative dataset |
| Performance | Representative plan, row reads, DB time, end-to-end latency, memory |
| Index change | Query plan impact, writes, disk, locks, rollout and rollback |
| Compatibility | API shape, error behavior, order and old clients unchanged |

## Controlled comparison

1. Capture baseline query and result fixture (including authorization scopes).
2. Record explain/plan only in an authorized safe environment. Note engine, version, statistics and parameter values.
3. Make one justified change at a time when feasible.
4. Run semantic regression tests first. Performance without correctness is failure.
5. Compare query count, work performed, representative latency distribution and resource usage, not a one-off wall-clock result.
6. Record confounders: warm vs cold cache, network, data volume, plan cache, locks and workload concurrency.
7. Roll back if correctness or isolation regresses, even if some benchmark improves.

## Reporting example

```text
Correctness: 17 focused tests passed (observed)
Authorization: cross-account fixture passed (observed)
Query count: 51 -> 2 at 50 results (observed, dev dataset)
Plan/latency: not measured; no speedup claim
Risk: very large ID batches may require provider-specific chunking
```

Do not write numbers like these as results unless you actually measured them; they are an illustrative report format.
