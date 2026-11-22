---
name: portainer-stack
description: >-
  Gated Portainer stack deploy or update.
---

# /portainer-stack

1. If the user did not authorize Portainer stack mutate, say so and stop.
2. Load skill `portainer-stack-deploy` with rules `portainer-stacks` /
   `portainer-endpoints` / `portainer-safety`.
3. Require an explicit deploy/update verb naming the stack; resolve
   endpoint first.
4. Return endpoint + stack + status (no tokens or env secret values).
