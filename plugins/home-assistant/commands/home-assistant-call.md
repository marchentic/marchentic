---
name: home-assistant-call
description: >-
  Gated Home Assistant service-call checklist via REST API.
---

# /home-assistant-call

1. If the user did not authorize a service call, say so and stop.
2. Load skill `home-assistant-service-call` with `home-assistant-entities`,
   `home-assistant-services`, and `home-assistant-safety`.
3. Warn on unlock/disarm/garage/HVAC; never invent entity_ids.
4. Return domain.service + entity_id + resulting state — no tokens.
