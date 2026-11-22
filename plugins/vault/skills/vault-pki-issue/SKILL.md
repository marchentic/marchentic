---
name: vault-pki-issue
description: >-
  Checklist for issuing a Vault PKI leaf certificate: resolve mount and
  role, confirm constraints, issue, report CN/serial only. Prefer MCP.
  Skip when no certificate issue ask.
---

# Vault PKI issue

## Gate

User asked to issue / mint / generate a TLS certificate from Vault PKI.
Prefer connected Vault MCP. Skip pure KV work or policy-only asks.

Always load `vault-pki` and `vault-refuse-leak`.

## Checklist

1. **Mount** — named by the user or discovered via `list_mounts` /
   default only after confirming a PKI mount exists. **Done when** the
   PKI mount path is known, or ask stopped.
2. **Role** — `list_pki_roles` / `read_pki_role`. Confirm allowed domains,
   TTL caps, and issuer. **Done when** `role_name` matches the ask’s CN
   constraints, or you stopped instead of widening the role.
3. **Common name** — exact CN (and SAN intent) from the user. Do not
   invent hostnames. **Done when** CN is explicit.
4. **TTL** — use the user’s TTL when given; otherwise role/mount default.
   Prefer shorter. **Done when** TTL is chosen without exceeding
   `max_ttl`.
5. **Issue** — `issue_pki_certificate` only after an explicit issue verb.
   **Done when** the tool returned success metadata.
6. **Receipt** — report mount, role, CN, serial, expiry/TTL. **Never**
   paste the private key or full PEM. **Done when** the reply proves
   issue without secret material.
7. **Safety** — no `enable_pki` / issuer create / role delete unless the
   user also asked. **Done when** only the authorized issue (and any
   explicitly requested setup) ran.

## Report shape

- Mount + role name
- CN + serial + expiry (or TTL)
- Where material should be consumed next (operator handoff) — without
  key bytes
- Next step only if asked (install on workload, rotate old cert)
