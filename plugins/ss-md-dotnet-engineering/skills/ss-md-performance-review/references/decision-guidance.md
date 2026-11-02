# .NET Performance Guidelines

Use these guidelines when implementing, diagnosing, reviewing, or improving .NET code against workload and resource constraints. Meet the required operating conditions with the simplest correct, reliable design---not maximum speed at any cost. Preserve functionality and public contracts; change behavior only when an explicit requirement authorizes it or an optimization requires a documented and approved trade-off.

Distinguish a demonstrated bottleneck, a clear avoidable inefficiency, a correctness defect, an explicit capacity requirement, and a speculative optimization. Follow the repository's target framework, supported platforms, deployment model, and architecture.

For a non-obvious optimization, add a brief nearby comment only when future readers cannot infer its purpose; state the constraint or bottleneck and any non-obvious trade-off. Put benchmark evidence and verification in the change description rather than duplicating it in code comments.

## Optimization boundaries and decision-making

- Prefer simple, idiomatic modern .NET code. Do not optimize code merely because a theoretically faster alternative exists.
- Fix obvious, low-risk inefficiencies when the improvement is straightforward and preserves behavior. Do not require a benchmark for every minor improvement.
- Prioritize algorithmic complexity, unnecessary repeated work, database access, network I/O, blocking, and resource contention before low-level allocation optimizations.
- When a relevant choice has materially different alternatives, consider those alternatives before selecting an implementation. Do not default to the last technique used or the newest available API.
- Compare alternatives against the actual workload: CPU-bound vs. I/O-bound, synchronous vs. asynchronous, bounded vs. unbounded, read-heavy vs. write-heavy, sequential vs. concurrent, and expected data size and lifetime.
- Consider performance, resource consumption, correctness, ownership and lifetime, complexity, compatibility, and operational implications. Prefer the simplest option that meets the requirement.
- Do not investigate unrelated techniques or perform exhaustive comparisons where alternatives have no meaningful relevance to the problem.
- Do not introduce custom data structures, pooling, spans, unsafe code, parallelism, caching, or architectural abstractions without a concrete reason.
- Distinguish performance improvements from general code-quality improvements.
- When no meaningful optimization opportunity exists, leave the code unchanged.
