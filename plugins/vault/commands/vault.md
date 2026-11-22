---
name: vault
description: >-
  Read, write, rotate, or delete Vault KV secrets and PKI with leak-safe
  craft (MCP first).
---

# /vault

1. If the user did not authorize Vault/secret/PKI work, say so and stop.
2. Load `vault` and follow the load map (`vault-secrets`, `vault-pki`,
   `vault-external-secrets`, `vault-auth`, `vault-policy`, always
   `vault-refuse-leak`).
3. Prefer Vault MCP. Never invent mounts/paths/roles. Never paste secret
   values or private keys into chat.
4. For certificate issue, follow skill `vault-pki-issue`. For credential
   rotation, follow skill `vault-secret-rotation`.
5. Confirm outcomes with a non-secret receipt (mount + path + key/role/CN
   /serial as relevant).
