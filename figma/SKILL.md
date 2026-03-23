---
name: figma
description: Use Figma MCP tools to fetch design context, screenshots, variables, and assets from Figma and translate nodes into project-native code. Use when the task includes Figma URLs, node IDs, design-to-code work, or Figma MCP setup and troubleshooting.
---

# Figma

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(design)/figma

Original skill content licensed under Apache-2.0; adapted for Codex.

The upstream skill directory includes its own `LICENSE.txt` with the Apache License, Version 2.0.

## Goal

Use Figma MCP to turn Figma nodes into implementation-ready context, then translate that context into code that matches the target project rather than copying generated output blindly.

Use [references/figma-workflow.md](references/figma-workflow.md) for the required tool order and adaptation rules.

## Workflow

### 1. Fetch the design context first

Start with the exact node or frame the user cares about.

Use:

- `get_design_context` first
- `get_metadata` only when the node is too large or you need to narrow scope
- `get_screenshot` for visual validation of the exact variant being implemented

Do not start implementation before you have both structured context and a visual reference.

### 2. Narrow scope when needed

If the design payload is too large:

- inspect metadata
- identify the exact node IDs required
- re-fetch only the necessary nodes

Keep the working set small and specific.

### 3. Handle assets correctly

When Figma MCP provides asset URLs:

- use returned localhost asset sources directly when present
- do not create placeholder assets if a real asset is provided
- do not add new icon libraries just to replicate Figma assets

### 4. Translate to project conventions

Treat generated output as a representation of design intent, not final project code.

Always adapt it to:

- the project’s component system
- design tokens and color system
- typography and spacing conventions
- routing, state, and data patterns already used by the repo

Prefer reusing existing components over duplicating primitives.

### 5. Validate against Figma

Before considering the work complete:

- compare visually against the screenshot
- check the right variant or state was implemented
- verify behavior as well as appearance

Aim for design fidelity without breaking the project’s established architecture.

## Rules

- Prefer project-native components over raw generated markup.
- Replace generic utility styling with the repo’s own styling system when appropriate.
- Preserve the semantics and interaction behavior implied by the design.
- If the link points to the wrong node or variant, correct the scope before coding.
- If the design conflicts with the repo’s design system, adapt carefully and note the tradeoff.

## Setup And Troubleshooting

When the issue is about MCP setup, auth, or missing design data, use the setup and troubleshooting checklist in [references/figma-workflow.md](references/figma-workflow.md).

## Limits

- This skill is for Figma-driven implementation and design-context retrieval.
- It should not assume generated Figma code matches the repo’s coding standards.
- It should not skip screenshot-based validation when visual fidelity matters.
