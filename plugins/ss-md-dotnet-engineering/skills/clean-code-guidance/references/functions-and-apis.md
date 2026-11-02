## Functions and APIs

Functions should make behavior easy to understand at the call site and straightforward to change.

- Keep a function focused on one coherent responsibility. Split it when distinct behavior can be named and understood more clearly, not just to meet a size preference.
- Keep the function's steps at a consistent level of abstraction where practical. Separate high-level decisions from low-level details when mixing them obscures the flow.
- Make inputs and outputs understandable at the call site.
  - Avoid boolean flags when they make one call represent substantially different operations.
  - Group parameters only when they form a meaningful concept; do not create parameter objects just to reduce an argument count.
  - Avoid output parameters or hidden dependencies when they make data flow harder to follow.
- Make side effects visible. Separate state-changing commands from queries when combining them would surprise callers.
- Handle errors at a meaningful boundary. Keep recovery behavior close to the code that can make a recovery decision.
- Remove duplication when it represents the same rule or behavior. Do not unify similar-looking code if the cases have different responsibilities or reasons to change.
