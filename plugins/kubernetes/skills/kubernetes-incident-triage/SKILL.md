---
name: kubernetes-incident-triage
description: >-
  Checklist for live Kubernetes incident triage: resolve namespace, status,
  events, then logs. Prefer MCP. Skip when no cluster symptom was asked.
---

# Kubernetes incident triage

## Gate

User named a failing workload, namespace outage, CrashLoop, Pending, or
"pods down." Prefer connected Kubernetes MCP. Skip create-manifest-only asks
(use `kubernetes-manifest-review` / `kubernetes-manifests`).

## Checklist

1. **Namespace** — user-named or `namespaces_list`. Do not guess prod.
   **Done when** ns is known or ask stopped.
2. **Workload status** — `pods_list_in_namespace` / `pods_get` /
   `resources_get` on Deployment/StatefulSet. Note ready, restarts, phase.
   **Done when** failing object names are listed from the API.
3. **Events** — `events_list` scoped to the object or namespace. Prefer
   Warning. **Done when** scheduling/pull/probe reasons are known or absent.
4. **Symptom map** — apply `kubernetes-triage` symptom tree (Pending,
   CrashLoop, ImagePull, OOM, Evicted). **Done when** one primary cause class
   is named.
5. **Logs** — only if still unclear; follow `kubernetes-logs` (tail +
   previous). **Done when** a short redacted excerpt supports the cause, or
   logs were unnecessary.
6. **Safety** — no delete/scale/exec unless explicit (`kubernetes-safety`).
   **Done when** the reply is diagnosis + next check, not an unauthorized
   mutate.

## Report shape

- Object / namespace
- Phase or container state + reason
- Event or log evidence (one short block)
- One recommended next step
