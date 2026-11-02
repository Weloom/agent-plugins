---
name: ss-md-domain-guided-development
description: "Choose and implement domain-grounded solutions when adding features to an existing business domain or changing business rules, concepts, invariants, ownership, or interactions between models. Also use for explicit DDD design or domain-readability reviews. Do not activate for formatting, purely technical changes, or straightforward CRUD without meaningful domain decisions."
user-invocable: true
disable-model-invocation: false
---

# Domain-guided development

Use domain understanding to find a suitable solution for the requirements and constraints, not the most DDD-looking design. `/ss-md-domain-guided-development` requests deliberate exploration; automatic activation uses the same reasoning at a depth proportional to the task.

## Start with the existing diagnostic loop

Read [model orientation](./references/model-orientation.md) and [the complete diagnostic loop](./references/diagnostic-loop.md). The loop includes all five steps, four possible directions, acceptance criteria, and qualifications. Follow it; do not replace it with a pattern checklist.

- **Establish meaning and scope:** trace the related existing behavior and a representative scenario for the feature. Identify rules, vocabulary, ownership, consistency requirements, and the actual difficulty.
- **Choose a direction:** extend the existing model if it fits naturally. Otherwise use the diagnostic signals to select relevant directions; they can combine and are not mandatory stages.
- **Apply a focused change:** implement when asked to implement; remain advisory when asked to review or plan. Preserve existing behavior except for the requested feature or approved rule change. Resolve uncertain business meaning before encoding it.
- **Verify the benefit:** test the new behavior, affected existing behavior, and the specific design claim. Separate intentional behavior changes from behavior-preserving refactoring.
- **Reassess:** stop or reconsider when the design merely relocates complexity, adds exceptions, or costs more than its benefit.

## Load further guidance only for a diagnosed need

These are separate, bundled files, not heading links into the full source document. Read only the relevant references; reassess the selection as understanding changes.

| Diagnosed need | Reference |
|---|---|
| Requirements fit awkwardly, exceptions multiply, or a concept may be missing | [Learn and refine the model](./references/model-refinement.md) |
| Ambiguous names or inconsistent terminology within a context | [Ubiquitous language](./references/ubiquitous-language.md) |
| Find where an existing or new rule belongs and how callers enforce it | [Connect model and implementation](./references/model-implementation.md) |
| Domain decisions mixed with workflows, persistence, UI, or frameworks | [Separate technical concerns](./references/technical-boundaries.md) |
| Decide identity, equality, associations, or ownership of behavior | [Choose model elements](./references/model-elements.md) |
| State transitions or atomic consistency requirements change | [Protect invariants](./references/invariants.md) |
| Concepts fit but callers reconstruct rules, effects, or sequencing | [Make rules explicit](./references/explicit-rules.md) |
| Share or move responsibilities across models, contracts, or team ownership | [Context relationships and model integrity](./references/context-boundaries.md) |

## Scope, coordination, and communication

- DDD reasoning establishes domain meaning, ownership, and solution direction. It does not require a particular programming paradigm or layered architecture.
- Consult architecture guidance only when implementation changes technical structure or dependencies; consult refactoring guidance only for behavior-preserving transformations. Do not load other skills just because DDD is active.
- If an understood business decision is obscured by I/O, hidden inputs, mutable intermediates, or effect sequencing, consult `ss-md-functional-csharp` for that specific technique or boundary; preserve consistency requirements. Use `ss-md-clean-code-guidance` only when a separate intent/readability decision remains unresolved. Neither is required to approve every domain change.
- Handoffs carry a concrete finding and unresolved decision, not a request to load every peer or launch another agent. Reuse loaded guidance; do not return to a source skill for the same decision. If a peer is unavailable, identify a material limitation rather than invent its guidance.
- Use authoritative project material and existing domain vocabulary. Distinguish evidence from hypotheses. Ask about unresolved business rules or ownership that materially affect the solution; do not ask for approval of every routine coding step.
- Compare meaningful alternatives when the diagnosis warrants it, not every possible pattern. Do not invent rules, abstractions, services, aggregates, or boundaries to justify a design.
- Briefly communicate the relevant scenario, evidence, chosen direction, and expected benefit. After implementation, report verification and remaining uncertainty. Do not require a new document or a lengthy report for every feature.

The bundled references are maintained with this plugin. Read only the relevant extracts during feature work.
