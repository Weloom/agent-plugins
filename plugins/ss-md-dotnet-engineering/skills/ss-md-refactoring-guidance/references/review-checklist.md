## Review checklist

Use these questions to catch plausible-looking refactors that do not actually improve the design:

- **Context and scope:** Was the surrounding responsibility examined, and does the change address the diagnosed problem rather than polish one fragment? Is any remaining migration or structural limitation explicit?
- **Extraction:** Does the new name explain an intention, or does it hide the same difficult code behind a vague label and many parameters?
- **Unification:** Do the merged implementations express one rule, or did flags and special cases accumulate to accommodate unrelated callers?
- **Movement:** Did the rule move with its state ownership, or did it leave behind synchronization, cyclic dependencies, or a longer navigation chain?
- **Simplification:** Did the removed wrapper or subtype carry policy, dispatch, or supported extension behavior that the replacement has lost?
- **Verification:** Would the selected tests detect the plausible mistakes in this transformation, or were expectations changed to fit the result?
- **Migration:** Can both old and migrated callers reach a consistent implementation, and is temporary duplication distinguishable from intentional compatibility support?
