---
name: google-workspace-drive-audit
description: >-
  Checklist for Drive sharing audit: resolve file, list permissions, check
  public/link access, report blast radius. Prefer MCP. Skip when no sharing
  or exposure ask was made.
---

# Google Workspace Drive audit

## Gate

User asked who can access a file/folder, whether a link is public, to tighten
sharing, or to review Drive exposure. Prefer connected Google Workspace MCP.
Skip pure content-edit asks (use Docs/Sheets or create/copy flows).

## Checklist

1. **Resolve** — `search_drive_files` / `list_drive_items` (scope `drive_id`
   for Shared Drives). **Done when** `file_id` is from MCP.
2. **Permissions** — `get_drive_file_permissions` and/or
   `manage_drive_access` with `action=list`.
   **Done when** roles and principals are listed.
3. **Public / link** — `check_drive_file_public_access` by name when useful;
   `get_drive_shareable_link` for the current link; note
   `set_drive_file_permissions` link_sharing state from permission list.
   **Done when** you can say private vs anyone-with-link vs domain.
4. **Mutate only if asked** — revoke/update/grant or turn link_sharing `off`
   only with an explicit verb (`google-workspace-safety`). Prefer narrowing
   over broadening.
   **Done when** no unauthorized share change ran.
5. **Report** — file name/id, principals + roles, link/public status,
   recommended tighten if overshared.
   **Done when** findings cite MCP, not guesses.

## Report shape

- File name + id
- Principals and roles (summarized)
- Link / public status
- Optional: one recommended permission change (do not apply unless asked)
