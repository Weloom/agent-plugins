## 8. LINQ and Database Access

LINQ syntax is not itself evidence of a bottleneck. Database execution, query translation, data volume, and round trips are often more important than C# query syntax.

- Distinguish LINQ to Objects (`IEnumerable<T>`) from provider-backed queries (`IQueryable<T>`). Inspect generated SQL and query plans for EF Core or other providers when database performance is in question.
- Filter and project at the data source when it reduces transferred data. Investigate N+1 queries, loading unused columns/relations, missing indexes, and unnecessary round trips before micro-optimizing C# query syntax.
- Avoid repeated enumeration of expensive, stateful, or database-backed queries. Materialize with `ToList`/`ToArray` only when a snapshot, reuse, or ownership boundary requires it.
- Use `Any()` when only existence matters; use `Count` when the count itself is required. If a collection already exposes a cheap count, use it where appropriate.
- Preserve ordering, null handling, duplicate behavior, side effects, and provider translation when rewriting queries.
- Consider EF Core `AsNoTracking` for read-only queries when change tracking is unnecessary. Consider compiled queries only for measured, frequently executed query-compilation overhead; neither is a blanket default.
- Consider PLINQ only for sufficiently expensive independent CPU-bound in-memory work. Do not use it to parallelize database or I/O queries by default.
