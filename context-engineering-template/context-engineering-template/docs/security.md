---
type: security_policy
status: active
priority: p1
updated: 2026-06-04
context_policy: retrieve_only
owner: project
---

# Security And Permission Boundary

## Security Principles

- Least privilege by default.
- Lower security risk outranks delivery speed and implementation convenience.
- Destructive actions require explicit confirmation.
- Secrets must not be committed to repository docs, prompts, fixtures, logs, or workflows.
- Logs should avoid sensitive payloads and private file paths when possible.

## Data Classification

| Data | Sensitivity | Handling |
|---|---|---|
| Public configuration | Low | Safe to document when it does not widen permissions |
| User content | Medium/High | Minimize logging, copying, and prompt exposure |
| Credentials / tokens | Critical | Never store in docs, prompts, examples, or test fixtures |
| Generated summaries | Low/Medium | Keep concise and free of secrets or incident-only detail |

## Automated Checks

- `npm run security:scan` performs a high-confidence secret scan across docs, bootstrap files, and workflows.
- `npm run docs:refresh` includes link, schema, secret, ADR, and task-marker guards.
- CI must run `git diff --exit-code` after `npm run docs:refresh` so generated-policy drift cannot slip through silently.

## Approval-Gated Changes

- Credential storage or retrieval.
- Network egress behavior.
- File-system write/delete behavior outside the intended project boundary.
- Permission expansion.
- Telemetry or analytics behavior.
- Shell execution that accepts untrusted input.

## Security Review Triggers

Perform explicit security review before implementation when any of these change:

- Authentication, authorization, or session handling
- Secret handling or secure storage
- Cross-process execution, shelling out, or plugin loading
- External webhooks, third-party APIs, or network permissions
- Data import/export, serialization, or untrusted file parsing

## Review Checklist

1. What new trust boundary is introduced or widened?
2. What user or system input crosses that boundary?
3. What is the least-privilege version of this design?
4. How does the change fail safely?
5. What logging or audit trail is needed without leaking secrets?
