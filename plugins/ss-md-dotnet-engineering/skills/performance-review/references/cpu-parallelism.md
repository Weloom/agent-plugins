## 6. CPU Parallelism and Partitioning

Use parallel execution only for independent CPU-bound work large enough to outweigh scheduling and coordination. It can reduce throughput or increase latency when work is small, uneven, or already parallelized.

- Use `Parallel.For`/`Parallel.ForEach` for suitable synchronous CPU-bound loops. Use `Parallel.ForEachAsync` for asynchronous iteration with bounded concurrency; it is not a reason to wrap CPU-bound work in `async`.
- Configure `ParallelOptions` when a maximum degree of parallelism or cancellation is required. Avoid nested parallelism and oversubscription; include other thread-pool and library work in the concurrency budget.
- Choose partitioning based on workload. Default partitioning is usually sufficient; consider range/static partitions for predictable uniform work or smaller/dynamic chunks for uneven work only when scheduling and load-balancing costs matter.
- Use `Partitioner<T>` or custom partitioning only when default partitioning demonstrably performs poorly or work distribution needs explicit control.
- Reduce contention by accumulating results locally and combining them after the loop rather than updating one shared collection or counter per item.
- For multi-stage asynchronous processing, consider `System.Threading.Tasks.Dataflow` or `Channel<T>` when coordination, bounded capacity, or backpressure is required. Do not introduce them for a simple, naturally bounded loop.
- Use `ParallelLoopState.Stop()` when no further iteration is useful and `Break()` when lower-index iterations must still be allowed to complete. Use these controls only when early termination is part of the actual requirement.
