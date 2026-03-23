# Reference

## Dependency Categories

When assessing a candidate for deepening, classify its dependencies.

### 1. In-process

Pure computation or in-memory state with no I/O.

This is almost always deepenable directly. Merge the modules and test the resulting boundary.

### 2. Local-substitutable

Dependencies that have realistic local stand-ins, such as an in-memory filesystem or a local database substitute.

Deepen the module if the substitute is good enough for the tests. Test the deepened boundary with the stand-in.

### 3. Remote but owned

Your own services across a network boundary.

Prefer a ports-and-adapters shape:

- define a port at the module boundary
- keep the core logic in the deep module
- inject transport-specific adapters
- test with an in-memory adapter

### 4. True external

Third-party services you do not control.

Mock only at that boundary. The deep module should depend on an injected port for the external integration.

## Testing Strategy

Core principle: replace, do not layer.

- old shallow unit tests often become redundant once strong boundary tests exist
- new tests should verify observable behavior at the deepened module boundary
- tests should survive internal refactors
- assertions should target public outcomes, not internal wiring

## Refactor Proposal Template

```markdown
## Problem

Describe the architectural friction:

- which modules are shallow and tightly coupled
- what risk exists in the seams
- why the area is hard to navigate or maintain

## Proposed Interface

Describe the chosen interface:

- its shape
- how callers use it
- what complexity it hides

## Dependency Strategy

State which category applies and how dependencies are handled.

## Testing Strategy

- boundary behaviors to verify
- shallow tests that become redundant
- environment or stand-ins required for testing

## Implementation Recommendations

Durable guidance that is not tied too tightly to current file paths:

- what the module should own
- what it should hide
- what it should expose
- how callers should migrate
```
