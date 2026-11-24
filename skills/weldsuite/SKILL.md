---
name: weldsuite
description: How to work in a WeldSuite workspace through the WeldSuite MCP server. Use whenever the user asks to look up, summarise, create or change anything in WeldSuite, such as CRM contacts, customers, leads, opportunities, activities and quotes, WeldDesk helpdesk conversations, WeldFlow projects, tasks, sprints and milestones, WeldMail, WeldChat, calendar events, WeldDrive files, WeldKnow pages or time entries, or mentions a WeldSuite record by name or number.
---

# Working in WeldSuite

The `weldsuite` MCP server gives you the user's WeldSuite workspace on the EU
edition (`mcp.weldsuite.eu`). Every tool runs as the signed-in user, with
exactly the permissions of their workspace role, and every change lands in the
audit trail and fires the same automations as a change made in the browser.

## Before the first call

- **No WeldSuite tools?** The connector isn't signed in. In Claude Code, ask
  the user to run `/mcp`, pick **weldsuite** and finish the sign-in in the
  browser. In the Claude apps it is under **Customize → Connectors**.
- **Only a `list_workspaces` tool?** The account belongs to several
  workspaces and the sign-in didn't say which one to use. Call it and show
  the user the list. Each workspace has its own address
  (`https://mcp.weldsuite.eu/mcp/w/<workspace>`): the user can add the one
  they want as a separate connector (Claude Code:
  `claude mcp add --transport http weldsuite-<workspace> <address>`; Claude
  apps: **Customize → Connectors → Add custom connector**) and work through
  that one. Nothing else works on this connection until then.
- **A tool you expected is missing?** Tools follow the user's role. Say
  which permission is missing; don't reach for the same data another way.

## Who is "me"?

No tool returns the signed-in user. When a request is about the user's own
work ("my tasks", "my conversations", "my deals"), ask for their name or email
once, find them with `get_settings_members`, and use that member's id as
`assigneeId`, `ownerId` or `userId` for the rest of the conversation.

## Finding records

| Area | Start with |
| --- | --- |
| WeldCRM | `search_customers`, `search_contacts`, `search_leads`, `search_opportunities`, `search_activities`, `search_quotes` |
| WeldDesk | `search_conversations`, then `get_conversation` with `include: messages` |
| WeldFlow | `search_projects`, `search_tasks`, `search_milestones`, `search_sprints` |
| WeldMail | `list_mail_threads`, `search_emails` |
| WeldChat | `search_channels`, `search_chat_messages` |
| Calendar | `search_calendars`, `search_calendar_events` |
| WeldDrive | `search_files`, `search_folders` |
| WeldKnow | `list_knowledge_spaces`, `search_knowledge_pages` |
| Time | `search_time_entries` |
| Workspace | `get_settings_members` |

- Search first, then `get_*` the record you need. Tools accept a record's
  number (`123`), its name, or the id from an earlier search; prefer the id
  once you have it.
- Refer to records by name, not by id: "the Acme Industries lead", not
  "lead 01HX3…". Show an id only when the user asks for it.
- Lists are cursor-paginated. Pass the returned `cursor` to read on, say when
  there are more results, and summarise long lists instead of pasting them.
- Statuses, stages and types come from the workspace's own configuration.
  Quote them as they are.
- WeldSuite is the system of record. Never invent names, statuses,
  assignees, amounts or dates. Look them up, and say so when you can't find
  one.

## Changing things

- Do what the user asked and nothing more. Before creating, changing or
  deleting anything they didn't explicitly ask for, show what you are about
  to do and wait for a yes. When you propose several changes at once, show
  them as a list the user can approve or trim.
- Anything a customer or outsider will see needs the user's go-ahead on the
  exact text first: a helpdesk reply (`add_conversation_message` with
  `kind: message`), a chat message, a calendar invite to outside attendees.
  Internal notes (`kind: note`) and mail drafts (`create_mail_draft`, which
  never sends) are the safe defaults.
- Deleting needs an explicit request. A refused call means the role lacks
  that permission; report it rather than retrying another way.
- After a change, say what changed in plain terms: "moved the Acme
  opportunity to Negotiation", not the returned payload.

## When something goes wrong

- **Rate limit exceeded:** wait the number of seconds the error gives, then
  carry on.
- **Not a member, or no permissions:** the user's access changed. Ask them
  to check with a workspace admin, or reconnect to the right workspace.
- **A tool fails or does the wrong thing:** say what you tried and what came
  back, and suggest the user contacts WeldSuite support
  (www.weldsuite.eu/support).
