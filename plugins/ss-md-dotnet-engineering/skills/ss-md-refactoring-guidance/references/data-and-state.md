## Data, state, and domain concepts

Make data meaning, ownership, and mutation explicit.

- **Encapsulate mutable state** behind operations that preserve its owner's invariants; avoid accessors that merely expose internal representation.
- **Use domain types** to centralize meaningful values and rules. Prefer named fields over positional conventions; keep simple transport records when no domain behavior belongs there.
- **Prefer immutable value objects** with consistent value equality and hashing. Give entities stable identity independent of their changing attributes.
- Preserve equality, sharing, mutation visibility, and serialized formats when changing an existing representation. Stricter validation is a separate behavior change.
- **Name domain constants and alternatives** with meaningful constants or types, without wrapping obvious literals or creating behaviorless hierarchies.
- **Control collection mutation** through its owner, including aliases to incoming collections. Distinguish live views from snapshots; read-only collections do not imply immutable elements.
- **Keep one authoritative source of state.** Derive values when practical; give caches and synchronized copies explicit update and invalidation rules.
- Keep calculation-only state local to an invocation. Represent mode-specific state explicitly rather than populating otherwise meaningless fields.
- Prefer one-way relationships unless reverse navigation is needed. Maintain both ends of a bidirectional relationship through one consistent update mechanism.
