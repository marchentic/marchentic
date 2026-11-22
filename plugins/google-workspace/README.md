# google-workspace

Google Workspace craft — Gmail, Drive, Calendar, Docs, Sheets. Install when
the project uses Google Workspace MCP (or equivalent).

## Rules (Cursor)

Agent-requested (not always-on):

| Rule | Purpose |
| --- | --- |
| `google-workspace-gmail` | Search / read / draft / send / labels / filters |
| `google-workspace-drive` | Files, folders, copy, permissions, sharing |
| `google-workspace-calendar` | Events, free/busy, OOO, focus time |
| `google-workspace-docs` | Docs and Sheets read/edit |
| `google-workspace-safety` | Send / share / delete / public-link gates |

## Skills

| Skill | Purpose |
| --- | --- |
| `google-workspace` | Index / gate / Procedure |
| `google-workspace-compose-email` | Draft-before-send compose checklist |
| `google-workspace-drive-audit` | Permissions / public-link audit checklist |

## Commands

- `/google-workspace` → Workspace surface craft (MCP first)

## Defaults

- Never invent message, file, event, or spreadsheet ids.
- Pass `user_google_email` as the connected MCP documents (example pattern:
  `admin@nodadyoushutup.com`); do not paste tokens in chat.
- Search/read/draft is the default; send, share, trash, and deletes need an
  explicit verb.
- Prefer named-user Drive grants over anyone-with-link.
- Neighbor non-Workspace mail/drive/calendar products — out of scope.

## Diagrams

- [`docs/google-workspace-workflow.drawio`](docs/google-workspace-workflow.drawio) —
  gate → route (Gmail / Drive / Calendar / Docs-Sheets) → evidence; mutate
  refuse branch
