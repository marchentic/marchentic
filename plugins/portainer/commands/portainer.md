---
name: portainer
description: >-
  Portainer endpoint/stack/container craft via API/UI.
---

# /portainer

1. If the user did not authorize Portainer work, say so and stop.
2. Load `portainer` with rules `portainer-endpoints` /
   `portainer-stacks` / `portainer-containers` / `portainer-safety` as
   the load map requires.
3. Prefer Portainer API/UI (no Portainer MCP in the live catalog). Never
   invent endpoint, stack, or container ids.
4. Return endpoint + stack/container + short finding (no tokens). For
   fleet audits prefer skill `portainer-endpoint-audit` or
   `/portainer-audit`; for stack deploy/update prefer
   `portainer-stack-deploy` or `/portainer-stack`.
