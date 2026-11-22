---
name: prometheus
description: >-
  Prometheus discover, PromQL query, or discover-then-query via MCP.
---

# prometheus

1. Load `prometheus`. Prefer a ready Prometheus MCP.
2. Follow the skill gate and load map (`prometheus-discover`,
   `prometheus-query`, `prometheus-safety`; use
   `prometheus-discover-then-query` when the metric is unknown).
3. Never invent metric/label names; report evidence (PromQL, values,
   target health — no secrets; no admin tools without explicit ask).
