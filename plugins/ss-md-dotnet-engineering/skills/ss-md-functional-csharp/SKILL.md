---
name: ss-md-functional-csharp
description: "Apply functional and declarative C# guidance for explicit requests, preservation of established pure calculations, non-mutating inputs, immutable results or separated effects, or diagnosed problems with hidden inputs, mutable intermediate state, composition, or outcome propagation. Can be selected from Clean Code, DDD, refactoring, architecture, or performance findings. A lambda, record, or LINQ expression alone is not a trigger; do not rewrite by default."
user-invocable: true
disable-model-invocation: false
---

# Apply functional and declarative C# guidance

Activate through explicit intent, established design properties in affected code, or a concrete diagnosed need. Preserve properties more strongly than adopting new techniques. Functional and imperative code can coexist; the goal is a clear, reliable boundary, not a uniform paradigm.

## Recognize the boundary before choosing a technique

Read [orientation and priorities](./references/orientation.md) and [recognition and preservation](./references/design-properties.md). Inspect callers, tests, implementation, and authoritative project decisions. Identify the property to preserve or the actual problem to improve; a lambda, record, or static method is not proof of purity or a reason to refactor.

Do not introduce a clock read, database write, message, mutable capture, or input mutation inside a calculation relied upon as pure. Preserve explicit outcomes and their error, cancellation, and evaluation contracts. If requirements conflict with an established boundary, surface the conflict and resolve the intended contract rather than silently erode it.

## Load only the relevant technique

| Observed need | Reference |
|---|---|
| Calculation mixed with I/O, hidden inputs, or mutable service state | [Separate calculations and effects](./references/calculations-and-effects.md) |
| Partial results, mutable flags, aliases, or read-only APIs that imply too much | [Immutable values and ownership](./references/immutable-values.md) |
| A caller needs to supply a focused policy, calculation, or action | [Functions and delegates](./references/functions-and-delegates.md) |
| Meaningful repeated flow or useful stable inputs | [Composition and specialization](./references/composition.md) |
| Ambiguous inputs, Boolean modes, casts, or distinct alternatives | [Types and alternatives](./references/types-and-alternatives.md) |
| Repeated absence/failure handling obscures a dependent calculation | [Optional and fallible operations](./references/optional-and-fallible.md) |
| Incremental output, deferred execution, or captured resource lifetimes | [Lazy and deferred evaluation](./references/lazy-evaluation.md) |

Use ordinary C#, available .NET APIs, and established project abstractions. Do not add functional dependencies or invent a general framework to obtain a technique. Direct calls, explicit branching, loops, and private mutable accumulators may be the clearest implementation.

## Decide, preserve, and verify

Read [verification guidance](./references/verification.md) before accepting a change. Check the caller's clarity and the affected contracts: non-mutating inputs, effects, outcomes, capture, deferred execution, ordering, resource lifetime, and relevant costs. Do not infer purity from equal results in a few tests.

Correctness, business invariants, contracts, ownership, and operational constraints come first. Within them, preserve established design properties and prefer explicit inputs, meaningful results, and visible effects. New functional techniques need a concrete benefit, not a style preference. Test intentional behavior changes separately and do not claim a preservation check proves all possible behaviors.

## Conditional coordination

- Accept a focused finding from `ss-md-clean-code-guidance`, `ss-md-domain-guided-development`, `ss-md-refactoring-guidance`, `ss-md-dotnet-architecture`, or `ss-md-performance-review`. State the property or decision it concerns, then select only applicable references.
- Use `ss-md-domain-guided-development` if business meaning or model ownership is uncertain; `ss-md-refactoring-guidance` if a safe structural migration is needed; `ss-md-dotnet-architecture` if a responsibility/dependency boundary changes; `ss-md-performance-review` if copying, allocation, or execution choices threaten an actual workload constraint. Use `ss-md-clean-code-guidance` only for an unresolved intent/readability decision, not to approve every functional change.
- A handoff is a request for specific guidance, not delegation to another agent or permission for broader changes. Reuse skills already loaded; do not bounce back to a source skill for the same decision. If a peer is unavailable, state the limitation when material and use applicable project guidance without inventing its contents.
- Remain advisory for review or planning requests. Ask before materially expanding scope or changing a contract. Record subsystem-wide preservation constraints in existing scoped instructions or architecture decisions when warranted, not in "functional" labels on individual methods.

The bundled references are maintained with this plugin. Read only the required extracts.

Don't apply automated comments to the files you change like "This file has been changed by AI ..."
