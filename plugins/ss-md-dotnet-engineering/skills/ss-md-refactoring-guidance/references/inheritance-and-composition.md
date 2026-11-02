## Inheritance, composition, and generalization

Use these guidelines when shared behavior is duplicated across types, inherited behavior is inappropriate, or one hierarchy mixes independent dimensions of variation.

- **Pull up** behavior or state when the subtypes share its meaning and invariants. **Push down** members that belong only to particular subtypes.
  - Compare actual behavior and initialization requirements before merging similar implementations.
  - Compare behavior through the base-type contract. A new "not supported" exception is a violation when that contract promises the operation, but not when the established contract explicitly allows optional operations.
  - Unused inherited implementation is not sufficient reason to rebuild a hierarchy. Act when it exposes inappropriate operations, constrains changes, or makes the model misleading.
- **Extract a superclass or subclass** only when it names a meaningful relationship in current code. **Collapse a hierarchy** when a level no longer contributes a useful distinction.
- **Choose inheritance or delegation by the relationship.**
  - Keep inheritance when a subtype can stand in for the base type and shared behavior genuinely belongs there.
  - Prefer delegation when the object uses a capability without being that kind of object, or when variations need independent composition.
  - Do not replace a shared mutable delegate with inheritance: turning shared state into per-instance inherited state changes which objects observe updates.
- **Form Template Method** when related types share the same algorithmic steps but vary in well-defined details.
  - First give corresponding steps compatible meanings, then pull up the common sequence while preserving the distinct step implementations. Similar-looking bodies can hide differences that need tests before unification.
  - If the supposed template needs many flags, optional hooks, or subtype checks, reconsider whether there is one algorithm.
- Before a hierarchy transformation, inspect affected constructors, overrides, dispatch, type checks, and supported extension points.
  - Preserve behavior visible through the base type, not just direct calls on concrete types.
  - Check persistence or serialization assumptions when type identity changes. Replacing inheritance with delegation may require a compatibility plan, not just moving method bodies.
