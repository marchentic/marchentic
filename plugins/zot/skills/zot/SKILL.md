---
name: zot
description: >-
  Agnostic Zot OCI registry craft: repository/tag inventory and gated
  delete/GC via API/UI. Never invent repo or tag names; refuse credential
  dumps. Skip when the user did not authorize this surface.
---

# Zot

## Gate

No explicit Zot ask → **skip**. Other OCI registry products are out of
scope — this plugin owns Zot only.

No Zot MCP was discovered in the live harness catalog. Prefer Zot API/UI
with a resolved base URL. If an MCP appears later, discover tools from the
live map; do not invent tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Repositories | list repos, registry shape |
| Tags | tags, digests, manifests, referrers |
| Audit | “what’s in Zot”, repo fleet inventory |
| GC | garbage collect, prune blobs |
| Mutate risk | delete tag/repo, GC, auth/anonymous policy |

## Load map

| Need | Rule / skill |
| --- | --- |
| Repository list / resolve | `zot-repos` |
| Tag / manifest / referrer inventory | `zot-tags` |
| Repo fleet checklist | `zot-repos` · skill `zot-repo-audit` |
| GC checklist | `zot-safety` · skill `zot-gc-run` |
| Delete / GC / auth / secrets | `zot-safety` (always) |

## Defaults

1. Never invent repository or tag names — list/resolve first.
2. Resolve the registry base URL from config/env — never hardcode a host.
3. Resolve **repository** before tag mutate or GC.
4. Prefer tag delete over full repo wipe; prefer scoped GC after deletes.
5. Never paste htpasswd / token secrets into chat.
6. Own Zot only — other OCI registries are out of scope.

## Procedure

1. Decide the surface (repos / tags / audit / GC / gated delete).
   **Done when** you can name one surface, or you skipped.
2. Resolve base URL + repository (+ tag) from list or user paste.
   **Done when** every name you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and compound skill for audit or GC). Always
   apply `zot-safety`. **Done when** the action matches the ask and the
   reply has **no** registry credentials.
4. Stop after a short receipt unless the user also used an explicit
   destructive or GC verb. **Done when** the reply has repo + tag and no
   unauthorized delete/GC ran.
