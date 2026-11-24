---
name: account-brief
description: Prepare a one-page brief on a customer, company or contact from WeldSuite before a meeting or call, covering who they are, open deals, recent activity, open support issues and agreed follow-ups, with suggested talking points. Use when the user says prep me for, brief me on, what's going on with, or before a meeting with a customer or contact.
argument-hint: <customer, company or contact name>
---

# Account brief

Build a brief on `$ARGUMENTS`.

## Gather

1. Find the account with `search_customers`; if nothing matches, try
   `search_contacts` and use the contact's company. When several match, ask
   which one.
2. `get_customer` for the details, and `search_contacts` with its
   `companyId` for the people.
3. `search_opportunities` with `customerId`: open deals, their stage, amount,
   close date and next step.
4. `search_activities` with `customerId`: the last ten calls, emails,
   meetings and notes, plus anything planned.
5. `search_quotes` with the customer's name for recent quotes.
6. `search_conversations` with `q` set to the customer's name or main
   contact's email, `state: open`, for open helpdesk issues. Read the newest
   one or two with `get_conversation`.
7. If the user's meeting is in the calendar, `search_calendar_events` with
   the customer's name to find it and its attendees.

## Write the brief

```
# <Customer> — brief for <meeting, date>

**Who they are:** one or two lines: industry, size, how long a customer, owner.
**People:** name, role, last contact, for the two to five who matter.
**Open deals:** deal, stage, amount, close date, next step. Flag overdue next steps.
**Recent activity:** the last few touches, newest first, one line each.
**Open support issues:** subject, priority, how long open. Flag anything urgent.
**Promises outstanding:** follow-ups we committed to and haven't done.
**Talking points:** three to five, tied to the facts above.
**Risks:** anything that could hurt the relationship or a deal.
```

Leave out a section that has nothing in it, and say when data looks thin
(for example, no activity logged in 90 days). Don't change anything; offer
`/weldsuite:log-activity` after the meeting.
