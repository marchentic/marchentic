---
name: yarr
description: >-
  Media fleet (*arr / Plex / qBit / Seerr) via yarr MCP (gated mutates).
---

# /yarr

1. If the user did not authorize *arr / Plex / qBit / Seerr work, say so
   and stop.
2. Load `yarr` with the load-map rules for the surface (inventory / arr /
   plex / qbit / seerr) and always `yarr-safety` when a mutate is
   possible.
3. Prefer yarr MCP (`user-mcp_yarr`). Resolve service tool + ids/hashes —
   never invent them.
4. Return service + title/id + short finding. For queue triage, prefer
   skill `yarr-download-triage` or `/yarr-queue`.

