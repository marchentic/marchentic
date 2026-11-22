---
name: runpod
description: >-
  Agnostic RunPod craft: list pods/endpoints/templates/GPUs and gated
  create/start/stop/delete via user-mcp_runpod. Never invent ids; cost-aware
  defaults. Skip when the user did not authorize this surface.
---

# RunPod

## Gate

No explicit RunPod / GPU cloud / pod / serverless endpoint ask (and no named
pod or endpoint on the RunPod MCP) → **skip**. Prefer connected
`user-mcp_runpod`. Other GPU providers are out of scope.

Route by intent:

| Surface | Signals |
| --- | --- |
| Inventory | list pods, endpoints, templates, GPUs, volumes, billing |
| Pod lifecycle | create / start / stop / restart / delete pod |
| Endpoint / serverless | create / update / deploy / run / purge / delete endpoint |
| Catalog | GPU types, capacity, data centers, hub repos |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / get pods, endpoints, templates, GPUs, billing | `runpod-inventory` |
| Create / update / lifecycle / delete | `runpod-mutate` |
| Pod start/stop/delete checklist | skill `runpod-pod-lifecycle` |
| Endpoint create/deploy checklist | skill `runpod-endpoint-deploy` |
| Gates, cost, refuse secrets | `runpod-safety` (always) |

## Defaults

1. Never invent pod, endpoint, template, volume, or job ids — list/resolve first.
2. Prefer `user-mcp_runpod`; use only tools on the live MCP map.
3. Read inventory before any mutate (`runpod-inventory`).
4. Prefer cheapest GPU that meets the need; state billing while running.
5. Prefer stop / scale-to-zero when idle unless asked to leave up.
6. Never paste API keys, registry passwords, or env secret values into chat.
7. Non-RunPod GPU clouds are out of scope.

## Procedure

1. Decide the surface (inventory / pod lifecycle / endpoint / catalog).
   **Done when** you can name one surface, or you skipped because none was asked.
2. Resolve ids from MCP lists or user paste; never invent.
   **Done when** every id used in gets or mutates was listed/read this turn.
3. Follow the load-map rule and compound skill when lifecycle or endpoint
   deploy is in play. Always apply `runpod-safety`.
   **Done when** actions match the ask and no unauthorized mutate ran.
4. Stop with a short receipt: id + name + status (inventory), or action + id
   + cost note (mutate). **Done when** evidence is cited — no secrets.
