---
name: solid-principles
description: >-
  Teach, assess, and pragmatically apply SOLID object-oriented design principles.
  Use for SOLID explanations, OOP practice, class/interface design reviews,
  diagnosing coupling or responsibility problems, and behavior-preserving refactoring.
  Supports learn, apply, and verify modes; do not invoke merely because code exists.
---

# SOLID Principles — Learn · Apply · Verify

## Purpose
Help a developer understand *why* a design choice matters and help a coding agent make only justified, testable changes. This skill is a design lens, not a mandate to introduce interfaces, layers, or patterns.

## Route the request
- **LEARN**: The user asks to explain, compare, practice, quiz, or understand SOLID. Start with their language and experience level. Use `references/principles.md` and the examples. Explain one principle at a time if appropriate; teach a concrete failure mode, a minimal improvement, trade-offs, and a check-for-understanding. Do not edit project files.
- **APPLY**: The user asks to implement, review, or refactor real code. Inspect relevant files, tests, callers, project conventions, and observable contracts first. Only then evaluate SOLID and propose the smallest useful change. See `references/review-checklist.md`.
- **VERIFY**: The user asks to assess a proposed design, code change, or AI-generated output. Compare before/after behavior, interfaces and consumers, meaningful tests, and unnecessary complexity. See `references/verification.md`.
- **MIXED**: Explain a concept briefly, apply it to evidence in the project, then verify. If actual code is unavailable, label examples as hypothetical and do not claim repository findings.

## Core definitions, used carefully
- **SRP — Single Responsibility**: A module should have one coherent reason to change (one actor or policy responsibility), not merely one method.
- **OCP — Open/Closed**: Stable code should permit needed variations through appropriate extension points; don't introduce abstractions for speculative variations.
- **LSP — Liskov Substitution**: A subtype must preserve the observable promises of its base contract, including preconditions, postconditions, and invariants.
- **ISP — Interface Segregation**: Clients should not be forced to depend on operations they do not need; prefer cohesive contracts.
- **DIP — Dependency Inversion**: High-level policy and lower-level details should depend on suitable abstractions when that boundary has practical value. Dependency injection is one possible technique, not the definition of DIP.

## APPLY workflow
1. **Scope**: Restate desired outcome, functional/nonfunctional constraints, code boundaries, and whether edits are authorized. Identify test/build commands from the repository; never fabricate results.
2. **Evidence**: Read relevant implementations, usage sites, tests, dependency registrations, configuration, and existing patterns. Collect file/line evidence when available.
3. **Diagnose**: Identify a concrete maintenance, correctness, testing, or extensibility cost. Separate observed facts from assumptions. A principle label alone is never proof.
4. **Decide**: Compare no change, minimal local change, and larger abstraction. Prefer no change where current design is adequate. Do not force all five principles.
5. **Implement** (only when requested): Make the smallest coherent diff, preserve public behavior and compatibility, follow project conventions, avoid unrelated cleanup.
6. **Verify**: Exercise focused tests plus relevant broader checks if available. Explicitly report commands, pass/fail/not run, remaining risks, and any contract changes.
7. **Explain**: Show the before/after design, measurable benefit, alternative rejected, and any learning takeaway.

## Decision gates — do NOT automatically refactor
- A large class, many methods, a conditional, direct construction, or absence of an interface is **not by itself** a SOLID violation.
- Do not add a strategy, factory, interface, or service for a single stable implementation without a demonstrated seam.
- Inheritance is not an LSP problem unless substitutability is broken under the actual contract.
- Duplication can be acceptable when behaviors change independently; prefer clarity over accidental coupling.
- Maintain security, performance, data correctness, thread safety, public API and persistence compatibility.
- Respect existing architecture; avoid silently converting the entire project to a different style.
- When in doubt, present the trade-off and ask before broad or breaking changes; if a small safe task is possible, do that first.

## Expected output
**LEARN**: Principle → problem → real example → minimal improvement → when *not* to use → 1–2 exercises/quiz questions.

**APPLY/VERIFY**: 
1. **Finding** (principle, severity, precise evidence; or “no actionable issue found”).
2. **Why it matters** (real impact, not slogans).
3. **Minimal solution** and trade-offs (including no-change alternative).
4. **Change summary** (if modified) and **behavior/contract compatibility**.
5. **Verification** (commands/results, gaps and risks).

## References
- `references/principles.md` — nuances, diagnostic questions and common misconceptions.
- `references/review-checklist.md` — review and severity rules.
- `references/verification.md` — behavior-preserving verification protocol.
- `examples/csharp.md` — C# examples (SRP, OCP, LSP, ISP, DIP).
- `examples/typescript.md` — TypeScript examples (SRP, OCP, LSP, ISP, DIP).
- `references/exercises.md` — guided exercises and expected reasoning.
- `evals/cases.json` — positive, negative and regression evaluation prompts.
- `evals/README.md` — repeatable manual evaluation and scoring.

## Coexistence
Use with Superpowers for workflow and tests, Ponytail for simplicity, and existing repository governance skills for evidence/lessons. Never override explicit project requirements or stronger security/correctness constraints.
