## Responsibilities, cohesion, and duplication

Use these guidelines when responsibilities are misplaced or one rule requires coordinated edits across several places.

- **Move Method / Move Field:** Put behavior and state with the concept that owns the rule. Move a cohesive calculation, not surrounding orchestration; preserve dependency direction and one authoritative state owner.
- **Extract Class / Inline Class:** Extract a group that has a coherent responsibility and a meaningful name; inline a class whose separate identity no longer helps.
- **Consolidate duplication:** Share implementations of the same rule that should change together, preserving edge cases. Keep independently evolving rules separate even when their formulas match.
- Place shared rules in an appropriate domain owner rather than a generic utility module. Prefer temporary duplication over a shared helper full of caller-specific flags.
- **Hide Delegate / Remove Middle Man:** Hide navigation that couples callers to internal relationships. Remove forwarding layers only when their isolation or policy does not justify their cost.
- Move calculations toward their data rather than adding forwarding methods throughout a navigation chain. Expose a delegate only when callers can legitimately depend on it.
