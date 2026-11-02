## 6. Method Design and Stepwise Refinement

**Goal:** short methods with small, meaningful inputs, read from intent down to implementation. Optimize for understanding, not the smallest line or parameter count.

### A. Keep parameter lists small

- **SHOULD** pass only the inputs the operation needs. Prefer a few meaningful parameters over long lists of primitives.
- **SHOULD** group related inputs into a narrowly named, preferably immutable parameter object, such as `PlaceOrderCommand` or `ShippingRateRequest`. Keep temporary operation data local to the call/workflow; do not store it in service fields.
- **MUST NOT** use a generic argument bag, dictionary, or growing `Context` object merely to hide a long signature. Group by meaning, not convenience.
- **SHOULD** pass each submethod only the values or cohesive object it needs, not the entire request by default. Keep dependencies constructor-injected and cancellation tokens explicit.
- **SHOULD** replace flags selecting unrelated behaviors with named operations. A parameter object must not conceal a class or method with too many responsibilities.

```text
Avoid:  CalculateShipping(weight, width, height, depth, country, postalCode, ...)
Prefer: CalculateShipping(shipment, destination)
```

Use existing domain value objects when they fit. New parameter types follow the one-type-per-file rule; do not create a new type for every trivial call.

### B. Keep methods short and cohesive

- **SHOULD** give each method one coherent purpose at one level of abstraction. Extract meaningful steps when a method mixes orchestration, calculations, mapping, or I/O details.
- **SHOULD** use guard clauses and early returns to reduce nesting while preserving validation and cleanup behavior.
- **SHOULD** treat length, deep nesting, and many locals as review signals, not impose an arbitrary line-count limit.
- **MUST NOT** shorten code through compressed expressions, meaningless wrappers, or excessive fragmentation. A straightforward small method needs no decomposition.

### C. Refine intent into named steps

**Stepwise refinement / top-down design:** describe the operation first, then implement each step at progressively finer detail. The **newspaper metaphor** presents the headline before supporting detail: readers understand the purpose before inspecting the mechanics.

1. Name the operation and identify its coherent steps.
2. **SHOULD** make the top-level orchestration method primarily call intention-revealing submethods or collaborators at a comparable abstraction level.
3. Keep loops, parsing, calculations, and infrastructure mechanics in the step that owns them, not interleaved with the high-level workflow.
4. Repeat decomposition only while it improves understanding. Keep small supporting methods private; extract a class only for an independent responsibility.
5. **SHOULD** place the main operation before its private supporting methods, with details following in approximate reading/call order.

```text
PlaceOrderAsync
  -> ValidateRequest
  -> LoadOrderAsync
  -> ApplyPlacement
  -> SaveChangesAsync
```

This is a reading structure, not a requirement that every top-level statement be a method call. Guards, local assignments, branching, and explicit transaction/resource scopes may remain where they clarify control flow. **MUST** preserve exception propagation, cancellation, disposal, transaction boundaries, and side-effect ordering when extracting steps.
