---
name: claim-task
description: Claim a WeldFlow task in WeldSuite, assigning it to the current user and moving it to in progress, without starting the work. Use when the user says claim this task or wants to mark a task as theirs.
argument-hint: <task number, name or link>
disable-model-invocation: true
---

# Claim a WeldFlow task

Claim task `$ARGUMENTS`.

1. `get_task` to confirm it exists and read its assignee and status.
2. If someone else is assigned, say who and ask before taking it over.
3. If you don't know the user's member id, find it with
   `get_settings_members` (ask the user which member they are if it isn't
   clear).
4. `update_task`: set `status` to `in_progress` and add the user to the
   assignees.
5. `create_task_comment`: "Claimed from Claude Code."
6. Print: `Claimed #<number>: <title>. Next: /weldsuite:fix-task <number>`.

Don't start implementing in this skill.
