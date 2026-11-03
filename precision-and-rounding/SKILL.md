---
name: precision-and-rounding
description: >-
  Inspect, preserve, and safely modify an existing project's numeric precision,
  rounding, and calculation conventions. Use for decimal or floating-point bugs,
  quantity/rate/percentage calculations, serialization or database precision,
  rounding-mode changes, cross-service numeric mismatches, and numerical refactors.
  Discover the project's established policy before choosing types or rounding modes.
---

# Precision and Rounding — Project-First

## Purpose

Prevent accidental numeric behavior changes. The project's **verified existing contract** takes precedence over generic preferences. This skill does not prescribe Half-Up, Half-Even, 2 decimal places, `decimal`, or any global rounding mode by default.

Use with a general debugging or testing workflow; this skill is the numerical decision specialist, not a replacement for root-cause analysis or test execution.

## Non-negotiable rules

1. **Discover before modifying.** Inspect the affected calculation end-to-end, not just the line that rounds a value. See [project-discovery.md](references/project-discovery.md).
2. **Separate facts from guesses.** Cite file paths, code references, configuration and observed tests for every claim about project behavior. Search results are leads, not proof of runtime behavior.
3. **Never silently change policy.** No implicit switch from Half-Even to Half-Up, no automatic conversion to fixed 2dp, no change to when rounding occurs, and no broad numeric-type migration.
4. **Preserve behavior by default.** For bugs and improvements, change only what is required. If requested behavior conflicts with existing behavior, explicitly identify the conflict and its affected scope.
5. **Do not infer an intentional policy from one incidental call.** Check callers, overrides, framework defaults, docs and executable tests; multiple policies may coexist by field, operation, tenant, currency, or version.
6. **Missing decision-critical evidence means stop the policy change.** State the unknown and ask for the smallest needed clarification; you may still document findings or add characterization tests that do not alter production behavior.
7. **No invented verification.** Never claim tests passed, values were inspected, or business rules were confirmed unless actually observed.
8. **No project disclosures.** Never copy sensitive values or proprietary implementation into a public skill artifact. Use generic examples.

## Mode selection

- **Learn** — user asks about a numeric concept: explain precise semantics, assumptions, a worked example and common counterexample. Do not pretend the example represents their project.
- **Audit** — user asks why results differ or requests an assessment: trace code/config/storage/outputs; report observed policy and unknowns; don't edit.
- **Apply** — user requests implementation or fix: perform discovery, scope the change, implement minimally, verify.
- **Verify** — user asks to check an existing change: compare old/new contracts, evaluate boundary tests and report measured evidence.

## Adaptive effort

- **Lightweight:** isolated formatting/display issue with verified rounding helper and no persisted or externally observed effects. Inspect helper and callers, patch narrowly, run focused tests.
- **Standard:** numeric bug in one calculation chain or API field. Trace input → transformations → rounding → output, locate configured policy, characterize current behavior, verify relevant boundaries.
- **Deep:** persistent values, external contracts, aggregates, distributed computations, precision migrations, cross-language discrepancies, or anything with uncertain impact. Build a policy map and impact assessment before proposing changes.

Small diffs can still be high-risk; choose effort by impact and uncertainty.

## Workflow

### 1. Establish the target and scope

Identify the exact field, value type, calculation stage, caller, expected result, and whether the user requests **preservation**, **bug correction**, or an **intentional policy change**. Identify impacted deployments/versions if relevant.

### 2. Discover the existing policy

Follow [project-discovery.md](references/project-discovery.md). Read relevant code and tests, then trace:

`source/input → parse → numeric representation → math → quantize/round → aggregate → storage → serialize → UI/report`

For each rounding boundary record: *operation, value scale, numeric type, mode, midpoint behavior, sign handling, configuration origin, and evidence*. Distinguish intermediate and final rounding, plus display-only formatting. Do not assume all stages share one policy.

### 3. Resolve authority and conflicts

Prefer explicit user-accepted requirements / domain contracts, then authoritative project specs and versioned settings, then tests asserting intended behavior, then implementation and observed runtime. This is an **investigation order**, not a license to override a currently deployed API or persisted contract. When sources conflict, show the conflict and seek a decision before changing semantics.

If policy is unclear, default to **no production behavior change** rather than inventing a rule. When the environment is inaccessible, state inspection limits plainly.

### 4. Diagnose the numerical failure

Consider binary floating-point representation, scale and type limits, intermediate rounding, premature formatting, sign symmetry, midpoint tie behavior, locale, JSON/DB conversions, integer overflow, cancellation, sum-before/after-rounding, and cross-service differences. Use [numeric-failure-patterns.md](references/numeric-failure-patterns.md).

### 5. Choose the smallest compatible change

Prefer the existing helper/configuration and established dependency boundaries. Explicitly avoid scattered calls to rounding functions, duplicating a utility, widening data types across the project, or introducing a new rounding strategy without authorization.

For an intentional policy change, prepare a compatibility and migration plan (stored data, APIs, caches, client code, historic calculations, feature flags if applicable). See [policy-decisions.md](references/policy-decisions.md).

### 6. Verify with evidence

Use [verification-matrix.md](references/verification-matrix.md). Characterize baseline behavior, test requested change, and run relevant regression/integration tests where possible. Compare exact numbers and formatting, not just approximate equality when exactness is required. Do not regenerate baselines to hide regressions.

### 7. Report the outcome

Use this concise output format (omit irrelevant fields for a trivial change):

```text
Scope: <component / operation>
Existing policy: <mode, scale, stage, type or UNKNOWN>
Evidence: <paths/config/tests/runtime; or inspection limitation>
Problem: <actual numerical mismatch and reproduction>
Decision: <preserve / minimal correction / authorized change / blocked>
Changes: <what changed, what did not>
Compatibility: <affected consumers, storage, historical behavior>
Verification: <commands & observed results; untested paths>
Open questions: <only decision-critical unknowns>
```

## Important distinctions

- **Precision** (available meaningful digits), **scale** (digits after decimal), **rounding** (how discarded digits are chosen), and **formatting** (how values are presented) are different concerns.
- **Truncation** is not automatically Round Down. For negative values, toward-zero and toward-negative-infinity differ.
- “Round Up/Down” are ambiguous business labels; translate them into precise operations and test positive **and negative** values.
- **Half-Up**, **Half-Away-From-Zero**, **Half-Even** and language defaults are not interchangeable, especially for negative midpoints.
- Floating-point numbers should not be judged by their printed decimal alone. Check representation and language/runtime semantics.
- Display rounding must not silently rewrite stored or intermediate values.

## Supporting material

- [Project discovery](references/project-discovery.md)
- [Policy decisions and compatibility](references/policy-decisions.md)
- [Numeric failure patterns](references/numeric-failure-patterns.md)
- [Verification matrix](references/verification-matrix.md)
- [Language examples](examples/language-notes.md)
- [Evaluation cases](evals/cases.json)
