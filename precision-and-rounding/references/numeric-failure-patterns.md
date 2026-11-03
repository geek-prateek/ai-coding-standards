# Numeric failure patterns to investigate

| Symptom | Check | Avoid |
| --- | --- | --- |
| `0.1 + 0.2` surprising output | Binary floating-point representation | Treating printed decimal as exact binary input |
| One-cent/one-unit discrepancies | Rounding boundary (per-line vs after sum), tie policy | Adding arbitrary epsilon |
| Negative midpoint differs | Toward-zero vs floor; Half-Up vs Half-Away-From-Zero | Assuming labels uniquely define a mode |
| Values differ across runtimes | Numeric type, default rounding mode, conversion, language version | Applying one language's defaults to another |
| Value changes after JSON | Numeric encoding, JavaScript number limits, string-to-number conversion | Changing server algorithm without tracing transport |
| Database silently changes scale | Column precision/scale, implicit conversion, ORM mapping | Altering DB schema without migration impact analysis |
| Totals mismatch line items | Sum before/after quantizing, intermediate precision | Forcing sum of rounded lines to match rounded raw total without a rule |
| Locale-dependent values | Decimal separator, grouping, parsing culture | Parsing UI-formatted strings as raw numbers |
| Unexpected overflow | Range, checked operations, precision cap | Replacing with floating point without correctness tests |
| Different paths produce different values | Missing helper call, duplicated rounding, config override | Introducing one blanket rounding rule |

## Worked examples (illustrative, not defaults)

- Round-to-2dp Half-Even on **exact decimal** values: `1.245 → 1.24`, `1.255 → 1.26`.
- Round-to-2dp Half-Away-From-Zero on exact values: `1.245 → 1.25`, `-1.245 → -1.25`.
- Directed modes differ for negative numbers: truncate-to-2dp `-1.239 → -1.23`; floor-to-2dp `-1.239 → -1.24`.
- Rounding at different boundaries: individually rounding `0.005 + 0.005` to 2dp (with Half-Away-From-Zero) yields `0.01 + 0.01 = 0.02`; summing exact values first and rounding once yields `0.01`.

Tie examples assume the underlying values are represented **exactly**. Binary `float`/`double` calculations may not behave as the decimal notation suggests.

## Domain-specific caveat

Money often motivates decimal/fixed-point, but this is not a universal mandate. Graphics and scientific workloads may intentionally use floating-point. Follow the domain accuracy contract and existing architecture rather than applying one global numeric type.
