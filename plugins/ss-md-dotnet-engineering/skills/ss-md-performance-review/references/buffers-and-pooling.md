## 4. Buffers, Spans, and Pooling

These techniques can reduce copying and allocation, but introduce stricter lifetime, ownership, and reset requirements. Use them when data movement or repeated buffer allocation is a meaningful cost---not simply because the APIs are available.

- Use `Span<T>`/`ReadOnlySpan<T>` for synchronous access to contiguous memory when avoiding a copy or allocation matters. Use `Memory<T>`/`ReadOnlyMemory<T>` when the view must be stored or remain valid across an `await`.
- Use `ref struct` only when stack-bound lifetime or non-escaping state is required. Respect language/runtime restrictions on fields, captures, boxing, and async/iterator use.
- Consider `ArrayPool<T>` when repeated buffer allocation is costly. Return each rental exactly once, including on exceptions; process only the logical length, and clear sensitive contents or retained references when required.
- Consider `ObjectPool<T>`/`DefaultObjectPool<T>` (`Microsoft.Extensions.ObjectPool`) only when object construction/allocation is measured as costly and instances can be reset and safely reused. Pooling is not a cache and does not guarantee reuse.
- Use `stackalloc` only for small, bounded sizes---not directly from untrusted or unbounded input.
- Prefer safe span-based and framework/package APIs over `unsafe` or pointers unless profiling justifies the added risk.
- Compare these techniques with ordinary arrays, strings, streams, and other straightforward managed APIs. The simpler approach is usually preferable when the measured difference is insignificant.
