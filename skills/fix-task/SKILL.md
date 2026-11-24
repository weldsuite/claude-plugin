---
name: fix-task
description: Take a WeldFlow task from the WeldSuite board to a finished change in the current repository. Loads the task, claims it, implements and verifies the change, then comments on the task and moves it to review or done. Use when the user says fix task, works on a WeldFlow task, or gives a task number, name or WeldFlow link.
argument-hint: <task number, name or link>
disable-model-invocation: true
---

# Fix a WeldFlow task

Fix WeldFlow task `$ARGUMENTS`.

## 1. Resolve the task

- Call `get_task` with the number, name or id. For a link, use the task id
  or number in it. For free text, call `search_tasks` and confirm the match
  with the user when more than one task fits.
- If the task is `done` or `cancelled`, ask before reopening it.

## 2. Dispatch

Run the `weldflow-dispatcher` agent with the task. It reads the task and
this repository and returns a dispatch plan: type, suspected area, open
questions. If it returns questions, ask the user before going on.

## 3. Implement

Run the `weldflow-task-fixer` agent with the task and the dispatch plan,
unless the user passed `--here`, in which case follow the same steps
yourself in this conversation. The fixer claims the task, makes the change,
runs the project's checks and comments on the task.

## 4. Report

Show the task's new status and a short summary of the change and how it was
verified.

## Stop and ask first

- Schema migrations, data deletion or anything that touches production.
- Work outside what the task describes.
- A task assigned to someone else.
