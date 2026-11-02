## 2. Allocations, Garbage Collection, and Object Lifetimes

Use this section when profiles show allocation pressure, GC pauses, retained memory, or resource leaks. A nonzero allocation count alone is not a problem.

- Focus on frequent allocations in hot paths or large and long-lived allocations that materially affect the workload. Investigate temporary objects, repeated conversions, closures, boxing, and string construction when they show up in measurements or are clearly unnecessary.
- Prefer straightforward string interpolation or concatenation for a few known parts. For repeated appends in a loop, consider `StringBuilder`; use lower-allocation formatting techniques only when formatting is measured as significant. Avoid quadratic repeated concatenation.
- Investigate retained object graphs as well as allocation rate. Treat LOH and POH behavior as diagnostic concerns; address repeated large allocations or long-lived pins when traces show impact.
- Dispose owned `IDisposable`/`IAsyncDisposable` resources deterministically (`using`/`await using`). Use `SafeHandle` for native handles; finalizers are not a general substitute for deterministic cleanup.
- Change GC mode, latency settings, or heap limits only after measuring the deployed workload and understanding effects on pauses, throughput, and memory.
