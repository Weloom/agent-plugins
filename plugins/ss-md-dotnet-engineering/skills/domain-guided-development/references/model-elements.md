## Choose model elements by meaning

Use these guidelines when assigning identity, behavior, dependencies, and module ownership. Determine the concept's role in the affected model before choosing its implementation; verify domain identity and behavior rather than inferring them from storage shape.

- **Entity:** choose when continuity matters despite changing attributes. Define identity and equality across the lifecycle; a database key alone does not establish a domain need for identity. An immutable record can still represent an entity; distinguish it from a value object by meaning, not by methods or mutability.
- **Value object:** choose when attributes determine meaning. Use value equality and prefer immutability; replace a value rather than mutating an instance shared by owners.
  - The same concept can have different roles in different contexts: an address can be a delivery value or an independently tracked location.
- **Domain service:** use for a domain operation that has no natural entity or value-object owner. Express it in domain terms and keep it stateless; a function or module can implement it. Functions operating on entity or value data can still express behavior belonging to those concepts; do not group unrelated rules into a generic service.
- **Modules:** group cohesive domain concepts under meaningful names. Avoid technical grab bags and cyclic dependencies that obscure ownership.
- **Associations:** implement only needed navigation, direction, and multiplicity. A conceptual relationship does not require bidirectional object references.
