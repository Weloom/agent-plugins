## 10. Events and Event-Driven Architecture

Distinguish intent, internal facts, and external contracts:

| Message | Meaning | Ownership |
|---|---|---|
| Command: `PlaceOrder` | Request that may be accepted or rejected | An explicit logical handler; not a broadcast fact |
| Domain event: `OrderPlaced` | Fact within a domain model | Domain; application handles reactions |
| Integration event: `OrderPlacedIntegrationEvent` | Committed fact shared across boundaries | Stable, versioned producer contract |

Use events to decouple independent reactions or cross boundaries. **SHOULD NOT** replace a clear local call with events when the caller requires an immediate, atomic result.

### Publication and delivery

```text
Business change + outbox entry
          | same database transaction
          v
        Commit -> Outbox publisher -> Broker -> Consumer
```

- **MUST** define domain-event dispatch timing. Reactions required for local atomic consistency participate before commit; post-commit reactions need an explicit failure/recovery strategy.
- **MUST NOT** publish an externally visible success event for uncommitted state.
- **SHOULD** use a transactional outbox when a committed change and eventual publication must not diverge. In-memory dispatch after commit alone cannot guarantee delivery.
- **MUST** assume duplicates unless stronger end-to-end guarantees are proven. Make consumer effects idempotent; use durable deduplication/inbox state where required and coordinate it with local effects.
- **MUST** acknowledge messages only after the required processing is durably complete. Define bounded retries for transient failures and dead-letter/quarantine handling for poison messages.
- **MUST** define ordering requirements and concurrency behavior; do not assume global ordering. Handle stale or out-of-order events where the transport permits them.

### Contracts and operations

- **SHOULD** use immutable, minimal payloads with event identity, occurrence time, schema/version strategy, and correlation metadata. Do not serialize aggregates, EF entities, or secrets.
- **MUST** evolve integration contracts compatibly or introduce explicit versions. Map domain events to external contracts instead of coupling consumers to domain internals.
- **MUST** make eventual consistency visible in use-case behavior. Long-running processes need explicit state, timeout, recovery, and compensation rules.
- **SHOULD** propagate tracing context and monitor publication failures, consumer failures, outbox backlog, and dead letters. An accepted message is not proof of completed business work.
- **MUST NOT** introduce event sourcing merely because events are used; persisting events as the source of truth is a separate architectural decision.
