---
name: home-assistant-service-call
description: >-
  Gated Home Assistant service-call checklist: resolve entity_id, confirm
  service, high-risk warn, POST /api/services, prove state.
---

# Home Assistant service call

## Gate

User authorized a **service call** (turn on/off, set, unlock, disarm, …)
with an explicit verb naming the entity. Prefer REST API (no HA MCP
discovered). Skip inventory-only asks.

Always load `home-assistant-entities`, `home-assistant-services`,
`home-assistant-safety`, and skill `home-assistant`.

## Checklist

1. **Resolve** — `GET /api/states/<entity_id>` or states list match.
   **Done when** entity exists.
2. **Service** — confirm domain/service via `GET /api/services` when unsure.
   **Done when** domain.service is explicit.
3. **Risk** — for unlock/disarm/garage/HVAC, restate effect; cite
   `home-assistant-safety`.
   **Done when** intent still matches.
4. **Call** — `POST /api/services/<domain>/<service>` with entity_id + data.
   **Done when** API accepted or returned a clear error.
5. **Prove** — `GET /api/states/<entity_id>`; report new state.
   **Done when** receipt has entity_id + service + state — no token.

## Report shape

- entity_id + prior state
- domain.service + key data
- resulting state
- high-risk warning acknowledged when applicable
