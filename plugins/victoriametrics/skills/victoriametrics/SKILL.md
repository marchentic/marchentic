---
name: victoriametrics
description: >-
  Agnostic VictoriaMetrics craft: discover metrics/labels/series/TSDB,
  MetricsQL/PromQL instant/range queries, and alerts/rules inventory via
  MCP. Prefer VictoriaMetrics MCP; discover before guessing. Skip when the
  user did not authorize this surface.
---

# VictoriaMetrics

## Gate

No explicit VictoriaMetrics / MetricsQL / VM / vmselect / vmalert /
PromQL-on-VM ask and no named metric or query → **skip**. Prefer a
connected VictoriaMetrics MCP. Bare product name alone is not enough for
a broad dump.

Route by intent:

| Surface | Signals |
| --- | --- |
| Discover | which metrics, labels, series, TSDB, top/active queries, alerts |
| Query | rate, value now, trend, topk, explain/prettify expression |
| Discover→query | fuzzy surface ("CPU", "error rate") then need a value |
| Safety | secrets in alerts, heavy global cardinality, huge dumps |

## Load map

| Need | Rule / skill |
| --- | --- |
| Metrics / labels / series / TSDB / alerts inventory | `victoriametrics-discover` |
| Instant / range / explain / prettify | `victoriametrics-query` |
| Unknown metric → live value | `victoriametrics-discover` · `victoriametrics-query` · skill `victoriametrics-discover-then-query` |
| Redaction / cardinality refuse | `victoriametrics-safety` (always with the above) |

## Defaults

1. Never invent metric or label names — list/resolve first.
2. Discover before query when the metric is unknown this turn.
3. Prefer live MCP over remembered MetricsQL from other environments.
4. Rate then sum on counters; bound cardinality (`topk`, aggregation,
   modest `limit`/`topN`/`step`).
5. Prefer MCP tools discovered on the live VictoriaMetrics MCP; do not
   invent tool names.
6. Use `explain_query` / `prettify_query` when teaching or sharing long
   expressions.
7. Neighbor dashboard / Explore products are out of scope except as
   context the user already named — this plugin owns VictoriaMetrics MCP.

## Procedure

1. Decide the surface (discover vs query vs discover→query). **Done when**
   you can name one surface, or you skipped because none was asked.
2. Resolve metric/label names from MCP (`metrics`, `series`,
   `metrics_metadata`, …) or from names the user pasted. **Done when**
   every name you will use was listed/read, or you stopped instead of
   inventing.
3. Follow the load-map rule (and `victoriametrics-discover-then-query`
   when the metric was unknown). Always apply `victoriametrics-safety`.
   **Done when** the discovery or MetricsQL matches the ask and the reply
   has **no** secret dumps or unauthorized heavy global TSDB pulls.
4. Stop after a short finding unless the user also asked for a wider
   window. **Done when** the reply has tool + expression or discovery
   evidence + finding (or miss).
