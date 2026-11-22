---
name: freshservice
description: >-
  File or manage Freshservice tickets with create-only gates, body shape,
  updates, and honest status.
---

# /freshservice

1. If the user did not authorize Freshservice/ticket work and named no ticket,
   say so and stop.
2. Otherwise load `freshservice` and follow the gate, load map, and procedure.
3. For body authoring / filing shape, load `freshservice-ticket-author`.
4. Prefer Freshservice MCP when ready; otherwise the operator’s configured
   API/UI path — never invent workspace, ticket ids, or tool names.
5. Return ticket id / URL with evidence (no secrets).
