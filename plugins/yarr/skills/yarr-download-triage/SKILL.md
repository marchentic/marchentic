---
name: yarr-download-triage
description: >-
  Checklist for qBittorrent queue triage via yarr MCP qbit_* tools.
  Resolve instance and hash; mutates need explicit verb. Skip when no
  download-queue ask.
---

# Yarr download triage

## Gate

User asked about qBittorrent queue state, stuck torrents, pause/resume,
add, or remove via yarr MCP. Skip pure *arr metadata search without
download follow-up.

Always load `yarr-qbit` and `yarr-safety`.

## Checklist

1. **Instance** — resolve the `qbit_*` tool from the live MCP list and
   the user's category (movie/TV/books/cross-seed). Ask once if several
   match. **Done when** one tool is chosen from the live list.
2. **Status** — `service_status`. **Done when** reachability is known.
3. **Queue** — `download_queue` (modest page size). Match by name → take
   `hash` from results. **Done when** hash is from queue or user paste.
4. **Diagnose** — summarize state/progress/errors for the matched
   torrent(s). **Done when** a short finding answers the ask or names
   the blocker.
5. **Mutate only if asked** — `download_pause` / `download_resume` /
   `download_add` / `download_remove` need an explicit verb; file delete
   needs verb covering files (`yarr-safety`). **Done when** refused or
   applied with blast note.
6. **Receipt** — qBit tool + name/hash + action result. **Done when** no
   secrets in the reply.

## Report shape

- qBit tool name
- Torrent name + hash
- State / action taken
- Whether files were deleted (if remove)

