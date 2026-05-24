---
type: coding_conventions
status: active
priority: p1
updated: 2026-05-24
context_policy: retrieve_when_planning
owner: project
---

# Coding Conventions

## Purpose

Keep implementation style stable across AI-assisted sessions. This file should contain durable conventions only, not temporary task notes.

## Naming

| Item | Convention |
|---|---|
| Files | `<FILE_NAMING_RULE>` |
| Functions | `<FUNCTION_NAMING_RULE>` |
| Classes / Components | `<CLASS_OR_COMPONENT_RULE>` |
| Tests | `<TEST_NAMING_RULE>` |

## Code Style

- Prefer small functions with one clear responsibility.
- Keep side effects near application boundaries.
- Avoid hidden global state unless documented in architecture notes.
- Do not introduce a new dependency when an existing project dependency or standard library feature is enough.
- Prefer explicit error paths over silent fallback behavior.

## Error Handling

- User-facing errors should be actionable.
- Internal errors should preserve enough context for debugging.
- Do not swallow exceptions silently.
- Do not expose secrets, credentials, tokens, or private paths in error messages.

## Logging

- Logs must not contain secrets or sensitive user data.
- Debug logs should be removable, gated, or clearly scoped.
- Long command output belongs in session logs, not in always-retrievable docs.
