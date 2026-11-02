## 3. Folder and File Organization

Group by business capability, then use case or a meaningful technical responsibility:

```text
Domain\
  Ordering\
    Order.cs
    OrderLine.cs
    OrderStatus.cs
    OrderId.cs
    Events\
      OrderPlaced.cs
Application\
  Ordering\
    PlaceOrder\
      PlaceOrderCommand.cs
      PlaceOrderHandler.cs
      PlaceOrderValidator.cs
      PlaceOrderResult.cs
    Ports\
      IOrderRepository.cs
Infrastructure\
  Persistence\
    Configurations\
      OrderConfiguration.cs
    Repositories\
      OrderRepository.cs
```

**File rules**

- **MUST** declare exactly one named type per hand-written, type-bearing C# file. The filename matches the type name, including casing.
- This includes classes, interfaces, records, structs, enums, named delegates, and test/support types. **MUST NOT** declare nested types or additional top-level types. Having only one consumer is not an exception.
- **MUST NOT** split a hand-written type across partial declarations. Exclude generated code and framework-required generated partial companions from this restriction.
- Files containing only global usings or assembly/module attributes, and top-level entry points, are not type-bearing files. **MUST NOT** use that exception to add extra types.
- **MUST NOT** make a type public merely because it moves to its own file. Prefer `internal` for implementation details; recognize that extracting a private nested type broadens its visibility.

**Folder rules**

- **SHOULD** keep related types together rather than create project-wide `Enums`, `Records`, `Interfaces`, or `Models` folders.
- **SHOULD** subdivide a growing area by meaningful concepts, such as `Ordering\Orders` and `Ordering\Returns`, not an arbitrary file-count threshold.
- **MUST NOT** create empty speculative folders. Keep `Common` small and admit only genuinely shared responsibilities.
- **SHOULD** align namespaces with code folders, excluding repository containers such as `src` and `tests`.
