# Domain-Driven Design Guidelines

Apply these guidelines where domain complexity justifies a domain model. Do not add DDD patterns and layers to simple code merely to satisfy a checklist.

For feature implementation, reviews, and edits, start with the diagnostic loop and consult the sections relevant to the affected behavior. Prefer verified domain meaning and required behavior over superficial uniformity; do not broaden a focused change into an unrequested redesign.

## Read the code as an expression of a domain model

- A **domain model** selects concepts, relationships, and rules that explain the behavior the software supports. It is not simply its class structure or database schema.
- Express the model using objects, records, functions, or modules as appropriate to the codebase. Require clear responsibility for domain rules, not a particular programming paradigm; identity and consistency requirements still apply to immutable data.
- A **bounded context** defines where a model and its language have consistent meanings. Similar names or implementations do not establish shared meaning; module, service, and deployment boundaries are evidence, not proof.
- A **context map** describes existing bounded contexts and their relationships: model ownership, dependencies, collaboration, and translation. It is not merely a technical dependency diagram or a proposed architecture.
- Distinguish boundaries: a bounded context governs meaning; an **aggregate** groups objects whose consistency is protected through a root; modules and services organize implementation. Do not substitute one boundary for another.
- Prefer improvements that clarify domain rules and make them safer to change. Uniformity, reuse, and abstraction help only when they preserve the relevant meanings and constraints.
