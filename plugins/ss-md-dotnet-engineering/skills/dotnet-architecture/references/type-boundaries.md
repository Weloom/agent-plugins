## 5. Type Responsibilities and Boundaries

Choose a role because it describes behavior, not to complete an architectural checklist.

### Domain: decisions and valid state

- **Entity:** identity and lifecycle; owns behavior affecting its state.
- **Aggregate root:** protects invariants within a consistency boundary; controls aggregate mutations. **MUST NOT** expose mutable internals that bypass those rules.
- **Value object:** value-based equality and validated semantics; **SHOULD** be immutable. A C# record alone does not establish domain validity.
- **Domain service:** business behavior that does not naturally belong to an entity or value object; not application orchestration.
- **Policy / specification:** a named decision or eligibility rule; extract when it makes the business meaning clearer.
- **Domain event:** a meaningful business fact; not a command or transport envelope.

Prefer `order.Cancel(reason)` over setters that let callers construct invalid transitions. **MUST** enforce invariants regardless of caller; request validation cannot replace them.

### Application: intentions and coordination

- **Command / query:** describes a state-changing intention or a read request, respectively.
- **Handler / use-case service:** coordinates authorization, loading, domain behavior, persistence, and outcomes for one use case.
- **Validator:** checks input shape and basic constraints; does not become the sole owner of business rules.
- **Result / read model:** carries outcomes or projected data without domain behavior.
- **Port:** defines a capability needed by the application, using transport-independent types.
- **Workflow / process manager:** coordinates a multi-step, potentially long-running business process and its recovery state.

Commands and queries do not require MediatR, separate databases, or a broker. **SHOULD** use ordinary calls unless dispatch infrastructure serves a concrete need.

### Adapters: external mechanisms

- **Endpoint / consumer:** translates protocol input and metadata into application calls and maps outcomes to protocol behavior.
- **Repository / read adapter:** persists aggregates or produces query projections.
- **External client / gateway:** implements access to an external system.
- **DbContext / mapping configuration:** owns persistence tracking and database mapping, not business policy.
- **Worker:** schedules or receives work and invokes application behavior; it is not an alternate home for business rules.

**Boundary check:** a class should have one coherent responsibility and explicit dependencies. Extract a concept when it has its own meaningful contract, not simply because a method is long or needs a direct unit test.
