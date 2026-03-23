---
name: jira-assistant
description: Use Atlassian or Jira MCP tools to search, create, update, comment on, assign, and transition Jira issues. Use when the user wants Jira issue management, sprint work updates, issue searches, or ticket status changes.
---

# Jira Assistant

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(development)/jira-assistant

Original skill content licensed under CC BY 4.0; adapted for Codex.

The upstream repository `LICENSE` states that repository source code is MIT-licensed, while `SKILL.md` content is CC BY 4.0 unless otherwise specified.

## Goal

Use Jira MCP or Atlassian MCP tooling to manage Jira work items efficiently and consistently.

This includes:

- searching for issues
- reading issue details
- creating tasks, epics, and subtasks
- editing fields
- adding comments
- transitioning status
- managing assignees or sprint-related work

Use [references/config-detection.md](references/config-detection.md) for configuration discovery and common query patterns.

## Configuration

Before performing operations, determine:

- project key
- cloud ID or site identifier
- relevant Jira URL if needed

Look for configuration in local project context first, such as:

- `AGENTS.md`
- workspace rules or repo docs
- project-specific Jira configuration files

If configuration is not available locally, use Jira or Atlassian search tooling to discover accessible projects. Ask the user only if the project choice is still ambiguous.

Once determined, reuse that configuration for the rest of the conversation.

## Workflow

### 1. Search first

For broad or natural-language requests, start with search-style Jira tooling when available.

Examples:

- issues in a project
- tasks assigned to me
- bugs in progress

This is usually faster and easier than starting with strict JQL.

### 2. Use JQL for precise filtering

When the user needs exact filtering, use JQL-based issue search.

Always include the relevant project in the query unless the user explicitly wants cross-project results.

### 3. Fetch issue details when needed

If you already have an issue key or unique result, fetch the issue details before editing or transitioning it.

### 4. Create issues carefully

Before creating an issue:

- determine the issue type
- check required fields if the tooling supports it
- use the detected project configuration
- write a clear summary
- use structured Markdown in the description

Avoid brittle implementation detail such as file paths in Jira descriptions unless the user explicitly wants them.

### 5. Transition and update safely

Before transitioning status:

- inspect available transitions when required by the API
- confirm you are acting on the correct issue

Before editing:

- preserve important existing context when practical
- avoid destructive overwrites unless the user asked for them

## Default Description Shape

When creating implementation-oriented issues, prefer a structure like:

```markdown
## Context

## Objective

## Technical Requirements

- [ ] Requirement 1
- [ ] Requirement 2

## Acceptance Criteria

- [ ] Criterion 1
- [ ] Criterion 2

## Technical Notes

## Estimate
```

Keep the summary short and the description specific enough to be actionable.

## Best Practices

- search broadly first, then narrow with JQL
- keep descriptions in Markdown
- use the detected project configuration consistently
- keep technical notes high level unless the user requests more detail
- use subtasks only when they clearly belong under a parent issue
- avoid stale implementation detail like fragile file paths

## Limits

- This skill is for Jira issue operations, not Confluence content.
- It should not assume project configuration without checking local context first.
- It should not use JQL by default when a natural-language search is enough.
