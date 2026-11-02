## Conditional logic and decision structure

Make the decision and its alternatives explicit without hiding evaluation or failure behavior.

- **Name complex decisions** with intention-revealing predicates and actions; predicate names must not conceal side effects.
- **Consolidate conditions** that express one decision, and move genuinely shared work outside branches. Matching results alone do not make independent rules equivalent.
- Preserve short-circuiting, evaluation order, call counts, and effect timing when simplifying branches or expressions.
- **Use guard clauses** to separate special cases from the main path; retain `if`/`else` when alternatives deserve equal emphasis. Preserve overlapping-case priority and required cleanup.
- Replace flags that merely simulate an exit with `return`, `break`, or equivalent control flow; retain flags that represent real state.
- **Use polymorphism** when case-specific behavior belongs to distinct variants; repeated type checks strengthen, but are not required for, that choice. Keep a conditional or pattern match when cases are clearer together.
- Use subclasses for substitutable kinds; use strategy or state objects for independent or changeable behavior.
- **Use special-case objects** for absence with defined behavior. Keep absent, unknown, invalid, and failed distinct; never turn a failure into a successful-looking default.
- **Use assertions** for established internal invariants, not input validation or expected errors. Assertions must have no required side effects and must remain safe to disable.
