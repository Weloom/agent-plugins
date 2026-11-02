## 4. Naming Conventions and Grammar

| Element | Convention | Examples |
|---|---|---|
| Solution, project, assembly, namespace | PascalCase segments separated by dots | `Acme.Commerce.Domain` |
| Code folder; type and matching file | PascalCase | `Ordering`, `OrderStatus.cs` |
| Interface | `I` + PascalCase | `IOrderRepository` |
| Method, local function, property, event | PascalCase | `PlaceOrder`, `OrderNumber` |
| Parameter and local variable | camelCase | `orderId`, `totalAmount` |
| Private instance field | `_camelCase` | `_orderRepository` |
| Constant and enum member | PascalCase | `MaximumRetries`, `Shipped` |
| Generic type parameter | `T` or descriptive `TName` | `T`, `TEntity` |
| Awaitable-returning method | PascalCase + `Async` | `LoadOrderAsync` |
| Repository containers | Conventional lowercase | `src`, `tests`, `docs`, `scripts` |

**Grammar:** types use nouns or noun phrases; methods use verbs describing behavior. Use qualifier + subject + role where useful: `ShippingRateCalculator`. Commands express intent (`PlaceOrderCommand`); events express completed facts (`OrderPlaced`).

- **SHOULD** prefer precise role nouns: `Logger`, `EmailSender`, `OrderReader`, `CancellationPolicy`. `LoggerService` is usually redundant; `LoggingService` suggests a broader capability.
- **SHOULD** use `Service` only for a cohesive capability without a more informative role name. DI registration does not justify the suffix.
- **MUST NOT** use `Helper`, `Utility`, `Manager`, or stacked suffixes as substitutes for defining responsibility. Do not merely rename a dumping ground.
- **SHOULD** treat acronyms as words in new identifiers: `Http`, `Json`, `Api`, `Id`. Preserve framework/external names and established repository conventions.
- **SHOULD** use business vocabulary consistently. Avoid abbreviations, redundant namespace prefixes, and names revealing only implementation details.
- **MUST** preserve ecosystem filenames such as `appsettings.json`; do not PascalCase every file.
- External contracts follow their own conventions: typically camelCase JSON and lowercase kebab-case route segments. **MUST NOT** break published contracts for naming consistency.
- **MUST** match filename casing in references and avoid files differing only by case. Verify case-only renames are recorded by Git and work on case-sensitive systems.

Follow established identifier conventions in the code; use templates or architecture checks for project and folder conventions.
