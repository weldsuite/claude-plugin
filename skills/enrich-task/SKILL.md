---
name: enrich-task
description: Interview the user to fully specify an under-specified WeldFlow task, then append an Enriched analysis section to the task description in WeldSuite. Use before implementing a vague bug or feature, or when the user says enrich or spec this task.
argument-hint: <task number, name or link>
disable-model-invocation: true
---

# Enrich a WeldFlow task

Enrich task `$ARGUMENTS` before anyone implements it.

1. `get_task`, and `search_task_comments` for the task, to read everything
   already written.
2. If the description already has an `## Enriched analysis` section, say so
   and stop. Never overwrite it.
3. Look through this repository just enough to ask informed questions:
   likely files, existing patterns, similar features.
4. Interview the user in short rounds of one to four questions until scope,
   behaviour and acceptance criteria are clear. After the first round, offer
   to stop with what you have.
5. Draft the section:

   ```markdown
   ---
   ## Enriched analysis

   **Problem:** …

   | Decision | Choice |
   | --- | --- |

   **Acceptance criteria**
   - …

   **Out of scope**
   - …

   **Where to look:** paths in this repository
   ```

6. Show the draft. Only on the user's yes, `update_task` with the original
   description followed by the new section. Keep the original text exactly
   as it was.
7. Suggest `/weldsuite:fix-task <number>` next.
