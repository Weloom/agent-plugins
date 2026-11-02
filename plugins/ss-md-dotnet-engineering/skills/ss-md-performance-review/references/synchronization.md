## 7. Synchronization and Thread Safety

Correctness comes before throughput. Choose a primitive that matches the scope and operation; do not replace synchronization with a faster-looking primitive unless the whole invariant remains safe.

- Prefer single ownership, immutable state, or message passing when practical; they can avoid both locks and race conditions.
- Use C# `lock` for short synchronous critical sections over shared in-process state, with a private lock object (or `System.Threading.Lock` where supported).
- Use `Monitor` directly only when its additional features---such as timed acquisition or condition coordination---are needed. Do not mix `Monitor` calls with a `lock` on the same object without a clear design.
- Use `SemaphoreSlim` for asynchronous mutual exclusion or bounded in-process concurrency. Use `Mutex` only when mutual exclusion must cross process boundaries, accepting its greater OS synchronization cost.
- Use `Interlocked` for simple atomic operations. It does not make a multi-step invariant atomic; `volatile` does not replace a lock or make compound operations safe.
- Keep critical sections short; do not `await` inside `lock`. For async mutual exclusion, use an async-compatible primitive and release it in `finally`.
- Treat lock-free code as advanced: consider it only when contention is measured and memory ordering, progress guarantees, retries, starvation, and correctness can be validated.
- Do not change synchronization primitives solely to pursue theoretical throughput gains. Validate races, cancellation, shutdown, and failure paths; benchmarks do not establish thread safety.
