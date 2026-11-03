## Classes, modules, and responsibility

This section helps assess whether code is cohesive and whether changes will remain localized.

- Keep each class or module centered on a clear responsibility. Its contents should relate to a common purpose or reason to change.
- Split a component if it can help create a clearer boundary or limit unrelated change. Do not split it merely to achieve a preferred class or file size.
- Encapsulate state and invariants when that prevents callers from depending on internal details.
- Keep dependencies explicit. Avoid coupling components that do not need to know about each other.
- Isolate likely sources of change behind stable interfaces when that reduces impact. Do not add interfaces or layers without a concrete benefit.
- Choose conditional logic or polymorphism based on which makes the current domain clearer. Do not introduce a hierarchy solely to eliminate a simple conditional.
