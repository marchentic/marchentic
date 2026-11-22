---
name: harbor-project-audit
description: >-
  Checklist for Harbor project fleet inventory: resolve base URL, list
  projects, visibility, then sample repo/artifact counts on focused
  projects. Skip when no inventory/audit ask.
---

# Harbor project audit

## Gate

User asked what projects exist, for Harbor fleet inventory, or a short
audit of visibility. Prefer Harbor API/UI (no Harbor MCP in the live
catalog). Skip retention purge (`harbor-retention-run`) and delete asks
(apply `harbor-safety` only after an explicit verb).

Always load `harbor-projects` and `harbor-safety`.

## Checklist

1. **Base URL** — from config/env; never hardcode.
   **Done when** the product URL is explicit (no credentials).
2. **List projects** — API/UI.
   **Done when** names/ids come from the live surface or user paste.
3. **Per-project note** — visibility + repo count when available.
   **Done when** each focused project has a one-line note.
4. **Optional sample** — for projects in scope, list a few repos /
   recent tags via `harbor-artifacts` read paths.
   **Done when** the user wanted depth, or you stopped at the project
   list when that was enough.
5. **Safety** — no tokens; no invented deletes.
   **Done when** the reply is inventory-only unless a mutate was
   explicitly authorized.

## Report shape

- Harbor base URL (host only)
- Project list (name / id / visibility / repo count)
- Optional repo/tag sample per focused project
- One recommended next check (artifact scan, retention, or gated mutate)
