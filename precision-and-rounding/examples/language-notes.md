# Language examples: discover actual behavior, do not transplant a default

These are **illustrative probes**, not recommendations for project policy.

## C#

```csharp
// Decimal values are exact for these literals, but the policy is explicit.
var even = Math.Round(1.245m, 2, MidpointRounding.ToEven);       // 1.24
var away = Math.Round(1.245m, 2, MidpointRounding.AwayFromZero); // 1.25
```

`Math.Round` overloads and numeric types matter. Search for shared rounding utilities, explicit modes, legacy overloads, configuration and call sites; do not replace them indiscriminately.

## JavaScript / TypeScript

```ts
const x = 0.1 + 0.2;
console.log(x); // approximately 0.30000000000000004
const display = x.toFixed(2); // "0.30" (string, display formatting)
```

`toFixed` is not a universal arithmetic policy. Investigate whether the project already uses decimal libraries, scaled integers, or dedicated formatting. Beware loss of precision with large integer values and cross-layer JSON number conversions.

## Python

```python
from decimal import Decimal, ROUND_HALF_EVEN, ROUND_HALF_UP
x = Decimal('1.245')
print(x.quantize(Decimal('0.01'), rounding=ROUND_HALF_EVEN))  # 1.24
print(x.quantize(Decimal('0.01'), rounding=ROUND_HALF_UP))    # 1.25
```

For exact decimal inputs, construct from strings rather than accidental binary-float conversion. Inspect application `decimal` contexts and per-operation overrides.

## Java

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

var x = new BigDecimal("1.245");
System.out.println(x.setScale(2, RoundingMode.HALF_EVEN)); // 1.24
System.out.println(x.setScale(2, RoundingMode.HALF_UP));   // 1.25
```

Inspect `BigDecimal` construction, scale, `MathContext`, rounding modes, and database/JSON conversions. Avoid using binary floating-point constructors where exact decimal literals are required.

## General rule

Before choosing an implementation, identify the programming language/runtime version and how the **actual repository** handles its numeric contract. These examples deliberately demonstrate multiple policies and should never be used to assert what an unrelated application needs.
