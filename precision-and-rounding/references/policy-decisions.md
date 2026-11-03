# Policy decisions and safe changes

## Decision matrix

| Situation | Agent action |
| --- | --- |
| Existing rule proven, request is bug fix | Preserve rule; fix implementation that violates it |
| Existing rule proven, request explicitly changes it | Analyze impacts, implement scoped rule with verification and migration strategy if needed |
| Multiple rules intentionally coexist | Preserve each scope and dispatch/config resolution |
| Spec and implementation conflict | Report conflict; ask which contract is authoritative before changing behavior |
| No observable policy | Do not silently choose a mode or scale; propose options and smallest clarifying question |
| Only display is wrong | Change formatting only if storage/arithmetic is already correct |
| Numeric type is insufficient | Recommend targeted representation change and test compatibility; avoid sweeping global rewrite |

## Decision quality checklist

- Is the requested numeric behavior expressed with concrete input/output examples, including negative and tie values?
- Is it a calculated value, persisted value, transmitted value, or a formatted string?
- At which stage is rounding authorized? Rounding before vs after aggregation may produce different totals.
- Are values from previous runs replayed or recalculated? Does changing policy alter historical results?
- Do current consumers assume a specific scale, JSON representation or DB schema?
- Are alternative algorithms being compared against the **same** domain contract?
- If mode is configured dynamically, did the proposed code preserve the effective settings resolution path?

## Policy change contract

For intentional behavior changes, report:

1. Old policy and verified examples.
2. New requested policy with ties/sign/scale/rounding-stage examples.
3. Scope (fields, versions, users, operations) and fallback behavior.
4. Expected deltas and backward compatibility (API, stored data, exports, clients, caches).
5. Migration/backfill/recalculation decision and rollback path when relevant.
6. Verification and release gating.

If project policy is not known, do not generate a default policy just to complete the task.
