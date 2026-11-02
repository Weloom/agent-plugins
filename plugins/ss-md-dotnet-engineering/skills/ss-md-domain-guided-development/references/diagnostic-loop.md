## Diagnose before changing the model

Use this loop when implementing features in an existing domain, changing business rules, reviewing the model, or refactoring domain code. Keep the scope proportional to the change; a local correction or natural extension does not require a system-wide redesign.

1. **Establish meaning and scope.** Trace a representative scenario through the code. Identify required behavior, relevant rules, and the observed difficulty; determine whether the change stays within one model or affects another model's meaning, ownership, or contract.
   - For local behavior changes, inspect the affected rules and consistency requirements; do not require system-wide mapping.
   - Before sharing domain code or moving responsibilities across models, inspect the affected context relationships.
   - Use existing maps and authoritative project material where available. If absent, form a small, evidence-based account of the relevant relationships; mark uncertain boundaries and ownership as hypotheses rather than inventing them.
2. **Choose a direction.** Use the diagnostic signals below to identify what needs improvement. If existing concepts express the feature naturally, extend them without redesign. Directions can combine; they are not mandatory stages.
3. **Apply a focused change.** Address the diagnosed problem without unrelated restructuring. Preserve required behavior; do not introduce new domain rules to make the proposed design work.
4. **Verify the benefit.** Test required behavior and the specific claim: clearer rules, equivalent results from a consolidated mechanism, or predictable composition. Separate intentional behavior changes from behavior-preserving refactoring.
5. **Reassess.** Repeat as understanding improves. Stop or reconsider when a change only relocates complexity, adds exceptions, or costs more than its demonstrated benefit.

### Choose a direction based on the diagnosed problem

| Direction | Diagnostic signal | Action and acceptance criterion |
|---|---|---|
| **Recognize and adapt a pattern** | A responsibility, relationship, or source of variation resembles a studied problem. | Evaluate the pattern's assumptions and consequences. Use analysis patterns for domain insight and design patterns for suitable implementation structure; a design pattern can also express a domain concept. Accept it when it clarifies the actual problem without unused roles or speculative flexibility. |
| **Consolidate or adopt an established solution** | Duplicate code or different implementations may solve the same problem; complex custom code may have an established alternative. | Compare meanings, invariants, ownership, and reasons for change before sharing. Evaluate a published model, formalism, third-party implementation, or focused in-house mechanism. Accept consolidation when semantics fit, results remain correct, and integration and maintenance costs justify it. Similar code alone is insufficient. |
| **Discover a deeper model** | Exceptions multiply, new requirements fit awkwardly, or experts do not recognize the model's language - even when code is tidy. | Explore missing concepts and incorrect relationships with domain experts and concrete scenarios. Change language, responsibilities, and tests together. Accept the model when it explains the rules more naturally and removes compensating complexity; adding classes alone is not progress. |
| **Refine a supple, expressive design** | The concepts fit, but callers must inspect implementation, manage hidden sequencing, or understand incidental dependencies. | Apply the explicit-concepts and interfaces guidelines below. Accept the design when callers can express domain intent, predict effects, and compose operations without reconstructing the algorithm. Cosmetic renaming alone is insufficient. |

- **Adapt patterns to the problem.** Adapt useful reasoning without copying an entire structure. Preserve established meanings when borrowing terminology; rename concepts that have acquired different meanings.
- **Separate domain rules from computational procedures.** A generic subdomain models supporting concepts; a cohesive mechanism solves a computational problem posed by a model. Extract such procedures when they obscure the rules being changed, not merely because they are complex. Preserve algorithms that express distinguishing domain knowledge rather than treating them as interchangeable utilities.
- **Standardize only what is understood.**
  - Use a coherent subset of an established solution when sufficient; compare semantic fit, dependencies, and maintenance cost.
  - Do not let a generic solution replace application-specific rules merely to simplify integration. Sharing domain code across contexts requires an explicit relationship and ownership decision.
  - Do not freeze an immature model into a framework.

In implementation and reviews, connect decisions to **code evidence -> chosen direction -> expected benefit**. Report uncertain domain assumptions as questions, not established facts or defects. Do not demand a pattern or redesign solely because one is available.
