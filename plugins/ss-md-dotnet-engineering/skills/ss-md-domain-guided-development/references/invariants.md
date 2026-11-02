## Protect invariants with aggregates

Use these guidelines before splitting or combining aggregate state or changing update paths. Identify required consistency first; verify that every affected state transition still preserves the invariants, not merely that the new structure compiles.

- Start with invariants: identify the rules that must hold when a change completes, then choose the aggregate boundary that can enforce them.
- Route changes through the aggregate root's operations or domain functions that enforce the whole aggregate's rules. With immutable data, validate the resulting state before accepting or persisting it; immutability alone does not enforce invariants.
- Keep the boundary focused, but do not split objects whose invariants genuinely require atomic changes merely to make aggregates smaller.
- Reference other aggregates through their roots, commonly by identity; do not retain direct access to their mutable internals.
- For cross-aggregate changes, state the consistency requirement explicitly.
  - Use delayed coordination only when the domain permits temporary inconsistency.
  - If immediate consistency is required, review the boundaries and transaction design rather than silently weakening the rule.
