# Config Detection

## Look For Configuration In

- `AGENTS.md`
- workspace rules files
- repo documentation or setup docs
- project-specific Jira config files

## Required Values

- project key
- cloud ID or site identifier
- site URL when required by the tool

## Fallback Strategy

1. inspect local context for Jira configuration
2. use Jira or Atlassian search tools to discover available projects
3. if multiple projects are plausible, ask the user which one to use
4. reuse the chosen configuration for the rest of the conversation

## Common JQL Patterns

```jql
project = ABC AND assignee = currentUser() AND status = "In Progress"
project = ABC AND created >= -7d
project = ABC AND type = Epic AND status != Done
project = ABC AND assignee is EMPTY AND status = "To Do"
project = ABC AND updated >= startOfWeek()
```

## Issue Creation Notes

- prefer Markdown descriptions
- keep summaries short
- avoid file paths unless specifically requested
- include acceptance criteria for implementation tasks
