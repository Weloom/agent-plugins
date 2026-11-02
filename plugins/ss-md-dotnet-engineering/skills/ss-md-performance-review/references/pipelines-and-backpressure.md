## 9. Pipelines, Channels, and Backpressure

Use these when producers and consumers or processing stages need explicit coordination. The main benefit is often bounded resource use and flow control, not raw speed.

- Use bounded `Channel<T>` for lightweight asynchronous producer/consumer communication. Choose wait, drop, or reject behavior based on whether completeness or freshness matters.
- Use TPL Dataflow when a multi-stage message pipeline, block linking, completion propagation, or per-block parallelism makes the design clearer than manual task coordination.
- Use `ActionBlock<T>` for independent action processing when its bounded capacity, ordering, and parallelism options fit the requirement.
- Batch when it amortizes fixed per-item costs, but cap batch size and wait time to protect latency and memory.
- Prefer a simple loop or a small, bounded set of tasks for straightforward workflows. Do not add a pipeline abstraction solely for performance.
- Use single-reader/single-writer optimizations only when those constraints hold through normal operation, failure, and shutdown.
