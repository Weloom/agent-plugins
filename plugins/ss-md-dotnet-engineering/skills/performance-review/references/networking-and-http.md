## 11. Networking and HTTP

Network latency, connection management, and payload size often dominate. Optimize the measured path while preserving HTTP/network endpoints, message formats, and retry semantics.

- Use `IHttpClientFactory` or an appropriately long-lived `HttpClient`/handler; avoid creating one client per request. Set connection lifetime to fit DNS and deployment behavior.
- Define timeouts and cancellation. Retry only transient failures when the operation is safe to repeat; bound attempts and backoff, and avoid multiplying retries across layers.
- Stream large request/response bodies when full buffering is unnecessary. Avoid redundant buffering and copies; bound buffers so slow consumers cannot cause unbounded memory use.
- Measure before replacing high-level .NET HTTP clients with raw sockets or `SocketAsyncEventArgs`; lower-level networking APIs add state, lifetime, and error-handling costs.
- Compare serialization/compression end-to-end across CPU, allocations, payload size, and realistic network conditions---not only isolated serializer speed or encoded size.
- For large transfers, preserve framing, message-size limits, partial read/write handling, cancellation, resume, and security constraints.
