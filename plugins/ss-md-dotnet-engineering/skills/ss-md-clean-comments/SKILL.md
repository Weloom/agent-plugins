---
name: ss-md-clean-comments
description: "Clean up comments in requested code: clarify, correct, or remove redundant, obsolete, inaccurate, or change-history comments. Use only when the user explicitly asks to review or clean comments."
user-invocable: true
disable-model-invocation: true
---

# Clean up code comments

1. Limit edits to comments in the files or scope the user requested. Do not change runtime behavior or use comment cleanup as a reason for unrelated refactoring.
2. Read [comment guidance](./references/comments.md) and follow the comment-layout rules below.
3. Keep comments that explain intent, non-obvious constraints, important context, warnings, required notices, or actionable TODOs.
4. Remove or rewrite comments that are redundant, obvious, inaccurate, obsolete, vague, commented-out code, or merely describe a past change.
5. Keep short descriptions of 10 words or fewer on one line when practical. Use more lines when accuracy or understanding needs them.
6. Review the diff to confirm each remaining comment matches current behavior and that code was not changed unnecessarily.

Do not add documentation boilerplate solely to satisfy a convention unless the project or API contract requires it.

The references are maintained with this plugin. Use the bundled files; do not look for a separate guideline collection in the application repository.
