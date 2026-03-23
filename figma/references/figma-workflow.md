# Figma Workflow

## Required Tool Order

1. `get_design_context`
2. `get_metadata` only if scoping or truncation requires it
3. `get_screenshot`
4. fetch assets if needed
5. implement using project conventions
6. validate against the screenshot

## Adaptation Rules

- treat generated React or Tailwind as design intent, not final style
- reuse existing components and tokens
- prefer repo-native typography, spacing, and color primitives
- preserve interaction and layout behavior from the design

## Asset Rules

- use localhost asset sources directly when provided
- do not add icon packages just to mimic design assets
- do not substitute placeholders when the asset already exists in the MCP payload

## Link Guidance

- use the exact Figma frame or node link when possible
- if the node is too broad, narrow to the specific variant before implementation

## Troubleshooting

- if MCP output is too large, inspect metadata and request smaller nodes
- if assets appear missing, verify whether the returned payload includes localhost asset URLs
- if setup is the problem, check MCP configuration and auth before debugging implementation
