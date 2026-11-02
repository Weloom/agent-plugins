## 12. Anti-Patterns and Preferred Alternatives

| Avoid | Prefer |
|---|---|
| `Helpers`, `Utils`, `Managers`, or `Services` as dumping grounds | A precise responsibility beside its business feature |
| Renaming `OrderHelper` to `OrderService` without changing its scope | Split unrelated responsibilities and place behavior with its owner |
| Global `Enums`, `Records`, or `Models` folders | Business-oriented folders containing one type per file |
| Anemic entities with rules scattered through services | Encapsulated domain behavior where real invariants exist; simple CRUD where it fits |
| Business rules enforced only by controllers or consumers | Shared application policy and domain invariants |
| A service/interface/repository for every class or table | Abstractions at meaningful capability and aggregate boundaries |
| Generic CRUD repositories wrapping EF Core without added semantics | Direct EF Core where permitted, or focused repositories/read adapters |
| Private methods exposed solely to tests | Public-behavior tests or extraction of a real concept |
| Identical DTO copies at every layer | Separate contracts when ownership, exposure, or evolution requires them |
| Service locators, static dependencies, or captive scopes | Explicit injection, composition-root registration, valid lifetimes |
| Fire-and-forget business work or publish-and-hope events | Owned asynchronous execution with durable recovery when required |
| Unbounded retries or claims of exactly-once processing | Bounded retries, idempotent effects, explicit failure handling |
| Shared databases or a shared kernel used to bypass module boundaries | Owned data and deliberate module contracts |
| Broad exceptions converted into empty results or apparent success | Explicit failures mapped at the appropriate boundary, with diagnostic context |
| Large reorganizations mixed into unrelated fixes | Focused changes that preserve behavior and can be verified |

**Review and completion checks**

- Confirm dependency direction, business-rule ownership, naming, and one-type-per-file compliance for changed code.
- Check every affected entry path, DI registration, persistence adapter, event contract, and test stage; do not fix only the visible caller.
- Verify analyzer coverage rather than assuming a rule covers nested types, enums, records, and delegates. Add a focused check when strict enforcement is required.
- Run the smallest relevant build, analyzers, and tests; include integration validation when wiring, persistence, or messaging changes.
- Keep necessary architectural decisions and directly affected documentation current. Record concrete deviations, not boilerplate explaining obvious code.
- If no architectural problem affects the task, leave the structure unchanged.
