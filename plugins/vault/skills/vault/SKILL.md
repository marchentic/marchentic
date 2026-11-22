---
name: vault
description: >-
  HashiCorp Vault craft: gated KV read/write/delete, PKI issue, auth/policy
  hygiene, external-sync key honesty, and hard refuse to paste credentials.
  Prefer Vault MCP. Skip when the user did not authorize Vault work.
---

# Vault

## Gate

No explicit Vault / secret path / mount / PKI / auth / policy ask and no
named mount or path → **skip**. Prefer a connected Vault MCP when Vault
work is in play. Bare product name alone is not enough.

Route by intent:

| Surface | Signals |
| --- | --- |
| KV secrets | list / read / write / delete / rotate secret or KV mount |
| PKI | enable PKI, issuer, role, issue cert, TLS leaf |
| External sync | remoteRef keys, sync missing properties, consumer path match |
| Auth | AppRole, Kubernetes auth, JWT/OIDC, token mint/revoke |
| Policy | ACL HCL, capabilities, least privilege |
| Leak | pasted credential, commit secret, rotate after exposure |

## Load map

| Need | Rule / skill |
| --- | --- |
| Read / write / delete KV | `vault-secrets` |
| Rotate a KV secret end-to-end | `vault-secrets` · skill `vault-secret-rotation` |
| Mounts / PKI roles / certs | `vault-pki` |
| Issue a leaf certificate | `vault-pki` · skill `vault-pki-issue` |
| KV keys for external secret sync | `vault-external-secrets` |
| Auth method / binding / token hygiene | `vault-auth` |
| ACL policy author/review | `vault-policy` |
| Leak / commit / chat hygiene | `vault-refuse-leak` (always with the above) |

## Defaults

1. Never invent mount paths, secret keys, role names, issuer names, or
   policy names.
2. Prefer landing values in Vault over printing them in chat.
3. Delete, mount-delete, role-delete, and broad list need an explicit verb.
4. App wiring and cluster manifest craft are out of scope — this plugin
   owns the Vault surface only.
5. When an external-secret consumer reads Vault, keep path/property names
   aligned with that consumer — do not invent a parallel key set.
6. On every Vault turn, refuse leaks: report paths and names, never secret
   values or private keys.
7. Prefer MCP tools discovered on the live Vault MCP; do not invent tool
   names.

## Procedure

1. Decide the surface (KV / PKI / sync / auth / policy / leak-rotate).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve ids from MCP (`list_mounts`, `list_secrets`, `list_pki_roles`,
   …) or from paths the user named. **Done when** every mount/path/role
   you will use was listed/read, or you stopped instead of inventing one.
3. Follow the load-map rule (and compound skill for issue or rotation).
   Always apply `vault-refuse-leak`. **Done when** the action matches the
   ask and the reply has **no** secret values.
4. Stop after a non-secret receipt unless the user also used an explicit
   destructive or issue verb. **Done when** the reply has mount + path
   (and key/role/CN/serial as relevant) and no unauthorized
   write/delete/issue ran.
