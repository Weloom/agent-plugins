## Refactoring and cleanup

Refactoring should improve the code without hiding behavior changes or creating unrelated review work.

- Preserve existing behavior unless the task explicitly requests a change. For risky changes, identify important behavior and use tests to protect it.
- Make changes in focused, reviewable steps. Keep the code in a verifiable state and run relevant checks after meaningful changes.
- Improve the code directly related to the task, but avoid broad cleanup that makes it difficult to review the requested change.
- Remove dead code, obsolete paths, redundant state, and unnecessary indirection when it is safe and within scope. Check for compatibility or external-use constraints before deleting apparently unused code.
- Prefer changes that make intent clearer or reduce meaningful duplication. Do not optimize for fewer lines or fewer abstractions as goals in themselves.
- Treat code smells as reasons to investigate, not commands to refactor. Confirm the issue in context and choose the least disruptive effective improvement.
