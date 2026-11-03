# Verify mode: behavior-preserving design evaluation

## Before change
1. Capture intended behavior (inputs, outputs, errors, side effects, rounding/currency/timezone if applicable).
2. Locate tests and key callers; note unsupported/unverified assumptions.
3. Identify public API, serialization, database and dependency-injection contracts.

## After change
1. Run the narrowest relevant tests, then broader tests/build/lint where feasible.
2. Include boundary/negative/error cases and subtype contract tests when relevant.
3. Compare before/after observable behavior, not only class counts or line count.
4. Check the actual reason for change has improved.
5. Check whether abstractions, object allocations, branching and indirection increased without a benefit.

## Report format
- Scenario/contract checked
- Evidence/commands and observed result: PASS / FAIL / NOT RUN
- Any changed behavior, public contract or performance trade-off
- What was not verified and why
- Recommendation: accept / revise / revert / no change

Never claim tests pass without actually running them; distinguish illustrative examples from executable project tests.
