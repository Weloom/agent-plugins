## 15. Reflection, Interop, and Hardware-Specific Paths

These approaches can address specialized constraints but increase complexity, compatibility, or safety costs. Use them only for a demonstrated need that ordinary managed code or framework/package APIs cannot meet.

- Avoid repeated reflection or reflective invocation in hot paths. Cache metadata/delegates when appropriate, or use source generators/compile-time registration when dynamic discovery is not required. Reflection at startup or for genuinely dynamic extensibility may be appropriate.
- Isolate native interop and `unsafe` code behind a small boundary. Verify ABI, ownership, pinning duration, errors, platform support, and shutdown; use `SafeHandle` for native handles.
- Prefer source-generated interop such as `LibraryImport` when supported and appropriate, but benchmark the complete call path rather than assuming it is faster.
- Consider GPU acceleration or hardware intrinsics only for sufficiently large, parallel workloads. Include data transfer, setup, synchronization, hardware availability, deployment, and fallback costs; retain a portable path when required.
- Keep specialized code only when an end-to-end, production-representative comparison shows a meaningful win that justifies testing and maintenance.
