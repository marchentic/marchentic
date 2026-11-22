# grafana

Grafana observability craft — dashboards, Explore, incidents, alerting.
Install when Grafana MCP is available.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `grafana-dashboards` | Dashboard search / summary / panel queries / update |
| `grafana-explore` | Explore metrics / logs / profiles + datasource resolve |
| `grafana-incidents` | Incident lifecycle + OnCall read |
| `grafana-alerting` | Alert rules CRUD + routing read |
| `grafana-safety` | Destructive gates (dashboard/datasource/rule/incident/plugin) |

## Skills

| Skill | Purpose |
| --- | --- |
| `grafana` | Index / gate / Procedure |
| `grafana-explore-investigate` | Explore investigation checklist |
| `grafana-dashboard-author` | Dashboard author/review checklist |

## Commands

- `/grafana` → Explore / incidents / alerting (read-first)
- `/grafana-dashboard` → dashboard search / author / patch

## Defaults

- Never invent dashboard, datasource, folder, rule, or incident ids.
- Read/search/query is the default; mutates need an explicit verb.
- Discover labels/metrics before heavy PromQL/LogQL.
- Prefer dedicated MCP tools over raw API; deeplink when useful.
- Neighbor standalone metrics/log platforms — out of scope except as Grafana
  datasources.

## Diagrams

- [`docs/grafana-workflow.drawio`](docs/grafana-workflow.drawio) —
  gate → route (Explore / dashboard / alert / incident) → evidence; mutate
  refuse branch
