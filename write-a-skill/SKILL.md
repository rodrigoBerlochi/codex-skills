---
name: write-a-skill
description: Create new Codex skills with proper structure, concise trigger metadata, progressive disclosure, and optional bundled references or scripts. Use when the user wants to create, draft, or refine a new skill.
---

# Write A Skill

## Source

Adapted for Codex from:
https://github.com/mattpocock/skills/tree/main/write-a-skill

Original skill content licensed under MIT; adapted for Codex.

## Goal

Create a new Codex skill that is small, clear, and actually useful in real work.

A good skill gives Codex procedural guidance it would not reliably infer on its own, while keeping the main `SKILL.md` compact and pushing detailed material into references only when needed.

## Process

### 1. Gather requirements

Clarify:

- what task or domain the skill covers
- the concrete use cases it should handle
- what should trigger the skill
- whether it needs scripts, references, or just instructions

If the use cases are still vague, ask for examples before drafting.

### 2. Draft the skill

Create:

- `SKILL.md` with frontmatter and concise operating instructions
- `references/` files only if extra detail is genuinely needed
- `scripts/` only when deterministic operations or reusable tooling justify them

Prefer a small, usable skill over a comprehensive but bloated one.

### 3. Check the trigger metadata

The description matters most because it determines when the skill should fire.

Make sure it says:

- what capability the skill provides
- when it should be used
- concrete triggers, keywords, or contexts

Prefer descriptions that are precise enough to distinguish the skill from adjacent ones.

### 4. Review and refine

Verify:

- the skill is scoped tightly
- instructions are specific where needed but not verbose
- references are one level deep from `SKILL.md`
- terminology is consistent
- no time-sensitive claims are embedded unless necessary

## Recommended Structure

```text
skill-name/
├── SKILL.md
├── references/
│   └── topic.md
└── scripts/
    └── helper.sh
```

Use `references/` for optional supporting material and `scripts/` for deterministic helpers.

## SKILL.md Shape

Keep `SKILL.md` focused on:

- purpose
- trigger guidance
- the main workflow
- links to optional references

Do not turn the folder into a documentation dump.

## Heuristics

- add scripts when the same code would otherwise be regenerated repeatedly
- split files when details are rarely needed or the main skill becomes too large
- keep examples short and concrete
- favor instructions Codex can act on directly

## Review Checklist

- [ ] Description clearly says when to use the skill
- [ ] Scope is narrow enough to be triggered reliably
- [ ] Main instructions are concise
- [ ] Supporting details are moved to references only when needed
- [ ] Scripts are included only for deterministic or repetitive tasks
