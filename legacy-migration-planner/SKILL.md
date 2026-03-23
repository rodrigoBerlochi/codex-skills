---
name: legacy-migration-planner
description: Plan legacy system migrations, modernization efforts, monolith decomposition, consolidation, rewrites, or framework upgrades. Use when the user wants an incremental migration strategy, strangler-fig style planning, or a migration roadmap rather than immediate implementation.
---

# Legacy Migration Planner

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(architecture)/legacy-migration-planner

Original skill content licensed under CC BY 4.0; adapted for Codex.

The upstream repository `LICENSE` states that repository source code is MIT-licensed, while `SKILL.md` content is CC BY 4.0 unless otherwise specified.

## Goal

Produce an evidence-based migration plan for legacy systems or large-scale architectural change.

This skill is for planning, not implementation. The output should help a team migrate incrementally with clear seams, sequencing, rollback paths, and testing safety nets.

Use [references/checklists.md](references/checklists.md) for the phase checklist and expected output structure.

## Core Rules

- Never guess about unknown acronyms, internal terms, or business requirements.
- Cite evidence for codebase observations with file references.
- Research current and target technologies before recommending them.
- Prefer incremental migration over big-bang replacement unless the evidence strongly supports otherwise.
- Include rollback strategy and success criteria for each migration stage.

## Workflow

Always separate the work into two phases:

1. research
2. plan

Do not jump straight to the migration design before understanding the current system, constraints, and risks.

### 1. Research the current system

Inspect:

- project structure and entry points
- configuration and dependency manifests
- module boundaries and responsibilities
- integration points and external dependencies
- deployment or runtime constraints when visible

Record what exists today before proposing change.

### 2. Identify candidate domains or migration slices

Group the system into bounded contexts or migration units that can be planned independently.

Use architectural seams that are meaningful for the migration direction, such as:

- business domains
- vertical features
- deployable subsystems
- frontend route or shell boundaries
- integration boundaries around external systems

### 3. Research the stack and target options

Before recommending a migration path, verify:

- current stack versions
- target stack maturity and maintenance status
- official migration guides
- compatibility constraints
- known migration pitfalls

If the migration crosses language, framework, or deployment model boundaries, make that explicit in the plan.

### 4. Map risks and dependencies

Identify migration blockers and risk multipliers, such as:

- shared databases
- circular dependencies
- tightly coupled modules
- shared UI shells or runtime containers
- operational dependencies
- missing test coverage

Assess which risks can be isolated and which require program-level coordination.

### 5. Choose migration direction and seams

Define:

- the migration direction
- the incremental seam or facade strategy
- how old and new paths will coexist during transition
- how traffic, callers, or workflows move over gradually

The strangler fig pattern is often a good default, but not automatically the right answer.

### 6. Produce per-slice migration plans

Create one plan per domain or migration slice. Each should include:

- current state
- target state
- migration steps
- testing strategy
- rollback strategy
- success metrics

Keep plans independent enough that they can be sequenced clearly.

### 7. Produce a consolidated roadmap

Write an overall roadmap that captures:

- sequencing across slices
- dependencies between slices
- critical milestones
- risk mitigation timing
- completion criteria

## Output

A strong migration plan should include:

- research findings
- dependency and risk summary
- target architecture direction
- seam or facade strategy
- one plan per migration slice
- a top-level roadmap

## When To Challenge The User

Push back when:

- the migration direction is assumed without evidence
- the team wants a rewrite without a transition plan
- no rollback path exists
- there is no realistic testing safety net
- the proposed boundaries ignore the current coupling

## Scope Limits

- This skill produces plans, not implementation code.
- It should not recommend technologies without current verification.
- It should not merge research and planning into one vague document.
