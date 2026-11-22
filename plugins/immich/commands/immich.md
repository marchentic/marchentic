---
name: immich
description: >-
  Immich inventory, search, or gated share/delete craft via Immich API.
---

# /immich

1. If the user did not authorize Immich library work, say so and stop.
2. Load skill `immich` with rules `immich-library`, `immich-mutate`, and
   always `immich-safety`.
3. Prefer Immich REST API (no Immich MCP discovered — do not invent tools).
   List before mutate; never invent ids; never paste API keys or media bytes.
4. Return id + name/count (read) or action + ids (mutate). For search use
   skill `immich-library-search` or `/immich-search`; for share/delete use
   `immich-share-or-delete` or `/immich-share`.
