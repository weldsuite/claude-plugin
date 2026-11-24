---
name: done-task
description: Close out a WeldFlow task after the work is verified, commenting with the pull request or commit and moving the task to review or done in WeldSuite. Use when the user says the task is done or wants to close it.
argument-hint: <task number, name or link> [pull request URL or commit]
disable-model-invocation: true
---

# Close a WeldFlow task

Close out the task in `$ARGUMENTS` (`<task> [pull request URL or commit]`).

1. Check the work: run this project's usual lint, type-check and test
   commands for what changed, and `git status` for stray files.
2. If a check fails, stop. Show the failure and leave the task as it is.
3. `create_task_comment` with a short summary of the change and the pull
   request URL or commit, when given.
4. `update_task`: `status` `review` when there is a pull request, `done`
   otherwise.
5. Print: `Closed #<number>. Status: <status>. Ref: <pull request, commit or none>`.

Never mark a task done when verification failed, unless the user explicitly
says to.
