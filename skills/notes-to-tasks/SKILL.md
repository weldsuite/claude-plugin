---
name: notes-to-tasks
description: Turn meeting notes, a call transcript, an email or a brainstorm into WeldFlow tasks with owners, due dates and priorities in the right project, created only after the user approves the list. Use when the user pastes notes and asks to create tasks, capture action items, or turn this into to-dos.
argument-hint: "[project name] then paste the notes"
---

# Notes to tasks

Turn the notes in this conversation into WeldFlow tasks, in the project named
in `$ARGUMENTS` if there is one.

1. **Pull out the action items:** something someone agreed or was asked to
   do. Skip discussion, opinions and things already done. Keep the owner and
   any date that was said.
2. **Resolve them against WeldSuite:**
   - Project: `search_projects`. Ask when no project is named and more than
     one fits.
   - Owners: match the names to members with `get_settings_members`. Leave
     an owner empty rather than guessing.
   - Duplicates: `search_tasks` in the project with a few key words from
     each item, and mark items that look like an existing task.
   - Customer: when the notes are about a customer, find it with
     `search_customers` so tasks can be linked with `customerId`.
3. **Show the list:**

   | # | Task | Owner | Due | Priority | Note |

   Titles start with a verb and stand on their own. Put the context from the
   notes in the description. Mark possible duplicates.
4. Let the user change or drop items. On their yes, `create_task` for each
   remaining item with `projectId`, `title`, `description`, `assigneeIds`,
   `dueDate` and `priority`.
5. List what was created. If the notes were from a customer meeting, offer
   `/weldsuite:log-activity` to record the meeting in WeldCRM.
