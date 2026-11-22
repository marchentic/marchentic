---
name: home-assistant
description: >-
  Home Assistant inventory, audit, or gated service-call craft via REST API.
---

# /home-assistant

1. If the user did not authorize Home Assistant work, say so and stop.
2. Load skill `home-assistant` with rules `home-assistant-entities`,
   `home-assistant-services`, and always `home-assistant-safety`.
3. Prefer REST/WebSocket API (no HA MCP discovered — do not invent tools).
   List before mutate; never invent entity_ids; never paste tokens.
4. Return entity_id + state (read) or domain.service + entity_id + state
   (mutate). For audits use skill `home-assistant-entity-audit` or
   `/home-assistant-audit`; for service calls use
   `home-assistant-service-call` or `/home-assistant-call`.
