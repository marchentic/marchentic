---
name: velero-restore
description: >-
  Gated Velero restore: prove backup, scope namespaces, confirm, create, get.
---

# /velero-restore

1. If the user did not authorize a Velero **restore** with an explicit verb,
   stop — inventory only is not enough.
2. Load skill `velero` and `velero-restore-run` with rules `velero-inventory`,
   `velero-mutate`, and `velero-safety`.
3. Prefer `user-mcp_velero`. Prove backup Completed; warn overwrite risk;
   `velero_restore_create` with `confirm=true`; then `velero_restore_get`.
4. Return backup + restore names, phases, and namespace scope.
