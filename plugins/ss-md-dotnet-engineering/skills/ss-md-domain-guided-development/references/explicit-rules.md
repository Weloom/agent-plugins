## Make important concepts and rules explicit

Use these guidelines when concepts are understood but the code makes their rules or effects hard to reason about.

- **Explicit concepts:** represent a meaningful rule, policy, or constraint directly when that removes scattered interpretation. Use a specification for a reusable domain predicate when useful; do not wrap every conditional in a class.
- **Intention-revealing interfaces:** expose domain intent and significant effects so callers need not reconstruct the algorithm.
- **Predictable effects:** prefer side-effect-free calculations and make mutation explicit. State relevant preconditions, postconditions, and invariants; enforce rules in code and verify them with tests.
- **Conceptual contours:** split and combine responsibilities along coherent domain distinctions and observed reasons for change, not uniform class sizes. If a change requires repeated exceptions to an existing abstraction, reconsider that abstraction rather than adding more flags or special cases.
- **Minimal dependencies:** keep independently meaningful calculations or values independent; do not reduce meaningful types to primitives just to remove references.
- **Composition:** where meaningful, use operations closed over a value type, such as combining specifications into another specification.
  - Let callers state rules or desired outcomes while focused mechanisms perform the computation.
  - Prefer ordinary composable APIs over a DSL or rule engine unless its additional complexity solves a demonstrated problem.
