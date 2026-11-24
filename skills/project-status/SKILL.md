---
name: project-status
description: Write a status report for a WeldFlow project, covering progress, what's in flight, what's overdue or blocked, milestones and the active sprint, with the risks and decisions needed, and optionally post it to the project. Use for a project update, status report, weekly report, sprint review or when the user asks how a project is going.
argument-hint: <project name> [since date]
---

# Project status report

Report on project `$ARGUMENTS` (a project name, and optionally the date the
report covers from, default seven days ago).

## Gather

1. `search_projects` to find the project; `get_project` for its details,
   owner and dates.
2. `search_tasks` with `projectId`, following the cursor, to get every task
   with its status, priority, assignees, due date and last update.
3. `search_milestones` with `projectId`, and `search_sprints` with
   `projectId` and `status: active`.
4. For blocked or overdue high-priority tasks, `search_task_comments` with
   `taskId` to see the latest word.

## Work out

- **Done** in the period: tasks in `done` whose completion or last update
  falls after the start date. If the tasks don't show when they were
  finished, list what is done and say the period can't be told apart.
- **In flight:** `in_progress`, `review` and `testing`, with who has them.
- **Overdue:** due date passed and not `done` or `cancelled`.
- **Blocked or stuck:** tasks that comments call blocked, or in progress for
  much longer than their estimate.
- **Milestones:** next ones, their dates, and whether the open tasks behind
  them can make it.
- **Sprint:** done versus planned, days left.

## Report

```
# <Project> — status, <date>

**Overall:** on track | at risk | off track, and one sentence why.

**Done since <date>:** …
**In progress:** …
**Overdue:** task, assignee, due date
**Blocked:** task, what's blocking it
**Milestones:** name, date, on track or not
**Risks and decisions needed:** …
**Next week:** …
```

Base "overall" on the facts above, not on optimism. Then offer to post the
report to the project with `create_project_message`, only on the user's yes.
