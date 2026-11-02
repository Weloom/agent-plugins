## Isolate domain behavior from technical concerns

Use these guidelines to classify the responsibilities mixed into an affected execution path: domain decisions, workflows, persistency, presentation, and technical operations. It is relevant when moving logic out of a handler, reusing behavior through another entry point, or changing persistence or frameworks without changing business rules. Decide which responsibilities must stay together to enforce the rules and which dependencies should be separated; do not turn a local change into a new layered architecture.

- **Domain:** own business decisions, rules, and state transitions.
- **Application:** coordinate a use case, transactions, and calls to domain and infrastructure capabilities; do not duplicate business policy here.
- **Presentation and infrastructure:** handle interaction and technical mechanisms. Input-format checks may live at the entry point; enforce business rules in the domain code responsible for them, so callers cannot bypass those rules.
- Protect domain meaning from UI, schema, and framework details through suitable boundaries. Add an abstraction when it separates a real responsibility or dependency, not automatically for every implementation.
