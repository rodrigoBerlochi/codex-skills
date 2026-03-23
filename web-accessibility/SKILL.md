---
name: web-accessibility
description: Audit and improve web accessibility using WCAG 2.1 principles. Use when the user asks for an accessibility review, WCAG compliance help, keyboard or screen-reader support, or wants a web interface made more accessible.
---

# Web Accessibility

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(quality)/web-accessibility

Original skill content licensed under MIT; adapted for Codex.

The upstream repository generally notes CC BY 4.0 for `SKILL.md` content unless otherwise specified, and this upstream `SKILL.md` explicitly declares `license: MIT`.

## Goal

Audit and improve web accessibility using WCAG 2.1 and practical assistive-technology checks.

Focus on issues that materially affect usability for keyboard users, screen-reader users, low-vision users, and users affected by motion, timing, or interaction constraints.

Use [references/wcag-summary.md](references/wcag-summary.md) when you need a compact checklist of common failures and remediation patterns.

## Core Model

Use the WCAG POUR framework:

- perceivable
- operable
- understandable
- robust

Target AA conformance by default unless the user asks for a different standard.

## Workflow

### 1. Determine scope

Clarify or infer:

- which pages, flows, or components matter most
- whether the task is an audit, implementation help, or remediation work
- whether the user wants a report, code fixes, or both

### 2. Inspect the implementation

Check:

- semantic HTML usage
- form labeling and validation
- keyboard interaction
- focus management and focus visibility
- image alt text and icon button naming
- color contrast and non-color cues
- ARIA usage
- dynamic content announcements
- page structure and landmarks

When possible, prefer inspecting real code and UI behavior over giving generic advice.

### 3. Prioritize by impact

Focus first on high-impact issues such as:

- missing form labels
- inaccessible interactive elements
- broken keyboard navigation
- missing focus states
- missing alt text on meaningful images
- insufficient contrast
- incorrect use of ARIA instead of native controls

Avoid burying critical barriers under minor polish suggestions.

### 4. Recommend or implement fixes

Prefer fixes that:

- use native HTML elements first
- preserve or improve keyboard support
- create accessible names and relationships
- keep focus order logical
- announce state changes appropriately
- avoid regressions in existing flows

### 5. Validate

Use a mix of:

- static inspection
- automated tooling when available
- manual keyboard testing
- zoom and reduced-motion checks

If a full accessibility report is requested, document findings with severity and concrete remediation guidance.

## Reporting

When asked for an audit or report, structure it with:

- executive summary
- critical issues
- serious issues
- moderate issues
- recommended fixes
- residual testing gaps

Include code references with line numbers where possible.

## Practical Rules

- Prefer native controls over ARIA re-creations.
- Never remove focus indicators without a stronger replacement.
- Do not rely on color alone to convey status or errors.
- All meaningful images need appropriate text alternatives.
- All interactive elements need an accessible name.
- All functionality should be keyboard accessible.
- Respect `prefers-reduced-motion` for motion-heavy interfaces.
- Avoid treating automated audit scores as complete proof of accessibility.

## Limits

- Automated tools catch only part of the problem.
- Screen-reader behavior and usability often require manual validation.
- Accessibility fixes can affect layout and interaction design, so watch for regressions.
