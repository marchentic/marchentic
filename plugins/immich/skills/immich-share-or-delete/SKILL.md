---
name: immich-share-or-delete
description: >-
  Gated Immich share-link or trash/delete checklist: resolve ids, warn
  exposure or permanence, mutate via API, receipt without secrets.
---

# Immich share or delete

## Gate

User authorized **share** link create/revoke or **trash**/**delete** with
an explicit verb naming objects. Prefer Immich API (no Immich MCP
discovered). Skip inventory-only asks.

Always load `immich-library`, `immich-mutate`, `immich-safety`, and skill
`immich`.

## Checklist

1. **Resolve** — list/search proves album/asset ids this turn.
   **Done when** every id exists.
2. **Path** — share vs trash vs permanent delete; prefer trash when delete
   intent is soft.
   **Done when** path is explicit.
3. **Warn** — share = URL exposure; delete = permanent when emptying trash.
   Cite `immich-safety`.
   **Done when** intent still matches.
4. **Act** — API mutate per `immich-mutate`.
   **Done when** API accepted or clear error.
5. **Receipt** — action + ids + outcome — no keys or media bytes.
   **Done when** evidence cited.

## Report shape

- action + object ids
- warning acknowledged (exposure or permanence)
- outcome
