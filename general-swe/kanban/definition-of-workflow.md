# Definition of Workflow: {Team or service}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | *The team.* |
| **Agreed** | YYYY-MM-DD |
| **Reviewed** | *When you last checked this still describes reality.* |

*The one artefact Kanban requires. Six elements below, all mandatory. A board without them is a task list with columns.*

*Keep it on the board. A workflow definition in a wiki is consulted after the decision it was meant to inform.*

---

## 1. What a work item is

*The unit of value that moves through this workflow. State it precisely enough that two people would split a large request the same way.*

*This decides what everything else means. If some items are two hours and others are three weeks, your cycle time distribution describes nothing.*

> **Example.** A work item is one customer-visible change that can be released independently. Work larger than five days is split before it is started.

**Types.** *List them, and link the [work item types](work-item-types.md) definitions.*

---

## 2. When work starts and finishes

*Two points on the board. Everything between them is counted.*

*The single most consequential line in this document. Cycle time is measured from the start point, so moving it changes every number you report. Teams that leave it implicit usually discover that half the team counts from "picked up" and half from "requested", and the difference is weeks.*

| | |
|---|---|
| **Started** | *Entering the "In progress" column. Not when the request arrived.* |
| **Finished** | *Deployed to production and verified. Not merged.* |

*Everything before the start point is an option, not a commitment. Distinguishing the two is what lets a backlog grow without lying about your workload.*

---

## 3. States

*The columns, in order, with what each means. One line each.*

*Split a state into active and waiting where work genuinely queues. "In review" that mixes "being reviewed" with "waiting for a reviewer" hides your largest delay, and hidden queue time is where most cycle time actually goes.*

| State | An item here is | Leaves when |
|---|---|---|
| *Options* | *Requested, not committed* | *Pulled at replenishment* |
| *In progress* | *Actively being built* | *Pull request open and CI green* |
| *Waiting for review* | *Queued, nobody working on it* | *A reviewer picks it up* |
| *In review* | *Being reviewed* | *Approved* |
| *Done* | *In production and verified* | |

---

## 4. How WIP is controlled

*The limits, where they apply, and what happens when one is reached.*

*Limits must be enforced by the board, not by intention. A number written on a wiki page is a suggestion.*

| Where | Limit | Why this number |
|---|---|---|
| *In progress* | *3* | *Team of 5, allows one pair plus one solo item* |
| *Waiting for review + In review* | *4* | *Review is our longest queue* |
| *Whole board* | *8* | |

**When a limit is reached.** *The rule, written before the first time it happens.*

> **Example.** Nobody starts new work. Help finish something already started, or if nothing can be helped, pick up improvement work. Breaking a limit requires the whole team to agree, in the open, and gets logged.

*Set the first limit slightly below your current WIP, then lower it while cycle time keeps improving. Starting from a number someone read in a book produces either no change or a revolt.*

---

## 5. Explicit policies

*The rules for moving an item from one state to the next, and the rules for how work enters at all. Written on the board, next to where the decision happens.*

*The Kanban Method's guidance is that policies should be "sparse, simple" and agreed by everyone involved, and that they enable self-organisation rather than replacing judgement. A board with twenty policies has a compliance problem, not a flow problem.*

**Pull criteria.** *What must be true for an item to move into each state. This is the policy that stops work piling up in a column because "it's basically done".*

| Into | Requires |
|---|---|
| *In progress* | *Acceptance criteria agreed, no unresolved dependency* |
| *In review* | *CI green, description explains why* |
| *Done* | *Deployed, verified in production, changelog entry* |

**Replenishment.** *When items enter the Options column, how many, and who decides. Weekly is common. Say what happens if something urgent arrives between replenishments.*

**Blocked work.** *How an item is marked blocked, who is told, and after how long it escalates. See the [blocker log](blocker-log.md).*

**Aged work.** *What happens when an item's age passes the SLE. Not "we notice": say who does what.*

---

## 6. Service Level Expectation

*A forecast of how long an item takes, in two parts: an elapsed time and a probability.*

> **{85}% of work items finish within {8} days or less.**

*Calculate it from your own history, do not choose it. Take the cycle times of the last 30 to 50 completed items, sort them, and read off the 85th percentile. If you have no history, say so, publish a provisional figure and recalculate after a month.*

*Per type if types differ materially, which they usually do.*

| Type | SLE | Based on |
|---|---|---|
| *Feature* | *85% within 8 days* | *Last 40 items* |
| *Defect* | *85% within 3 days* | *Last 30 items* |

**What we do when an item is about to breach it.** *The action, named. This is the entire point of having an SLE: it converts work item age into a trigger rather than a statistic.*

---

## Changing this

*Who may change it and when. Any team member may propose; the team agrees at the flow review. Record what changed and when, because a change to the start point or the states breaks comparability with your own past data and you will want to know why the graph jumped.*

| Date | Change | Reason |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**Describe what you do, then change it.** The Kanban Method's first change principle is to start with what you do now. A Definition of Workflow describing an aspirational process gives you metrics from a system nobody is running.

**One page.** If it does not fit on the board, it will not be read at the board.

**Sections 2 and 6 are the ones teams skip.** Without an agreed start point, cycle time is uncomputable. Without an SLE, you have numbers and no expectation to compare them against, so nothing ever counts as a problem and nothing gets fixed.

**Where this lives:** on the board. WIP limits configured as limits, pull criteria in column descriptions, this document on the board's front page.
