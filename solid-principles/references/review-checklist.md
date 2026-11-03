# Practical code review checklist

## Evidence first
- Identify relevant source paths, callers, current tests, registration/configuration and intended behavior.
- For each finding, provide file/line locations when available and quote only a minimal snippet.
- Label unknowns; never invent requirements or benchmark improvements.

## Per-principle prompts
| Principle | Investigate | Counterexample / no change |
|---|---|---|
| SRP | Independent policies mixed and frequently edited together? | Cohesive methods serving one business policy |
| OCP | Frequent new variants require changing stable code in risky places? | Small, closed branch set |
| LSP | Subtype rejects valid base input or weakens guarantees? | Honest inheritance with preserved contract |
| ISP | Consumers/implementers depend on unrelated unused members? | Cohesive interface shared by all clients |
| DIP | Domain rule hardcodes volatile IO/provider behavior? | Pure helper or stable concrete dependency |

## Severity
- **High**: Demonstrated correctness/contract breach or change likely to cause serious regression.
- **Medium**: Concrete repeated coupling/change-cost with feasible focused fix.
- **Low**: Readability or future optional improvement; generally do not block.
- **None**: No actionable issue; explicitly say so.
Do not rate style preference as high severity.

## Refactor choice
1. Could **no change** be the right answer?
2. Can a local method/function extraction or parameter suffice?
3. Is an interface/strategy necessary for observed variants or test boundaries?
4. Will change break DI, serialized shapes, public API, persistence, or callers?
5. Does new complexity exceed the cost of the current design?
