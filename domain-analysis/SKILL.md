---
name: domain-analysis
description: Map business domains, classify subdomains, and suggest bounded contexts using DDD strategic design. Use when the user asks what domains exist in a codebase, where to draw service boundaries, how to identify bounded contexts, or how to assess domain cohesion.
---

# Domain Analysis

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(architecture)/domain-analysis

Original skill content licensed under CC BY 4.0; adapted for Codex.

The upstream repository `LICENSE` states that repository source code is MIT-licensed, while `SKILL.md` content is CC BY 4.0 unless otherwise specified.

## Goal

Analyze a codebase through Domain-Driven Design strategic design:

- identify business concepts
- group them into subdomains
- classify subdomains as core, supporting, or generic
- suggest bounded contexts based on ubiquitous language
- surface low-cohesion boundaries and cross-domain coupling

Use [references/quick-reference.md](references/quick-reference.md) for the decision trees and fast heuristics.

## Core Principles

### Subdomains

- Core domain: where the business differentiates itself
- Supporting subdomain: business-specific but not differentiating
- Generic subdomain: common capability that could often be bought or reused

### Bounded contexts

A bounded context is a linguistic boundary. Inside it, key terms should have one clear meaning.

Do not derive contexts from technical layers alone. Favor business language and capability boundaries over controller/service/repository splits.

## Process

### 1. Extract domain concepts

Scan for business-facing concepts, not infrastructure.

Look for:

- entities and aggregates
- business services and workflows
- use cases and handlers
- controllers, resolvers, or endpoints that reveal business capabilities

Focus on what the system is about, not how the framework is wired.

### 2. Group by ubiquitous language

For each concept, determine:

- which business vocabulary it belongs to
- whether the same term means something different elsewhere
- which concepts naturally belong together

If the same word has different meanings in different parts of the system, that is a strong bounded-context signal.

### 3. Identify subdomains

A real subdomain should have:

- a distinct business capability
- recognizable business value
- a coherent vocabulary
- multiple related concepts that work together

Classify each one:

- core: competitive advantage, high change pressure, domain expertise required
- supporting: important and business-specific, but not the differentiator
- generic: commodity capability, common infrastructure, or reusable support

### 4. Assess cohesion

Judge each candidate domain or context using:

- linguistic cohesion: shared vocabulary
- usage cohesion: concepts used together
- data cohesion: direct relationships
- change cohesion: whether they evolve together

High cohesion suggests a good boundary. Low cohesion suggests mixed concerns or the wrong grouping.

### 5. Find domain issues

Look for:

- linguistic mismatch: different vocabularies mixed together
- cross-domain dependencies that leak internal models
- mixed responsibilities inside one class or module
- generic concerns embedded in core business logic
- concepts that cannot be assigned cleanly to one domain

Do not assume every dependency is bad. The question is whether the boundary is clear and intentional.

### 6. Suggest bounded contexts

For each strong domain candidate, propose a bounded context with:

- a context name
- its ubiquitous language
- the concepts it owns
- its main upstream and downstream integrations
- the likely integration pattern

Useful patterns include:

- customer/supplier
- anti-corruption layer
- open host service
- published language
- domain events

## Output Format

Structure the output like this:

```markdown
## Domain Map

For each domain:
- type: core, supporting, or generic
- business capability
- ubiquitous language
- key concepts
- cohesion assessment
- important dependencies
- suggested bounded context

## Cross-Domain Issues

For each issue:
- location or area
- concepts involved
- why the boundary is weak
- recommendation

## Suggested Bounded Contexts

For each context:
- owned concepts
- boundary description
- integration needs
- implementation notes at a high level

## Recommendations

- high priority
- medium priority
- low priority
```

## Heuristics

- Group by business language, not technical layer.
- Prefer one context per coherent language, not one context per entity.
- If two concepts always change together and share language, they may belong together.
- If two concepts use the same term differently, they probably need separate contexts.
- Generic capabilities should not dominate core domain code.

## Limits

- Static code inspection cannot fully recover business intent.
- Real domain boundaries are stronger when validated with domain experts.
- Team structure may reveal useful hints, but should not be the sole basis for the domain model.
