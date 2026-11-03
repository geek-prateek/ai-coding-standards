# Project discovery: evidence before policy

## Search sequence (adapt to the repo)

1. Locate the user-visible failing field, method, service, API endpoint, or UI component. Follow callers and downstream consumers.
2. Locate central numeric helpers, domain value objects, converters, wrappers, and application configuration. Look for mode/scale settings with field-specific or tenant-specific overrides.
3. Locate numerical behavior in tests, fixture data, snapshots, documentation, contracts and migrations.
4. Locate input parsing (culture, exponent, decimal separators), arithmetic operations, intermediate quantization, aggregations and serialization.
5. Check database column types and scale, ORM mappings, transport types, JSON serialization, and front-end formatting. Never mistake UI display precision for persistence precision.
6. If ambiguity remains, reproduce representative cases with the **actual runtime and dependency versions**; do not rely on assumptions about library defaults.

Suggested search terms (not exhaustive): `round`, `quantize`, `decimal`, `precision`, `scale`, `toFixed`, `toPrecision`, `format`, `Math.Round`, `MidpointRounding`, `setScale`, `ROUND_HALF`, `BigDecimal`, `numeric`, `decimal(,)`, `money`, `Parse`, `Double`, `Float`, `Convert`, `JSON`, `currency`, `rate`, `unit`, `total`.

Prefer repository search that excludes generated artifacts and secrets. Search findings are hypotheses until traced and verified.

## Policy inventory template

| Field/operation | Source type | Math/intermediate type | Rounding boundary | Mode & tie handling | Scale | Config/override | Storage/transport | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Example only: line total | decimal text | fixed-point decimal | after multiplying | project-defined | configurable | per module | DB numeric / JSON string | paths/tests |

**Never fill unknown cells with assumed values.** Mark `UNKNOWN` and identify what evidence would resolve them.

## Authority and precedence

Different scopes can intentionally have different rules. Map them individually: project-wide vs module vs field vs customer setting vs calculation stage vs historic version. Read the effective runtime resolution order from code, not from the property names.

Check whether a helper is invoked or bypassed, whether settings are loaded correctly, and whether UI, background job, batch processing and API use the same path.

## Cross-layer discrepancy example

If backend stores `1.005` and UI shows `1.00`, distinguish backend calculation from JavaScript formatting, serialization and floating-point representation. Do not modify backend policy until the mismatch is localized.
