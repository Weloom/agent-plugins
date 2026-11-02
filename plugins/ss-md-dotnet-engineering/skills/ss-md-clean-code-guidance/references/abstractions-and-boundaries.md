## Abstractions, data, and boundaries

Abstractions are valuable when they hide meaningful complexity or isolate change; unnecessary ones make code harder to follow.

- Hide implementation details behind a stable, useful interface when doing so reduces coupling or makes callers simpler.
- Choose objects, data structures, and functions based on the behavior and invariants they need to represent.
  - Encapsulate state when doing so protects invariants or prevents callers from coordinating internal steps.
  - Keep simple data-transfer types simple when they do not own meaningful behavior.
- Avoid long chains of navigation through another component's internals. Prefer an operation or interface that expresses what the caller needs.
- Keep external and third-party APIs at clear boundaries. Translate external details when allowing them to spread would couple unrelated code to those APIs.
- For unfamiliar or risky dependencies, use a focused experiment or test to establish behavior before building substantial logic around assumptions.
- Add an abstraction when it clarifies the domain, isolates likely change, or removes meaningful duplication. Avoid speculative abstractions based only on possible future reuse.
