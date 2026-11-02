# Refactoring and Code-Quality Guidelines

Use these guidelines when reviewing, refactoring, or cleaning up existing code. The goal should be to improve the design so that the code communicates its intent and is easier to change, while preserving the behavior people and other software rely on.

Also use them when a feature or bug fix needs structural improvement to avoid a workaround. Keep the requested behavior change explicit and separate from behavior-preserving transformations. A simple change with no structural problem does not need a refactoring exercise.

## Diagnose the responsibility and choose a coherent scope

**Inspect broadly enough to understand the responsibility; change only what is needed to improve it coherently.** Small execution steps are a safety measure, not a reason to choose the smallest possible patch.

1. **Establish the problem and surrounding responsibility.** Trace a representative path through the affected code, its callers, collaborators, and state owner. Inspect relevant tests and parallel implementations. Look for who owns the rule, what must change together, and which contracts or effects callers rely on.
2. **Expand investigation when evidence points outward.** Follow scattered policy, duplicated decisions, shared mutable state, caller-specific flags, or repeated coordination to the responsible boundary. Check runtime wiring and configuration when relevant. Stop expanding when ownership, affected behavior, and the proposed boundary are understood; do not survey the entire repository by default.
3. **Diagnose before selecting a transformation.** Use the smell guidance to connect code evidence to a maintenance problem. A long method may contain misplaced responsibilities; extracting its body into helpers may preserve that problem. Similar code may represent independently evolving rules rather than duplication to remove.
4. **Choose the smallest coherent improvement, not necessarily the smallest diff.** Compare a local edit with a responsibility-level correction when both are plausible. Select by clearer intent, appropriate ownership, reduced coordination, compatibility, and verification cost. A multi-file change can be more focused than a one-file workaround; a smell alone does not justify a broad redesign.
5. **Evaluate the proposed result in its surroundings.** Check whether callers become simpler and rules gain a clear owner, rather than acquiring flags, forwarding layers, hidden sequencing, cyclic dependencies, or synchronized copies of state. Explain the structural benefit, not just fewer lines or smaller methods.
6. **Resolve a material scope mismatch.** If the requested quick fix would worsen the design, explain the evidence and a coherent alternative. Ask before materially expanding authorized scope, changing public contracts or behavior, or making a costly migration. Do not silently ship a harmful patch or silently launch a redesign. Routine changes within the agreed responsibility do not need approval at every step.

Then follow the safe workflow below. Preserve a clear distinction between investigation scope, authorized change scope, and the size of each verified execution step. For a review or plan, report the diagnosis and recommendation without treating the request as permission to edit.
