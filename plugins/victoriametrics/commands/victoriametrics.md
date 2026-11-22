---
name: victoriametrics
description: >-
  VictoriaMetrics discover, MetricsQL query, or discover-then-query via MCP.
---

# victoriametrics

1. Load `victoriametrics`. Prefer a ready VictoriaMetrics MCP.
2. Follow the skill gate and load map (`victoriametrics-discover`,
   `victoriametrics-query`, `victoriametrics-safety`; use
   `victoriametrics-discover-then-query` when the metric is unknown).
3. Never invent metric/label names; report evidence (MetricsQL, values,
   cardinality — no secrets).
