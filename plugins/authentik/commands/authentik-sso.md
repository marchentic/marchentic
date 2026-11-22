---
name: authentik-sso
description: >-
  Onboard or bind an Authentik SSO application + provider (gated; no
  secrets in chat).
---

# /authentik-sso

1. If the user did not ask to onboard/bind an Authentik SSO app, say so
   and stop.
2. Load `authentik-sso-onboard` and follow its checklist (providers →
   flows → app bind → optional groups).
3. Apply `authentik-safety` on every mutate. Never paste client secrets.
4. Return app slug + provider pk/type + flow slugs — no secret material.
