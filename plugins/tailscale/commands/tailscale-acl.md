---
name: tailscale-acl
description: >-
  Review or gated-change Tailscale ACL/grants (minimal diff; no keys in
  chat).
---

# /tailscale-acl

1. If the user did not ask about Tailscale ACL/grants, say so and stop.
2. For review-only: load `tailscale-acls` and summarize. For changes:
   load `tailscale-acl-change` and follow its checklist.
3. Apply `tailscale-safety` on every mutate. Never paste auth keys.
4. Return a short policy diff summary — no API tokens or key material.
