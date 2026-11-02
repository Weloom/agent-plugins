## Verification and evidence

Choose checks for the diagnosed mechanism and requirement, not just the easiest metric to collect.

- Establish a baseline for existing behavior when feasible. For new functionality, test against the agreed constraints and a suitable comparison when relevant; do not invent a before/after result.
- Use isolated benchmarks for local CPU or allocation questions, load tests for latency and capacity, and sustained runs for retention or resource growth. Include warmup, sample duration, cold/warm caches, payload distribution, and representative concurrency when they affect interpretation.
- Test thresholds as specified, including units, percentiles, measurement scope, and operating conditions. If both latency and memory are constrained, verify both. A configured worker limit or passing unit test does not demonstrate throughput or a memory ceiling.
- Check results, errors, ordering, cancellation, disposal, shutdown, and shared-state invariants as applicable. Controlled interleavings can test known race scenarios; a clean benchmark or stress run alone does not prove thread safety.
- For overload or dependency degradation, exercise bounded queueing, timeouts, cancellation, and recovery as relevant. Check whether backlogs drain and resources are released. Use an authorized, isolated environment; do not load-test production or third-party systems without permission.
- Keep runtime, build mode, hardware, data, and load comparable. Record material differences and measurement variability rather than compare unrelated runs as proof of improvement.
- Report the target, observations, verification conditions, trade-offs, and remaining gaps. If tools, a representative environment, or sufficient evidence are unavailable, distinguish implementation from verified compliance and state the remaining check. Do not fabricate numbers or silently relax the threshold.
- Do not add a benchmark framework, observability stack, dependency, or load-test service for every small improvement. Prefer existing tooling and the smallest sufficient check; straightforward, low-risk inefficiencies do not require a benchmark.
