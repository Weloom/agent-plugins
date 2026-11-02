## Recognize smells; do not enforce metrics mechanically

Use smells to locate a maintenance problem, then use the relevant section below to choose a response. Size or syntax alone does not determine the remedy. Respect explicit repository limits, but do not invent universal line-count or complexity thresholds.

| Signal | Evidence to look for | Decision guidance |
|---|---|---|
| Duplicated code | One rule must be updated in several places. | Consolidate the shared rule; do not merge unrelated rules because their syntax matches. |
| Long method | Multiple intentions, tangled local state, or low-level details obscure the main flow. | Extract meaningful steps; retain a cohesive routine when splitting it only adds navigation. |
| Large class | Groups of fields and methods serve unrelated responsibilities. | Extract a cohesive responsibility, not an arbitrary number of members. |
| Divergent change | One class changes for several unrelated kinds of requirement. | Separate the responsibilities that change for different reasons. |
| Shotgun surgery | One conceptual change requires scattered, coordinated edits. | Bring that responsibility together; do not confuse this with divergent change. |
| Feature envy | A method interprets or manipulates another object's data to perform that object's work. | Investigate moving behavior; orchestration across objects is not automatically misplaced. |
| Inappropriate intimacy | Classes depend on each other's representation or bypass each other's invariants. | Clarify ownership and reduce access to internals. |
| Data clumps / primitive obsession | The same values travel together, or domain rules are repeatedly rebuilt around primitives. | Model the concept and its rules when that is clearer than repeated interpretation. |
| Type-based conditionals | A decision selects behavior by an object's kind; repeated decisions amplify the cost of adding a kind. | Consider polymorphism where the behavior belongs to the variants. Repetition strengthens the case but is not a prerequisite; retain a clear local switch when variant types would add more complexity. |
| Parallel inheritance hierarchies | Adding one subtype requires a matching subtype elsewhere. | Investigate an association or delegation that removes lockstep hierarchy growth. |
| Refused bequest | A subtype cannot meet a required base-type contract, or inherits implementation it does not use. | Contract incompatibility is strong evidence for delegation. Unused implementation alone is a weak smell; change it only when it causes confusion or coupling. |
| Temporary field | A field is meaningful only during one calculation or mode. | Consider a local variable, method object, or explicit state model. |
| Message chain | Callers know several levels of another object's internal relationships. | Hide unstable navigation where useful; fluent calls on one abstraction are not automatically a problem. |
| Middle man | Most changes require adding forwarding methods without adding meaning or policy. | Consider bypassing the wrapper if no useful boundary is lost. |
| Lazy class | A live class has too little responsibility to justify a separate concept. | Consider Inline Class; lack of responsibility does not mean the class is unused. |
| Speculative generality | Hooks, parameters, or hierarchies exist for unsupported hypothetical variation. | Simplify what has no present purpose, preserving supported extension points. |
| Data class | Callers repeatedly perform domain operations on exposed data. | Move domain responsibility to its owner; transport records need not become behavioral objects. |
| Incomplete library class | The same missing operation is repeatedly reimplemented for an unmodifiable dependency. | Consider a small local helper or extension; do not fork the library by default. |

Use a smell as a diagnosis, not a verdict. "This eligibility rule is duplicated in three workflows, so a policy change can leave them inconsistent" identifies a reason to refactor; "duplicated code" alone does not establish that the copies express the same rule.
