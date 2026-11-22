---
name: argocd-sync
description: >-
  Gated Argo CD sync, prune, or resource action on a named Application.
---

# /argocd-sync

1. If the user did not authorize a sync / prune / resource-action /
   Application mutate, say so and stop.
2. Load `argocd` with rules `argocd-apps` then `argocd-sync`. Prefer a
   status read (`argocd-app-status`) before live sync when the reason is
   unclear.
3. Prefer Argo CD MCP. Require an explicit verb naming the Application
   (and resource for actions). Prefer `dryRun=true` when prune risk is
   ambiguous; do not invent prune/cascade flags.
4. Return app + action + post-read sync/health (or delete confirmation).
   No unauthorized mass-sync.
