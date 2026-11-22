---
name: freshservice
description: >-
  Agnostic Freshservice ITSM craft: create-only ticket filing with clear
  description shape, update notes, status honesty, and no invented workspace
  ids. Prefer Freshservice MCP when ready; otherwise the operator’s configured
  API path — never invent tools. Skip when the user did not authorize ITSM work.
---

# Freshservice

## Gate

No explicit Freshservice / ticket / incident / service-request / problem /
change ask and no named ticket id → **skip**. Prefer a connected Freshservice
MCP when ready; if none is connected, use the operator’s configured API or UI
path once — **do not invent credentials or tool names**. Bare product name
alone is not enough.

Route by intent:

| Surface | Signals |
| --- | --- |
| Create | “file”, “open a ticket”, incident / service request / problem / change |
| Update | named ticket id + revise / note / comment / fix description |
| Status | resolve, close, pending, assign, priority |
| Author body | description shape, Overview / Impact / outcome |

## Load map

| Need | Rule / skill |
| --- | --- |
| May I create? | `freshservice-create` |
| Ticket body shape | `freshservice-ticket` · skill `freshservice-ticket-author` |
| Edit existing ticket | `freshservice-update` |
| Status / priority / assign | `freshservice-status` |

## Defaults

1. Create-only unless the user adds an explicit implement verb.
2. Never invent workspace, group, requester, category, or ticket ids.
3. Keep status honest — do not mark resolved without evidence.
4. Incidents and service requests always get Overview / Impact / Details /
   Requested outcome (and Next steps when useful) per `freshservice-ticket`.
5. Leave new tickets in the default created / Open state unless asked to
   assign or resolve.
6. Prefer additive notes on update; full description rewrites only when asked.
7. No Freshservice MCP was discovered in this environment catalog — craft
   from these rules; when an MCP appears later, prefer it without inventing
   tool names ahead of time.
8. Own the ITSM ticket surface only — other trackers and product code are out
   of scope on a create-only ask.

## Procedure

1. Decide the surface (create vs update vs status vs body-only).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve ids from connected tools or named context (workspace, ticket id,
   group). **Done when** every id you will send was returned/named, or you
   stopped instead of inventing one.
3. Follow the load-map rule (and `freshservice-ticket-author` when shaping or
   filing a body). **Done when** the body matches `freshservice-ticket` or the
   status/update honesty rules hold.
4. Stop after create/update/status unless the user also used an implement
   verb. **Done when** the reply contains the ticket id or URL (or a clear
   failure), and no product code was edited on a create-only ask.
