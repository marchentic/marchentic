---
name: home-assistant-audit
description: >-
  Home Assistant entity/area audit: unexpected on/open/unlocked states.
---

# /home-assistant-audit

1. If the user did not authorize Home Assistant work, say so and stop.
2. Load skill `home-assistant-entity-audit` with `home-assistant-entities`
   and `home-assistant-safety`.
3. Inventory only unless mutate was also authorized.
4. Return focused entity_id + state lines — no tokens.
