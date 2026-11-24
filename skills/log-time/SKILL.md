---
name: log-time
description: Turn a description of the user's day or week into WeldSuite time entries on the right projects and tasks, with durations, billable flags and descriptions, created after the user approves them. Also checks for gaps and double bookings. Use when the user says log my time, fill in my timesheet, or describes what they worked on and for how long.
argument-hint: "[date or week] then describe the work"
---

# Log time

Log time for `$ARGUMENTS` (default: today) from what the user describes.

1. **Parse the work:** for each block, what was done, for how long (or from
   when to when), and for which client, project or task. Ask about anything
   without a duration; don't guess hours.
2. **Match it:** `search_projects` for each project, and `search_tasks` with
   `projectId` when a specific task is mentioned. Ask when a match is
   ambiguous.
3. **Check what's already logged:** `search_time_entries` with the user's
   `userId` (see the `weldsuite` skill) and `fromDate` and `toDate` for the
   period. Flag overlaps with new entries and days with gaps.
4. **Show the timesheet:**

   | Date | Project | Task | Duration | Billable | Description |

   Durations in hours and minutes; totals per day. Billable follows the
   project's usual practice from earlier entries when the user didn't say.
5. On yes, `create_time_entry` for each row with `projectId`, `taskId`,
   `date` (YYYY-MM-DD), `duration` in minutes, `billable`, `description`, and
   `startTime` and `endTime` when the user gave times.
6. Report the totals created. Don't submit entries for approval unless the
   user asks.
