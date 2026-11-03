## Comments and documentation

Use comments to clarify intent or context that the code cannot express clearly. Prefer improving class and class member names, structure, or interfaces over explaining unclear code in comments. Keep comments accurate, concise, and close to the code they explain; update or remove them when the code changes.

Don't apply automated comments to the files you change like "This file has been changed by AI ..."


### Good comments

- **Required notices:** Include legal notices or other text required by law, license, or project policy.
- **Warnings:** Call out important risks, consequences, or constraints that are not evident from the code.
- **TODOs:** Mark known, actionable follow-up work. Keep TODOs specific enough to act on and remove them when resolved.
- **Intent:** Explain why the code exists or why a non-obvious approach is necessary.
- **Clarification:** Explain a low-level detail at the point where it matters, if the code alone is not clear.
- **Context:** Add important domain or operational context that a maintainer needs but cannot reasonably infer.
- **API documentation:** Briefly document classes and public members when their purpose or behavior is not self-evident. Keep class documentation to 25 lines or fewer and follow the repository's language and API documentation conventions.
- **Data examples:** Show special formats or codes when an example makes a constraint easier to understand. For example: `External IDs use the format ORG-123456.`

### Avoid

- **Mumbling:** Write comments clearly and directly; do not leave vague fragments that readers must decipher.
- **Over-compression:** Do not mangle an important explanation to make it shorter. Explain the necessary detail clearly.
- **Redundancy:** Do not restate obvious names, domain concepts, or behavior already clear from the code.
- **Mandated boilerplate:** Do not document every argument or member solely to satisfy a convention or silence a warning, unless the project or API contract requires it.
- **Obvious narration:** Do not describe what the code plainly does.
- **Closing-brace comments:** Do not add comments such as `} // end if`.
- **Grouping comments:** Do not use comments merely to label blocks or sections of code.
- **Change history:** Do not describe tickets, bug fixes, authorship, or past changes. Comments should explain current behavior or relevant intent.
- **Inaccurate or obsolete comments:** Correct or remove comments that no longer match the code.
- **Commented-out code:** Remove disabled code rather than preserving it in comments; use version control to recover prior implementations.
- **Comment substitutes:** Do not use comments to compensate for unclear code, a poor interface, or misplaced responsibility when a code change would clarify it.

## Comments and Documentation

- If a description is of 10 words or fewer, keep the comment's surrounding start- and end-tag on the same line. For example:

  ```csharp
  /// <summary>Gets the current processing status.</summary>
  ```