---
name: answer-conversation
description: Draft a reply to a WeldDesk helpdesk conversation using the customer's history and the WeldKnow knowledge base, then post it as an internal note or, on the user's explicit approval of the exact text, send it to the customer. Use when the user asks to answer, reply to or draft a response for a support conversation or ticket.
argument-hint: <conversation number, subject or customer>
---

# Answer a helpdesk conversation

Answer conversation `$ARGUMENTS`.

## Understand it

1. Find it: `search_conversations` with `q` (a number like `#42`, the
   subject or the customer), then `get_conversation` with
   `include: messages`. Read the whole thread, including internal notes.
2. Check the customer: `search_customers` or `search_contacts` by name or
   email, and their recent conversations, so you know about earlier problems
   and promises.
3. Look for answers in the knowledge base: `search_knowledge_pages` with the
   key terms, and `get_knowledge_page` for the best matches.

## Draft

- Answer what the customer actually asked, in the language they wrote in,
  in the workspace's tone from earlier replies.
- Use only facts from the thread, the customer record and the knowledge
  base. When you don't know something (a fix date, a refund decision), say
  so to the user instead of promising it to the customer.
- Link knowledge pages where they help.
- Keep it short: what happened, what to do, what happens next.

Show the draft with the sources you used.

## Post

- **Default:** post it as an internal note (`add_conversation_message` with
  `kind: note`) so a teammate can review or send it.
- **Send to the customer** (`kind: message`) only when the user approves the
  exact text. Replies go out on API and chat conversations; for email and
  phone conversations, say the reply must be sent from the WeldDesk inbox.
- Offer to update `priority`, `tags` or `state` with `update_conversation`
  when the reply settles it.
- If no knowledge page covered the answer, offer `/weldsuite:kb-article` to
  write one.
