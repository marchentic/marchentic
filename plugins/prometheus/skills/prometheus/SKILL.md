---
name: prometheus
description: >-
  Agnostic Prometheus craft: discover metrics/labels/targets, PromQL
  instant/range queries, and gated TSDB admin via MCP. Prefer Prometheus
  MCP; discover before guessing. Skip when the user did not authorize this
  surface.
---

# Prometheus

## Gate

No explicit Prometheus / PromQL / metrics / targets / scrape / recording-rule
ask and no named metric or PromQL → **skip**. Prefer a connected Prometheus
MCP. Bare product name alone is not enough for a broad dump or admin call.

Route by intent:

| Surface | Signals |
| --- | --- |
| Discover | which metrics, labels, series, targets, cardinality |
| Query | rate, value now, trend, topk, histogram, alert expression |
| Discover→query | "show CPU" / unknown metric then need a value |
| Admin / safety | delete series, snapshot, reload, quit, secret-looking config |

## Load map

| Need | Rule / skill |
| --- | --- |
| Metrics / labels / series / targets | `prometheus-discover` |
| Instant / range / exemplars | `prometheus-query` |
| Unknown metric → live value | `prometheus-discover` · `prometheus-query` · skill `prometheus-discover-then-query` |
| Admin gate / redaction / cardinality | `prometheus-safety` (always with the above) |

## Defaults

1. Never invent metric, label, job, or instance names — list/resolve first.
2. Discover before query when the metric is unknown this turn.
3. Prefer live MCP over remembered PromQL from other environments.
4. Rate then sum on counters; bound cardinality (`topk`, aggregation,
   `truncation_limit`).
5. Prefer MCP tools discovered on the live Prometheus MCP; do not invent
   tool names.
6. Confirm before `delete_series`, `clean_tombstones`, `snapshot`,
   `reload`, or `quit` (`prometheus-safety`).
7. Neighbor dashboard / Explore products are out of scope except as
   context the user already named — this plugin owns Prometheus MCP.

## Procedure

1. Decide the surface (discover vs query vs discover→query vs admin).
   **Done when** you can name one surface, or you skipped because none
   was asked.
2. Resolve metric/label/job ids from MCP (`label_values`, `series`,
   `list_targets`, …) or from names the user pasted. **Done when** every
   name you will use was listed/read, or you stopped instead of inventing.
3. Follow the load-map rule (and `prometheus-discover-then-query` when the
   metric was unknown). Always apply `prometheus-safety`. **Done when**
   the discovery or PromQL matches the ask and the reply has **no**
   secret dumps or unauthorized admin calls.
4. Stop after a short finding unless the user also asked for a wider
   window or admin mutate. **Done when** the reply has tool + PromQL or
   discovery evidence + finding (or miss), and no unauthorized destructive
   tool ran.
