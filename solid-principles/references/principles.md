# SOLID — working knowledge, not slogans

## SRP: Single Responsibility Principle
Question: *Which distinct policy owners could require this module to change?* A CSV parser and notification sender often change for different reasons, but extracting a two-line private helper does not automatically improve SRP. Cohesion matters more than method count.

## OCP: Open/Closed Principle
Question: *Which variability exists today and is costly to add?* A policy interface can help when more than one calculation policy is already needed. A three-level hierarchy anticipating theoretical future countries is usually speculative. A switch may be best for a closed, stable set.

## LSP: Liskov Substitution Principle
Question: *Can every documented caller use the subtype without surprising behavior?* Consider accepted inputs (preconditions), guarantees (postconditions), errors, and side effects. An exception thrown for an input permitted by the base contract is a red flag. Not every override is a violation.

## ISP: Interface Segregation Principle
Question: *Does a client depend on methods it never uses or cannot meaningfully implement?* Splitting unrelated readers/writers can improve independent consumers. Do not fragment a cohesive contract into dozens of single-method interfaces.

## DIP: Dependency Inversion Principle
Question: *Is business policy coupled to a volatile detail or external resource?* A narrow gateway at the boundary may help. Constructor injection is not intrinsically DIP; depending on a giant leaky interface may still couple policy to details. Internal pure helpers generally do not need an interface.

## Useful distinctions
- SOLID is about design trade-offs, not syntax rules.
- Testing difficulty can be a clue, not proof.
- Ask whether the proposed abstraction has at least one real consumer or meaningful boundary.
- Prefer composition when inheritance would impose weak subtype contracts.
- Prefer preserving behavior over a theoretically 'cleaner' class graph.
- Explain why a proposed design will be easier to change, and which change scenario demonstrates that claim.
