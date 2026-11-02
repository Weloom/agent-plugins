## Larger refactorings and performance

### Larger refactorings

Use an incremental migration when responsibilities span many files or layers, such as separating domain rules from presentation or untangling independent inheritance dimensions. A useful end state does not justify an unverified jump to it.

1. Select one entangled responsibility, not a target folder structure. For example, isolate a business calculation currently tied to a screen's lifecycle.
2. Exercise that responsibility through its current boundary. Identify the persistence mappings, events, or external callers that cannot change in the same step.
3. Extract the rule behind a small delegation point. Keep the old entry point functioning while moving its implementation; introduce temporary scaffolding only where coexistence needs it.
4. Migrate one caller or responsibility at a time. During coexistence, maintain one authoritative write path rather than two independently mutable versions of the same state.
5. Remove transitional paths when their callers have migrated. Identify a retained path as compatibility support rather than leaving it indistinguishable from obsolete code.

- **Separate Domain from Presentation:** Move business decisions so they can be exercised without constructing UI controls. Retain rendering and UI interaction in the presentation; preserve validation triggers and event ordering while migrating.
- **Tease Apart Inheritance:** If subclasses combine independent dimensions, such as output format and regional rules, extract one dimension into a collaborating object instead of adding subclasses for every combination.
- **Extract Hierarchy:** For a class whose flags select distinct kinds of behavior, extract one coherent kind at a time. If the selection changes during an instance's lifetime, prefer a replaceable state/strategy component over an instance subclass.
- Keep each completed slice useful on its own. A partial separation can remove a real dependency even when the remaining migration spans later tasks.

### Performance

Use measurement to decide whether performance concerns should alter a clarity-focused refactor.

- Do not reject small methods or useful objects solely because of assumed call or allocation overhead. Runtime inlining and allocation behavior depend on the language and execution environment; inspect the actual hot path before trading clarity for presumed savings.
- For a known hot path or explicit resource budget:
  1. Measure the affected operation using representative input sizes, runtime configuration, and concurrency where relevant.
  2. Profile to locate the cost rather than optimizing the most complicated-looking code.
  3. Change the measured bottleneck, rerun behavioral checks, and remeasure under comparable conditions.
  4. Remove a speculative optimization that brings no meaningful improvement. Stop tuning when the required budget is met.
- Include allocations, I/O, or query counts when those are the mechanism at risk. Extracting a helper that reruns a database query inside a loop can matter far more than the helper call overhead.
- Preserve an existing optimization's documented constraint and benchmark when improving its structure. A local microbenchmark does not establish an end-to-end latency improvement, and ordinary profiling is not sufficient evidence for a hard real-time deadline.
