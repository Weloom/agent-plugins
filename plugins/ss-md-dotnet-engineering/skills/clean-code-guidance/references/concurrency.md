## Concurrency and asynchronous code

Concurrency guidance matters when work can overlap or share mutable state; do not impose it on unrelated synchronous code.

- Minimize shared mutable state and make ownership of shared data clear.
- Prefer independent tasks and isolated or immutable data when they reduce coordination.
- Understand the project's concurrency primitives and execution model. A thread-safe collection does not automatically make a sequence of operations safe.
- Keep locks and other critical sections small. Avoid calling unknown, blocking, or reentrant work while holding a lock.
- Make cancellation, timeout, failure, and shutdown behavior explicit. Ensure concurrent work has a clear lifecycle.
- Test relevant ordering, race, and failure cases. Treat intermittent failures as possible evidence of a concurrency defect, not as noise to ignore.
