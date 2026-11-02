## Learn and refine the domain model

Use these guidelines to determine whether the existing concepts and relationships can explain the behavior being added, corrected, or simplified. It is especially relevant when a requirement needs repeated exceptions or the same rule has conflicting interpretations. Identify which concepts or relationships need refinement before choosing types, functions, or modules. If the existing concepts already explain the required behavior, but their rules or effects are unclear in code, use "Make important concepts and rules explicit" instead.

- Treat the model as a working understanding, not a one-time translation of requirements. Test candidate concepts against concrete scenarios, including exceptions.
- Resolve ambiguous rules with domain experts or authoritative project material. If meaning remains uncertain, identify the unresolved decision rather than inventing a rule.
- Model the concepts and relationships needed to explain the behavior, not every real-world detail or a copy of the database or screens.
- When complexity persists, test whether a concept is missing or a relationship is wrong before hiding the existing procedure behind another abstraction.
