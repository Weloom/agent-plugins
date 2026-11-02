## Tests

Tests should make intended behavior clear and make change safer, not merely increase test count.

- Test observable behavior and important contracts. Avoid coupling tests to private implementation details unless those details are themselves part of the contract.
- Focus each test on one behavior or a closely related set of outcomes. Use names and setup that make a failure's meaning apparent.
- Cover relevant boundary conditions and failure paths, especially those affected by the change or near known defects.
- Keep tests deterministic and independent. Isolate time, randomness, concurrency, and external services where practical.
- Use assertions that clearly express the expected result. Multiple assertions are appropriate when they describe one coherent behavior; avoid combining unrelated checks into one test.
- Follow the project's existing test structure and commands. Run focused tests for the changed behavior, then broader tests when the change's impact warrants it.
- Do not weaken or remove a test just to make a change pass. If a test is wrong or obsolete, establish why and update it to reflect the intended contract.
- Use test-first development when it improves feedback or design. Regardless of sequence, protect changed behavior with reliable tests.
