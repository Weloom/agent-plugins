## Tests as a safety net

Choose tests for plausible mistakes in the proposed transformation.

- **Target the changed mechanism.**
  - Branch restructuring: check values at, below, and above relevant thresholds; cover overlapping guards in their priority order and expected failures.
  - Moving state or behavior: check mutation visibility, initialization, and behavior through old and new calling paths where both remain supported.
  - Representation or algorithm changes: check empty inputs, duplicates, ordering, equality, rounding, and errors where those can differ.
  - Test each behavioral variant. Test combinations when variants interact; do not expand independent alternatives into every possible combination by default.
- **Characterize before restructuring unfamiliar code.** Capture current outputs, errors, and significant side effects through a reachable boundary. An observed result is a baseline, not evidence that the result is correct.
  - For a broad input space, differential tests can compare old and new implementations using independent input/state copies. Property-based tests can exercise known invariants across generated inputs.
  - Compare more than return values when mutations or effects matter. Neither technique justifies changing an unexplained difference.
  - If a suspected defect emerges, give its correction an explicit regression test rather than changing characterization expectations inside the structural step.
- **Keep the safety net sensitive.** Existing behavioral assertions should usually survive a private extraction or move.
  - Adapt fixture wiring and call sites as needed. Do not delete assertions or rewrite expected values merely to accommodate a failed refactor.
  - Prefer outcome checks over private-helper names or incidental call counts. Keep interaction assertions when counts or order are contractual, such as charging once or committing only after validation.
  - Control clocks, randomness, and external dependencies using existing test seams when they make results nondeterministic. A flaky result is not a verified checkpoint.
- **Keep tests readable independently.** A small amount of repeated setup can make different cases clearer than a shared helper with flags. Share stable fixture mechanics; use parameterized cases when the same assertion applies to different data, not to hide different rules in one test.
- If existing failures mask the affected behavior, establish an isolated passing check or narrow the transformation. If only manual verification is feasible, identify the exercised paths and remaining gaps rather than treating a successful build as equivalent coverage.
