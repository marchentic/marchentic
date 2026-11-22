---
name: portainer-stack-deploy
description: >-
  Checklist for gated Portainer stack deploy/update: resolve endpoint,
  prove stack name, confirm explicit verb, then deploy via API/UI with a
  short receipt. Skip when no deploy/update ask.
---

# Portainer stack deploy

## Gate

User asked to deploy, update, or re-apply a Portainer stack. Prefer
Portainer API/UI. Skip inventory-only asks (`portainer-endpoint-audit`)
and container-only stop/remove (`portainer-containers`).

Always load `portainer-stacks`, `portainer-endpoints`, and
`portainer-safety`.

## Checklist

1. **Verb** — require explicit deploy / update / apply this turn naming
   the stack. **Done when** the verb and stack name are present, or you
   stopped and asked once.
2. **Endpoint** — resolve via `portainer-endpoints` list.
   **Done when** the endpoint id/name is proven this turn.
3. **Stack** — list stacks on that endpoint; match name or confirm create.
   **Done when** update targets an existing name, or create is explicit.
4. **Payload** — stack file / compose content from the user or repo path
   they named — do not invent services. Cite env **key names** only.
   **Done when** the deploy payload source is known.
5. **Act** — deploy/update via API/UI; never invent MCP tool names.
   **Done when** the mutate ran only after steps 1–4.
6. **Receipt** — endpoint + stack + status; no tokens or secret values.
   **Done when** the reply matches the report shape.

## Report shape

- Endpoint name/id
- Stack name/id
- Action (deploy vs update)
- Resulting status
- "No API tokens or env secrets shown"
