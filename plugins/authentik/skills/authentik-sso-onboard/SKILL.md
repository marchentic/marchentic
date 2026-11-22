---
name: authentik-sso-onboard
description: >-
  Checklist for onboarding an SSO application in Authentik: resolve or
  create provider, bind application, confirm flows — without pasting
  client secrets. Skip when no app/provider onboard ask.
---

# Authentik SSO onboard

## Gate

User asked to add / onboard / wire a new SSO application in Authentik
(OIDC, SAML, or proxy) or to bind an existing provider to an app. Prefer
Authentik REST API (no Authentik MCP discovered). Skip pure inventory
(“list my apps”) and flow-only MFA changes.

Always load `authentik-providers`, `authentik-apps`, `authentik-flows`,
and `authentik-safety`.

## Checklist

1. **Authorize** — confirm an explicit create/bind verb this turn naming
   the application (or create intent). **Done when** verb is present, or
   you refuse and stop.
2. **Base URL** — resolve Authentik URL from operator config/env. **Done
   when** base is known without inventing a host.
3. **Protocol pick** — OIDC/OAuth2 vs SAML vs proxy from the RP docs the
   user named. **Done when** one provider type is chosen.
4. **Flows** — list flows; pick authorization (+ authentication /
   invalidation as required) by slug/designation — never invent flow
   pks (`authentik-flows`). **Done when** flow pks are from list/get.
5. **Provider** — list existing providers for a reuse candidate; else
   create under authorization with redirect URIs / ACS / external host
   **exactly as the user or RP docs stated** (`authentik-providers`).
   **Done when** provider pk exists and **no secret was pasted into
   chat**.
6. **Application** — create or patch app with slug + provider pk
   (`authentik-apps`). **Done when** app GET shows the binding.
7. **Access** — if the user named groups, resolve group UUIDs and apply
   only with an explicit membership verb (`authentik-safety`). **Done
   when** groups were skipped, listed, or updated under authorization.
8. **Receipt** — app name/slug, provider name/type/pk, client_id or
   entity id **names**, flow slugs — zero secrets. **Done when** the
   reply has that shape.

## Report shape

- Application name + slug
- Provider type + pk + client_id / entity id (names only)
- Flow slugs used
- One next step for the operator (RP config fields to copy from Authentik
  UI/metadata — not secrets from chat)
