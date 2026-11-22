---
name: uptime-kuma-pause-or-delete
description: >-
  Gated Uptime Kuma pause/resume/delete checklist: resolve ids, prefer pause,
  mutate via API/UI, receipt without secrets.
---

# Uptime Kuma pause or delete

## Gate

User authorized **pause**, **resume**, or **delete** with an explicit verb
naming monitor/page/channel ids. Prefer API/UI (no Uptime Kuma MCP
discovered). Skip inventory-only asks.

Always load `uptime-kuma-monitors`, `uptime-kuma-mutate`,
`uptime-kuma-safety`, and skill `uptime-kuma`.

## Checklist

1. **Resolve** — list proves ids this turn.
   **Done when** every id exists.
2. **Path** — prefer pause when delete intent is soft; confirm delete is
   permanent enough for this ask.
   **Done when** path is explicit.
3. **Act** — pause/resume/delete per `uptime-kuma-mutate`.
   **Done when** API/UI accepted or clear error.
4. **Receipt** — action + ids + resulting status — no secrets.
   **Done when** evidence cited.

## Report shape

- action + ids + names
- resulting status
- pause-over-delete note when applicable
