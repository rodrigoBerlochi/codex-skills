---
name: improve-codebase-architecture
description: Explore a codebase for architectural improvements that deepen shallow modules, improve testability, reduce coupling, and make the system easier to navigate. Use when the user wants architecture review, refactoring candidates, tighter module boundaries, or a more AI-navigable codebase.
---

# Improve Codebase Architecture

## Source

Adapted for Codex from:
https://github.com/mattpocock/skills/tree/main/improve-codebase-architecture

Original skill content licensed under MIT; adapted for Codex.

## Goal

Explore a codebase the way an implementation agent experiences it, surface architectural friction, and propose refactors that deepen shallow modules.

A deep module has a small interface hiding substantial implementation complexity. Deep modules tend to be easier to test, easier to reason about, and easier to navigate than clusters of thin modules with leaky seams.

Use [references/reference.md](references/reference.md) for dependency categories, testing strategy, and the RFC template.

## Process

### 1. Explore the codebase

Navigate the codebase organically and treat friction as signal.

Look for:

- concepts split across too many files
- shallow modules whose interface is nearly as complex as their implementation
- internal helper extraction done mainly for testability rather than design clarity
- tightly coupled modules with brittle seams
- areas that are untested or difficult to test through a public boundary

Do not force rigid heuristics. The question is where the architecture makes understanding or change harder than it should be.

### 2. Present candidate deepening opportunities

Present a numbered list of promising candidates. For each candidate, include:

- cluster: the modules or concepts involved
- why they are coupled: shared types, repeated call patterns, split ownership of one concept
- dependency category: based on [references/reference.md](references/reference.md)
- test impact: which current tests could be replaced by boundary tests

Do not jump to an interface proposal yet. First confirm which candidate the user wants to explore.

### 3. Frame the problem space

For the chosen candidate, explain:

- the constraints the new interface must satisfy
- the dependencies it must work with
- a rough illustrative sketch of the kind of boundary being designed

This sketch is for grounding, not for prematurely locking in one design.

### 4. Design multiple interfaces

Generate multiple materially different interface designs. When helpful, use sub-agents or parallel exploration to produce alternatives.

Bias the designs around different constraints:

- minimal interface: 1-3 entry points if possible
- maximum flexibility: broader extensibility for varied callers
- common-case optimized: make the default path trivial
- ports and adapters: when cross-boundary dependencies dominate

For each design, provide:

1. interface signature in plain English
2. a usage example
3. the complexity hidden internally
4. the dependency strategy
5. the tradeoffs

Then compare the designs and give a recommendation. Be opinionated. If the best answer is a hybrid, say so explicitly.

### 5. Turn the recommendation into an actionable plan

Once an approach is chosen, prepare a refactor proposal that captures:

- the problem
- the chosen interface
- the dependency strategy
- the testing strategy
- implementation recommendations

Use the template in [references/reference.md](references/reference.md).

If the user wants a GitHub issue, create it only after the contents are settled.

## Principles

- Prefer deeper modules over thin orchestration layers.
- Prefer testing at the module boundary over testing shallow internal seams.
- Replace redundant shallow tests once better boundary tests exist.
- Separate architectural guidance from brittle file-path detail unless the user explicitly asks for file-level planning.
