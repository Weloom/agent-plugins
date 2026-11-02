## Separate calculations from effects

**Use when:** I/O, hidden inputs, or changing state obscure a calculation or decision.
**Gain:** explicit inputs and results let readers understand and test the rule independently of execution. This section separates responsibilities; the delegates and composition sections explain how to supply and combine behavior.

- **Calculate, then execute.** Separate eligibility, pricing, allocation, or proposed changes from database writes, messages, file operations, and external calls. Return a meaningful decision or proposed change; let orchestration apply it.
  - Preserve the consistency boundary. If a decision depends on state that can change before execution, retain the transaction, concurrency check, or revalidation needed to keep it valid.
  - Do not split one invariant-preserving operation into independently callable steps that allow invalid intermediate states.
- **Pass relevant facts explicitly.** Supply the calculation with the time, rates, policies, and data it actually needs. Obtain them at the application boundary rather than reading a clock, random generator, global configuration, or mutable service inside the calculation.
  - Pass a captured timestamp when the calculation needs one time value, not a clock abstraction that it can query repeatedly.
  - Do not pass an entire service container or infrastructure service when a value suffices. Supply a function only when the calculation genuinely needs variable behavior; a callback that reads changing external state does not make the calculation pure.
- **Do not mutate calculation inputs.** Produce a result rather than altering arguments or objects reached through them. If in-place processing is the actual contract, name and document that effect instead of presenting it as a calculation.
- **Keep effects evident from the contract.** A method that reads like a query must not unexpectedly save data or trigger actions. Encapsulation may hide execution details, but not significant mutation, failure, or ordering requirements.
- **Use ordinary C# structure.** Named methods and local functions can separate calculation from execution without delegates or new classes. Use `Task<T>` for asynchronous results and await effectful operations in orchestration; asynchronous execution does not imply purity.
- **Preserve necessary sequencing.** Do not run independent-looking delegates concurrently until their ordering, shared state, and external constraints are understood. Separating decisions from execution does not authorize parallelization.
