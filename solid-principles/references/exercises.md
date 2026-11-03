# Guided exercises — generic software scenarios

For each scenario, diagnose the issue (or say "no actionable violation"), explain its consequences, propose the smallest justified improvement, and identify verification. Do not refactor simply to check off a principle.

1. **SRP (beginner):** `DocumentImportService` both parses document contents and sends notification emails. Parsing rules and notification templates change independently. What should be separated, and what coordination remains?
2. **OCP (intermediate):** A text exporter supports two fixed formats with a short switch, and no new formats are planned. Is a strategy hierarchy warranted? Why or why not?
3. **LSP (intermediate):** `INameFormatter.Format(string? value)` promises null is accepted, but one implementation throws on null. What is broken and what contract tests should run?
4. **ISP (intermediate):** A read-only article screen depends on an interface requiring create, update and delete operations. What contract should the screen use?
5. **DIP (intermediate):** A domain validation service reads records directly from a database library. Where might a narrow boundary help? What abstractions would be excessive?
6. **Mixed (advanced):** A 600-line text-processing class is cohesive, stable, well-tested and owned by one policy. A reviewer requests five interfaces purely because of its size. Is there sufficient evidence to change it?

## Expected reasoning (not exact answers)
1. Separate independently changing parsing and notification policies while preserving orchestration and observable behavior.
2. Likely no change; OCP does not require speculative extension points.
3. Behavioral LSP breach; test null, empty and ordinary strings for every implementation according to the declared promise.
4. Depend on focused read operations; split only when consumers justify it.
5. Consider a narrow data-access port when the external dependency creates a real coupling or testability problem; avoid interfaces for every helper.
6. No; require demonstrated maintenance costs, separate reasons to change, or broken contracts.

## Self-check scoring (0–2 each)
- Correctly identifies a demonstrated problem (or lack of one).
- Describes concrete impact, not only a slogan.
- Proposes a proportionate change and its trade-offs.
- Describes tests and compatibility risks.

Total: 0–8 points per exercise.
