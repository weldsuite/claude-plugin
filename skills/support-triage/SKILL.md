---
name: support-triage
description: Triage the WeldDesk helpdesk queue, going through open conversations, oldest waiting first, to summarise each, suggest priority, tags and an owner, flag urgent and at-risk customers, and apply the changes the user approves. Use when the user asks to triage the inbox or queue, what's waiting in support, or which tickets need attention.
argument-hint: "[unassigned | mine | all] [how many, default 20]"
---

# Support triage

Triage the helpdesk queue for `$ARGUMENTS` (`unassigned` by default; `mine`
or `all`; and how many, default 20).

## Read the queue

1. `search_conversations` with `state: open`, `sort: waiting_longest`, and
   `unassigned: true` or the user's `assigneeId` (see the `weldsuite` skill
   for finding it).
2. For each conversation, `get_conversation` with `include: messages` and
   read the latest customer message.

## Triage table

| # | Customer | Subject | Waiting | Summary | Suggested priority | Tags | Owner |

- **Priority:** `urgent` for outages, data loss, security or payment
  problems; `high` for a blocked customer or one waiting much longer than
  usual; otherwise `medium` or `low`.
- **Owner:** suggest from the department and who handled the customer's
  last conversations. Look teammates up with `get_settings_members`.
- Call out separately: anything urgent, several conversations about the same
  problem (a possible incident), and customers with an open deal in WeldCRM
  (`search_customers`, then `search_opportunities`).

## Apply

Show the changes as a list. On the user's yes, apply only those with
`update_conversation` (`priority`, `tags`, `assigneeId`, `departmentId`).
Offer `/weldsuite:answer-conversation` for the ones that need a reply.

Don't reply to customers or close conversations in this skill.
