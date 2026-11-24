---
name: list-tasks
description: List open WeldFlow tasks from WeldSuite as a prioritised backlog and suggest which to pick up next. Use when the user asks for their backlog, open bugs, what to work on next, or the tasks in a project.
argument-hint: "[project name] [bugs]"
disable-model-invocation: true
---

# List WeldFlow tasks

Build a backlog from WeldSuite for `$ARGUMENTS` (a project name, `bugs`, or
nothing for everything open).

1. If a project was named, find it with `search_projects`. Otherwise list the
   projects so the table can show project names.
2. Call `search_tasks` for tasks in `backlog`, `todo` and `in_progress`.
   Filter to bugs when the user asked for bugs. Follow the cursor until you
   have the open work, or the first 100 tasks for a large workspace.
3. Show a table:

   | # | Title | Project | Priority | Status | Assignee |

4. Recommend three to five tasks to pick up next, weighing priority, how
   clearly the task is described, and impact. Say why for each.
5. Don't claim or change anything. Suggest `/weldsuite:fix-task <number>`
   or `/weldsuite:enrich-task <number>` next.
