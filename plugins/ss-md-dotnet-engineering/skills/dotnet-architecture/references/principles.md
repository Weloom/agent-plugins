# .NET Architecture and Code Organization Guidelines

Use when creating, writing, reviewing, refactoring, or cleaning up .NET solutions. Organize code so business behavior, ownership, and dependency boundaries are easy to find and difficult to violate. Apply these rules to changed code; do not turn a focused task into an unrelated architectural rewrite.

**MUST / MUST NOT** are requirements. **SHOULD / SHOULD NOT** are defaults; deviate only for a concrete, documented reason. **MAY** identifies an option, not something to implement automatically. Resolve conflicts with explicit repository requirements before changing structure or behavior.

## 1. Architectural Principles and Dependency Rules

**Default:** a modular monolith, organized by business capability, with inward dependencies and feature-oriented folders. Use DDD where business complexity warrants it; do not force a rich domain model onto simple CRUD.

- **MUST** keep business invariants independent of HTTP, message brokers, persistence implementations, and external SDKs.
- **MUST** keep project and module dependencies acyclic. Dependencies follow responsibilities, not whichever reference makes compilation easiest.
- **SHOULD** separate domain decisions, application orchestration, and external adaptation. A layer is a responsibility boundary, not a mandatory pass-through class.
- **SHOULD** define module boundaries around business capabilities and language. A bounded context owns its model and contracts; it is not merely a folder or necessarily a separate deployment.
- **MUST NOT** bypass another module's boundary by accessing its tables, repositories, or internal entities. Use explicit module contracts or events.
- **SHOULD** keep behavior near the state and rules it governs, and prefer composition over inheritance used only for code reuse.
- **SHOULD** choose the simplest structure that meets current needs. Split processes or introduce messaging for concrete requirements, not architectural fashion.

Before introducing a boundary or abstraction, identify its owner, responsibility, consumers, and consistency requirements. Preserve public contracts and behavior unless the task explicitly authorizes a change.
