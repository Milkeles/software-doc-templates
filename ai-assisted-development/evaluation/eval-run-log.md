# Eval run log: {Feature or agent behavior}

*Also called: eval log.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *Link the [evaluation plan](evaluation-plan.md) this log tracks runs against* |
| **Owner** | |
| **Reviewed** | *Cadence, e.g. every release or every eval-set update* |

---

## The log

| Date | Eval set version | Score | Notable failures | Change since last run |
|---|---|---|---|---|
| | | | | |

*Log a run even when nothing changed and the score held steady. A flat trend is only visible if the flat runs are recorded too, not just the ones with a surprise in them.*

---

## Trend

| | |
|---|---|
| **Direction** | *Improving, flat, or degrading, over the last several runs* |
| **If degrading, likely cause** | *A model or prompt change, an eval-set change, or a real regression in the system being evaluated. Say which, since the fix is different for each* |

---

## Eval set changes

*A record of when and why the eval set itself grew or changed, separate from the score history above. An eval set that never grows stops catching new failure modes as the system's real usage changes.*

| Date | Change | Reason |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**Record the score even when the eval set changed.** A score that moved because the eval set got harder is not the same signal as a score that moved because the system got worse. Note the eval-set version alongside every score so the two don't get confused later.

**A degrading trend is a finding, not an embarrassment.** Treat it the way a missed SLO or a rising toil trend is treated elsewhere in this repository: an input that competes for prioritization, not something to quietly absorb.

**Grow the eval set on purpose, and write down why.** A static eval set stops reflecting real usage the moment usage patterns shift. The eval-set-changes table exists so that growth is a deliberate, recorded decision rather than something that happens invisibly between runs.

**Where this lives:** wherever the team already tracks recurring engineering work. This is an operational record, not a durable reference; keep it as lightweight as the team's other running logs.

---

## Related documents

- [`evaluation-plan.md`](evaluation-plan.md). The method this log records the results of running
