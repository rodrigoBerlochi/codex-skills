---
name: security-best-practices
description: Perform framework-aware security best-practice reviews and write secure-by-default code. Use when the user asks for security guidance, a security review, secure coding help, or a prioritized security report for a Python, JavaScript/TypeScript, or Go codebase.
---

# Security Best Practices

## Source

Adapted for Codex from:
https://github.com/tech-leads-club/agent-skills/tree/main/packages/skills-catalog/skills/(security)/security-best-practices

Original skill content licensed under Apache-2.0; adapted for Codex.

The upstream skill directory includes its own `LICENSE.txt` with the Apache License, Version 2.0.

## Goal

Use language- and framework-specific security guidance to:

- write secure-by-default code
- spot major security issues while working
- produce a prioritized security report when requested
- propose or implement focused fixes carefully

## Workflow

### 1. Identify the stack

Determine the languages and major frameworks in scope.

Inspect the repository and gather evidence from:

- dependency manifests
- framework config files
- entrypoints and app bootstrapping
- frontend and backend structure

If the project includes both frontend and backend, consider both.

### 2. Load the relevant guidance

Use [references/framework-selection.md](references/framework-selection.md) to map the detected stack to the appropriate security guidance.

Read only the files relevant to the current stack. If multiple stacks are present, read all applicable guidance before making recommendations.

If no matching guidance exists, rely on well-established security practice and say clearly when framework-specific guidance is missing.

### 3. Choose the operating mode

This skill supports three modes:

- secure-by-default implementation: use the guidance while writing new code
- passive review: flag critical or high-impact issues encountered during normal work
- explicit security report: audit the scoped area and produce a prioritized report

### 4. Produce findings carefully

When reviewing or reporting:

- prioritize critical and high-severity issues
- explain impact briefly and concretely
- cite code references with line numbers
- distinguish certain findings from lower-confidence concerns
- avoid noisy advice that is not material to the current system

### 5. Fix incrementally

If the user wants fixes:

- address one finding at a time
- minimize regressions and behavior changes
- follow project testing flows
- explain any security-sensitive change briefly in code comments when needed

Avoid bundling unrelated security fixes into one change unless the user asks for that.

## Reporting

When the user asks for a report, write it to a markdown file such as `security_best_practices_report.md`, unless they specify another path.

Structure the report with:

- executive summary
- findings grouped by severity
- numeric IDs for findings
- short impact statements for critical findings
- code references with line numbers
- recommended remediations

After writing the report, summarize the key findings to the user and state where the file was written.

## Important Guidance

- Do not treat missing TLS in local development as an automatic finding.
- Be careful with `Secure` cookies in non-TLS development environments.
- Avoid recommending HSTS casually; it has operational risk if applied incorrectly.
- Avoid exposing incremental public IDs when unpredictable identifiers are practical.
- Respect project-specific documented exceptions, but call them out if they materially weaken security.

## Limits

- This skill is not a substitute for full threat modeling.
- Do not present uncertain claims as confirmed vulnerabilities.
- Do not recommend technologies or controls blindly; verify they fit the actual stack and environment.
