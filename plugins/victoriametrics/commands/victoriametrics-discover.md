---
name: victoriametrics-discover
description: >-
  Discover VictoriaMetrics metrics/labels then query when needed (MCP checklist).
---

# victoriametrics-discover

1. Load `victoriametrics-discover-then-query` (and the primary
   `victoriametrics` skill for routing). Prefer a ready VictoriaMetrics MCP.
2. Follow the discover → label confirm → bounded MetricsQL checklist.
3. Never invent metric/label names; apply `victoriametrics-safety`.
