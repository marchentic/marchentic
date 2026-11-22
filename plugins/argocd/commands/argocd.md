---
name: argocd
description: >-
  Argo CD Application status, tree, or events via MCP.
---

# /argocd

1. If the user did not authorize Argo CD / Application work, say so and
   stop.
2. Load `argocd` with rule `argocd-apps` (and skill `argocd-app-status`
   for health/sync triage).
3. Prefer Argo CD MCP. List/resolve apps before inventing names; never
   invent Application namespace or project.
4. Return app + sync/health (+ tree/event finding when relevant). For an
   explicit sync/prune/action ask, prefer `/argocd-sync` and rule
   `argocd-sync`.
