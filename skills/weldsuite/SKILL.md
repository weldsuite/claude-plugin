---
name: weldsuite
description: How to work in a WeldSuite workspace through the WeldSuite MCP server. Use whenever the user asks to look up, summarise, create or change anything in WeldSuite, such as CRM contacts, customers, leads, opportunities and quotes, WeldDesk helpdesk conversations, WeldFlow projects, tasks and sprints, WeldChat messages, calendar events, WeldDrive files, WeldKnow pages, social posts or domains, or mentions a WeldSuite record by name or number.
---

# Working in WeldSuite

The `weldsuite` MCP server gives you the user's WeldSuite workspace. Every tool
runs as the signed-in user, with exactly the permissions of their workspace
role, and every change lands in the audit trail and fires the same automations
as a change made in the browser.

## Before the first call

- **No WeldSuite tools?** The connector is not signed in. In Claude Code, ask
  the user to run `/mcp`, pick **weldsuite** and finish the sign-in in the
  browser. In the Claude apps, it is under **Customize → Connectors**.
- **Only a `list_workspaces` tool?** The account belongs to several
  workspaces and the connection doesn't say which one to use. Call it, show
  the user the list, and follow the instructions it returns. Nothing else
  works until then.
- **A tool you expected is missing?** Tools follow the user's role. Say which
  permission is missing; don't try to reach the same data another way.

## Finding records

| Area | Start with |
| --- | --- |
| WeldCRM | `search_contacts`, `search_customers`, `search_leads`, `search_opportunities` |
| WeldDesk | `search_conversations`, then `get_conversation` |
| WeldFlow | `search_projects`, `search_tasks`, then `get_task` |
| WeldChat | `search_chat_messages` |
| Calendar | `search_calendar_events` |
| WeldDrive | `search_files`, `search_folders` |
| WeldKnow | `search_knowledge_pages` |
| Social | `search_social_posts` |
| Workspace | `get_settings_members`, `search_time_entries` |

- Search first, then `get_*` the record you need. Tools accept a record's
  number (`123`), its name, or the id returned by an earlier search; prefer
  the id once you have it.
- Lists are cursor-paginated. Pass the returned `cursor` to read on, and
  summarise long lists instead of pasting them.
- WeldSuite is the system of record. Never invent ids, names, statuses,
  assignees or amounts: look them up, and say so when you can't find one.

## Changing things

- Do what the user asked and nothing more. Before creating, changing or
  deleting anything they did not explicitly ask for, say what you are about
  to do and wait for a yes.
- Anything that leaves the workspace (sending email, posting to social
  media, starting an outreach campaign, replying to a customer) needs the
  user's go-ahead on the exact content first.
- Deleting needs an explicit request. If a delete is refused, the role lacks
  the delete permission; report it rather than looking for a workaround.
- After a change, say what changed and on which record.

## When something goes wrong

- **Rate limit exceeded:** wait the number of seconds the error gives, then
  carry on.
- **Not a member / no permissions:** the user's access changed. Ask them to
  check with a workspace admin, or reconnect to the right workspace.
- If a tool is broken or can't do what the user needs, `submit_feedback`
  sends a short report to the WeldSuite team. Leave out passwords, keys and
  personal details.
