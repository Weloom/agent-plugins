## 7. Service Layers and Use-Case Orchestration

Route different entry points to shared application behavior:

```text
HTTP request -> Endpoint / HTTP adapter --+
                                         +-> Use-case handler -> Domain behavior
Queue message -> Consumer ---------------+          |
                                                   +-> Ports -> Infrastructure
```

Decide where logic belongs by asking:

1. **Would this rule still apply through another transport?** Put shared use-case policy in Application and business invariants in Domain.
2. **Does it interpret HTTP or broker mechanics?** Keep it in the corresponding adapter.
3. **Is it genuinely a different business operation?** Define a separate application use case, even if only one transport currently invokes it.

- **MAY** extract substantial transport orchestration into `PlaceOrderHttpAdapter`. Simple mapping and one application call belong directly in the endpoint.
- **MUST NOT** pass `HttpContext`, broker SDK messages, or transport response types into domain/application contracts. Translate identity and metadata into explicit application inputs.
- **MUST** enforce use-case authorization for every entry path. HTTP authentication and endpoint authorization do not protect queue or internal invocations; explicitly model trusted system callers.
- **MUST** assign ownership of transactions, idempotency, retries, and side effects. Avoid nested handlers that accidentally repeat authorization, commit independently, or publish duplicate work.
- **SHOULD** extract cohesive shared domain/application operations when use cases overlap. Do not build generic service chains or dispatch one handler through another solely for reuse.
- **MUST NOT** equate transport retry with safe business retry. Determine whether the operation can be repeated before acknowledging or retrying messages.

Name roles, not levels: `PlaceOrderConsumer`, `PlaceOrderHandler`, `OrderPlacementPolicy`, `CheckoutWorkflow`; avoid `ApiOrderService` and `ApplicationOrderService` as the only distinction.
