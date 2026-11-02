## Compose optional and fallible operations

**Use when:** successive operations can be absent or fail, and repeated checks obscure their successful path.
**Gain:** map and bind express the dependent calculation once while consistently propagating absence or failure. This is the practical role of monadic composition here, not a requirement to add monad types to simple code.

- **Choose the outcome semantics first.**
  - Use an optional value for legitimate absence without an error.
  - Use the project's result type for an expected failure that needs an explanation.
  - Preserve exceptions and cancellation according to existing contracts; do not convert every failure into absence or an undifferentiated result.
- **Reuse the project's abstraction.** C# has no universal built-in `Option<T>`, `Maybe<T>`, or `Result<T>`. These names and the operations below describe roles, not APIs that must exist. Use direct nullable or explicit branching when sufficient; do not introduce a package solely to obtain monadic syntax.
- **Map a successful value.** A map operation transforms `T` into `U` inside an existing optional or result value, preserving absence or failure. Keep the transformation free of effects when it is presented as an ordinary calculation.
- **Bind dependent operations.** A bind operation accepts a function from `T` to another wrapped result and avoids nesting wrappers. Use it when the next operation can itself be absent or fail, not merely to replace every method call with a chain.
- **Preserve the abstraction's contract.** Mapping or binding an absent/failed value must not invoke its success function or lose its failure information. Composition should not change results merely because stages are regrouped; avoid callbacks whose hidden effects make grouping significant.
- **Choose failure behavior deliberately.** Dependent operations normally stop on the first failure. Independent validation may need all errors collected instead; do not replace error accumulation with a fail-fast chain without changing the contract explicitly.
- **Handle outcomes at a clear boundary.** Use the established match, switch, or equivalent handling to choose the next action. Do not repeatedly unwrap with exceptions, suppress nullability warnings, or substitute defaults that turn missing or invalid data into apparent success.
- **Keep asynchronous composition explicit.** For `Task`-wrapped results, await or use established async-aware helpers without blocking on `.Result` or `.Wait()`. Do not leave accidental `Task<Task<T>>` or nested result wrappers. `Task<T>` represents asynchronous completion, not purity or all domain failures.
