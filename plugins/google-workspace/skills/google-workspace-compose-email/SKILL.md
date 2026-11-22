---
name: google-workspace-compose-email
description: >-
  Checklist for Gmail compose: search/read context, draft-before-send, thread
  correctly, redact secrets. Prefer MCP. Skip when no mail compose/reply/send
  was asked.
---

# Google Workspace compose email

## Gate

User asked to draft, reply, forward carefully, or send mail. Prefer connected
Google Workspace MCP. Skip Drive/Calendar/Docs-only asks.

## Checklist

1. **Context** — if replying or “about that email,” `search_gmail_messages`
   then `get_gmail_thread_content` / `get_gmail_message_content`.
   **Done when** `thread_id` / `message_id` (and Message-ID for
   `in_reply_to`) are from MCP when needed.
2. **Recipients** — use only addresses the user named (or that appear on the
   thread they asked to reply to). No invented CC/BCC.
   **Done when** `to` / `cc` / `bcc` are explicit.
3. **Draft** — `draft_gmail_message` with `subject`, `body`, optional
   `thread_id`, `quote_original`, attachments via MCP URLs.
   **Done when** a draft exists, unless the user already said send.
4. **Send gate** — call `send_gmail_message` only with an explicit send verb
   this turn (`google-workspace-safety`). Prefer sending the composed content
   the user approved.
   **Done when** send succeeded or you stopped at draft.
5. **Report** — subject, to, draft vs sent, message/thread id.
   **Done when** reply cites MCP evidence and redacts secrets.

## Report shape

- Action: draft | sent
- Subject + recipients (no secret bodies)
- Message / thread id
- One next step (e.g. user review draft) when still a draft
