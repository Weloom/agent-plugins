## Express inputs and alternatives with types

**Use when:** callers rely on casts, flags, or implicit conventions to construct inputs or interpret alternatives.
**Gain:** types and explicit cases reveal legal choices and let the compiler catch misuse. Define the outcome here; use the optional/fallible section when several operations must propagate that outcome.

- **Use generics to preserve relationships.** Express the input/output relationship with type parameters instead of `object`, `dynamic`, or casts. Add constraints for capabilities actually required; do not introduce generic parameters that provide no useful variation.
- **Preserve meaningful distinctions.** Use named types for units, constraints, or outcomes when confusion is plausible. Use ordinary values or small named tuples when their local meaning is clear; do not introduce a wrapper for every expression.
- **Represent distinct alternatives explicitly.** Replace combinations of Boolean mode flags or optional fields with meaningful alternatives when they describe different cases. Use the project's established types or a small deliberate representation; do not build a universal union framework.
- **Use pattern matching for decisions.** Prefer a switch expression or a clear pattern when it exposes a mapping from cases to results more directly than mutable assignment and nested branching. Use a switch statement or ordinary conditionals when executing actions or sequencing is clearer.
- **Handle the full input domain.** Include legitimate missing and unexpected cases; avoid a catch-all arm that silently treats an unknown value as success. A C# class hierarchy or enum should not be assumed closed merely because current cases are known.
- **Keep expressions legible.** Avoid nested ternaries, intricate patterns, or expression-bodied members that hide the main alternatives. Extract a named predicate only when the name communicates the condition better.
- **Use nullability accurately.** Nullable reference annotations describe contracts and enable analysis; they do not enforce runtime validity. `T?` is not a universal substitute for explicit outcome types, especially when absence and failure have different meanings.
