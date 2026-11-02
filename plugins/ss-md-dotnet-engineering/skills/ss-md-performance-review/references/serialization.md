## 12. Serialization

Serialization can dominate CPU, allocations, startup, and network/storage payload costs. Change serializers or formats only when end-to-end measurements justify it and compatibility is preserved.

- Prefer `System.Text.Json` for standard JSON where it meets the contract. Use `JsonSerializerContext` source generation when startup, trimming, Native AOT compatibility, or repeated metadata/reflection costs matter.
- Use `Utf8JsonWriter` or stream-based `JsonSerializer` APIs when avoiding intermediate strings or whole-payload buffers is important; preserve encoding, escaping, and wire-format behavior.
- Consider binary serializers (for example, protobuf implementations) only when payload size/throughput requirements justify the dependency and the schema/versioning contract is explicit. Do not switch formats as an invisible internal optimization if clients depend on the existing wire format.
- Benchmark representative object graphs, payload sizes, cold start, throughput, allocations, and compatibility. Include compression and transport costs in end-to-end comparisons.
- Do not replace a serializer solely because a microbenchmark reports a faster result on a different object model or workload.
