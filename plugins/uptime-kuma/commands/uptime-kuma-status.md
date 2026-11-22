---
name: uptime-kuma-status
description: >-
  Uptime Kuma fleet status: down/paused monitor sweep via API/UI.
---

# /uptime-kuma-status

1. If the user did not authorize Uptime Kuma work, say so and stop.
2. Load skill `uptime-kuma-fleet-status` with `uptime-kuma-monitors` and
   `uptime-kuma-safety`.
3. Inventory only unless mutate was also authorized.
4. Return counts + down/paused table — no secrets.
