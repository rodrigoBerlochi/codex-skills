---
name: tdd
description: Use test-driven development with a red-green-refactor loop when implementing features or fixing bugs, especially when the user asks for TDD, test-first work, red-green-refactor, or behavior-focused tests through public interfaces.
---

# Test-Driven Development

## Source

Adapted for Codex from `mattpocock/skills/tree/main/tdd` (MIT License).

## Philosophy

Tests should verify behavior through public interfaces, not implementation details.

Good tests are integration-leaning: they exercise real code paths through public APIs and describe what the system does. They should usually survive internal refactors.

Bad tests are coupled to implementation. Warning signs include mocking internal collaborators, testing private helpers, or failing after a refactor that did not change behavior.

Use [references/tests.md](references/tests.md) for examples and [references/mocking.md](references/mocking.md) for boundary-mocking guidance.

## Anti-Pattern: Horizontal Slices

Do not write all tests first and all implementation afterward. That produces speculative tests that lock in imagined structure.

Prefer vertical slices:

```text
WRONG
RED:   test1, test2, test3
GREEN: impl1, impl2, impl3

RIGHT
RED -> GREEN: test1 -> impl1
RED -> GREEN: test2 -> impl2
RED -> GREEN: test3 -> impl3
```

Each test should respond to what was learned in the previous cycle.

## Workflow

### 1. Plan the slice

Before writing code:

- Inspect the repo's existing test tooling and conventions.
- Confirm or infer the public interface that should change.
- List the highest-value behaviors to test first.
- Identify chances to create [deep modules](references/deep-modules.md).
- Prefer interfaces that stay easy to test. See [references/interface-design.md](references/interface-design.md).

Ask the user for clarification only when interface or behavior expectations are materially ambiguous. Otherwise, proceed with the smallest sensible slice.

### 2. Write one failing test

Write one test for one behavior and run only the relevant test target if possible.

```text
RED: write one failing test
```

This tracer bullet should prove the path works end-to-end.

### 3. Write the minimum code to pass

Implement only enough to make the current test pass.

```text
GREEN: write the smallest implementation that passes
```

Rules:

- One test at a time.
- No speculative features.
- Keep tests focused on observable behavior.
- Re-run the narrowest useful test command first, then broader validation as confidence grows.

### 4. Refactor after green

Once the current slice is green, improve the design without changing behavior.

Look for:

- Duplication
- Shallow modules
- Unclear interfaces
- Logic that belongs deeper behind a simpler API

See [references/refactoring.md](references/refactoring.md).

Never refactor while red.

## Checklist Per Cycle

```text
[ ] Test describes behavior, not implementation
[ ] Test uses the public interface
[ ] Test would survive internal refactoring
[ ] Code is minimal for this test
[ ] No speculative behavior was added
[ ] Relevant tests were run
```
