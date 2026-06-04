---
type: task_index
status: active
priority: p0
updated: 2026-05-24
context_policy: always_retrievable
owner: project
---

# Active Tasks

## Active Queue

### TASK.001 - Define Current Scope

- Status: todo
- Priority: P0
- Owner: project
- Started: `<DATE>`
- Related docs:
  - `docs/project.md`
  - `docs/memory/current.md`
- Acceptance criteria:
  - [ ] Current project purpose is filled in.
  - [ ] Startup context remains compact.
- Validation:
  - [ ] `npm run docs:refresh`
- Notes:
  - Keep detailed narrative in session logs.

### TASK.002 - Implement Smallest Safe Vertical Slice

- Status: todo
- Priority: P0
- Owner: project
- Started: `<DATE>`
- Related docs:
  - `docs/architecture.md`
  - `docs/testing.md`
- Acceptance criteria:
  - [ ] Smallest useful feature path works.
  - [ ] Validation commands are documented.
- Validation:
  - [ ] `npm run docs:refresh`
- Notes:
  - Put task-level detail in `docs/tasks/task-template.md` copies when needed.

## Strategy

Keep `active.md` compact. Every active task must include an `Owner` from `docs/team/members.md`. Use `project` only for placeholder or unassigned setup work; `doing` tasks should be assigned to a real member. Put task-level details in dedicated `docs/tasks/*.md`, detailed implementation notes in per-member session logs, and future ideas in `docs/tasks/backlog.md`.

## Next Phase Candidates

- `<NEXT_PHASE_CANDIDATE_1>`
- `<NEXT_PHASE_CANDIDATE_2>`
