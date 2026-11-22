# home-assistant

Agnostic Home Assistant craft: entity/state inventory, entity audits, and
gated service calls via REST/WebSocket API. No Home Assistant MCP discovered
— do not invent tools. Keep long-lived access tokens out of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `home-assistant-entities` | States / areas / devices inventory via API |
| `home-assistant-services` | Gated service calls and automation mutate |
| `home-assistant-safety` | Read-only default, high-risk gates, token refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `home-assistant` | Index / gate / procedure |
| `home-assistant-entity-audit` | Config → scope → unexpected on/open/unlocked |
| `home-assistant-service-call` | Resolve → warn → POST service → prove state |

## Commands

- `/home-assistant` → HA inventory or gated craft
- `/home-assistant-audit` → Entity/area audit pass
- `/home-assistant-call` → Gated service-call checklist

## Related capabilities

- Non-HA IoT clouds and vendor mobile apps are out of scope — this plugin
  owns Home Assistant entity/service surfaces via API/UI only.

## Diagrams

- [`docs/home-assistant-workflow.drawio`](docs/home-assistant-workflow.drawio) —
  gate → route → inventory / audit / service-call branches
