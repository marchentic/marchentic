---
name: prometheus-discover
description: >-
  Discover Prometheus metrics/labels then query when needed (MCP checklist).
---

# prometheus-discover

1. Load `prometheus-discover-then-query` (and the primary `prometheus`
   skill for routing). Prefer a ready Prometheus MCP.
2. Follow the discover → label confirm → bounded PromQL checklist.
3. Never invent metric/label names; apply `prometheus-safety`.
