## Compose and specialize functions

**Use when:** operations repeat a meaningful sequence or become simpler with stable inputs supplied once.
**Gain:** named stages expose the calculation's flow, while specialization removes repeated setup from callers. The delegates section chooses how to represent one behavior; this section assembles behaviors without obscuring their order.

- **Separate stable flow from variable behavior.** Accept a focused function when a repeated operation differs only in a genuine policy or transformation. Keep domain-relevant differences visible; do not generalize unrelated procedures because their control flow looks similar.
- **Prefer direct composition first.** Named intermediate results and ordinary function calls often communicate stages more clearly than a custom `Compose` or `Pipe` abstraction. Use existing composition helpers when they improve the reading of the actual operation.
- **Specialize only useful inputs.** Partial application can return a function with a stable policy or value already supplied. C# has no general built-in currying syntax; a clear lambda, local function, or method is usually sufficient.
  - Capture stable values deliberately. Capturing a reference to mutable configuration does not fix its contents at function creation.
  - Do not turn a clear multi-parameter method into nested `Func` returns unless staged application has a real caller benefit.
- **Name semantic stages.** A reader should see which rule or transformation each stage performs. Do not replace meaningful names with generic chains of `Apply`, `Run`, or `Execute`.
- **Preserve effects and order.** Purity makes composition easier to reason about; it does not make functions interchangeable or permit arbitrary reordering. Preserve dependencies, exceptions, and evaluation order required by the contract. For effectful stages, also preserve invocation count and external sequencing; use explicit orchestration when those are the main responsibility.
- **Keep policy distinct from its solver.** Let domain-facing code specify constraints and desired results while focused code performs traversal, search, or optimization. A renamed procedural helper is insufficient if callers still manage the solving steps.
