---
type: architecture_spec
status: active
priority: p1
updated: 2026-06-04
context_policy: retrieve_only
owner: project
---

# Architecture

## System Overview

This template uses a decoupled documentation architecture. Startup context stays minimal, durable policy lives in targeted reference files, and automation scripts derive indexes or validate invariants without becoming the source of truth.

```text
Agent -> CLAUDE.md -> docs/index.md -> current state + active tasks -> targeted reference docs
                                                    |
                                                    v
                                           guard scripts + CI checks
                                                    |
                                                    v
                                         generated indexes and summaries
```

## Layers

| Layer | Responsibility | Depends On |
|---|---|---|
| Bootstrap | Define startup read order and minimal session rules. | Reference docs only |
| Routing | Map user intent to the smallest relevant documentation set. | Bootstrap, reference docs |
| Working state | Hold current strategy, active tasks, and historical execution notes in separate stores. | Routing rules |
| Reference policy | Store durable rules for security, architecture, testing, dependencies, UI, and coding style. | None beyond bootstrap metadata |
| Guard automation | Validate schemas, links, secrets, task markers, generated outputs, and narrative routing. | Working state and reference policy files |
| Generated summaries | Publish derived indexes such as decision summaries and completed-task indexes. | Guard automation inputs only |

## Modules

| Module | Responsibility | Notes |
|---|---|---|
| `CLAUDE.md` | Minimal boot instructions for every AI session. | Must stay compact and stable. |
| `docs/index.md` | Retrieval router and document map. | First lookup step after bootstrap. |
| `docs/memory/current.md` | Current strategy, constraints, and next move. | No historical narrative. |
| `docs/tasks/active.md` | Active task queue and status. | No long execution logs. |
| `docs/*.md` reference docs | Durable policy and architecture knowledge. | Read by intent, not recursively. |
| `docs/adr/*.md` | Architecture and policy decisions. | AI may propose; humans accept. |
| `scripts/docs-*.mjs` | Deterministic guards and derived-document generators. | Should not become policy owners. |
| `docs/state/*.json` | Small machine-readable summaries. | Generated or maintained as lightweight indexes. |

## Dependency Direction

- Bootstrap files may point to any reference document, but must not embed full reference content.
- Current state documents may reference reference docs and ADRs, but must not duplicate them.
- Guard scripts may read source docs and write only generated artifacts such as `docs/decisions.md` or `docs/tasks/completed.md`.
- Reference docs must not depend on session logs for current truth.
- Domain rules for a real adopted project should live above infrastructure details and remain replaceable across transport, storage, or UI changes.

## Data Contracts

The stable contracts in this template are the frontmatter schema, task marker format, ADR naming/status rules, and generated summary shapes. When those contracts change, update the corresponding guard scripts and add or update an ADR if the change affects workflow semantics.

## Architecture Constraints

- Security policy outranks delivery convenience when architecture tradeoffs are evaluated.
- Memory and CPU efficiency should improve through bounded, measurable changes rather than accidental coupling.
- Historical narrative belongs in session logs; startup and planning docs stay short.
- Generated files must be deterministic so CI can detect drift with a simple diff.
- New automation should stay decoupled from product-specific frameworks unless the template is intentionally specialized.

## Open Architecture Questions

- Should the template add language-specific overlays for Google style guides such as Go, Java, Python, and TypeScript?
- Should future generated summaries include a first-class security review index in addition to task and decision summaries?
