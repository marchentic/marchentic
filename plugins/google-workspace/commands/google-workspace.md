---
name: google-workspace
description: >-
  Operate on Gmail, Drive, Calendar, Docs, or Sheets with Google Workspace
  craft (MCP first).
---

# /google-workspace

1. If the user did not authorize Google Workspace work and named no mail,
   file, event, or doc, say so and stop.
2. Otherwise load `google-workspace` and follow the matching rule
   (`google-workspace-gmail`, `google-workspace-drive`,
   `google-workspace-calendar`, `google-workspace-docs`,
   `google-workspace-safety` for send/share/delete/public link).
3. Prefer Google Workspace MCP. Pass `user_google_email` as the MCP documents
   (example pattern: `admin@nodadyoushutup.com`). Never invent ids or
   accounts.
4. For compose/reply use skill `google-workspace-compose-email`; for sharing
   audits use `google-workspace-drive-audit`.
5. Return message/thread ids, file links, event times, or doc URLs with
   evidence — never invent localhost hosts; never dump secrets.
