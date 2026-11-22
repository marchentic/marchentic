---
name: kubernetes
description: >-
  Agnostic Kubernetes craft: portable manifest authoring plus pods, events,
  logs, and node summary via MCP. Prefer Kubernetes MCP. Skip when the user
  did not authorize cluster or manifest work. Destructive actions need an
  explicit ask.
---

# Kubernetes

## Gate

No explicit Kubernetes / pod / namespace / cluster / manifest / workload ask
and no named object → **skip**. Prefer a connected Kubernetes MCP for live
cluster work. Bare product name alone is not enough.

Route by intent:

| Surface | Signals |
| --- | --- |
| Live triage | pod status, Pending, CrashLoop, events, "what's broken" |
| Logs | logs, previous container, crash output |
| Manifests | Deployment/Service YAML, review manifests, portable craft |
| Secrets-as-refs | ExternalSecret, SecretStore, ESO |
| Addons | LoadBalancer, Ingress, Postgres operator, cache |
| Mutate | delete, scale, exec, apply, privileged |

## Load map

| Need | Rule / skill |
| --- | --- |
| Write / review manifests | `kubernetes-manifests` · skill `kubernetes-manifest-review` |
| Pod / workload status | `kubernetes-triage` · skill `kubernetes-incident-triage` |
| Logs / previous crash | `kubernetes-logs` |
| ExternalSecret / SecretStore | `kubernetes-external-secrets` |
| Load balancer / ingress / Postgres operator / cache | `kubernetes-addons` |
| Delete / scale / exec / apply risk | `kubernetes-safety` |

## Defaults

1. Never invent cluster context, namespace, or pod names — list/resolve.
2. Read-only triage is the default (get/list/log/events/top).
3. Manifest edits follow `kubernetes-manifests` (YAML floor is in that rule);
   do not encode site GitOps paths or secret-store layout here.
4. Metrics and dashboards are out of scope — this plugin owns k8s API triage
   and portable manifest craft.
5. Site-specific overlays stay in private site repos — keep this plugin
   agnostic.
6. External-secret payloads live in the project's secret provider — never
   commit plaintext Secrets beside ExternalSecrets.
7. Mutates need an explicit verb this turn — see `kubernetes-safety`.

## Procedure

1. Decide the surface (live triage vs manifest craft vs mutate).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve ids from MCP (namespace, pod, workload) or from files on disk for
   manifest work. **Done when** every id you will use was listed/read, or you
   stopped instead of inventing one.
3. Follow the load-map rule (and compound skill when reviewing or
   incident-triaging). **Done when** status/logs match the symptom tree or the
   YAML matches `kubernetes-manifests`.
4. Stop after evidence unless the user also used an implement/mutate verb.
   **Done when** the reply has object + phase/reason or file paths, and no
   unauthorized cluster mutate ran.
