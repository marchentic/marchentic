---
name: argocd
description: >-
  Agnostic Argo CD craft: list/get apps, sync status, and gated sync/action
  via MCP. Prefer Argo CD MCP; never invent app names. Skip when the user
  did not authorize this surface.
---

# Argocd

## Gate

No explicit Argo CD / Application / sync ask and no named Argo CD app →
**skip**. Bare "GitOps" without Argo CD is out of scope. Prefer a
connected MCP. Bare product name alone is not enough for a broad mutate.

Route by intent:

| Surface | Signals |
| --- | --- |
| App status | health, sync status, OutOfSync, Degraded, tree, events |
| Logs / resources | managed resources, workload logs, resource events |
| Sync / refresh | sync, refresh, prune, dry-run sync |
| Resource action | restart, delete-pod, listed actions on a child |
| App CRUD | create / update / delete Application |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / get / tree / events / logs / projects / clusters | `argocd-apps` |
| Status triage checklist | `argocd-apps` · skill `argocd-app-status` |
| Sync / prune / resource actions / create / update / delete | `argocd-sync` |
| Explicit gated sync run | `argocd-sync` (status first via `argocd-app-status` when unclear) |

## Defaults

1. Never invent Application name, Application namespace, project, revision,
   or cluster server — list/resolve first.
2. Read status/events/tree before syncing when the reason is unclear.
3. Sync, prune, resource actions, and Application CRUD need an explicit
   verb naming the app (and resource when scoped).
4. Prefer `dryRun=true` on sync when prune risk is ambiguous.
5. Prefer MCP tools discovered on the live Argo CD MCP; do not invent
   tool names.
6. Pod / Deployment triage outside an Application is out of scope —
   this plugin owns Argo CD Applications.
7. Site overlays and private app catalogs stay in private site repos —
   keep this plugin agnostic.

## Procedure

1. Decide the surface (status vs logs/resources vs sync vs action vs
   CRUD). **Done when** you can name one surface, or you skipped because
   none was asked.
2. Resolve ids from MCP (`list_applications`, `get_application`) or from
   names the user pasted. **Done when** every id you will use was
   listed/read, or you stopped instead of inventing one.
3. Follow the load-map rule (and `argocd-app-status` for health/sync
   triage). Apply `argocd-sync` gates before any mutate. **Done when**
   status evidence matches the ask, or the authorized mutate completed
   and was re-read.
4. Stop after evidence unless the user also used an explicit sync /
   action / CRUD verb. **Done when** the reply has app + sync/health (or
   mutate result), and no unauthorized sync/prune/delete ran.
