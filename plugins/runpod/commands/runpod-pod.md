---
name: runpod-pod
description: >-
  Gated RunPod pod start/stop/restart/delete checklist via MCP.
---

# /runpod-pod

1. If the user did not authorize a pod lifecycle action, say so and stop.
2. Load skill `runpod-pod-lifecycle` with `runpod-inventory`, `runpod-mutate`,
   and `runpod-safety`.
3. State cost impact; never invent pod ids.
4. Return pod id + status + cost note — no secrets.
