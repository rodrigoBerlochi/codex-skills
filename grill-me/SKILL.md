---
name: grill-me
description: Rigorously interview the user about a plan, design, or implementation approach to expose gaps, resolve dependencies, and reach a concrete shared understanding. Use when the user wants to stress-test an idea, be grilled on a design, or explicitly says "grill me".
---

# Grill Me

## Source

Adapted for Codex from:
https://github.com/mattpocock/skills/tree/main/grill-me

Original skill content licensed under MIT; adapted for Codex.

## Goal

Stress-test a plan or design until the open decisions, assumptions, risks, and sequencing constraints are clear.

Use this skill when the user wants hard questioning rather than passive feedback.

## Behavior

Interview the user relentlessly about the plan, but keep the questions productive:

- walk each meaningful branch of the decision tree
- resolve dependency order between decisions
- surface missing constraints and hidden assumptions
- point out tradeoffs and failure modes
- give a recommended answer with each question when possible

Do not ask questions that can be answered by inspecting the repository, docs, or current implementation. Check local context first and use that to sharpen the next question.

## Question Style

Ask questions that force clarity, such as:

- What exact problem is this solving?
- What alternatives were rejected and why?
- What must remain unchanged?
- What would make this approach fail in production?
- Which interfaces, contracts, or migrations are involved?
- How will correctness be verified?
- What is the rollback plan if the change stalls halfway through?

Each question should move the design forward, not just prolong discussion.

## Output

Keep the exchange structured around decisions:

- question
- recommended answer
- consequence if answered differently

When enough clarity is reached, summarize:

- the resolved decisions
- the remaining open questions
- the biggest risks
- the next concrete step
