# vault

HashiCorp Vault craft for Claude Code, Cursor, GitHub Copilot, and OpenAI
Codex — KV read/write/delete, PKI issue, auth/policy hygiene, external-sync
key honesty, and hard refuse to leak credentials. Install when Vault MCP
(or equivalent) is available.

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `vault-secrets` | KV read/write/delete + mount hygiene (MCP tool map) |
| `vault-pki` | PKI mounts / issuers / roles / issue |
| `vault-external-secrets` | Vault KV payloads for external secret sync |
| `vault-auth` | Auth method binding + token hygiene |
| `vault-policy` | ACL least-privilege craft |
| `vault-refuse-leak` | No secrets in chat/commits/logs |

## Skills

| Skill | Purpose |
| --- | --- |
| `vault` | Index / gate / Procedure |
| `vault-pki-issue` | Leaf certificate issue checklist |
| `vault-secret-rotation` | KV rotate-without-echo checklist |

## Commands

- `/vault` → KV, rotate, auth/policy, or general Vault craft
- `/vault-pki` → PKI issue / role / mount craft

## Defaults

- Never invent mount, path, key, role, issuer, or policy names — list/resolve.
- Prefer landing values in Vault over printing them in chat.
- Delete / mount-delete / role-delete / issue need an explicit verb.
- Receipts use names (and CN/serial for certs) — never secret values or
  private keys.
- External-sync consumers: keep path/property names aligned; manifests are
  out of scope.

## Diagrams

- [`docs/vault-workflow.drawio`](docs/vault-workflow.drawio) —
  gate → KV/sync vs PKI vs rotate/auth-policy → receipt; refuse leak branch
