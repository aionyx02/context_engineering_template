---
type: dependency_policy
status: active
priority: p1
updated: 2026-05-24
context_policy: retrieve_when_planning
owner: project
---

# Dependencies

## Dependency Rules

- Prefer built-in language features, standard libraries, and existing dependencies first.
- New runtime dependencies require explicit justification.
- Large framework, infrastructure, database, authentication, or build-system dependencies require an ADR.
- Security-sensitive dependencies require review before adoption.
- Remove unused dependencies when the owning feature is removed.

## Current Dependencies

| Dependency | Purpose | Scope | Replaceable? | Notes |
|---|---|---|---|---|
| `<PACKAGE>` | `<PURPOSE>` | runtime/dev | yes/no | `<NOTES>` |

## Rejected Dependencies

| Dependency | Reason rejected | Date |
|---|---|---|
| `<PACKAGE>` | `<REASON>` | `<DATE>` |

## Dependency Change Checklist

- [ ] Existing dependency cannot solve the need.
- [ ] License and maintenance status are acceptable.
- [ ] Security implications are understood.
- [ ] Bundle size or runtime cost is acceptable when relevant.
- [ ] Tests or validation commands cover the new dependency path.
