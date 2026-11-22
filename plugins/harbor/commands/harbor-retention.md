---
name: harbor-retention
description: >-
  Gated Harbor retention purge.
---

# /harbor-retention

1. If the user did not authorize Harbor retention, say so and stop.
2. Load skill `harbor-retention-run` with rules `harbor-artifacts` /
   `harbor-projects` / `harbor-safety`.
3. Require an explicit retention/purge verb naming the project; resolve
   scope first (prefer dry-run).
4. Return project + scope + result (no robot tokens or admin passwords).
