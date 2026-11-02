## 9. Data Access, Repositories, and External Adapters

Choose the boundary by the operation, not by a universal CRUD abstraction:

| Need | Preferred approach |
|---|---|
| Load and save a business aggregate | Aggregate-specific repository when a domain boundary is useful |
| Return filtered/projected data | Read adapter returning a use-case read model |
| Simple CRUD without a rich domain | Direct EF Core in the application use case may be appropriate under the chosen dependency model |
| Call payments, email, storage, or another system | Capability-specific port and adapter, not a generic repository |

**Repository contract**

- **SHOULD** describe aggregate-oriented operations using domain/application types, not mirror every `DbSet` method. Do not create a repository per table.
- **SHOULD** place the interface in Application when it serves orchestration, or Domain when domain behavior genuinely requires that abstraction. Keep implementation in Infrastructure.
- **MUST NOT** expose database connections or EF tracking APIs through repository contracts. Translate expected provider failures into meaningful application outcomes where needed; preserve diagnostic causes and let unexpected failures reach the host's error boundary.
- **SHOULD NOT** expose `IQueryable` across an encapsulated data-access boundary. Keep provider execution inside the adapter and return explicit projections or materialized results.
- **MUST** make save/commit ownership explicit. Repository methods must not unexpectedly commit fragments of a larger use case.

**Queries and consistency**

- Reads **MAY** bypass aggregates and use optimized projections; **MUST** still enforce authorization, tenant isolation, and appropriate consistency.
- **MUST** define transaction boundaries for writes and handle concurrency conflicts deliberately. Do not overwrite conflicting changes silently.
- **MUST NOT** assume a local database transaction covers an external API or broker. Use an outbox, workflow, or compensating action when reliable cross-system coordination is required.
- **SHOULD** use EF Core's existing tracking and unit-of-work capabilities. Add custom repositories or units of work only when they establish a useful contract, not as mechanical wrappers.
- Direct EF Core use couples that application path to EF Core; **MUST** treat it as an explicit architectural choice, not claim strict persistence independence.
- **SHOULD** verify mappings, constraints, transactions, and query translation against the actual database engine through self-contained integration tests.
