## Error handling and invalid states

Error handling should preserve useful context and make failure behavior explicit.

- Represent and handle failures using the language and repository's established conventions.
- Do not silently swallow errors or return a success-shaped fallback when the operation failed.
- Include useful context when reporting or propagating an error. Preserve the underlying cause; avoid duplicate logging at multiple layers unless each layer has a distinct responsibility.
- Handle expected failures where the code can recover or provide a useful response. Do not disguise unexpected failures as normal results.
- Keep the normal path readable. Make failure and recovery paths clear without allowing them to obscure the operation's purpose.
- Validate external input at appropriate boundaries and preserve established invariants internally.
- Follow project conventions for optional values, nullability, exceptions, and result types. Do not apply a blanket rule such as "never use null" without regard to the language or existing design.
- Do not pass an absent or invalid value to code that cannot safely handle it. Use explicit optional values, meaningful defaults, or boundary validation as appropriate.
