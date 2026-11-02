# Syntax Guidelines

Use these guidelines when writing, reviewing, or editing code. Apply them to changed code without turning a focused task into an unrelated formatting cleanup.

## Formatting and local consistency

- Match indentation, braces, whitespace, and line endings in the surrounding code. For new files, use nearby comparable files as examples.
- Do not search for or analyze formatting configuration files, install a reference configuration, or invoke a formatter as part of this guidance.
- **MUST NOT** change the existing blank-line spacing of untouched code unless explicitly asked to adjust or normalize spacing.
- When explicitly asked to normalize blank-line spacing, remove every empty line and only preserve blank lines in these obvious cases:
  - Before a comment that documents the code following it.
  - After a scope-ending `}` when it separates that scope from subsequent code.
  - Between type declarations, such as classes and enums.
  - Between properties, fields, methods, and other members when they are distinct declarations.

## Comments and Documentation

- Keep a concise description of 10 words or fewer on one line, including its documentation-comment syntax. For example:

  ```csharp
  /// <summary>Gets the current processing status.</summary>
  ```

- Use multiple lines when needed to explain important context clearly. Do not sacrifice accuracy or understanding to meet the short-comment guideline.
- Add comments only when they clarify intent, a non-obvious constraint, or important context; do not restate syntax or behavior that is already clear from the code.

## Verification

- Inspect the diff to confirm that whitespace cleanup stays within the requested files and scope and does not change behavior.
- Preserve untouched blank-line spacing unless normalization was requested. Do not automatically format the whole repository.
- Formatting does not implement the judgment-based comment rules, remove every unnecessary blank line, or prove that C# compiles. Use code review for intent and comment content, explicit cleanup for deliberate spacing changes, and project builds/tests for syntax and behavior.