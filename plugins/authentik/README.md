# authentik

Agnostic Authentik IdP craft — applications, providers, flows, and group
access inventory with destructive gates. Install when Authentik SSO / OIDC
/ SAML is in play. No Authentik MCP is assumed; craft uses the Authentik
REST API. Neighbor IdPs and reverse-proxy wiring stay out of scope.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `authentik-apps` | Applications list/craft + group access inventory |
| `authentik-providers` | OIDC / SAML / proxy providers (no secret dumps) |
| `authentik-flows` | Flows / stages; MFA/recovery risk gates |
| `authentik-safety` | Delete / disable / secrets / privilege / MFA weaken |

## Skills

| Skill | Purpose |
| --- | --- |
| `authentik` | Index / gate / Procedure |
| `authentik-sso-onboard` | App + provider onboard checklist |

## Commands

- `/authentik` → Authentik surface craft (read-first)
- `/authentik-sso` → gated SSO app + provider onboard

## Defaults

- Never invent application, provider, flow, or group ids — list/resolve.
- Read-only inventory is the default; mutates need an explicit verb.
- Transport: Authentik REST API (prefer a real Authentik MCP later; never
  invent tool names).
- No client secrets, API tokens, signing keys, or user credentials in chat.
- Reverse-proxy / ingress wiring — out of scope here.

## Diagrams

- [`docs/authentik-workflow.drawio`](docs/authentik-workflow.drawio) —
  gate → route apps/providers/flows → evidence; mutate refuse branch
