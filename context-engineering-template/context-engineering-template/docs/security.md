---
type: security_policy
status: active
priority: p1
updated: 2026-05-24
context_policy: retrieve_only
owner: project
---

# Security And Permission Boundary

## Security Principles

- Least privilege by default.
- Destructive actions require explicit confirmation.
- Secrets must not be committed to repository docs or logs.
- Logs should avoid sensitive payloads.

## Data Classification

| Data | Sensitivity | Handling |
|---|---|---|
| Public configuration | Low | Safe to document |
| User content | Medium/High | Minimize logs and copies |
| Credentials / tokens | Critical | Never store in docs or prompts |

## Approval-Gated Changes

- Credential storage or retrieval.
- Network egress behavior.
- File-system write/delete behavior.
- Permission expansion.
- Telemetry or analytics behavior.
