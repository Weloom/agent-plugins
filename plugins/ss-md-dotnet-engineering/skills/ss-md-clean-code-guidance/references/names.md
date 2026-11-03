## Names

Names are a primary guide to understanding code without tracing every implementation detail.

- Choose names that communicate the value's meaning or the function's behavior in its context.
- Prefer searchable, pronounceable names. Avoid cryptic abbreviations, misleading terms, and names that differ only superficially.
- Use the same term for the same concept throughout the relevant codebase.
- Name functions so callers can understand their purpose and significant side effects.
- Match name specificity to scope: short names can work in small local scopes; wider-scope concepts usually need more context.
- Replace a literal with a named constant when the value has domain meaning, is non-obvious, or must be changed consistently. Do not name obvious values without a comprehension benefit.
