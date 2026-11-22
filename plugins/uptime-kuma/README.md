# uptime-kuma

Agnostic Uptime Kuma craft: monitors, status pages, and notification channels
with gated pause/delete via API/UI. No Uptime Kuma MCP discovered — do not
invent tools. Prefer pause over delete; keep API keys and webhook secrets out
of chat.

## Rules (Cursor)

| Rule | Purpose |
| --- | --- |
| `uptime-kuma-monitors` | Monitors/pages/channels inventory and create/update craft |
| `uptime-kuma-mutate` | Gated pause/resume/delete via API/UI |
| `uptime-kuma-safety` | Read-only default, prefer pause, secret refuse |

## Skills

| Skill | Purpose |
| --- | --- |
| `uptime-kuma` | Index / gate / procedure |
| `uptime-kuma-fleet-status` | List → classify up/down/paused |
| `uptime-kuma-pause-or-delete` | Resolve → prefer pause → mutate |

## Commands

- `/uptime-kuma` → Inventory or gated craft
- `/uptime-kuma-status` → Fleet down/paused sweep
- `/uptime-kuma-pause` → Gated pause/delete checklist

## Related capabilities

- Prometheus/Grafana alerting fleets are out of scope — this plugin owns
  Uptime Kuma monitor/page/channel surfaces via API/UI only.

## Diagrams

- [`docs/uptime-kuma-workflow.drawio`](docs/uptime-kuma-workflow.drawio) —
  gate → route → inventory / fleet-status / pause-delete branches
