---
name: coupling-analysis
description: Analyze coupling between modules using integration strength, distance, and volatility. Use when the user asks whether modules are too coupled, wants a dependency or integration-quality review, needs decoupling candidates, or wants an architectural health assessment.
---

# Coupling Analysis

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(architecture)/coupling-analysis

The upstream repository is MIT-licensed for source code, and its `SKILL.md` content is described in the repository `LICENSE` as CC BY 4.0 unless otherwise specified.

## Goal

Analyze a codebase using the three-dimensional coupling model from _Balancing Coupling in Software Design_:

1. Integration strength: what is shared between components
2. Distance: where the coupling lives
3. Volatility: how often the components change

Use this to decide whether modules should stay separate, be merged, be wrapped in a stronger contract, or be redesigned around a cleaner boundary.

## Core Model

The guiding balance rule is:

```text
BALANCE = (STRENGTH XOR DISTANCE) OR NOT VOLATILITY
```

A design is usually balanced when:

- strong coupling stays local
- distant components interact through weak contracts
- stable components can tolerate stronger coupling better than volatile ones

Maintenance risk increases when coupling is strong, distant, and volatile at the same time.

## When To Use

Apply this skill when the user wants to:

- analyze coupling or architectural health
- understand why changes cascade across modules
- identify decoupling or merging opportunities
- review dependency quality between packages, services, or layers

Do not use this as a substitute for domain-boundary design or component-sizing analysis when the real question is business capability decomposition.

## Process

### 1. Gather context

Clarify or infer:

- the scope of analysis
- the abstraction level: functions, classes, packages, services
- whether git history is available
- which areas are core business logic versus generic support

Business context matters because volatility is not only technical. Core business areas usually change more than support or generic infrastructure.

### 2. Build the structural map

For each relevant module, record:

- name and location
- primary responsibility
- direct dependencies

Build a directed dependency graph where `A -> B` means `A` depends on `B`.

Remember that the flow of knowledge is opposite the arrow: `B` exposes something that `A` must know about.

### 3. Assess distance

Estimate distance from the nearest shared boundary:

- same function or method: minimal
- same class or object: very low
- same package or namespace: low
- same library or deployable unit: medium
- different services: high
- different systems or organizations: maximum

If separate teams own the modules, increase the effective distance.

### 4. Classify integration strength

For each dependency, classify the strongest applicable type.

#### Intrusive coupling

The downstream depends on internals that were not designed as a public integration surface.

Signals:

- reflection or private-member access
- reading another service's database directly
- monkey-patching internals
- dependence on internal config or file structure

This is the strongest and usually the worst form.

#### Functional coupling

Modules share business behavior or workflow constraints.

Key forms:

- sequential: order matters
- transactional: success or failure must happen together
- symmetric: the same rule or algorithm is duplicated and must stay synchronized

Signals:

- duplicated business logic
- comments like "remember to update X when Y changes"
- coordinated deployments for one behavior change
- cascading failures when one rule changes

#### Model coupling

The upstream exposes its internal model, and the downstream learns more than it actually needs.

Signals:

- sharing rich internal domain objects
- exposing internal enums, codes, or field names directly
- returning broad internal DTOs where only a narrow contract is required

#### Contract coupling

The upstream exposes an intentional, integration-specific contract separate from its internal model.

Signals:

- dedicated DTOs or snapshots per use case
- versioned interfaces
- simple public types
- explicit adapter, facade, anti-corruption, or published-language patterns

This is usually the healthiest form.

### 5. Estimate volatility

Use the best available signals:

- business domain type: core, supporting, generic
- git history and co-change patterns
- TODO or FIXME density
- API version churn
- comments indicating evolving business rules

Increase the apparent volatility of a supporting area if changes repeatedly propagate into it from a volatile core area.

### 6. Diagnose balance

Use a simple maintenance heuristic:

```text
MAINTENANCE_EFFORT = STRENGTH × DISTANCE × VOLATILITY
```

Treat this qualitatively rather than numerically.

High strength + high distance + high volatility is critical.

High strength + low distance is often acceptable or even good cohesion.

Low strength + high distance is usually healthy loose coupling.

Low strength + low distance can still signal unnecessary local fragmentation.

## Report Format

Structure the output like this:

```markdown
## Executive Summary

- modules analyzed
- dependencies mapped
- critical and moderate issues
- overall health assessment

## Dependency Map

Show the important edges with their coupling type.

## Issues

For each important issue:
- modules involved
- coupling type
- evidence
- strength, distance, volatility
- why this matters
- recommendation

## Positive Patterns

Call out good contracts, good encapsulation, and strong local cohesion.

## Prioritized Recommendations

- high priority
- medium priority
- low priority
```

## Heuristics

Ask:

- If an internal detail changes, who else must change?
- Was this contract intentionally designed, or did consumers leak into internals?
- Do modules that change together live together?
- Are distant components forced to share volatile details?
- Is there duplicated business logic that should become one owned capability?

## Recommendations

Typical fixes:

- intrusive coupling: create an explicit boundary and stop depending on internals
- functional symmetric coupling: centralize the shared rule or explicitly isolate ownership
- model coupling: replace internal models with integration contracts
- unhealthy local fragmentation: merge modules into a deeper one
- unhealthy distant coupling: weaken the contract and reduce shared assumptions

## Limitations

- Volatility is more reliable with git history than static inspection alone.
- Symmetric functional coupling often requires semantic reading, not just import graphs.
- Team boundaries and organizational distance may require user input.
- Runtime timing and identity coupling may not be visible from static code alone.
