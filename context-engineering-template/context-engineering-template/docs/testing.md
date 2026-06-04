---
type: testing_policy
status: active
priority: p1
updated: 2026-06-04
context_policy: retrieve_when_debugging
owner: project
---

# Testing Strategy

## Required Checks

For this template repository, the baseline validation commands are:

```bash
npm run lint
npm run security:scan
npm test
npm run docs:refresh
npm run docs:ready
```

## Test Layers

| Layer | Purpose | Command |
|---|---|---|
| Static checks | Script syntax validation for guard and test files | `npm run lint` |
| Unit tests | Guard behavior, path normalization, generated output stability | `npm test` |
| Integration checks | End-to-end docs refresh, link validation, schema validation, and generated index regeneration | `npm run docs:refresh` |
| Adoption readiness | Strict placeholder, lint, security, test, and docs-refresh checks for real project adoption | `npm run docs:ready` |
| CI drift check | Fail when generated docs change after refresh | `npm run docs:refresh` followed by `git diff --exit-code` in CI |

## Regression Policy

When fixing a bug:

1. Reproduce or document why reproduction is not possible.
2. Add a targeted test or guard when the behavior can regress silently.
3. Record root cause in the session log.
4. Update current docs only if durable behavior, policy, or active plan changed.

## Security Validation

- Run `npm run security:scan` before merging changes that touch docs, workflows, fixtures, or automation.
- Review approval-gated changes against `docs/security.md` before widening permissions or adding new execution paths.
- If a change touches secrets, credentials, shell execution, or network behavior, pair test evidence with a security rationale.

## UI / HTML Validation

This template does not ship a runtime UI. When the template is adopted into a UI project, add project-specific smoke, accessibility, and responsive validation commands here before relying on AI-generated UI changes.
