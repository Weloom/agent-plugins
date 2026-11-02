---
description: "Lightweight C# editing defaults for local formatting consistency, whitespace preservation, and concise comment layout."
applyTo: "**/*.cs"
---

- Follow applicable project instructions. Otherwise, match indentation, braces, and line endings in surrounding code; for new files, use nearby comparable files.
- Preserve untouched blank-line spacing unless explicitly asked to normalize it.
- Keep short documentation descriptions (10 words or fewer) on one line, including XML tags, when practical. Use multiple lines when clarity requires them; do not rewrite comment meaning merely for layout.
- Inspect the diff for formatting consistency and unrelated churn. Leave deliberate comment or whitespace cleanup to explicitly requested work.
- These defaults require no formatting-configuration analysis, formatter invocation, or build/test run. Follow the project's own tooling and verification requirements; formatting alone does not establish compilation or correctness.
