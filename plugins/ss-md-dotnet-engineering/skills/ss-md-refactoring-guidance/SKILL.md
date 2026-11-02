---
name: ss-md-refactoring-guidance
description: "Diagnose and improve existing code structure while preserving behavior. Use for refactoring, restructuring, extraction, inlining, simplification, duplication, or code smells, and when a feature or bug fix needs structural improvement to avoid a workaround. Examine the surrounding responsibility rather than assume the smallest diff is best. Do not activate for every edit or unrelated cleanup."
user-invocable: false
disable-model-invocation: false
---

# Diagnose and refactor coherently

**Inspect broadly enough to understand the responsibility; change only what is needed to improve it coherently.** Small execution steps do not imply a narrow diagnosis or the smallest possible patch.

## Diagnose before transforming

Read [diagnosis and scope](./references/diagnosis-and-scope.md). Follow its six decisions: understand the surrounding responsibility, expand investigation on evidence, diagnose the problem, choose a coherent improvement, evaluate its effects on callers and ownership, and resolve material scope mismatches.

Inspect relevant callers, collaborators, state ownership, parallel implementations, and tests. Follow evidence outward, not an arbitrary file radius. Stop when the affected responsibility is understood; do not perform a repository-wide audit by default.

Read [smell diagnosis](./references/smell-diagnosis.md) to classify the observed problem. Choose a transformation for the problem, not a problem for a favored pattern. A helper extraction that leaves misplaced ownership or awkward coordination intact may not be the right solution.

## Load the relevant transformation guidance

| Observed problem | Reference |
|---|---|
| Unclear intentions, poor method boundaries, tangled expressions or locals | [Names and composition](./references/names-and-composition.md) |
| Misplaced responsibilities, duplicated rules, scattered coordinated edits | [Responsibility and duplication](./references/responsibility-and-duplication.md) |
| Representation, mutable state, aliases, equality, or multiple sources of truth | [Data and state](./references/data-and-state.md) |
| Nested decisions, overlapping guards, flags, or case-specific behavior | [Decision structure](./references/decision-structure.md) |
| Shared behavior, inappropriate inheritance, dispatch, or independent variations | [Inheritance and composition](./references/inheritance-and-composition.md) |
| Suspected unused code, speculative abstractions, or excessive forwarding | [Abstraction and indirection](./references/abstraction-and-indirection.md) |
| A migration spans boundaries, or a hot-path constraint affects the transformation | [Larger changes and performance](./references/larger-changes-and-performance.md) |

These are separate bundled files. Load only relevant techniques and qualifications, not every reference.

## Execute safely and verify the design

Before editing, read [the safe workflow](./references/safe-workflow.md) and [test selection](./references/test-safety-net.md). Preserve contracts, errors, state sharing, side effects, ordering, and supported extension points. Use meaningful, independently verified steps and symbol-aware tools where available.

After each meaningful transformation, check affected behavior. At a stable point, use [the review checklist](./references/review-checklist.md) to assess the surrounding result, not only the edited fragment. Verify the structural claim as well as tests; fewer lines, smaller methods, or passing tests alone do not establish improvement.

If work remains necessary and authorized, continue rather than stop at the first passing extraction. If blocked or outside scope, identify the remaining problem and safe stopping point explicitly.

## Scope and coordination

- Activate for explicit refactoring and structural improvements genuinely needed by a feature or bug fix. Do not turn ordinary edits into cleanup exercises.
- Preserve behavior during structural transformations. Separate requested feature or defect corrections from refactoring and give changed behavior explicit tests.
- If a local patch would worsen design, explain why and propose a coherent alternative. Ask before materially expanding authorized scope or changing contracts or behavior; do not silently redesign or knowingly ship the harmful patch.
- Use domain-guided development when uncertainty concerns business meaning or model ownership, and architecture guidance when technical boundaries change. Do not automatically load all other skills.
- If mutable intermediate state, hidden inputs, or mixed calculations/effects drive the diagnosis, consult `ss-md-functional-csharp` to consider a suitable technique, not to mandate a rewrite. Also consult it when the affected code relies on established pure, non-mutating, or immutable boundaries. Use `ss-md-clean-code-guidance` only for an unresolved clarity decision.
- Carry the specific finding into a handoff, reuse loaded skills, and do not bounce back to the source for the same decision or launch another agent merely to load guidance. If a peer is unavailable, state a material limitation instead of inventing its instructions.
- Respect requests for review or planning without editing. Briefly explain evidence, the diagnosed problem, chosen scope, and expected benefit; report verification and remaining limitations without requiring a new document.

The bundled references are maintained with this plugin. Use only the extracts needed for the current responsibility.
