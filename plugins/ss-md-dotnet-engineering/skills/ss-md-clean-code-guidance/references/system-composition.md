## Architecture and system composition

Architecture guidance should reinforce the project's actual design, not invent a new one during a local change.

- Follow the repository's established architectural boundaries and dependency direction. Do not introduce a competing pattern without a task-driven reason.
- Keep construction, configuration, and application behavior separate when that makes dependencies easier to understand, test, or replace.
- Put composition decisions in the project's established entry point or composition mechanism rather than scattering construction logic across business code.
- Use factories or dependency injection when they clarify ownership, support substitution, or enable meaningful tests. Avoid using them as ceremony.
- Keep cross-cutting concerns consistent with existing project mechanisms rather than handling them differently in each feature.
- Adopt standards and frameworks when they fit the system and provide concrete value; do not add them simply because they are common or fashionable.
- Prefer architecture that can be tested and evolved incrementally. Avoid speculative design that adds complexity without serving a current requirement.
