---
name: freshservice-ticket-author
description: >-
  Author or rewrite a Freshservice ticket body against freshservice-ticket
  (Overview, Impact, Details, Requested outcome, Next steps). Use when filing
  or fixing description shape. Skip status-only asks.
---

# Freshservice ticket author

## Gate

User asked to file a ticket, shape a description, or fix an existing ticket’s
body. Skip pure status/assign moves (use `freshservice-status`) and skip
when create is not authorized (`freshservice-create`).

## Checklist

1. **Authorization** — create needs an explicit file verb; update needs a
   named ticket id. **Done when** the gate passes or you stopped.
2. **Type** — Incident / Service request / Problem / Change per user words
   (`freshservice-create` Types). **Done when** the type is stated.
3. **Ids** — workspace / group / requester / category from config or named
   context only — never invent. **Done when** every field you will set was
   resolved or omitted.
4. **Body** — load `freshservice-ticket`; fill Overview, Impact, Details,
   Requested outcome; add Next steps only when useful. **Done when** sections
   are present and secrets are redacted.
5. **Create vs update** — new ticket → `freshservice-create` procedure; edit
   → prefer note then description via `freshservice-update`. **Done when**
   the chosen path ran once.
6. **Stop** — create-only / update-only unless an explicit implement verb was
   added. **Done when** no unauthorized product code edits ran.

## Report shape

- Ticket id / URL (or create failure)
- Type + fields set (no secret values)
- Whether implement was requested (yes/no)
