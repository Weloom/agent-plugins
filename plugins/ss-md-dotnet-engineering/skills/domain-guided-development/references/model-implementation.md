## Keep the model connected to the implementation

Use these guidelines to trace the affected domain rule from its intended meaning through the domain code, callers, and tests that implement it. It is relevant when adding behavior to an existing model, consolidating scattered decisions, or checking whether a proposed refactoring changes only structure or also meaning. Establish which model element should own the rule and what behavior must remain observable; do not treat domain names or diagrams as proof that the implementation follows the model.

- Trace important domain rules to the code responsible for defining and enforcing them, whether objects, functions, or domain services. Domain names alone are insufficient if callers still duplicate or inconsistently apply the rules.
- Let implementation constraints inform model refinement, but do not maintain a conceptual model disconnected from the code. Modeling and implementation should evolve together.
- Express tests through domain scenarios and observable rules, not only private implementation structure.
- Update affected tests and model descriptions with the implementation; distinguish intended behavior from what the current code happens to do.
