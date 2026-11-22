---
name: home-assistant
description: >-
  Agnostic Home Assistant craft: entity/state inventory, gated service calls,
  and automation hygiene. No HA MCP discovered — use REST/WebSocket API or UI.
  Skip when the user did not authorize this surface.
---

# Home Assistant

## Gate

No explicit Home Assistant / entity / automation / service-call ask (and no
named `entity_id`) → **skip**. Prefer REST/WebSocket API with a resolved base
URL; use an HA MCP only when one is connected — never invent MCP tool names.
Non-HA IoT clouds are out of scope.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list entities, states, areas, devices |
| Audit | room/area sweep, unexpected on states |
| Service call | turn on/off, set, unlock, disarm |
| Automation hygiene | disable/delete automation or script; reload |

## Load map

| Need | Rule / skill |
| --- | --- |
| List entities / states / areas | `home-assistant-entities` |
| Service calls / automation mutate | `home-assistant-services` |
| Area/entity audit pass | skill `home-assistant-entity-audit` |
| Gated service call checklist | skill `home-assistant-service-call` |
| Gates, high-risk, refuse tokens | `home-assistant-safety` (always) |

## Defaults

1. Never invent entity_id — list/resolve first (`light.`, `switch.`, `sensor.`…).
2. No Home Assistant MCP discovered — use authenticated REST/WebSocket API; do not invent tools.
3. Resolve the HA base URL from config/env — never hardcode a host.
4. Prefer targeted service calls over restarting Home Assistant.
5. Never paste long-lived access tokens into chat.
6. Non-HA IoT platforms are out of scope.

## Procedure

1. Decide the surface (inventory / audit / service / automation).
   **Done when** you can name one surface, or you skipped because none was asked.
2. Resolve base URL and entity_ids from API lists or user paste; never invent.
   **Done when** every entity_id used was listed/read this turn.
3. Follow the load-map rule and compound skill when audit or service call
   is in play. Always apply `home-assistant-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: entity_id + state (inventory), or
   domain.service + entity_id + resulting state (mutate). **Done when**
   evidence is cited — no tokens.
