---
name: prometheus-discover-then-query
description: >-
  Checklist: discover Prometheus metric/labels via MCP, then run a bounded
  PromQL instant or range query. Prefer MCP. Skip when metric names are
  already known and only a query is asked.
---

# Prometheus discover-then-query

## Gate

User wants a value, rate, or trend but did **not** paste a verified metric
name, or named a fuzzy surface ("CPU", "error rate", "pod memory") that
still needs discovery. Prefer connected Prometheus MCP. Skip pure
inventory with no query intent (`prometheus-discover` alone) and skip when
the user already supplied exact PromQL to run (`prometheus-query` alone).

Always load `prometheus-discover`, `prometheus-query`, and
`prometheus-safety`.

## Checklist

1. **Surface** — restate the question as metric intent (resource, error
   rate, latency, saturation). **Done when** the intent is one sentence.
2. **Find candidates** — `label_values` with `label="__name__"` and a
   tightening `matches` regex when possible; optional `metric_metadata`
   for type/help. **Done when** a short shortlist exists (or a clear miss).
3. **Confirm labels** — `series` on the chosen metric; `label_values` for
   matchers you will use (`job`, `instance`, …). **Done when** every
   matcher label was seen in MCP output or pasted by the user.
4. **Pick tool** — instant `query` for a snapshot; `range_query` for a
   trend (default ~`1h` if unset — say so). **Done when** tool + window
   are explicit.
5. **Craft PromQL** — counters → `rate` then aggregate; gauges → direct
   aggregate; bound with `topk` / `by ()` / `truncation_limit`.
   **Done when** the expression uses only discovered names.
6. **Execute + explain** — run the MCP tool; one-sentence PromQL meaning
   with the finding. **Done when** values or a justified empty result
   are reported.
7. **Safety** — no config secret dumps; no admin tools unless explicitly
   asked (`prometheus-safety`). **Done when** reply is redacted and
   non-destructive unless authorized.

## Report shape

- Candidate metrics considered (from MCP)
- Chosen metric + key labels
- Exact PromQL + tool + window/step
- Short finding
- One next check (targets health, longer window, or tighter matchers)
