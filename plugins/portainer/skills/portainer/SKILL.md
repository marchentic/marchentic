---
name: portainer
description: >-
  Agnostic Portainer craft: endpoint/stack/container inventory and gated
  stack/container mutations via API/UI. Never invent endpoint ids; refuse
  token dumps. Skip when the user did not authorize this surface.
---

# Portainer

## Gate

No explicit Portainer / Docker UI stack / endpoint / container ask →
**skip**. Bare “Docker” alone is not enough unless Portainer is named or
clearly the ops surface. Checked-in Compose file authorship is out of
scope — this plugin owns Portainer UI/API ops against live endpoints.

No Portainer MCP was discovered in the live harness catalog. Prefer
Portainer API/UI with a resolved base URL. If an MCP appears later,
discover tools from the live map; do not invent tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Endpoints | list environments, endpoint health, pick where a stack lives |
| Stacks | list/deploy/update/delete stacks |
| Containers | list/stop/restart/remove containers, logs |
| Audit | “what’s on Portainer”, endpoint fleet inventory |
| Mutate risk | deploy, delete, prune, ACL/credential change |

## Load map

| Need | Rule / skill |
| --- | --- |
| Endpoint list / resolve / health | `portainer-endpoints` |
| Stack list / deploy / update / delete | `portainer-stacks` |
| Container list / stop / remove / logs | `portainer-containers` |
| Endpoint fleet checklist | `portainer-endpoints` · skill `portainer-endpoint-audit` |
| Stack deploy checklist | `portainer-stacks` · skill `portainer-stack-deploy` |
| Deploy / stop / delete / prune / secrets | `portainer-safety` (always) |

## Defaults

1. Never invent endpoint, stack, or container ids — list/resolve first.
2. Resolve the Portainer base URL from config/env — never hardcode a host.
3. Resolve **endpoint** before stack or container mutates.
4. Prefer named container stop over stack teardown; prefer stack update
   over delete+redeploy.
5. Never paste API tokens or stack env secret values into chat.
6. Own Portainer live ops only — Compose merge layouts and other
   orchestrators are out of scope.

## Procedure

1. Decide the surface (endpoints / stacks / containers / audit / gated
   mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve base URL + endpoint (+ stack/container) from list or user
   paste. **Done when** every id you will use was listed/read, or you
   stopped instead of inventing one.
3. Follow the load-map rule (and compound skill for audit or stack
   deploy). Always apply `portainer-safety`. **Done when** the action
   matches the ask and the reply has **no** tokens or env secret bodies.
4. Stop after a short receipt unless the user also used an explicit
   destructive or deploy verb. **Done when** the reply has endpoint +
   stack/container and no unauthorized delete/prune ran.
