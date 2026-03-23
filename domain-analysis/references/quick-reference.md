# Quick Reference

## Subdomain Classification

```text
Is it a competitive advantage?
  YES -> Core domain
  NO  -> Is it business-specific?
           YES -> Supporting subdomain
           NO  -> Generic subdomain
```

## Bounded Context Detection

```text
Same term, different meaning?
  YES -> Different bounded contexts
  NO  -> Possibly same context, verify cohesion
```

## Cohesion Signals

Score candidate groupings by:

- linguistic cohesion: shared vocabulary
- usage cohesion: used together
- data cohesion: direct relationships
- change cohesion: evolve together

Interpretation:

- 8-10: strong domain or context candidate
- 5-7: review and refine
- 0-4: likely wrong grouping

## Common Red Flags

- user or identity concepts mixed with billing logic
- content or catalog logic mixed with invoice or payment logic
- authentication concerns embedded inside core business workflows
- direct entity sharing across domains
- one context defined only by technical layer

## Healthy Patterns

- interface-based or event-based cross-domain integration
- value-object sharing instead of rich entity sharing
- anti-corruption layers around legacy or external contexts
- contexts named after business capabilities rather than frameworks

## Questions To Ask

- Does this capability differentiate the business?
- Is this language business-specific or generic?
- Do these concepts share one vocabulary?
- Do they change together?
- Does the same term mean something different elsewhere?
- Where should translation happen between contexts?
