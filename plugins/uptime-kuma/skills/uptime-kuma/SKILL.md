---
name: uptime-kuma
description: >-
  Agnostic Uptime Kuma craft: monitors, status pages, and notification channels
  with gated delete/pause via API/UI. No Uptime Kuma MCP discovered — do not
  invent tools. Skip when the user did not authorize this surface.
---

# Uptime Kuma

## Gate

No explicit Uptime Kuma / uptime monitor / status page ask (and no named
monitor id) → **skip**. Prefer API/UI with a resolved base URL; use an
Uptime Kuma MCP only when one is connected — never invent MCP tool names.
Prometheus/Grafana alerting fleets are out of scope as a substitute.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list monitors, pages, notifications, tags |
| Fleet status | who is down, pause state, heartbeat sweep |
| Create / update | new or edited monitor/page |
| Pause / delete | pause, resume, delete |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / create / update monitors and pages | `uptime-kuma-monitors` |
| Delete / pause / bulk risk | `uptime-kuma-mutate` |
| Fleet down/pause sweep | skill `uptime-kuma-fleet-status` |
| Pause or delete checklist | skill `uptime-kuma-pause-or-delete` |
| Gates, prefer pause, refuse secrets | `uptime-kuma-safety` (always) |

## Defaults

1. Never invent monitor, tag, or status-page ids — list/resolve first.
2. No Uptime Kuma MCP discovered — use authenticated API/UI; do not invent tools.
3. Resolve the instance base URL from config/env — never hardcode a host.
4. Prefer pause over delete when the user only wants quiet.
5. Never paste API keys or notification webhook secrets into chat.
6. Prometheus/Grafana rule fleets are out of scope for this plugin.

## Procedure

1. Decide the surface (inventory / fleet status / create-update / pause-delete).
   **Done when** you can name one surface, or you skipped because none was asked.
2. Resolve base URL and ids from API/UI lists or user paste; never invent.
   **Done when** every id used was listed/read this turn.
3. Follow the load-map rule and compound skill when fleet status or
   pause/delete is in play. Always apply `uptime-kuma-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: id + name + type + status (inventory), or
   action + ids (mutate). **Done when** evidence is cited — no secrets.
