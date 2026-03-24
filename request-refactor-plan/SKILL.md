---
name: request-refactor-plan
description: Create a detailed refactor plan with tiny, safe commits when the user wants to plan a refactor, write a refactoring RFC, scope a risky code change, or break a refactor into incremental steps before implementation.
---

# Request Refactor Plan

## Source

Adapted for Codex from:
https://github.com/mattpocock/skills/tree/main/request-refactor-plan

Original skill content licensed under MIT; adapted for Codex.

## Goal

Produce a concrete refactor plan that:

- explains the problem clearly
- defines scope and non-goals
- evaluates alternatives
- checks current code and test coverage
- breaks the work into the smallest practical commits

Use this skill when the user wants planning rather than immediate implementation, or when the refactor is risky enough that a written plan is the safer first step.

## Workflow

### 1. Gather the problem statement

Ask for the user's description of:

- the current problem
- why it is painful
- any solution ideas already considered
- constraints, deadlines, or compatibility requirements

If the user already provided enough detail, do not force another interview. Proceed and fill gaps only where they matter.

### 2. Inspect the codebase

Explore the relevant modules and verify the current state before proposing a plan.

Look for:

- current architecture and ownership boundaries
- coupling hotspots
- public interfaces that would change
- existing tests around the affected area

Do not rely only on the user's summary if the repository can be inspected directly.

### 3. Evaluate alternatives

Identify other viable approaches and explain the tradeoffs.

This is especially important when:

- the requested refactor may be larger than necessary
- a smaller interface change could solve the problem
- the refactor risks broad breakage or churn

Challenge weak assumptions directly but keep the discussion practical.

### 4. Tighten scope

Define:

- what will change
- what will not change
- which interfaces are in scope
- which behaviors must remain stable

If key details are missing, ask targeted follow-up questions. Prefer concrete boundaries over broad intent statements.

### 5. Review testing strategy

Inspect existing tests in the affected area and decide what confidence is missing.

Capture:

- which behaviors need coverage
- whether current tests are sufficient
- whether new tests should be added before, during, or after the refactor
- similar tests in the codebase that establish precedent

Prefer behavior-focused tests through public interfaces, not implementation-detail tests.

### 6. Break the work into tiny commits

Write the implementation plan as a sequence of small, safe commits. Each step should leave the codebase working.

Follow these rules:

- keep each commit narrow
- isolate mechanical renames from behavioral changes
- separate interface changes from deep internal cleanup where possible
- mention sequencing risks and rollback points when relevant

Prefer Martin Fowler style incremental refactoring over one large rewrite.

## Output Format

When delivering the plan, structure it like this:

```markdown
## Problem Statement

The developer-facing problem.

## Solution

The proposed solution and why it is preferred.

## Commits

A detailed implementation plan in tiny commits. Each commit should leave the codebase in a working state.

## Decision Document

Implementation decisions that were made, such as:

- modules to modify
- interfaces that change
- architectural decisions
- schema or API contract changes
- technical clarifications from the developer

Avoid brittle detail like exact file paths or code snippets unless the user explicitly asks for them.

## Testing Decisions

- what good tests should verify
- which modules or behaviors will be tested
- prior art or comparable tests in the codebase

## Out of Scope

What this refactor will not attempt.

## Further Notes

Optional follow-up notes, risks, or sequencing concerns.
```

## GitHub Issue

If the user wants the plan filed as a GitHub issue, prepare the issue body in the format above and create it only after the plan content is settled.
