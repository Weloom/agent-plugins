## 3. Data Structures and Collections

Choose by required operations, ordering, lifetime, and concurrency semantics first; compare performance for the relevant access pattern. Do not assume a concurrent or specialized collection is faster than a simpler collection.

| Need | Consider |
|---|---|
| Key-based lookup                   |  `Dictionary<TKey,TValue>`;`ConcurrentDictionary<TKey,TValue>` when shared concurrent access is required | 
| Membership tests                    | `HashSet<T>` | 
| Indexed sequence                    | Array or `List<T>` | 
| FIFO processing                     | `Queue<T>`; `ConcurrentQueue<T>` when shared concurrent access is required | 
| LIFO processing                     | `Stack<T>`; `ConcurrentStack<T>` when shared concurrent access is required | 
| Unordered concurrent add/take       | `ConcurrentBag<T>` when its unordered, work-distribution semantics fit; not for ordering or predictable key lookup | 
| Stable, read-heavy lookup data      | `FrozenDictionary<TKey,TValue>` or `FrozenSet<T>` when construction cost is amortized | 
 

- Set initial capacity when you know the approximate size and avoiding growth is likely to matter; do not over-allocate based on a guess.
- Do not assume `struct`/`record struct`, custom collections, frozen collections, or concurrent collections are faster. Account for copying, boxing, mutation, equality, construction cost, and access patterns before changing representation.
- Consider `in T` or `ref readonly T` for large structs passed frequently only when profiling shows copy cost. Prefer `readonly struct`; by-reference parameters can make call sites and aliasing harder to reason about.
- A read-only view does not necessarily make its backing collection immutable.
- Prefer built-in collections unless profiling identifies a meaningful gap and a custom structure can be tested and maintained.
