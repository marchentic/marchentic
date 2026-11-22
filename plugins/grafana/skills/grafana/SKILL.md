---
name: grafana
description: >-
  Grafana craft: dashboards, Explore (metrics/logs/profiles), incidents, and
  alerting via MCP. Prefer Grafana MCP. Skip when the user did not authorize
  observability work. Destructive changes need an explicit verb.
---

# Grafana

## Gate

No explicit Grafana / dashboard / Explore / alert / incident / OnCall ask
and no named dashboard/datasource/rule/incident → **skip**. Prefer a
connected Grafana MCP. Bare product name alone is not enough for mutates.

Route by intent:

| Surface | Signals |
| --- | --- |
| Dashboards | search, panel, folder, snapshot, patch dashboard JSON |
| Explore | PromQL, LogQL, profiles, datasource health, Sift |
| Incidents | open/resolve incident, timeline note, who is on-call |
| Alerting | alert rules, firing state, contact points, policies |
| Mutate | update dashboard, create datasource, create/delete rule, create incident, install plugin |

## Load map

| Need | Rule / skill |
| --- | --- |
| Search / author / patch dashboards | `grafana-dashboards` · skill `grafana-dashboard-author` |
| Explore metrics / logs / profiles | `grafana-explore` · skill `grafana-explore-investigate` |
| Incidents / OnCall read | `grafana-incidents` |
| Alert rules / routing read | `grafana-alerting` |
| Destructive dashboard / datasource / rule / incident / plugin | `grafana-safety` |

## Defaults

1. Never invent dashboard UID, datasource UID, folder UID, rule UID, or
   incident id — list/search/get first.
2. Discover metric/label names before complex PromQL/LogQL.
3. Prefer live MCP queries over guessing from memory.
4. Read/search/query is the default; mutates need an explicit verb
   (`grafana-safety`).
5. Prefer dedicated tools over `grafana_api_request`.
6. Operator replies: short findings + `generate_deeplink` when useful
   (user-facing host from MCP — no invented localhost URLs).
7. Neighbor standalone metrics/log platforms are out of scope except as
   Grafana datasources on this surface.

## Procedure

1. Decide the surface (dashboard vs Explore vs incident vs alerting vs
   mutate). **Done when** you can name one surface, or you skipped because
   none was asked.
2. Resolve ids from MCP (dashboard/datasource/folder/rule/incident).
   **Done when** every id you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and compound skill when investigating or
   authoring dashboards). **Done when** evidence matches the ask or the
   mutate was refused for lack of verb.
4. Stop after evidence unless the user also used an implement/mutate verb.
   **Done when** the reply has UID/title + finding or what changed, and no
   unauthorized mutate ran.
