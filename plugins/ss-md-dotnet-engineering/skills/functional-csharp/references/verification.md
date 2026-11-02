## Verify behavior and expressive clarity

**Use when:** accepting an implementation or recommending a functional refactoring.
**Gain:** evidence-based acceptance distinguishes clearer code from stylistic rewrites and catches changes to effects, outcomes, or evaluation timing. Apply only the checks relevant to the changed behavior.

- **Identify the improvement.** Connect the observed problem to the chosen approach and its benefit: fewer hidden inputs, less shared state, clearer alternatives, or simpler composition. Do not report the absence of a lambda, record, or monad as a defect.
- **Check the reading of the caller.** A reader should identify the intended rule, necessary inputs, possible results, and significant effects without tracing low-level execution. Fewer lines or expression syntax alone do not satisfy this criterion.
- **Test observable behavior.** Verify successful, absent, rejected, and exceptional outcomes where applicable, plus invariants and required ordering. Check that calculations leave inputs unchanged and effectful stages execute the intended number of times.
- **Test deferred and captured behavior when affected.** Include repeated or partial enumeration, changed captured inputs, resource disposal, cancellation, and delayed exceptions as relevant. Do not require unrelated tests for unaffected techniques.
- **Preserve relevant cost characteristics.** Consider extra enumeration, allocations, copying, delegate retention, stack depth, and deferred work. Measure meaningful hot-path trade-offs instead of assuming that functional style is inherently faster or slower.
- **Keep necessary imperative code.** Retain direct loops, mutation of private working state, and explicit resource orchestration where they express the actual responsibility more clearly. Isolate that implementation behind a useful contract rather than disguising it.
- **Keep the scope proportionate.** Reuse established types and helpers. Prefer one focused function or value over a new framework, dependency, DSL, or broad rewrite. Make intentional changes to contracts or behavior explicit and verify them separately.
