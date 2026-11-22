---
name: kubernetes-manifest-review
description: >-
  Review or author portable Kubernetes manifests against kubernetes-manifests
  (labels, probes, images, YAML floor). Skip live-cluster-only asks.
---

# Kubernetes manifest review

## Gate

User asked to write, fix, or review Deployment/Service/Ingress/Job YAML (or
similar) on disk. Skip pure live triage (use `kubernetes-incident-triage`).

## Checklist

1. **Scope files** — named paths or globs the user pointed at. **Done when**
   the file set is explicit.
2. **YAML floor** — load `kubernetes-manifests` (indent, quotes, no secret
   values). **Done when** each file parses and follows the floor.
3. **Workload shape** — labels/selectors match; probes present where required;
   images pinned (non-`latest` when policy says); resources sensible.
   **Done when** mismatches are fixed or listed as findings.
4. **Secrets** — plaintext Secret data → refuse; point to ExternalSecret /
   `kubernetes-external-secrets`. **Done when** no secret values remain in
   git-bound YAML you touched.
5. **Addons** — LB/Ingress/operator notes only via `kubernetes-addons`. Site
   overlays out of scope. **Done when** portable only.
6. **Apply** — editing files ≠ applying. Live apply needs explicit verb +
   `kubernetes-safety`. **Done when** you did not apply without authorization.

## Report shape

- Paths reviewed
- Must-fix vs note findings (with line/path)
- Whether apply was requested (yes/no)
