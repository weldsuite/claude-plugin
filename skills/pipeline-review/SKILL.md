---
name: pipeline-review
description: Review the WeldCRM sales pipeline, covering open opportunities by stage, a weighted forecast, stalled and at-risk deals, and the next step each deal needs, then update next steps or risk on the user's approval. Use for a pipeline review, forecast, deal review, sales meeting prep, or when the user asks which deals need attention.
argument-hint: "[pipeline] [owner] [this quarter | this month]"
---

# Pipeline review

Review the pipeline for `$ARGUMENTS` (a pipeline name, an owner, a period,
or nothing for everything open).

## Gather

1. `search_pipelines`, and `search_pipeline_stages` for the pipeline in
   scope, so stages appear in their real order.
2. `search_opportunities` for open deals, filtered by `pipeline` and
   `ownerId` when the user named them (see the `weldsuite` skill for finding
   the user's own id). Follow the cursor until you have them all.
3. For deals you flag, `search_activities` with `opportunityId` to see the
   last touch.

## Analyse

- **By stage:** count, total amount, and weighted amount (amount ×
  probability) per stage, in stage order.
- **Forecast** for the period: deals with a close date inside it, weighted
  and unweighted.
- **Needs attention**, with the reason:
  - close date already passed;
  - next step date passed, or no next step at all;
  - no activity in the last 14 days;
  - `riskLevel` high or medium;
  - large deal that hasn't moved stage in a long time.

## Report

```
# Pipeline review — <scope>, <date>

| Stage | Deals | Amount | Weighted |

Forecast <period>: <weighted> weighted, <total> total, <n> deals.

## Needs attention
| Deal | Customer | Owner | Stage | Amount | Problem | Suggested next step |
```

Then offer concrete updates: new `nextStep` and `nextStepDate`, a corrected
`closeDate`, or `riskLevel` and `riskReason`. Show them as a list and make
only the ones the user approves, with `update_opportunity`.
