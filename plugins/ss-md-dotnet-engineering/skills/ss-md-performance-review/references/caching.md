## 14. Caching

Caching trades computation or remote round trips for memory, staleness, consistency, and serialization. Use it only when reuse and cost are demonstrated and the consistency contract permits it.

- Use `IMemoryCache`/`MemoryCache` for bounded process-local reuse; define expiration, size limits, invalidation, and cache-miss behavior. It is not shared across service instances.
- Use `IDistributedCache` with a provider such as Redis when instances need a shared cache. Account for network latency/failure, serialization/deserialization, TTL, invalidation, key versioning, and consistency; a distributed cache may be slower than recomputation for small values.
- Consider `HybridCache` where supported by the target framework/packages when both local and distributed caching are useful; verify its stampede protection, serialization, and invalidation behavior against application requirements.
- Include every result-affecting dimension in keys (such as tenant, authorization, locale, and version). Bound memory, handle concurrent cache misses/stampedes, and avoid caching sensitive or rapidly changing values unless explicitly safe.
- Do not cache cheap work or add a cache before establishing a reuse pattern and invalidation strategy.
- Choose the simplest cache that satisfies the sharing, consistency, lifetime, and deployment requirements; do not introduce distributed caching when process-local caching or recomputation is sufficient.
