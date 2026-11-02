## Represent state with immutable values

**Use when:** mutable intermediate results or shared objects make values difficult to interpret.
**Gain:** completed, stable values reduce the state readers must track and prevent one caller's changes from unexpectedly affecting another. Use the types section to choose which distinctions the values must represent.

- **Return complete results.** Replace related mutable flags, output parameters, and partially populated objects with a meaningful return value. Use a named result type when its distinctions matter; a small named tuple can suffice for a local, unambiguous result.
- **Choose value semantics deliberately.** Use records for suitable value-like results and replacement via `with` when it expresses a changed value clearly. Verify that generated equality matches the intended meaning; collection members do not automatically gain sequence-based equality. Retain identity-based objects where continuity matters; do not convert entities into records merely for convenient syntax.
- **Distinguish shallow from deep immutability.**
  - `readonly` fields prevent reassignment, not mutation of referenced objects. `init` restricts property assignment, not changes inside the property value.
  - Record `with` expressions copy references unless explicitly replaced; referenced collections or objects may remain shared.
  - `IReadOnlyList<T>` and similar interfaces restrict the exposed operations but do not guarantee an immutable backing collection or immutable elements.
- **Protect ownership.** Use an appropriate immutable collection or defensive copy when callers must not change retained state. Verify element mutability as well as collection mutability.
- **Avoid unnecessary copying.** A pure function may use a private mutable accumulator or builder if it does not mutate inputs, escape before completion, or retain shared mutable state. Publish the completed result through the intended contract.
