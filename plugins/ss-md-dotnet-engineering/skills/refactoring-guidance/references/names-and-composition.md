## Names and method composition

Use these techniques when a reader must reconstruct intent from implementation details. The test is whether the surrounding code becomes understandable without repeatedly opening helpers.

### Names and method boundaries

- Name an operation for its intention or result, using established domain vocabulary. A useful name lets the caller reason about the operation without reading its implementation; `processData` merely conceals that implementation.
- **Extract Method** when a coherent fragment has a useful intention-revealing name.
  - Extraction can help even for one use or one line. Reuse is not a prerequisite.
  - Prefer a higher-level flow expressed in meaningful steps over a mixture of orchestration and low-level details.
  - If the helper needs many unrelated caller locals or several unrelated outputs, first separate the calculations or choose a smaller cohesive fragment. A vague name plus a large parameter list relocates complexity rather than explaining it.
- **Inline Method** when a helper's body is as clear as its name and the call adds no useful boundary. Inlining can also be a temporary step before extracting better boundaries.
  - Do not inline across overrides, recursion, or a meaningful extension point without examining those effects.
  - Extraction and inlining are alternatives chosen by clarity, not rules to maximize or minimize method count.
- Before extraction, identify inputs, outputs, writes, and early exits. Keep evaluation order and state changes intact; return a changed local value when needed.
  - First split tangled calculations or separate unrelated locals if that permits a simple extraction.
  - Consider a method object only when coupled local state still prevents useful decomposition. Keep its calculation state local to one invocation; moving locals into a shared service's fields introduces reentrancy and concurrency hazards.

### Expressions and local state

- Introduce an explaining variable to name a subexpression within one calculation. Prefer a named query for reusable domain knowledge or to enable extraction.
- Inline a temporary or replace it with a query when it adds no meaning or obstructs useful extraction.
- Preserve evaluation count and order for clock reads, I/O, and side-effecting calls. Measure the cost before replacing one expensive calculation with repeated queries.
- Keep a local snapshot when later state changes must not affect its value; a query of current state is not equivalent.
- Split variables reused for unrelated meanings; retain loop counters and accumulators with one continuing role.
- Use a separate local for a transformed input rather than reassigning the parameter.
- Preserve intentional object mutation and `ref`/`out` semantics; these differ from reassigning a by-value parameter.
