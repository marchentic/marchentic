---
name: runpod-pod-lifecycle
description: >-
  Gated RunPod pod lifecycle: resolve pod, cost note, start/stop/restart/delete
  via MCP, prove with get-pod. Skip when only inventory was asked.
---

# RunPod pod lifecycle

## Gate

User authorized pod **start**, **stop**, **restart**, **delete**, or a
create-then-start path with an explicit verb. Prefer `user-mcp_runpod`.
Skip pure list/get (use `runpod-inventory`) and endpoint-only asks.

Always load `runpod-inventory`, `runpod-mutate`, `runpod-safety`, and skill
`runpod`.

## Checklist

1. **Resolve** — `list-pods` / `get-pod` for the named id.
   **Done when** pod exists (or create path resolved GPU + image first).
2. **Cost** — state billing impact (start/create bills while running; stop
   ends GPU time; delete is permanent).
   **Done when** user intent still matches after the note.
3. **Act** — `start-pod` / `stop-pod` / `restart-pod` / `delete-pod` /
   `create-pod` per `runpod-mutate`.
   **Done when** MCP accepted the call or returned a clear error.
4. **Prove** — `get-pod` (skip after delete if gone); report status.
   **Done when** receipt has id + status + cost note — no secrets.

## Report shape

- pod id + name
- action + resulting status
- GPU / image hint when relevant
- cost note
