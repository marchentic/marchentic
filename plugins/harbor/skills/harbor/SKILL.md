---
name: harbor
description: >-
  Agnostic Harbor registry craft: projects/repos/artifacts inventory and
  gated delete/retention/robot changes via API/UI. Never invent project or
  digest names; refuse robot token dumps. Skip when unauthorized.
---

# Harbor

## Gate

No explicit Harbor / project / artifact / robot-account / retention ask →
**skip**. Other OCI registry products are out of scope — this plugin owns
Harbor only.

No Harbor MCP was discovered in the live harness catalog. Prefer Harbor
REST API/UI with a resolved base URL. If an MCP appears later, discover
tools from the live map; do not invent tool names.

Route by intent:

| Surface | Signals |
| --- | --- |
| Projects | list projects, visibility, members summary |
| Artifacts | repos, tags, digests, scan summaries |
| Retention | retention policy, purge old tags |
| Robots | robot account create / list (never paste secrets) |
| Audit | “what’s in Harbor”, project fleet inventory |
| Mutate risk | delete, retention run, robot create, ACL/public |

## Load map

| Need | Rule / skill |
| --- | --- |
| Project list / resolve / visibility | `harbor-projects` |
| Repo / artifact / tag / scan | `harbor-artifacts` |
| Project fleet checklist | `harbor-projects` · skill `harbor-project-audit` |
| Retention purge checklist | `harbor-artifacts` · skill `harbor-retention-run` |
| Delete / retention / robot / ACL / secrets | `harbor-safety` (always) |

## Defaults

1. Never invent project, repository, or artifact digests — list/resolve first.
2. Resolve the Harbor base URL from config/env — never hardcode a host.
3. Resolve **project** before repo/artifact mutates.
4. Prefer tag/artifact delete over repo or project wipe.
5. Never paste robot tokens or admin passwords into chat.
6. Own Harbor only — other OCI registries are out of scope.

## Procedure

1. Decide the surface (projects / artifacts / audit / retention / robots /
   gated delete). **Done when** you can name one surface, or you skipped.
2. Resolve base URL + project (+ repo/tag) from list or user paste.
   **Done when** every name you will use was listed/read, or you stopped
   instead of inventing one.
3. Follow the load-map rule (and compound skill for audit or retention).
   Always apply `harbor-safety`. **Done when** the action matches the ask
   and the reply has **no** robot tokens or admin passwords.
4. Stop after a short receipt unless the user also used an explicit
   destructive or retention verb. **Done when** the reply has project +
   repo/tag and no unauthorized delete/purge ran.
