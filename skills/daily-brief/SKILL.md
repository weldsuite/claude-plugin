---
name: daily-brief
description: Give the user a short brief on their day in WeldSuite, covering tasks due or overdue, helpdesk conversations waiting on them, deals with a next step due, follow-ups planned and today's calendar events, ending with a suggested order of work. Use when the user asks what's on my plate, plan my day, my day, what should I work on, or for a morning brief.
argument-hint: "[today | tomorrow | this week]"
---

# Daily brief

Brief the user on `$ARGUMENTS` (default: today).

First find out who the user is in WeldSuite (see "Who is me?" in the
`weldsuite` skill). Then gather, skipping any area their role can't read:

1. **Tasks:** `search_tasks` with `assigneeId` and `dueDateTo` set to the end
   of the period. Keep tasks not `done` or `cancelled`. Split into overdue
   and due in the period. Add `in_progress` tasks without a due date.
2. **Helpdesk:** `search_conversations` with `state: open`, the user's
   `assigneeId` and `sort: waiting_longest`.
3. **Deals:** `search_opportunities` with the user's `ownerId`; keep open
   deals whose next step date or close date falls in or before the period.
4. **Follow-ups:** `search_activities` with `assignedToId` and
   `status: planned`; keep those due in or before the period.
5. **Calendar:** `search_calendars` with the user's `ownerId`, then
   `search_calendar_events` per calendar, keeping events in the period.
   Calendar search has no date filter, so say if the list may be incomplete.

## Brief

```
# <Day, date>

**Meetings:** time, title, with whom.
**Overdue:** what slipped, oldest first.
**Due <period>:** tasks, follow-ups and deal next steps.
**Waiting on you:** helpdesk conversations, longest waiting first.

**Suggested order:** five or so items, fitted around the meetings, with the
reason for the order.
```

Keep it to what fits on one screen; link to more on request. Don't change
anything unless the user asks.
