## 8. Dependency Injection and Inversion of Control

**Inversion of control:** delegate composition and lifecycle control to the host/framework. **Dependency injection:** supply collaborators explicitly. **Dependency inversion:** inner policy owns the contract; an outer adapter implements it. Using a DI container alone does not establish correct dependency direction.

```text
Application -> IPaymentGateway <- PaymentGatewayClient
                    ^                  ^
                    +-- Host registers-+
```

### Construction and registration

- **SHOULD** use constructor injection for required collaborators. Construct value objects and ordinary local data directly; not every object belongs in DI.
- **SHOULD** introduce interfaces at real boundaries or meaningful substitution points, not for every class. A pure calculator can be a concrete dependency.
- **MUST** keep container configuration in host composition roots and focused registration extensions. Business/application code must not resolve dependencies through `IServiceProvider`, static containers, or service locators.
- **SHOULD** keep constructors free of I/O and business execution. Validate required configuration at startup; never register silent no-op substitutes for missing required integrations.
- **SHOULD** use typed configuration and established .NET abstractions, such as `ILogger<T>` and `IHttpClientFactory`, where applicable.

### Lifetime and ownership

| Lifetime | Suitable use | Constraint |
|---|---|---|
| Transient | Lightweight per-resolution collaborators | Must tolerate repeated construction |
| Scoped | Request/message unit of work; typically `DbContext` | Must not escape its scope or be used concurrently when not thread-safe |
| Singleton | Shared, thread-safe services | Must not capture scoped dependencies or caller-specific mutable state |

- **MUST** check dependency lifetimes transitively. A transient captured by a singleton effectively lives with that singleton.
- **MUST** create and dispose an explicit scope per background work unit when scoped dependencies are needed; long-lived workers must not capture a `DbContext`.
- **MUST** define disposal ownership. Let the container dispose resources it owns; explicitly manage resources created outside it according to their registration/ownership contract.
- **SHOULD** validate registrations and scopes in host tests. Do not repair dependency cycles with lazy resolution or factories; correct the responsibility boundary.
