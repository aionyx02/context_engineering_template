---
type: testing_policy
status: active
priority: p1
updated: 2026-05-24
context_policy: retrieve_when_debugging
owner: project
---

# Testing Strategy

## Required Checks

Replace with project-specific commands.

```bash
npm run lint
npm run test
npm run build
npm run docs:refresh
```

## Test Layers

| Layer | Purpose | Command |
|---|---|---|
| Static checks | Formatting, lint, type checks | `<COMMAND>` |
| Unit tests | Core logic | `<COMMAND>` |
| Integration tests | Cross-module behavior | `<COMMAND>` |
| E2E / smoke | User-visible workflow | `<COMMAND>` |

## Regression Policy

When fixing a bug:

1. Reproduce or document why reproduction is not possible.
2. Add a test or structured edge case when feasible.
3. Record root cause in the session log.
4. Update current docs only if behavior or active plan changed.


## UI / HTML Validation

When a task changes UI or HTML, validate the smallest useful path:

- Page renders without runtime errors.
- Main interactive controls are keyboard reachable.
- Forms expose labels and visible validation messages.
- Loading, empty, error, and success states are handled when applicable.
- Responsive layout does not break at the supported viewport widths.

Suggested optional commands when the project provides them:

```bash
npm run test:e2e --if-present
npm run build --if-present
```
