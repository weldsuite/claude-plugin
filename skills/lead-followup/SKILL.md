---
name: lead-followup
description: Find WeldCRM leads that have gone quiet, rank them by how promising they are, and draft personal follow-up emails into WeldMail drafts for the user to review and send. Use when the user asks which leads need a follow-up, who hasn't been contacted, or wants follow-up emails drafted.
argument-hint: "[days quiet, default 14] [owner]"
---

# Lead follow-up

Find leads that need a follow-up for `$ARGUMENTS` (how many days without
contact, default 14, and optionally an owner).

## Find them

1. `search_leads` for open, unqualified leads, filtered by `ownerId` when
   given. Skip leads whose status means lost or disqualified in this
   workspace.
2. For each, `search_activities` with `leadId` and take the newest activity.
   A lead is quiet when its newest activity is older than the threshold, or
   it has none.
3. Rank the quiet leads by `rating` and `score`, then by how long they've
   been quiet. Show the top ten:

   | Lead | Company | Owner | Last contact | Rating | Why follow up |

## Draft the emails

When the user picks leads to follow up:

1. Read the lead (`get_lead`) and its activities for context: what they
   asked about (`productInterest`, `need`, `notes`) and what was said last.
2. Find the user's mail account with `search_mail_accounts`.
3. Write a short, specific follow-up for each: refer to the last
   conversation, offer one clear next step. No generic templates.
4. Show the drafts. On the user's yes, save each with `create_mail_draft`.
   This never sends anything: the user reviews and sends from WeldMail.
5. Offer to set each lead's `nextAction` with `update_lead`.

Never log an activity for an email that hasn't been sent.
