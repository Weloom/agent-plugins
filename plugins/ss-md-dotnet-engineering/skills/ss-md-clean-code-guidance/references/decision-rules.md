# Clean Code Guidelines

These guidelines support implementation, code review, refactoring, and cleanup. Apply them in the context of the repository's language, tooling, architecture, and established conventions.

## General decision rules

- Preserve the task's intent and existing behavior unless the request explicitly asks for a behavior change.
- Follow the repository's established conventions and architecture when they are clear. Do not introduce a competing style or pattern based on personal preference.
- Keep changes focused. Do not expand a targeted fix into a broad cleanup or redesign.
- Treat principles as decision aids, not automatic transformations. Refactor when the change makes intent, correctness, or maintainability meaningfully better.
- Prefer the smallest change that fully addresses the problem. Do not sacrifice clarity or correctness just to minimize lines changed.
- Use these principles as quality criteria, not as a mandatory gateway through every specialist workflow. Correctness, business invariants, contracts, ownership, and operational constraints take priority over stylistic preferences. Preserve established design properties; choose new techniques by demonstrated clarity and suitability.
- Consult specialist guidance for an unresolved decision: DDD for business meaning, refactoring for structural transformation, architecture for responsibility and dependency boundaries, performance for concrete resource constraints, and functional guidance for obscured data flow or preservation of pure/immutable boundaries. None is automatically required by the others.
