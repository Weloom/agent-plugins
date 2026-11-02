## 5. Async/Await, Tasks, and Cancellation

Async primarily avoids occupying a thread while supported I/O is pending; it does not make I/O or CPU work intrinsically faster. Choose the execution model based on the work and bound concurrency.

- Use asynchronous .NET I/O APIs end-to-end where supported; avoid `.Result`, `.Wait()`, and sync-over-async. Do not wrap naturally asynchronous I/O in `Task.Run`.
- Use `Task.Run` for deliberate CPU offloading only when the application model benefits (for example, keeping a UI responsive). Server-side CPU work usually needs bounded parallelism, not one queued task per request.
- Choose concurrency based on the number and nature of operations:
    - For a small, known set of independent asynchronous operations, use `Task.WhenAll` when downstream capacity allows it.
    - For large or unbounded input, use bounded workers, `Parallel.ForEachAsync`, a bounded `Channel<T>`, or Dataflow rather than creating a task for every item.
    - For sequential or dependent operations, keep them sequential; concurrency does not help when operations depend on one another.
- Propagate `CancellationToken` through supported operations. The owner creates and cancels/disposes `CancellationTokenSource`; callees observe the token and generally should not cancel a caller-owned source. Link tokens only when combining cancellation scopes.
- Use `ValueTask<T>` only when synchronous completion is common and task allocation is measured as material; its consumption rules are more restrictive than `Task<T>`.
- Return an existing task directly only when doing so preserves exception timing, disposal, and control-flow semantics.
- Use `ConfigureAwait(false)` when library code need not resume on a captured context, not as a general performance switch.
