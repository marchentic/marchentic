---
name: kubernetes-manifest
description: >-
  Author or review portable Kubernetes manifests (read skill; no live apply
  unless the user explicitly asked).
---

# /kubernetes-manifest

1. If the user named no manifest path and no create/review ask, say so and
   stop.
2. Load `kubernetes` and skill `kubernetes-manifest-review` with
   `kubernetes-manifests` (and ESO/addons rules when relevant).
3. Edit or report findings on disk YAML only unless apply was explicit —
   then also follow `kubernetes-safety`.
4. Never commit plaintext secret values.
