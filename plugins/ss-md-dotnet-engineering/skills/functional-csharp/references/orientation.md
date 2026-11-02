# Functional and Declarative C# Guidelines

Use for C# code review, implementation, refactoring, and cleanup when calculations, decisions, or transformations are obscured by control flow, mutable state, or technical details.

Also use when extending code whose established contracts rely on pure calculations, non-mutating inputs, immutable results, explicit outcomes, or separated effects. Preserve those properties without requiring a comment that labels the code "functional." Explicit requests are another entry point, not the only one.

Prefer functional and declarative solutions that make the intended result easier to understand. This is a positive preference, not merely permission to use lambdas: when two solutions preserve behavior and relevant performance, favor the one that exposes the rule, inputs, and result with less execution detail.

## Orientation and navigation

- **Functional code** emphasizes functions that transform inputs into results, composition, and limited shared mutation. C# supports this alongside object-oriented design.
- **Declarative code** states a rule, relationship, or desired result without making callers manage the procedure that produces it. It need not use a special language or framework.
- A **pure calculation** depends only on its explicit inputs and has no observable effects on callers or external state. A lambda, expression-bodied member, or static method is not automatically pure.
- Keep necessary imperative execution, resource management, and algorithms behind clear contracts. Do not hide effects or sacrifice correctness to make a call site look declarative.

**Decision priority.** Preserve required behavior, invariants, error handling, and resource ownership first. Within those constraints, prefer explicit inputs, meaningful results, and visible effects over procedural detail. Abstraction is justified by clearer intent or simpler reuse, not by functional syntax alone.

| Observed problem or task | Relevant section |
|---|---|
| Decisions mixed with saving, messaging, time, or mutable service state | [Separate calculations from effects](./calculations-and-effects.md#separate-calculations-from-effects) |
| Mutable flags, partial results, shared objects, or misleading read-only APIs | [Represent state with immutable values](./immutable-values.md#represent-state-with-immutable-values) |
| A caller needs to supply a calculation, predicate, or action | [Represent behavior with functions and delegates](./functions-and-delegates.md#represent-behavior-with-functions-and-delegates) |
| Repeated execution structure or functions that need fixed inputs | [Compose and specialize functions](./composition.md#compose-and-specialize-functions) |
| Casts, ambiguous parameters, Boolean modes, or selection between known cases | [Express inputs and alternatives with types](./types-and-alternatives.md#express-inputs-and-alternatives-with-types) |
| Repeated absence/error checks or nested wrapped results | [Compose optional and fallible operations](./optional-and-fallible.md#compose-optional-and-fallible-operations) |
| Incremental output, expensive initialization, or repeated enumeration | [Control lazy sequences and deferred evaluation](./lazy-evaluation.md#control-lazy-sequences-and-deferred-evaluation) |
| Reviewing whether a functional rewrite improves the code | [Verify behavior and expressive clarity](./verification.md#verify-behavior-and-expressive-clarity) |

Use the affected sections, not every technique. Follow the project's C# version, existing abstractions, and error conventions. LINQ operators and query syntax are outside this guide's scope; recursion, expression trees, and general-purpose memoization frameworks are not required.

**No new functional dependencies.** Apply these guidelines using C# language features, the standard .NET APIs available to the project, and existing project abstractions. Do not add or install packages to introduce functional patterns or syntax. Reuse an existing functional library where established by the project, but do not build a replacement framework when a direct implementation suffices.
