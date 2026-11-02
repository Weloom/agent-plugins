## 10. File and Storage I/O

Use streaming and asynchronous I/O when data volume, latency, or concurrent operations make whole-file buffering or blocked threads costly.

- Use `FileStream` async methods with cancellation for asynchronous file operations. `FileOptions.Asynchronous` and `FileOptions.SequentialScan` are hints for relevant access patterns, not universal speed switches.
- Stream large files using `Stream`/`StreamReader`/`StreamWriter` rather than reading the entire content into memory when the operation can process incrementally.
- Use `System.IO.Pipelines` for high-throughput parsing/streaming when buffer management and partial reads are significant; it adds complexity and is unnecessary for ordinary file handling.
- Consider `RandomAccess` for measured concurrent/random access to files; use sequential streaming for sequential workloads.
- Add `BufferedStream` or custom buffering only when measurements show it helps beyond buffering already provided by the underlying stream or storage SDK.
- For cloud/object storage, use the provider SDK's streaming and transfer/concurrency options. Bound parallel transfers and buffers, and account for retries, request costs, and cancellation.
