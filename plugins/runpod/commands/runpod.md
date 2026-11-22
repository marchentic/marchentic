---
name: runpod
description: >-
  RunPod inventory or gated pod/endpoint craft via user-mcp_runpod.
---

# /runpod

1. If the user did not authorize RunPod GPU cloud work, say so and stop.
2. Load skill `runpod` with rules `runpod-inventory`, `runpod-mutate`, and
   always `runpod-safety`.
3. Prefer `user-mcp_runpod`. List before get; never invent pod or endpoint ids.
4. Return id + name + status (read) or action + id + cost note (mutate).
   For pod lifecycle use skill `runpod-pod-lifecycle` or `/runpod-pod`; for
   endpoint deploy use skill `runpod-endpoint-deploy` or `/runpod-endpoint`.
