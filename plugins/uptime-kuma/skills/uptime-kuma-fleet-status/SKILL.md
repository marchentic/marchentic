---
name: uptime-kuma-fleet-status
description: >-
  Uptime Kuma fleet checklist: list monitors, highlight down/paused, optional
  status-page skim. API/UI only; no Uptime Kuma MCP discovered.
---

# Uptime Kuma fleet status

## Gate

User asked what is down, whether monitors are healthy, or for a short fleet
status pass. Prefer API/UI (no Uptime Kuma MCP discovered). Skip mutate paths
unless also authorized.

Always load `uptime-kuma-monitors`, `uptime-kuma-safety`, and skill
`uptime-kuma`.

## Checklist

1. **Connect** — resolve base URL; list monitors.
   **Done when** monitor rows exist or auth failed.
2. **Classify** — group up / down / pending / paused.
   **Done when** each cited monitor has id + name + status.
3. **Optional pages** — list status pages when the ask includes public status.
   **Done when** page names noted or step skipped.
4. **Safety** — inventory only unless mutate also authorized.
   **Done when** receipt has no unauthorized delete/pause.

## Report shape

- Counts by status
- Down/paused table: id, name, type, target
- One recommended next step (gated pause/delete or create)
