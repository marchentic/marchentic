---
name: uptime-kuma-pause
description: >-
  Gated Uptime Kuma pause/resume/delete checklist via API/UI.
---

# /uptime-kuma-pause

1. If the user did not authorize pause/resume/delete, say so and stop.
2. Load skill `uptime-kuma-pause-or-delete` with `uptime-kuma-monitors`,
   `uptime-kuma-mutate`, and `uptime-kuma-safety`.
3. Prefer pause over delete; never invent ids.
4. Return action + ids + status — no secrets.
