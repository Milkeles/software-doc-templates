# Toil log: {Team or service}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | |
| **Owner** | |
| **Reviewed** | *Cadence, e.g. every sprint or every on-call rotation* |

*Google's SRE practice defines toil as work that is "manual, repetitive, automatable, tactical, devoid of enduring value, and that scales linearly as a service grows." Six characteristics worth checking against, not just the label: manual (a person's hands-on time counts even running a pre-written script), repetitive, automatable (a machine could do it as well), tactical (interrupt-driven, not planned), no enduring value ("if your service remains in the same state after you have finished a task, the task was probably toil"), and scaling linearly with service size, traffic, or user count. Google's own operating target caps toil at 50% of an engineer's time; uncapped toil is linked to career stagnation, low morale, and attrition.*

---

## The log

| Task | Trigger | Time spent | Toil characteristics present | Automatable? |
|---|---|---|---|---|
| | | | | |

*Log it even when it feels too small to write down. The value is in the total, not any single entry.*

---

## Toil budget

| | |
|---|---|
| **Toil this period** | *As a fraction of total on-call or operational time* |
| **Target ceiling** | |
| **Trend** | *Rising, falling, flat, versus last period* |

---

## Elimination candidates

*The highest-value automation targets, ranked by how much recurring time they'd return.*

| Task | Frequency | Estimated automation cost | Status |
|---|---|---|---|
| | | | |

---

## Notes on using this template

*Delete this section too.*

**Log toil even when the team is not currently overloaded.** The point of a log is catching the trend before it becomes a crisis, not documenting a crisis that's already obvious.

**"No enduring value" is the sharpest test in the definition.** If the system is in the exact same state after the task as before some future recurrence of the same problem, it was toil, no matter how much skill it took to execute.

**A rising toil trend is itself an escalation-worthy signal.** Treat it the way an SLO miss is treated: as an input that should compete for prioritization against feature work, not as background noise the team absorbs indefinitely.

**Where this lives:** wherever the team already tracks its own work, reviewed on a set cadence. This is an operational record, not a durable reference; let it be as lightweight as the team's existing tracking allows.

---

## Related documents

- [`error-budget-policy.md`](error-budget-policy.md). Where reliability work triggered by a budget miss often shows up here as reduced toil once it lands
- [`../../general-swe/foundations/runbook.md`](../../general-swe/foundations/runbook.md). A runbook whose steps never change is a strong candidate for the elimination table above
