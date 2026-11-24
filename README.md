# WeldSuite for Claude

Connect Claude to your [WeldSuite](https://www.weldsuite.eu) workspace on the
EU edition. Claude can look up and update your CRM, helpdesk, projects, tasks,
mail drafts, calendar, files, time and knowledge base, with exactly the
permissions your workspace role already has. The plugin adds ready-made skills
for the work people actually do every day: preparing for a customer meeting,
reviewing the pipeline, triaging and answering support, reporting on a project,
turning notes into tasks, logging calls and time, and, for developers, taking a
WeldFlow task from the board to a finished change.

## Skills

Claude picks these up on its own when your request fits, or you can run them
as slash commands.

**Sales**

| Skill | What it does |
| --- | --- |
| `/weldsuite:account-brief Acme` | One-page brief before a meeting: people, open deals, recent activity, open support issues, promises outstanding, talking points. |
| `/weldsuite:pipeline-review` | Pipeline by stage with a weighted forecast, deals that need attention and why, and suggested next steps you can apply. |
| `/weldsuite:lead-followup` | Leads that have gone quiet, ranked, with personal follow-up emails saved as WeldMail drafts. Nothing is sent. |
| `/weldsuite:log-activity` | Paste call or meeting notes; Claude logs the activity on the right customer, contact and deal, with follow-ups. |

**Support**

| Skill | What it does |
| --- | --- |
| `/weldsuite:support-triage` | Goes through the open queue, oldest waiting first: summary, priority, tags and owner for each, and possible incidents. |
| `/weldsuite:answer-conversation #42` | Drafts a reply from the thread, the customer's history and your knowledge base. Posts it as an internal note unless you approve sending. |
| `/weldsuite:kb-article` | Turns a solved conversation or your notes into a WeldKnow page, after checking for one that already exists. |

**Projects and your day**

| Skill | What it does |
| --- | --- |
| `/weldsuite:daily-brief` | Your meetings, overdue and due tasks, conversations waiting on you, deal next steps, and a suggested order. |
| `/weldsuite:project-status Website` | Status report: done, in flight, overdue, blocked, milestones, sprint, risks. Can post it to the project. |
| `/weldsuite:notes-to-tasks` | Paste meeting notes; get WeldFlow tasks with owners and due dates, checked for duplicates, created on your approval. |
| `/weldsuite:log-time` | Describe your day; get a timesheet on the right projects and tasks, checked for gaps and overlaps. |

**Developers (Claude Code)**

| Skill | What it does |
| --- | --- |
| `/weldsuite:list-tasks` | Prioritised backlog of open WeldFlow tasks. |
| `/weldsuite:fix-task 123` | Loads the task, plans, implements and verifies the change in your repository, then updates the task. |
| `/weldsuite:claim-task 123` | Assigns the task to you and sets it in progress. |
| `/weldsuite:done-task 123 <PR>` | Checks the work, comments with the pull request and moves the task to review or done. |
| `/weldsuite:enrich-task 123` | Interviews you to fill in a vague task, then appends the result to its description. |

There is also a `weldsuite` skill Claude uses in the background: how to find
records, when to ask before changing something, and what to do about sign-in,
permission and rate-limit errors. The developer skills come with two agents,
`weldflow-dispatcher` and `weldflow-task-fixer`.

## Install

In Claude Code:

```text
/plugin marketplace add weldsuite/claude-plugin
/plugin install weldsuite@weldsuite
```

Then run `/mcp`, choose **weldsuite** and sign in with your WeldSuite account
in the browser. There is no API key to create.

The connector is `https://mcp.weldsuite.eu/mcp`. If your account belongs to
more than one workspace, Claude shows you a list with each workspace's own
address; add the one you want as a connector of its own.

In the Claude apps, the connector and every skill except the developer ones
work; agents are a Claude Code feature.

## Things to ask

- "Prep me for my call with Acme Industries tomorrow."
- "Which deals in the sales pipeline need attention this week?"
- "Triage the unassigned support conversations."
- "Turn these meeting notes into tasks in the Website Redesign project."
- "I spent the morning on the Acme migration and two hours on support. Log it."

## Permissions and data

- Claude gets exactly the access your WeldSuite role has. Tools you can't
  use in WeldSuite aren't offered, and every call is checked again when it
  runs.
- Changes made through Claude show up in the audit trail and trigger the
  same automations and notifications as changes made in the browser.
- The skills ask before they change anything you didn't explicitly ask for,
  never send customer replies without your approval of the exact text, and
  save emails as drafts only.
- The plugin itself stores nothing. Your workspace data stays in WeldSuite
  in the EU, under the [WeldSuite privacy policy](https://www.weldsuite.eu/privacy).
  The records Claude reads to answer you are sent to Anthropic as part of
  your conversation, under your agreement with Anthropic.
- Disconnect any time with `/mcp` in Claude Code, or under Customize →
  Connectors in the Claude apps.

## Support

[www.weldsuite.eu/support](https://www.weldsuite.eu/support) or
support@weldsuite.org.

## License

MIT
