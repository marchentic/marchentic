---
name: google-workspace
description: >-
  Google Workspace craft: Gmail search/draft/send, Drive file ops and sharing,
  Calendar events, Docs and Sheets reads/edits. Prefer Google Workspace MCP.
  Skip when the user did not authorize Workspace work. Destructive or outbound
  actions need an explicit verb.
---

# Google Workspace

## Gate

No explicit Gmail / Drive / Calendar / Docs / Sheets / Google Workspace ask
and no named message, file, event, or doc → **skip**. Prefer a connected
Google Workspace MCP when any surface is in play. Bare product name alone is
not enough for send / share / delete.

Route by product:

| Surface | Signals |
| --- | --- |
| Gmail | email, inbox, thread, draft, send, label, filter |
| Drive | Drive, file, folder, share link, upload, permissions |
| Calendar | calendar, event, meeting, OOO, focus time, free/busy |
| Docs / Sheets | Doc, Spreadsheet, tab, cell range, table |
| Mutate / outbound | send, share publicly, trash, delete event, clear sheet |

## Load map

| Need | Rule / skill |
| --- | --- |
| Mail search / read / draft / send / labels | `google-workspace-gmail` · skill `google-workspace-compose-email` |
| Drive search / read / create / share | `google-workspace-drive` · skill `google-workspace-drive-audit` |
| Calendar list / create / update / freebusy | `google-workspace-calendar` |
| Docs or Sheets content | `google-workspace-docs` |
| Send / share / delete / public link / trash | `google-workspace-safety` |

## Defaults

1. Never invent user email, file id, event id, message id, or spreadsheet id.
2. Pass `user_google_email` as the connected MCP documents (example pattern:
   `admin@nodadyoushutup.com`). Do not ask the operator to paste tokens.
3. Search/read/draft is the default; send, share, trash, and deletes need an
   explicit verb this turn (`google-workspace-safety`).
4. Draft-before-send for new mail unless the user said “send”.
5. Prefer named-user Drive grants over anyone-with-link.
6. No secrets, tokens, or full mailbox dumps in chat.
7. Owns Workspace surfaces only — neighbor mail/drive/calendar products are
   out of scope.

## Procedure

1. Decide the surface (Gmail vs Drive vs Calendar vs Docs/Sheets vs mutate).
   **Done when** you can name one surface, or you skipped because none was
   asked.
2. Resolve ids from MCP (message/thread, file/folder, calendar/event,
   document/spreadsheet). **Done when** every id you will use was listed/read,
   or you stopped instead of inventing one.
3. Follow the load-map rule (and compound skill when composing mail or
   auditing Drive sharing). **Done when** evidence matches the ask or the
   outbound/destructive action was refused for lack of verb.
4. Stop after evidence unless the user also used a send / share / delete /
   implement verb. **Done when** the reply has ids/links + finding or what
   changed, and no unauthorized mutate ran.
