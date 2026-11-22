---
name: authentik
description: >-
  Authentik IdP apps, providers, flows — inventory or gated mutate via
  REST API (no Authentik MCP assumed).
---

# /authentik

1. If the user did not authorize Authentik / IdP work and named no app,
   provider, or flow, say so and stop.
2. Otherwise load `authentik` and follow the matching rule
   (`authentik-apps`, `authentik-providers`, `authentik-flows`,
   `authentik-safety`). For new SSO app + provider pairing, also follow
   `authentik-sso-onboard`.
3. Use Authentik REST API with a resolved base URL — no Authentik MCP was
   discovered; do not invent MCP tools. Never invent object ids.
4. Return name / slug / pk / type evidence — no client secrets, tokens,
   or signing keys.
