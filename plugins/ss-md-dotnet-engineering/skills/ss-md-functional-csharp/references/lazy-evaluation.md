## Control lazy sequences and deferred evaluation

**Use when:** output can be consumed incrementally or expensive work may never be needed.
**Gain:** callers can request results without managing production steps, and avoid unnecessary computation or full buffering. Choose laziness only when its timing and lifetime contract is suitable; deferred execution is not inherently clearer than an immediate result.

- **Choose the evaluation contract.**
  - Use `IEnumerable<T>` with an iterator for incremental synchronous production.
  - Use `Func<T>` to describe a callable computation; each invocation may recompute it.
  - Use `Lazy<T>` for on-demand initialization with a retained value, accounting for its configured concurrency and exception behavior.
  - Return a materialized collection when callers need fixed membership or repeated access without recomputation. Materialization alone does not freeze mutable elements; use the ownership rules in the immutable-values section when their state must also be stable.
- **Use `yield return` for natural incremental output.** A clear loop inside an iterator can be the best implementation. Consumers should receive meaningful elements without having to manage a producer's internal state.
- **Account for deferred execution.** Iterator bodies execute as enumeration advances, not when the iterator method is called. Validation inside the body is also deferred; use a non-iterator entry method delegating to an iterator when immediate validation is required.
- **Do not imply replay safety.** `IEnumerable<T>` does not guarantee cheap or repeatable enumeration. Re-enumeration may repeat I/O, observe different data, or fail. Avoid multiple passes without establishing that they are safe.
- **Control lifetime and ownership.** Do not return an iterator over a resource already disposed by the producing method. Arrange resource ownership so it remains valid during enumeration and is released on completion, early exit, or failure; disposal depends on correct consumer enumeration.
- **Inspect captured state and effects.** Deferred work may observe values after they change, and consumers may stop before all effects run. Do not use enumeration as an implicit command to perform required writes or messages.
- **Define failure and consumption behavior.** Preserve ordering, duplicate handling, empty output, termination, and when exceptions occur. Never force complete consumption of a potentially unbounded sequence merely to simplify a functional rewrite.
- **Use async streams only for asynchronous production.** When supported and appropriate, `IAsyncEnumerable<T>` and `await foreach` express incremental asynchronous results. Preserve cancellation and disposal behavior rather than blocking asynchronous work inside a synchronous iterator.
