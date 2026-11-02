---
name: dotnet-architecture
description: "Guide .NET architectural changes, especially when adding or moving classes, types, projects, modules, dependencies, services, or persistence boundaries. Use the relevant architecture guidance before proposing structural changes; do not impose layers on simple CRUD."
user-invocable: false
---

# Apply relevant .NET architecture guidance

Before adding or moving a type, changing its responsibility, or introducing a project, module, dependency, service boundary, or adapter:

1. Inspect the existing solution structure, nearby types, dependency direction, and established patterns.
2. Read [architectural principles](./references/principles.md), [project structure](./references/project-structure.md), and [folder and file organization](./references/file-organization.md). Read only other sections relevant to the proposed change.
3. Identify the type's responsibility, owner, callers, and dependencies before selecting a location or abstraction. Keep project dependencies acyclic and respect module boundaries.
4. Choose the simplest structure that fits the current system. Adding a class does not by itself justify a new layer, project, interface, or shared abstraction.
5. Preserve existing behavior and public contracts. Verify registrations, references, tests, and dependency rules affected by the change.

If architecture ownership or a boundary is ambiguous, ask for clarification or present the trade-off rather than inventing a system-wide design.

## Further guidance by decision

| Decision | Reference |
|---|---|
| Names and grammar | [Naming](./references/naming.md) |
| Domain, application, or adapter responsibility | [Type boundaries](./references/type-boundaries.md) |
| Method cohesion, parameters, and named steps | [Method design](./references/method-design.md) |
| Use-case coordination and service responsibilities | [Orchestration](./references/orchestration.md) |
| Registration, lifetimes, or owned resources | [Dependency injection](./references/dependency-injection.md) |
| Persistence or external integration | [Data access and adapters](./references/data-access.md) |
| Event contracts, publication, and delivery | [Events](./references/events.md) |
| Test placement, behavioral boundaries, and execution | [Testing](./references/testing.md) |
| Suspected architectural anti-pattern | [Anti-patterns](./references/anti-patterns.md) |

The bundled references are maintained with this plugin. Read only relevant files.

If a calculation boundary must remain independent of I/O and hidden state, consult `functional-csharp` for the relevant effect and input contracts. Use `clean-code-guidance` only for an unresolved clarity decision. These are conditional handoffs with a specific finding, not instructions to load every peer or launch another agent. Reuse already-loaded guidance and do not bounce back to the source skill for the same decision. If a peer is unavailable, state a material limitation instead of inventing its instructions.
