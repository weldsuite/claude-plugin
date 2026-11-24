# WeldSuite for Claude

Connect Claude to your [WeldSuite](https://www.weldsuite.org) workspace. Ask
Claude to look up and update your CRM contacts, customers, leads and
opportunities, helpdesk conversations, WeldFlow projects and tasks, chat
messages, calendar events, files and knowledge pages, all with the same
permissions your workspace role already has. Developers also get skills and
agents that take a WeldFlow task from the board to a finished, verified change
in their repository, and keep the task up to date while they work.

## What's included

| Part | What it does |
| --- | --- |
| **WeldSuite MCP server** | The `weldsuite` connector at `https://mcp.weldsuite.org/mcp`. You sign in with your WeldSuite account in the browser; there is no API key to create. |
| **`weldsuite` skill** | Teaches Claude how to find records, when to ask before changing something, and how to handle sign-in, permission and rate-limit errors. Claude uses it on its own when you ask about WeldSuite. |
| **Task skills** | `/weldsuite:list-tasks`, `/weldsuite:fix-task`, `/weldsuite:claim-task`, `/weldsuite:done-task`, `/weldsuite:enrich-task` |
| **Agents** | `weldflow-dispatcher` reads a task and your repository and plans the work; `weldflow-task-fixer` implements it and updates the task. |

The task skills and agents are for Claude Code. In the Claude apps you get the
connector and the `weldsuite` skill.

## Install

In Claude Code:

```text
/plugin marketplace add weldsuite/claude-plugin
/plugin install weldsuite@weldsuite
```

Then run `/mcp`, choose **weldsuite** and sign in. Pick the workspace you want
Claude to work in when the sign-in asks for it.

## Things to ask

- "Which leads haven't been contacted in the last 30 days?"
- "Summarise the open helpdesk conversations for Acme Industries."
- "Create a task in the Website Redesign project to review the new pricing page, due Friday."
- "What's on the team calendar next week?"
- `/weldsuite:list-tasks bugs`, then `/weldsuite:fix-task 123`

## Permissions and data

- Claude gets exactly the access your WeldSuite role has. Tools you can't use
  in WeldSuite aren't offered, and every call is checked again when it runs.
- Changes made through Claude show up in the audit trail and trigger the same
  automations and notifications as changes made in the browser.
- The plugin itself stores nothing. Your data stays in WeldSuite and is
  handled under the [WeldSuite privacy policy](https://www.weldsuite.org/privacy).
- Disconnect any time with `/mcp` in Claude Code, or under Customize →
  Connectors in the Claude apps.

More detail, including troubleshooting: [Connect an AI assistant
(MCP)](https://help.weldsuite.org/settings/mcp-server).

## Support

[www.weldsuite.org/support](https://www.weldsuite.org/support) or
support@weldsuite.org.

## License

MIT
