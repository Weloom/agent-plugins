---
name: performance-review
description: "Design, diagnose, and improve .NET code for speed, latency, throughput, CPU, memory budgets, or workload capacity. Use for explicit performance thresholds, profiling or optimization requests, resource exhaustion, hangs, contention, concurrency or parallelism risks, and overload-related stability or availability. Not for every async call or collection; general failover and disaster recovery need broader reliability analysis."
user-invocable: true
disable-model-invocation: false
---

# Meet performance and resource constraints

**Meet the required workload and resource constraints with the simplest correct, reliable design, not maximum speed at any cost.** Use for new implementation as well as diagnosis and optimization. `/performance-review` supports deliberate investigation; automatic activation requires a relevant symptom, explicit requirement, or concrete implementation risk.

## Establish constraints and diagnose

Read [decision guidance](./references/decision-guidance.md), [workload and operational boundaries](./references/workload-and-thresholds.md), and [the optimization workflow](./references/optimization-workflow.md).

Establish the operating conditions, metric, threshold, and relevant failure conditions. Trace the affected path and shared resources, not just the slow-looking method. Classify the problem: CPU cost, I/O, allocation, retained memory, contention, saturation, or correctness. Follow the workflow to compare relevant alternatives, implement a coherent change, verify, and reassess.

Ask when missing requirements materially affect the solution. Exploratory diagnosis can proceed without a numeric target, but cannot establish compliance with an unspecified threshold. Do not invent budgets or assume concurrency settings prove capacity.

## Load only relevant technical guidance

These are separate bundled files, not heading links into the full guideline.

| Diagnosed mechanism or constraint | Reference |
|---|---|
| Startup, publish mode, JIT, trimming, or AOT | [Runtime and deployment](./references/runtime-and-deployment.md) |
| Allocation pressure, retention, GC, or owned-resource leaks | [Memory and lifetimes](./references/memory-and-lifetimes.md) |
| Lookup, enumeration, collection operations, or representation | [Collections](./references/collections.md) |
| Copying, buffers, spans, pooling, or stack-bound lifetimes | [Buffers and pooling](./references/buffers-and-pooling.md) |
| Blocking, asynchronous I/O, task fan-out, or cancellation | [Async and cancellation](./references/async-and-cancellation.md) |
| Independent CPU work, partitioning, or oversubscription | [CPU parallelism](./references/cpu-parallelism.md) |
| Shared-state invariants, races, locks, or contention | [Synchronization](./references/synchronization.md) |
| Query translation, database round trips, or repeated enumeration | [Queries and databases](./references/queries-and-databases.md) |
| Producers outrun consumers, queues grow, or stages need flow control | [Pipelines and backpressure](./references/pipelines-and-backpressure.md) |
| Large files, buffering, transfer concurrency, or storage I/O | [File and storage I/O](./references/file-and-storage-io.md) |
| HTTP connections, timeouts, retries, or payload transfer | [Networking and HTTP](./references/networking-and-http.md) |
| Serialization CPU, payloads, wire compatibility, or metadata | [Serialization](./references/serialization.md) |
| Telemetry overhead or missing service-level evidence | [Logging and observability](./references/logging-and-observability.md) |
| Repeated expensive work with demonstrated reuse | [Caching](./references/caching.md) |
| Reflection, interop, unsafe code, intrinsics, or accelerators | [Specialized paths](./references/specialized-paths.md) |

## Verify the requirement, not a proxy

Before choosing checks, read [verification and evidence](./references/verification-and-evidence.md). Select correctness, benchmark, load, sustained-resource, or failure tests for the actual mechanism and threshold. Respect authorization and environment limits; do not run disruptive load against production or third parties without permission.

Check collateral constraints: faster batch processing is not a win if it exhausts the database pool or makes interactive requests unavailable. Benchmarks do not prove thread safety, availability, or worst-case real-time guarantees. Report the target, evidence, conditions, trade-offs, and unmet or unverified requirements; never fabricate measurements.

## Scope and stopping conditions

- Preserve functionality, contracts, ordering, cleanup, and failure semantics except for explicitly authorized changes. Do not silently drop work, weaken consistency, increase timeouts, or retry more to make a symptom disappear.
- Bound active work and queueing against shared capacity, including concurrent callers. More parallelism is not a default optimization.
- Fix clear low-risk inefficiencies without mandatory benchmarking. For non-obvious changes, require evidence proportional to the claim; do not introduce pooling, unsafe code, caching, custom structures, or new dependencies without a concrete need.
- Stop tuning when constraints are met; leave code unchanged when no useful improvement is supported. If verification is unavailable, state the gap rather than claim completion.
- Resource- and execution-related stability belongs here. Failover, disaster recovery, deployment continuity, and broader availability objectives require additional reliability or infrastructure analysis, not a claim that this skill covers them.
- Consult refactoring or architecture guidance only when the solution genuinely needs structural or boundary changes. Respect review- or planning-only requests; ask before materially expanding authorized scope.
- If shared mutation causes the diagnosed contention, consult `functional-csharp` to evaluate ownership, pure calculations, or immutable snapshots as alternatives. Also use it to preserve established calculation boundaries in affected code. Include copying, allocation, consistency, and lifetime costs; functional style is not automatically faster. Use `clean-code-guidance` only when a separate clarity decision remains unresolved.
- A handoff identifies evidence and an unresolved decision, not a mandatory peer-loading sequence or another agent. Reuse loaded guidance; do not return to the source skill for the same decision. If a peer is unavailable, report a material limitation rather than invent its guidance.

The bundled references are maintained with this plugin. Read only the extracts needed for the current workload.
