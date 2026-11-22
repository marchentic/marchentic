---
name: grafana-explore-investigate
description: >-
  Checklist for Grafana Explore investigation: resolve datasource, discover
  labels/metrics, query lean, deeplink. Prefer MCP. Skip when no Explore or
  metrics/logs symptom was asked.
---

# Grafana Explore investigate

## Gate

User named an Explore ask, PromQL/LogQL/profile question, datasource health
issue, error-rate spike, or "what's in logs/metrics." Prefer connected
Grafana MCP. Skip dashboard-JSON-only asks (use `grafana-dashboard-author` /
`grafana-dashboards`).

## Checklist

1. **Datasource** — `list_datasources` (filter `type`) → `get_datasource` /
   `check_datasources_health` if needed. **Done when** `datasourceUid` is
   from MCP.
2. **Discover** — Prometheus: `list_prometheus_metric_names` →
   `list_prometheus_label_values`. Loki: `list_loki_label_names` /
   `list_loki_label_values`, prefer `query_loki_stats` before heavy pulls.
   Profiles: `list_pyroscope_profile_types` + label tools.
   **Done when** every name in the expr was discovered or you stopped.
3. **Query** — `query_prometheus` / `query_loki_logs` /
   `query_prometheus_histogram` / `query_pyroscope` with a short window.
   Optional Sift: `find_error_pattern_logs`, `find_slow_requests`.
   **Done when** one short result summary answers the symptom.
4. **Safety** — no `create_datasource` / `update_datasource` unless explicit
   (`grafana-safety`). **Done when** no unauthorized mutate ran.
5. **Link** — `generate_deeplink` explore type when useful.
   **Done when** reply has finding + link or a clear skip reason.

## Report shape

- Datasource name / UID / type
- Expr (PromQL/LogQL/profile) + time range
- Short result summary (not raw megabytes)
- Optional Explore deeplink
- One recommended next check
