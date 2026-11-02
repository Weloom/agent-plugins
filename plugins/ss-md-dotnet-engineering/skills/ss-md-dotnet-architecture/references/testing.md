## 11. Test Structure and Execution

Separate execution requirements in project names and pipeline selection:

| Category / project suffix | Allowed dependencies | Default execution |
|---|---|---|
| `.UnitTests` | In-process code and controlled test doubles; no live I/O or external processes | Local feedback and every PR |
| `.IntegrationTests` | Self-contained application components and disposable, test-owned infrastructure | Separate PR job |
| `.ExternalIntegrationTests` | Provisioned environments, deployed systems, third-party sandboxes, credentials | Controlled environment stage, scheduled/manual job |

A containerized database is integration infrastructure, not a unit-test dependency. An in-process HTTP host may still be an integration test. Scope and environment dependency are different dimensions.

### Layout and names

```text
Domain.UnitTests\
  Ordering\
    OrderCancellationTests.cs
Application.UnitTests\
  Ordering\
    PlaceOrder\
      PlaceOrderHandlerTests.cs
Infrastructure.IntegrationTests\
  Ordering\
    OrderRepositoryTests.cs
  Fixtures\
    DatabaseFixture.cs
Api.IntegrationTests\
  Ordering\
    PlaceOrderEndpointTests.cs
ExternalIntegrationTests\
  Payments\
    PaymentGatewayTests.cs
```

- **SHOULD** organize tests by business behavior/use case, not mechanically mirror every implementation folder.
- **SHOULD** name methods consistently by action, condition, and outcome: `Cancel_WhenOrderIsShipped_RejectsCancellation`.
- **MUST** apply one type per file to fixtures, builders, fakes, enums, and records too.
- **SHOULD** keep focused support local: `OrderBuilder`, `FakePaymentGateway`, `DatabaseFixture`. Shared support must not pull integration dependencies into unit tests.

### Behavioral boundaries

- **SHOULD** test private logic through public behavior. **MUST NOT** make methods public solely for testing or use reflection as the normal way to invoke private methods.
- Extract a substantial rule only when it has a cohesive, independently meaningful responsibility; do not move private methods into a miscellaneous helper.
- **MAY** test genuine internal components with `InternalsVisibleTo`; do not widen visibility mechanically.
- **SHOULD** test outcomes, invariants, failure paths, and observable side effects rather than implementation call sequences. Use mocks at meaningful boundaries, not for every collaborator.
- **MUST** test relevant transaction, authorization, duplicate-delivery, retry, and concurrency behavior when those guarantees are part of the change.

### Execution contract

1. **Select projects explicitly.** Unit and self-contained integration jobs may run in parallel. Do not let a solution-wide command accidentally run external tests in a fast stage.
2. **Own test state.** Isolate data for parallel execution, dispose test infrastructure, control time/randomness where relevant, and avoid arbitrary sleeps.
3. **Isolate credentials and access.** Unit/self-contained integration suites must not require shared live services. External suites use dedicated test environments and least-privilege credentials, not production by default.
4. **Fail visibly.** Required external configuration missing from a selected job is a failure, not a silent pass/skip. Report deliberately excluded suites clearly.
5. **Verify the actual boundary.** Use production-relevant database/broker semantics where needed; an in-memory substitute cannot prove provider-specific behavior. Validate host DI wiring and enforce dependency rules with architecture checks where practical.
