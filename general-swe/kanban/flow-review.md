# Flow review: {period}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Period** | *From, to.* |
| **Present** | |
| **Items completed** | |

*Kanban has no Sprint boundary, so nothing makes a team look up from the board. This is that forcing function.*

*Pull the numbers from your tool. Do not retype them into this document; link the charts. What belongs here is what you concluded and what you changed.*

---

## The numbers

| Metric | This period | Last period | Trend |
|---|---|---|---|
| *Throughput* | | | |
| *Cycle time, 50th percentile* | | | |
| *Cycle time, 85th percentile* | | | |
| *Cycle time, 95th percentile* | | | |
| *Average WIP* | | | |
| *SLE met* | *__% against a target of 85%* | | |

*Report percentiles, never averages. Cycle time distributions have long right tails, so the mean sits below most of your data and describes an experience few customers had. The 85th percentile is what you promised; the 95th is what makes people angry.*

**By type.** *Repeat for each [work item type](work-item-types.md) that has its own SLE. Mixed numbers hide the problem in whichever type is smaller.*

---

## Work item age, right now

*The one leading indicator you have. Everything else in this document is about work that has already finished.*

*List every unfinished item older than the SLE, with what is happening to it. This is a live triage list, not a report.*

| Item | Age | SLE | State | Action |
|---|---|---|---|---|
| | *14d* | *8d* | *Waiting for review* | *Escalate today* |

*If this table is long, stop the review and deal with it. Discussing last month's cycle time while six items are aging past the expectation is the exact failure this metric exists to prevent.*

---

## Where time went

*Which states held work longest, and what proportion of total cycle time was waiting rather than working.*

*Flow efficiency, active time divided by total elapsed time, is often between 5 and 20 percent for knowledge work. Teams meeting that figure for the first time usually try to speed up the active portion, which is the smaller half. The queues are where the time is.*

| State | Median time in state | Share of cycle time | Active or waiting |
|---|---|---|---|
| | | | |

---

## Blockers

*Summarised from the [blocker log](blocker-log.md). Count and total days lost, grouped by cause.*

*Grouping is what makes this actionable. Seven separate incidents of "waiting on security review" are one problem with a size attached, and a size is what you need to raise it outside the team.*

| Cause | Times | Days lost | Owner of the fix |
|---|---|---|---|
| | | | |

---

## What we are changing

*One or two changes. With owners.*

*Kanban's change model is evolutionary: small adjustments, observed for effect, kept or reverted. That only works if you change one thing at a time. Two simultaneous changes and you will never know which one worked.*

| Change | Owner | We expect | Check at |
|---|---|---|---|
| *Lower review WIP limit from 4 to 2* | | *Review queue time halves* | *Next review* |

**Last period's changes.** *Did they do what you predicted? Keep, revert or adjust. Skipping this check is how boards accumulate policies nobody can justify.*

| Change | Expected | Actual | Keep or revert |
|---|---|---|---|

---

## Definition of Workflow changes

*Anything that changed in the [Definition of Workflow](definition-of-workflow.md) this period, and the effect on comparability.*

*Moving the start point or splitting a state breaks comparison with your own history. Note it here or someone will read a step in the graph as an improvement.*

---

## Notes on using this template

*Delete this section too.*

**These metrics describe the system, not people.** None of them can be attributed to an individual, which is what makes it safe to look at them honestly. The moment throughput becomes a personal target, it stops measuring anything: work items get smaller and nothing else changes.

**Recalculate the SLE from data, do not negotiate it.** An SLE set by what stakeholders want to hear is a forecast of nothing. If the 85th percentile is 14 days and someone wants 5, that is a conversation about the system, and this document is the evidence for it.

**Monthly is usually right.** Weekly produces noise a team will act on; quarterly is too slow for evolutionary change to feel connected to anything.

**Where this lives:** the wiki, with charts linked from the tool rather than pasted. Changes go to wherever your improvement work is tracked, with an owner.
