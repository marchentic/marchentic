---
name: vault-pki
description: >-
  Issue or manage Vault PKI certificates and roles with leak-safe craft
  (MCP first).
---

# /vault-pki

1. If the user did not authorize Vault PKI work, say so and stop.
2. Load `vault` → `vault-pki` + `vault-refuse-leak`. For leaf issue, follow
   skill `vault-pki-issue`.
3. Prefer Vault MCP PKI tools. Never invent mounts, issuers, or roles.
4. Report CN / serial / expiry only — never paste private keys or full
   PEM key material.
5. Enable mounts, create issuers/roles, or delete roles only on an
   explicit verb this turn.
