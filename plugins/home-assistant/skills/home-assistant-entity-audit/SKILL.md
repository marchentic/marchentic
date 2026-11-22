---
name: home-assistant-entity-audit
description: >-
  Home Assistant entity audit: config check, domain/area sweep, flag unexpected
  on/open/unlocked states. API/UI only; no HA MCP discovered.
---

# Home Assistant entity audit

## Gate

User asked what is on, what looks wrong, or for a short entity/area audit.
Prefer REST API (no HA MCP discovered). Skip pure single-entity get and
service-call paths.

Always load `home-assistant-entities`, `home-assistant-safety`, and skill
`home-assistant`.

## Checklist

1. **Connect** — `GET /api/config` (or `/api/`).
   **Done when** instance version/location hint is captured, or auth failed.
2. **Scope** — area/device/domain from the ask; else summarize by domain counts.
   **Done when** scope is explicit.
3. **Sweep** — `GET /api/states` filtered to scope; flag `on` / `open` /
   `unlocked` / `home` anomalies the user cares about.
   **Done when** each cited entity has entity_id + state.
4. **Safety** — inventory only unless user also authorized service calls.
   **Done when** receipt has no unauthorized mutate.

## Report shape

- Instance line (version/location — no token)
- Focused entities: entity_id, friendly_name, state
- One recommended next step (gated service call or further inventory)
