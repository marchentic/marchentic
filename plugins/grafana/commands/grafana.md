---
name: grafana
description: >-
  Investigate Grafana Explore, incidents, or alerting (MCP first; read-first).
---

# /grafana

1. If the user did not authorize Grafana/observability work and named no
   dashboard/datasource/rule/incident, say so and stop.
2. Load `grafana`. For Explore/metrics/logs prefer skill
   `grafana-explore-investigate` with `grafana-explore` / `grafana-safety`.
   For incidents use `grafana-incidents`; for alert rules use
   `grafana-alerting`.
3. Prefer Grafana MCP. Never invent UIDs or incident ids.
4. Return findings with evidence and deeplinks when available. Do not mutate
   unless explicitly asked.
