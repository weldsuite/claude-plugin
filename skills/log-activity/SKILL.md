---
name: log-activity
description: Log a call, meeting, email, demo or note to WeldCRM from what the user describes or pastes (meeting notes, a transcript, a summary), linked to the right customer, contact and deal, with the outcome and any follow-up. Use when the user says log this call, add a note to, record the meeting with, or pastes notes from a customer conversation.
argument-hint: <who it was with, or paste the notes>
---

# Log a CRM activity

Log the activity described in `$ARGUMENTS` (or in the conversation).

1. **Work out the facts:** type (`call`, `meeting`, `email`, `demo`,
   `note`, …), who it was with, when, what was discussed, the outcome, and
   any follow-up agreed. Ask only for what's missing and matters: who and
   when.
2. **Link it:** find the customer (`search_customers`), the contact
   (`search_contacts`) and, if a deal was discussed, the opportunity
   (`search_opportunities` with `customerId`). Ask when there is more than
   one plausible match.
3. **Show the activity** before saving:

   ```
   Meeting with Jane Doe (Acme Industries), 24 Nov, 30 min
   Deal: Acme renewal 2027
   Summary: …
   Outcome: …
   Follow-up: send revised quote by 28 Nov
   ```

4. On yes, `create_activity` with `type`, `subject`, `description`,
   `customerId`, `contactId`, `opportunityId`, `status: completed`,
   `startTime`, `duration` (minutes), `outcome` and, when agreed,
   `nextAction` and `followUpDate`.
5. **Follow-ups:** for each agreed action, offer a planned activity
   (`create_activity` with `status: planned` and a `dueDate`) or a WeldFlow
   task (`create_task`). If the deal moved forward, offer to update its
   stage or next step with `update_opportunity`.

Write the summary in the user's words and facts. Don't add commitments
nobody made.
