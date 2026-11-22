---
name: uptime-kuma
description: >-
  Uptime Kuma inventory, fleet status, or gated pause/delete craft via API/UI.
---

# /uptime-kuma

1. If the user did not authorize Uptime Kuma work, say so and stop.
2. Load skill `uptime-kuma` with rules `uptime-kuma-monitors`,
   `uptime-kuma-mutate`, and always `uptime-kuma-safety`.
3. Prefer API/UI (no Uptime Kuma MCP discovered — do not invent tools).
   List before mutate; never invent ids; never paste secrets.
4. Return id + name + type + status (read) or action + ids (mutate). For
   fleet status use skill `uptime-kuma-fleet-status` or `/uptime-kuma-status`;
   for pause/delete use `uptime-kuma-pause-or-delete` or `/uptime-kuma-pause`.
