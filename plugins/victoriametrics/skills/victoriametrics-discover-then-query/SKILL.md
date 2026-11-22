---
name: victoriametrics-discover-then-query
description: >-
  Checklist: discover VictoriaMetrics metric/labels via MCP, then run a
  bounded MetricsQL/PromQL instant or range query. Prefer MCP. Skip when
  metric names are already known and only a query is asked.
---

# VictoriaMetrics discover-then-query

## Gate

User wants a value, rate, or trend but did **not** paste a verified metric
name, or named a fuzzy surface ("CPU", "error rate", "pod memory") that
still needs discovery. Prefer connected VictoriaMetrics MCP. Skip pure
inventory with no query intent (`victoriametrics-discover` alone) and skip
when the user already supplied exact MetricsQL to run
(`victoriametrics-query` alone).

Always load `victoriametrics-discover`, `victoriametrics-query`, and
`victoriametrics-safety`.

## Checklist

1. **Surface** — restate the question as metric intent (resource, error
   rate, latency, saturation). **Done when** the intent is one sentence.
2. **Find candidates** — `metrics` and/or `metrics_metadata` (`search`
   keyword) with modest `limit`. **Done when** a short shortlist exists
   (or a clear miss).
3. **Confirm labels** — `series` + `label_values` for matchers you will
   use. **Done when** every matcher label was seen in MCP output or
   pasted by the user.
4. **Pick tool** — instant `query` for a snapshot; `query_range` for a
   trend (default ~1h if unset — say so; `start` required for range).
   **Done when** tool + window are explicit.
5. **Craft MetricsQL/PromQL** — counters → `rate` then aggregate; gauges
   → direct aggregate; bound with `topk` / `by ()`. Optional
   `prettify_query` / `explain_query`. **Done when** the expression uses
   only discovered names.
6. **Execute + explain** — run the MCP tool; one-sentence meaning with
   the finding. **Done when** values or a justified empty result are
   reported.
7. **Safety** — no secret dumps; no global heavy `tsdb_status` unless
   asked (`victoriametrics-safety`). **Done when** reply is redacted.

## Report shape

- Candidate metrics considered (from MCP)
- Chosen metric + key labels
- Exact MetricsQL/PromQL + tool + window/step
- Short finding
- One next check (TSDB cardinality, longer window, or tighter matchers)
