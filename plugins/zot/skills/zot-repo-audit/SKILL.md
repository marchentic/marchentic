---
name: zot-repo-audit
description: >-
  Checklist for Zot repository fleet inventory: resolve base URL, list
  repos, then sample tags on focused repositories. Skip when no
  inventory/audit ask.
---

# Zot repo audit

## Gate

User asked what repositories exist, for Zot fleet inventory, or a short
audit of the registry. Prefer Zot API/UI (no Zot MCP in the live catalog).
Skip GC (`zot-gc-run`) and delete asks (apply `zot-safety` only after an
explicit verb).

Always load `zot-repos` and `zot-safety`.

## Checklist

1. **Base URL** — from config/env; never hardcode.
   **Done when** the product URL is explicit (no credentials).
2. **List repositories** — catalog/list API or UI.
   **Done when** names come from the live surface or user paste.
3. **Per-repo note** — tag count when available.
   **Done when** each focused repo has a one-line note.
4. **Optional sample** — for repos in scope, list a few tags via
   `zot-tags` read paths. **Done when** the user wanted depth, or you
   stopped at the repo list when that was enough.
5. **Safety** — no credentials; no invented deletes.
   **Done when** the reply is inventory-only unless a mutate was
   explicitly authorized.

## Report shape

- Zot base URL (host only)
- Repository list (name / tag count)
- Optional tag sample per focused repo
- One recommended next check (referrers, GC, or gated delete)
