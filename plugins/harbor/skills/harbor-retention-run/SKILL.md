---
name: harbor-retention-run
description: >-
  Checklist for gated Harbor retention: resolve project, prove policy or
  tag scope, confirm explicit purge verb, then run via API/UI with a short
  receipt. Skip when no retention ask.
---

# Harbor retention run

## Gate

User asked to run retention, purge old tags, or apply a retention policy
on a Harbor project. Prefer Harbor API/UI. Skip inventory-only asks
(`harbor-project-audit`) and single-tag delete (still `harbor-safety`,
narrower path via `harbor-artifacts`).

Always load `harbor-artifacts`, `harbor-projects`, and `harbor-safety`.

## Checklist

1. **Verb** — require explicit retention / purge / expire this turn naming
   the project (and policy when known). **Done when** present, or you
   stopped and asked once.
2. **Project** — resolve via `harbor-projects` list.
   **Done when** the project name/id is proven this turn.
3. **Scope** — policy name and/or tag rules from list/UI; never invent
   "delete all tags older than X" without the user stating X.
   **Done when** the purge scope is explicit.
4. **Preview** — prefer dry-run / candidate list when the API/UI offers
   it. **Done when** the operator saw what would be removed, or the
   tool has no dry-run and you stated that.
5. **Act** — run retention via API/UI; never invent MCP tool names.
   **Done when** the mutate ran only after steps 1–4.
6. **Receipt** — project + policy/scope + result; no tokens.
   **Done when** the reply matches the report shape.

## Report shape

- Project name/id
- Policy or tag scope
- Action (dry-run vs applied)
- Count or names of affected tags when available
- "No robot tokens or admin passwords shown"
