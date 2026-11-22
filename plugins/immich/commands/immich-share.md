---
name: immich-share
description: >-
  Gated Immich share-link or trash/delete checklist via API.
---

# /immich-share

1. If the user did not authorize share or delete, say so and stop.
2. Load skill `immich-share-or-delete` with `immich-library`, `immich-mutate`,
   and `immich-safety`.
3. Warn on public URL exposure or permanent delete; prefer trash when soft.
4. Return action + ids + outcome — no keys.
