## 13. Logging and Observability

Logging and telemetry can add formatting, allocation, I/O, and cardinality costs. Reduce overhead without removing operationally necessary information.

- Use `Microsoft.Extensions.Logging` structured templates rather than eager interpolation/concatenation. For frequently executed log sites, consider `LoggerMessage` source generation (`LoggerMessageAttribute`) to reduce repeated parsing and allocations.
- Guard expensive argument construction when the relevant log level is disabled; do not add checks around cheap arguments without evidence.
- Avoid per-item debug/info logging in hot loops. Prefer sampled, aggregated, or appropriately leveled events while preserving the signals needed for diagnosis.
- Use metrics for trends and service-level indicators; traces/profiles for locating work. Keep metric dimensions bounded and never include sensitive or high-cardinality values as labels.
- Use OpenTelemetry when cross-service traces/metrics/logs are needed. Compare production telemetry before/after system-level optimizations; a microbenchmark cannot represent service behavior.
- Do not remove useful logs or telemetry simply to reduce overhead; first consider log level, structured logging, sampling, and aggregation.
