---
name: clean-code-guidance
description: "Assess and improve code clarity during implementation, review, or cleanup when intent, names, responsibilities, effects, dependencies, or failure paths are unclear. Use for explicit Clean Code requests or a concrete readability concern. Supplies quality criteria and routes diagnosed decisions to specialist guidance; not a mandatory gateway or a reason for unrelated cleanup."
user-invocable: true
disable-model-invocation: false
---

# Apply Clean Code quality criteria

Read [general decision rules](./references/decision-rules.md). Understand the requested change and nearby conventions, then identify a concrete comprehension problem. For an explicit review, inspect the requested scope and use [the review checklist](./references/review-checklist.md) to guide investigation, not require edits for every item.

Correctness, business invariants, contracts, ownership, and operational constraints take priority over stylistic preferences. Preserve established design properties; assess clarity through names, call sites, explicit inputs/results, and visible effects rather than line counts or one programming paradigm.

## Select only relevant quality guidance

| Concern | Reference |
|---|---|
| Misleading names, hidden domain vocabulary, or ambiguous operations | [Names](./references/names.md) |
| Comments conceal rather than clarify intent | [Comments](./references/comments.md) |
| Mixed responsibilities, abstraction levels, inputs, outputs, or effects | [Functions and APIs](./references/functions-and-apis.md) |
| Layout obscures structure or formatting churn threatens the task | [Formatting and organization](./references/formatting-and-organization.md) |
| Unhelpful abstractions or exposed implementation details | [Abstractions and boundaries](./references/abstractions-and-boundaries.md) |
| Hidden failures, invalid states, or ambiguous absence | [Errors and invalid states](./references/errors-and-invalid-states.md) |
| Tests obscure behavior, miss boundaries, or mask regressions | [Tests](./references/tests.md) |
| Unclear component responsibility or excessive coupling | [Classes and modules](./references/classes-and-modules.md) |
| Scattered construction or inconsistent composition | [System composition](./references/system-composition.md) |
| Unnecessary churn or cleanup without a demonstrated benefit | [Refactoring and cleanup](./references/refactoring-and-cleanup.md) |
| Shared state, overlapping work, or unclear cancellation/shutdown | [Concurrency](./references/concurrency.md) |

## Route a finding, not the entire task

| Finding and unresolved decision | Relevant skill |
|---|---|
| Business terminology, rules, invariants, or ownership are uncertain | `domain-guided-development` for domain meaning |
| Correcting the problem requires restructuring existing code | `refactoring-guidance` for diagnosis, coherent scope, and safe transformation |
| Type placement, dependency direction, or composition boundaries must change | `dotnet-architecture` for structural decisions |
| A concrete workload, allocation, latency, or contention constraint is involved | `performance-review` for evidence and resource trade-offs |
| Hidden inputs, mutable intermediates, mixed calculations/effects, or established pure/immutable boundaries need attention | `functional-csharp` for relevant techniques or preservation |

These are conditional handoffs, not a required pipeline. Identify the specific evidence and decision before loading another skill. Reuse loaded guidance and never return to a source skill for the same decision. Do not invoke other agents merely to follow a handoff. If a peer skill is unavailable, acknowledge a material limitation and follow existing project guidance rather than inventing the missing content.

Implement only authorized improvements, or provide findings when asked to review. Verify affected behavior and the clarity benefit; leave already clear code alone. Do not require functional rewrites, hierarchies, smaller methods, comments, or abstractions just to satisfy a checklist.

The bundled references are maintained with this plugin. Do not load all references during ordinary coding tasks.
