# Cycle retrospective: {Milestone or season}

*Also called: postmortem.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Cycle** | *Vertical slice / alpha / beta / gold / a named live-ops season* |
| **Dates** | *Start to end* |
| **Facilitator** | |
| **Present** | |

*This is not a [sprint retrospective](../../general-swe/agile-scrum/sprint-retrospective.md). A sprint retrospective looks at two weeks; this looks at a production milestone that can span months and multiple sprints inside it. Run this in addition to sprint retrospectives if your team uses Scrum underneath, not instead of them. Open with the same prime directive that template uses, for the same reason: naming a real problem has to cost the person naming it nothing.*

> Regardless of what we discover, we understand and truly believe that everyone did the best job they could, given what they knew at the time, their skills and abilities, the resources available, and the situation at hand.
>
> Norm Kerth, *Project Retrospectives*, 2001

---

## Did we hit the milestone

*Against the [business plan](../foundations/business-plan.md)'s milestone table, if one exists. What was the deliverable, and what did we actually ship.*

| Committed | Delivered | Gap |
|---|---|---|
| | | |

---

## The four patterns

*A survey of twenty published game postmortems found four problem categories recurring across the industry: scope, scheduling, crunch, and technology. Use them as a checklist so a real problem does not go unmentioned just because nobody happened to bring it up.*

### Scope

*Did the milestone's scope grow after it was set? Feature creep, driven by an expanding design document or by "just one more thing," was found to be a leading cause of trouble in the source survey above. Name what got added, and whether it was ever formally added to the plan or just accreted.*

### Scheduling

*Did any task take meaningfully longer than estimated? Underestimating task duration and setting ambitious milestone deadlines on top of it was the second recurring pattern. Look for tasks that were wrong by a similar factor across the milestone; a consistent multiplier is more useful than a list of individually-surprising delays.*

### Crunch

*Was there a period of sustained overtime? State it plainly, with dates and who it affected, even though this is the finding people are most tempted to soften. A crunch pattern that recurs milestone over milestone is a planning problem, not a commitment problem, and this section is where that becomes visible over time.*

### Technology

*Did tooling, platform, or engine maturity cause delay? New platforms and immature tools were the fourth recurring category. Distinguish a one-off technical surprise from a tool or pipeline the team will hit again next milestone.*

---

## Cross-discipline communication

*Game teams carry more job-role diversity than most software teams, and that diversity has been found to produce communication splits severe enough to affect delivery. Ask directly: was there a point where two disciplines, say art and engineering, or design and audio, discovered a disagreement later than they should have? What would have surfaced it earlier?*

---

## What went well

*Genuinely, not morale filler. A process, a review, a piece of tooling, a decision that held up. These are controls you already have; knowing which ones worked tells you what to protect.*

---

## Changes for next cycle
*One or two changes, each with an owner and a tracking reference. A retrospective that produces eight changes produces none, for the same reason the sprint retrospective template gives: a team stops believing in a list that never gets acted on.*

| Change | Owner | Ticket | How we will know it worked |
|---|---|---|---|
| | | | |

**Last cycle's changes.** *Check them first. Anything undone gets a decision now: done, dropped, or carried with a stated reason. Carrying an item silently teaches the team that this list is optional.*

| Previous change | Status | Effect |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**This runs on a milestone cadence, not a sprint cadence.** Trying to run this every two weeks produces a shallow version of a sprint retrospective with extra steps. Trying to run a sprint retrospective at milestone scale misses the crunch and cross-discipline patterns that only show up over months.

**Say crunch happened, if it did.** A retrospective that omits a crunch period everyone lived through teaches the team that the document is decorative. The value of naming it is entirely in the pattern becoming visible across several of these documents kept in a series, not in any single instance.

**Keep the series, not just the instance.** A retrospective that recurs for the third time is not the same finding as one that appears for the first time; it means an earlier fix addressed a symptom rather than the cause. That comparison is only possible if these are kept together and read as a set.

**Where this lives:** the wiki, kept in a series with the previous cycles. Actions go to the tracker, always.

---

## Related documents

- [`../../general-swe/agile-scrum/sprint-retrospective.md`](../../general-swe/agile-scrum/sprint-retrospective.md). The shorter-cadence event this complements rather than replaces
- [`../foundations/business-plan.md`](../foundations/business-plan.md). The milestone commitments this retrospective checks delivery against
- [`../foundations/game-design-document.md`](../foundations/game-design-document.md). Where scope creep traces back to an expanding design document
- [`../../general-swe/foundations/incident-postmortem.md`](../../general-swe/foundations/incident-postmortem.md). The same blameless discipline, applied to a single incident instead of a production phase
