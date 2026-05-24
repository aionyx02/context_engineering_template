---
type: agent_bootstrap
status: active
priority: p0
updated: 2026-05-24
context_policy: always_retrievable
owner: project
---

# CLAUDE.md

> Auto-loaded at session start. Detailed governance, ADR, and documentation-routing rules are in `docs/CLAUDE.md`.

## Session Start

1. Read `docs/index.md` for documentation routing.
2. Read `docs/memory/current.md` for current strategy, constraints, and next step.
3. Read `docs/tasks/active.md` for the active queue.
4. Retrieve additional documents by intent. Do not recursively load all docs.

## Session Close

Before final response, handoff, or commit:

1. Update only the smallest matching state document.
2. Put detailed execution notes, debugging narrative, and command-output history in `docs/memory/sessions/YYYY-MM-DD.md`.
3. Keep `docs/memory/current.md` and `docs/tasks/active.md` as current-state indexes only.
4. Put completed-task detail in the session log using `## COMPLETED: TASK_ID - summary`.
5. Run `npm run docs:refresh` when Node scripts are available.

## Project Overview

Replace this section with a short, durable project description.

- Product: `<PROJECT_NAME>`
- Primary goal: `<ONE_SENTENCE_GOAL>`
- Main users: `<TARGET_USERS>`
- Supported platforms: `<PLATFORMS>`

## Git Workflow Rules

```text
main <- always releasable
dev  <- integration
feature/<name> <- work branches
```

- Do not merge without explicit developer confirmation.
- Create feature branches from `dev` unless the repository policy says otherwise.
- Show diffs and pass relevant checks before merge.
- Never rewrite shared history without explicit approval.

## Build / Test Commands

Replace commands to match this project.

```bash
npm install
npm run lint
npm run test
npm run build
npm run docs:refresh
```

## Documentation Entry Points

- `docs/index.md` - documentation router
- `docs/project.md` - stable project facts
- `docs/memory/current.md` - short working memory
- `docs/tasks/active.md` - active work only
- `docs/CLAUDE.md` - governance and ADR rules
