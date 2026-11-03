# Verification matrix

## Baseline and contract

- Capture existing representative outputs *before* editing; when behavior is intended to change, record expected deltas explicitly.
- Run existing numeric/unit/integration tests and record commands, versions and outcomes.
- If no tests exist, add characterization tests with **observed** baseline behavior; do not encode guessed policies as facts.

## Case matrix (choose relevant cases)

1. Exact representable values; no rounding needed.
2. Just below, exactly at, and just above midpoint, using exact representation where possible.
3. Positive, negative, negative zero if applicable, and zero.
4. Null, absent, empty, malformed strings, NaN and Infinity when input types permit them.
5. Maximum/minimum allowed magnitudes, overflow, scale limits, scientific notation if supported.
6. Repeated additions and multiplication; intermediate vs final rounding.
7. Aggregate-before/after-rounding; individual line vs report total.
8. Multiple config scopes, overrides, feature flags and fallback resolution.
9. Parsing/locale boundaries; JSON round trips; database read/write scale.
10. Front-end display vs API/store values; backward compatibility with existing clients.
11. Historical/replay calculations and old persisted values if relevant.
12. Multiple runtimes or parallel execution paths expected to produce equivalent results.

## What counts as verification

- Exact input/output assertions for specified contract. For approximate numeric domains, use documented tolerances and error bounds, not arbitrary epsilon.
- Execute targeted unit tests and relevant integration tests where available.
- Record any unverified dependencies, unrun test suites, assumptions and environment limitations.
- Treat changed snapshots as differences requiring explanation, not automatic approval.
- For a true policy change, do **not** demand equality with old results; require scoped intentional differences and unchanged behavior outside scope.

## Fail-closed conditions

Do not ship a policy-changing patch when the decision depends on an unknown rounding mode, sign behavior, scale, calculation stage or backward-compatibility contract. Explain the unknown precisely; do not substitute a popular rounding convention.
