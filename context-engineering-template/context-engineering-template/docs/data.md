---
type: data_contracts
status: active
priority: p1
updated: 2026-05-24
context_policy: retrieve_when_planning
owner: project
---

# Data Contracts

## Purpose

Define durable data shapes, API contracts, persistence rules, and migration rules. Do not store temporary debugging output here.

## Core Entities

| Entity | Meaning | Owner | Notes |
|---|---|---|---|
| `<ENTITY>` | `<MEANING>` | `<MODULE_OR_LAYER>` | `<NOTES>` |

## API Contracts

| Endpoint / Function | Input | Output | Error shape |
|---|---|---|---|
| `<API_OR_FUNCTION>` | `<INPUT>` | `<OUTPUT>` | `<ERROR>` |

## Persistence Rules

- `<PERSISTENCE_RULE>`

## Migration Rules

- Schema changes require tests or validation steps.
- Breaking data format changes require an ADR.
- Backward compatibility must be documented when relevant.
- Data migration commands and output belong in session logs.

## Cache Rules

- `<CACHE_RULE>`
