---
name: authentik
description: >-
  Agnostic Authentik IdP craft: applications, providers, flows, and groups
  with gated destructive changes. Prefer Authentik REST API (no Authentik
  MCP discovered). Skip when the user did not authorize this surface.
---

# Authentik

## Gate

No explicit Authentik / IdP app / OIDC provider / SAML / SSO flow / group
ask and no named application slug or provider → **skip**. Other IdP
products (Keycloak, Authelia, generic “OIDC”) are out of scope — do not
absorb them here. Prefer a connected Authentik MCP when one exists;
otherwise Authentik REST API with a resolved base URL. Bare product name
alone is not enough for mutates.

Route by surface:

| Surface | Signals |
| --- | --- |
| Applications | app, slug, launch URL, provider binding |
| Providers | OAuth2/OIDC, SAML, proxy/forward-auth, client id |
| Flows | authentication/authorization/enrollment/recovery stages |
| Groups / access | group membership, who can reach an app |
| Risk / mutate | delete, disable, secret rotate, weaken MFA, broaden admin |

## Load map

| Need | Rule / skill |
| --- | --- |
| List / craft applications + group access inventory | `authentik-apps` |
| OIDC / SAML / proxy providers | `authentik-providers` |
| Flows / stages | `authentik-flows` |
| App + provider onboard checklist | skill `authentik-sso-onboard` |
| Delete / disable / secrets / MFA weaken / ACL widen | `authentik-safety` |

## Defaults

1. Never invent application, provider, flow, or group ids — list/resolve
   first.
2. Resolve the Authentik base URL from config/env — never hardcode a host.
3. No Authentik MCP was discovered — use REST API (Bearer token). Prefer
   MCP when ready; **do not invent MCP tool names**.
4. Prefer update-in-place over delete+recreate for provider/client changes.
5. Edge reverse-proxy wiring is out of scope — this plugin owns Authentik
   IdP craft only.
6. Never paste client secrets, API tokens, signing keys, or user
   credentials into chat — report names/slugs/pks only.
7. Cap large listings; summarize and tighten search.

## Procedure

1. Decide the surface (apps vs providers vs flows vs groups vs gated
   mutate). **Done when** you can name one surface, or you skipped
   because none was asked.
2. Resolve base URL + object ids via list/get (or user-pasted slug/pk).
   **Done when** every id you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and `authentik-sso-onboard` when pairing a
   new app with a provider). Always apply `authentik-safety` when a
   mutate is in play. **Done when** evidence matches the ask or the
   mutate was refused for lack of verb.
4. Stop after evidence unless the user also used an implement/mutate
   verb. **Done when** the reply has name + slug/pk + type (no secrets),
   and no unauthorized mutate ran.
