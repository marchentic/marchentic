---
name: argocd-app-status
description: >-
  Checklist for Argo CD Application status triage: resolve app, read
  health/sync, tree and events, short redacted finding. Prefer MCP. Skip
  when no status / health / OutOfSync ask.
---

# Argocd app status

## Gate

User asked for Application health, sync status, OutOfSync / Degraded /
Progressing diagnosis, resource tree, or recent sync events. Prefer
connected Argo CD MCP. Skip pure sync/create/delete asks without a status
read (those go through `argocd-sync` after an explicit mutate verb).

Always load `argocd-apps`. Load `argocd-sync` only if the user also asked
to sync or act after the triage.

## Checklist

1. **Resolve** — exact name from the user, else `list_applications`
   (`search` when known) → confirm with `get_application`. Pass
   `applicationNamespace` when non-default. **Done when** name +
   namespace are from MCP or paste, not invented.
2. **Status** — from `get_application`, report sync status, health,
   revision, destination, and whether automated sync is configured.
   **Done when** those fields are from a fresh read this turn.
3. **Tree** — if health is not Healthy or sync is OutOfSync,
   `get_application_resource_tree` and name failing/progressing children
   (kind + name). **Done when** one short tree finding explains the
   status, or the tree is Healthy/Synced.
4. **Events** — `get_application_events` (and `get_resource_events` for
   a named failing child) when the tree does not explain the failure.
   Summarize; redact secrets. **Done when** event signal is stated or
   explicitly absent.
5. **Resources / logs** — only when asked: filtered
   `get_application_managed_resources` / `get_resources`, or
   `get_application_workload_logs` with a real `resourceRef` from the
   tree. Keep excerpts short. **Done when** the asked resource/log slice
   is covered without a full dump.
6. **Stop or hand off** — do not sync, prune, or run resource actions
   unless the user used an explicit mutate verb this turn
   (`argocd-sync`). **Done when** the reply has app + sync/health +
   next check, and no unauthorized mutate ran.

## Report shape

- Application name + namespace (+ project)
- Sync status + health (+ revision when cheap)
- Failing child(s) or event signal
- One recommended next check (wait, fix source, or sync with explicit
  verb / `/argocd-sync`)
