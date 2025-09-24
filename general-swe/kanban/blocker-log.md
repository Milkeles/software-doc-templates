# Blocker log

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | *The team.* |
| **Reviewed** | *At every [flow review](flow-review.md).* |

*A blocked item is obvious on the board today and forgotten next month. This log makes blockers countable, and a count is what turns "we are always waiting on the security review" into a case with a number attached.*

*For teams whose flow problems are organisational rather than technical, which is most teams inside large companies, this is the highest-value document in the group.*

---

## What counts as blocked

*Define it, or the log will be inconsistent and the counts will be worthless.*

*The useful test is whether the team can act. If progress needs someone outside the team, or a thing that does not exist yet, it is blocked. If it is merely hard, it is not.*

> **Example.** Blocked means no member of this team can advance the item without a decision, an approval, an access grant or a delivery from outside the team. Difficulty is not a blocker.

**Marking it.** *How a blocked item is flagged on the board, so the state is visible at a glance rather than only in this log.*

---

## The log

*One row per blocked item. Opened when it blocks, closed when it moves.*

| Item | Blocked from | Blocked until | Days | Cause | Waiting on | Escalated |
|---|---|---|---|---|---|---|
| | | | | | | |

**Cause** *is the column that pays for the log. Use a small fixed set so rows group. Inventing a new cause each time gives you a diary instead of data.*

*A workable set: external approval, external team dependency, access or permission, information from a customer, environment or infrastructure, unclear requirement, third-party vendor.*

*"Unclear requirement" deserves its own cause even though it is uncomfortable, because it is the one blocker the team can usually fix upstream itself.*

---

## Escalation policy

*How long an item waits before someone acts, and who acts. Written in advance, because in the moment nobody wants to be the person who escalates.*

| Blocked for | Action | Who |
|---|---|---|
| *1 day* | *Raised in the daily meeting, owner assigned to chase* | *Team* |
| *3 days* | *Escalated to the blocking team's lead* | *Named person* |
| *5 days* | *Escalated to management, item considered for abandonment* | *Named person* |

*Include abandonment as an option and mean it. An item blocked for three weeks is occupying a WIP slot and producing nothing, and pulling it off the board is often the correct answer. Keeping it there to avoid admitting the loss is how boards silently lose capacity.*

**Blocked work and WIP limits.** *Decide now whether a blocked item still counts against the limit.*

*Counting it is the more honest choice, and the more uncomfortable one: it means blockers immediately reduce how much you can start, which is exactly the pressure that gets them resolved. Excluding blocked work from the limit lets a team accumulate stalled items indefinitely while still feeling busy.*

---

## Recurring blockers

*Causes appearing more than twice, promoted out of the log into something someone owns.*

*This table is the output of the whole document. A single blocker is bad luck. The same cause four times is a system problem, and it now has a size in days that makes the conversation possible.*

| Cause | Occurrences | Total days lost | Fix proposed | Owner | Status |
|---|---|---|---|---|---|
| *Waiting on security review* | *7* | *31* | *Pre-approved change categories* | | |

---

## Notes on using this template

*Delete this section too.*

**Log the days, not just the fact.** "We get blocked a lot" is dismissible. "Thirty-one working days lost to one queue last quarter" is not, and it is the same information.

**Do not use it to allocate blame.** The log records where work waits, and the answer is almost always a boundary rather than a person. A blocker log that becomes evidence against another team stops being filled in accurately within a month.

**Review the trend, not the incidents.** Individual blockers get handled by the escalation policy. The value of the log appears at the flow review, where the counts show which boundary to fix.

**Where this lives:** flagged on the board while an item is blocked, so it is visible where decisions are made. The log itself wherever your board tool records it, tallied into the flow review.
