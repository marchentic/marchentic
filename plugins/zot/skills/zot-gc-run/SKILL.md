---
name: zot-gc-run
description: >-
  Checklist for gated Zot garbage collection: confirm explicit GC verb,
  prefer tag deletes first, state blob-prune risk, then run via API/UI/CLI
  with a short receipt. Skip when no GC ask.
---

# Zot GC run

## Gate

User asked to garbage-collect, prune unreferenced blobs, or run Zot GC.
Prefer Zot API/UI/CLI. Skip inventory-only asks (`zot-repo-audit`) and
single-tag delete (still `zot-safety` via `zot-tags`).

Always load `zot-safety` (and `zot-repos` / `zot-tags` when scoping).

## Checklist

1. **Verb** — require explicit gc / prune / garbage-collect this turn.
   **Done when** present, or you stopped and asked once.
2. **Scope** — whole registry vs after named tag deletes; never invent
   "delete everything unused" without confirmation.
   **Done when** the GC scope is explicit.
3. **Prefer deletes first** — if the ask is really "remove these tags",
   do tag deletes under `zot-safety` before GC when that is enough.
   **Done when** the narrower path was considered.
4. **Risk** — state that GC removes unreferenced blobs and is hard to
   undo. **Done when** the receipt will include that note.
5. **Act** — run GC via authorized API/UI/CLI; never invent MCP tool
   names. **Done when** the mutate ran only after steps 1–4.
6. **Receipt** — scope + result; no credentials.
   **Done when** the reply matches the report shape.

## Report shape

- Base URL (host only)
- GC scope
- Action taken
- Note that unreferenced blobs were pruned (when applicable)
- "No registry credentials shown"
