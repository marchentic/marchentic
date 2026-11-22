---
name: tailscale-acl-change
description: >-
  Checklist for gated Tailscale ACL/grants changes via Admin API: GET,
  minimal diff, tests, PUT — never paste auth keys. Skip when no ACL
  mutate ask.
---

# Tailscale ACL change

## Gate

User asked to change, tighten, open, or replace Tailscale ACL policy /
grants / tagOwners / SSH ACL. Prefer Admin API (no Tailscale MCP
discovered). Skip pure device status (use `tailscale-devices`) and
read-only ACL review without a mutate verb.

Always load `tailscale-acls` and `tailscale-safety`.

## Checklist

1. **Authorize** — confirm an explicit mutate verb this turn naming the
   grant/tag/change (or “replace ACL”). **Done when** verb is present,
   or you refuse and stop.
2. **Tailnet** — resolve `{tailnet}` from operator config/env. **Done
   when** known without inventing it.
3. **GET current** — `GET /api/v2/tailnet/{tailnet}/acl`. **Done when**
   you have the live policy body this turn.
4. **Tags / devices** — if the change names hosts, resolve tags/hostnames
   via `tailscale-devices` so sources/destinations are real. **Done when**
   no invented tags remain.
5. **Minimal diff** — edit the smallest stanza set; prefer grants over
   whole-file rewrite; add/keep tests for the intended allow/deny.
   **Done when** blast radius is one sentence.
6. **Preview / PUT** — preview when available; then POST ACL under
   authorization only. **Done when** the write ran or you stopped.
7. **Receipt** — summarize changed src → dst:ports / tags / SSH rules —
   no tokens. Re-GET to confirm. **Done when** the reply has that shape.

## Report shape

- Tailnet id (non-secret)
- What changed (grants/tags/ssh) in one short block
- Tests added/updated (or explicitly none)
- One follow-up check (device connectivity / `tailscale status`)
