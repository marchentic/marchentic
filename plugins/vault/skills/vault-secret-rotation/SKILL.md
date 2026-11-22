---
name: vault-secret-rotation
description: >-
  Checklist for rotating a Vault KV secret: resolve path, write new value
  without echoing it, confirm key names, note consumers. Prefer MCP. Skip
  when no rotate/replace ask.
---

# Vault secret rotation

## Gate

User asked to rotate, replace, or refresh a credential stored in Vault
KV (including after a leak). Prefer connected Vault MCP. Skip PKI leaf
issue (use `vault-pki-issue`) and pure read-only inventory.

Always load `vault-secrets` and `vault-refuse-leak`. When a sync consumer
depends on the path, also load `vault-external-secrets`.

## Checklist

1. **Path** — exact mount + path (+ key) from the user or
   `list_secrets` / `read_secret` (names only). **Done when** targets are
   known, or ask stopped.
2. **Old material** — if it leaked in chat/logs, name the **type** and
   channel only — do not repeat the value. **Done when** exposure is
   acknowledged without reprinting secrets.
3. **New value** — prefer generating or accepting a value that goes
   straight into `write_secret`. Do not ask the user to paste the new
   secret back into chat when avoidable. **Done when** `write_secret`
   succeeded.
4. **Receipt** — mount + path + key names (+ version when returned). No
   values. **Done when** the reply proves write without secret bytes.
5. **Consumers** — remind that workloads / sync agents must pick up the
   new version (restart, refresh, or sync reconcile). Do not invent
   consumer names. **Done when** the operator knows to verify consumers
   they own.
6. **Invalidate** — when the user asked, delete the old key version or
   revoke the related token/auth material per their verb. **Done when**
   no unauthorized delete ran.
7. **External sync** — if remoteRef keys must stay stable, rotate **values
   only** under the same property names unless the user asked to rename.
   **Done when** path/property names still match the consumer contract.

## Report shape

- Mount + path + key names rotated
- Version metadata when available
- Consumer refresh reminder (generic)
- Explicit "value not shown" — never include the secret
