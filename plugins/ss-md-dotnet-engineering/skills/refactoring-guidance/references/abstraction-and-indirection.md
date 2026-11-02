## Dead code, abstraction, and indirection

Keep abstractions for demonstrated value, not their size, usage count, or hypothetical future.

- **Remove genuinely unused code**, accounting for configuration, runtime discovery, and external consumers—not just static references. Preserve required declarations and compatibility hooks; uncertain reachability is not evidence for deletion.
- **Avoid speculative generality:** add variation points for current requirements or supported extensions, not imagined scenarios. One implementation can still justify an isolation boundary.
- **Make indirection earn its cost** through clearer intent, centralized rules, policy enforcement, or dependency isolation. Consolidate layers when an existing owner provides the same benefit with less forwarding and coupling.
- Remove a layer only if doing so preserves its useful policy and boundaries without scattering rules or exposing internals. Fewer files or calls alone do not establish simpler design.
