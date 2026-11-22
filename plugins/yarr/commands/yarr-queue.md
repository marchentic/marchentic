---
name: yarr-queue
description: >-
  qBittorrent queue triage via yarr MCP (gated pause/resume/add/remove).
---

# /yarr-queue

1. If the user did not authorize qBit / download-queue work, say so and
   stop.
2. Load `yarr` and skill `yarr-download-triage` with rules `yarr-qbit` /
   `yarr-safety`.
3. Prefer yarr MCP. Resolve the `qbit_*` tool from the live list; take
   torrent hashes from `download_queue` — never invent them.
4. Return qBit tool + name/hash + state or action result (note if files
   deleted). Refuse mutates without an explicit verb.

