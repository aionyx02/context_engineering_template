---
type: project_overview
status: active
priority: p1
updated: 2026-06-04
context_policy: always_retrievable
owner: project
---

# Project Overview

## Product

`context-engineering-template` is a reusable repository template for AI-assisted software projects that need retrieval-first documentation, enforceable engineering policy, and lightweight automated guards.

## Goals

- Keep startup context small while making durable project knowledge discoverable.
- Make AI planning favor lower security risk, then memory and CPU efficiency, then decoupled design.
- Provide guard scripts and CI checks that catch documentation drift, risky content, and structural regressions early.

## Non-Goals

- This template is not a full application framework or starter kit for a specific product stack.
- This template does not replace project-specific architecture decisions, threat modeling, or test strategy.

## Stack

- Frontend: none by default; UI guidance is documentation-only until a real product adopts the template.
- Backend: Node.js CLI scripts for guard automation and repository checks.
- Database / storage: Markdown and JSON files stored in the repository.
- Infrastructure: Git-based workflow with GitHub Actions for CI enforcement.

## Platform Targets

- Local AI-assisted workflows using Codex, Claude, ChatGPT, or similar agents.
- GitHub-hosted repositories that can run Node 20-based validation in CI.

## Engineering Priorities

1. Lower security risk first.
2. Improve memory and CPU efficiency second.
3. Preserve decoupled architecture and replaceable boundaries third.
4. Optimize correctness, rollbackability, and testability before convenience shortcuts.

## Current Strategy

- Route AI through `CLAUDE.md`, `docs/index.md`, `docs/memory/current.md`, and `docs/tasks/active.md` before deep retrieval.
- Keep governance, security, architecture, and coding rules in dedicated reference docs instead of bloating startup context.
- Generate summaries and indexes from durable source files so CI can detect drift instead of trusting manual updates.
