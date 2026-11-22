---
name: grafana-dashboard
description: >-
  Search, review, or author Grafana dashboards via MCP (patch preferred).
---

# /grafana-dashboard

1. If the user did not authorize dashboard work, say so and stop.
2. Load `grafana` and skill `grafana-dashboard-author` with rules
   `grafana-dashboards` / `grafana-safety`.
3. Prefer Grafana MCP. Search before create; never invent dashboard or folder
   UIDs.
4. Return title/UID + what changed (or review notes) and a deeplink when
   available. Mutate only with an explicit verb.
