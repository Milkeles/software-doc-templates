# Live-ops plan: {Game}

*Also called: live-ops calendar, content calendar.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *The window this calendar plans for, e.g. next two quarters* |
| **Owner** | *Live-ops lead* |
| **Last reviewed** | YYYY-MM-DD |
| **Cadence** | *Name your rhythm, e.g. quarterly seasons with biweekly micro-updates* |

*A live game plans content in more than one rhythm at once: a larger seasonal cadence for major content, and a faster cadence for smaller items like events, balance passes, and cosmetics. Name both here, because a calendar that mixes the two without saying which is which makes neither commitment legible.*

---

## 1. Calendar

*Only list items that are agreed, estimated, and at least partially scoped. An unscoped idea on this calendar reads as a promise to anyone who sees it, the same discipline the general [deployment plan](../../general-swe/foundations/deployment-plan.md) already applies to release scope.*

| Window | Content | Type | Depends on | Status |
|---|---|---|---|---|
| *{Date range}* | *{Event or content name}* | *Seasonal / micro-update* | *{Feature, asset, or another team's deliverable}* | *Scoped / in progress / at risk / shipped* |

---

## 2. Capacity check

*Every item added to the calendar competes with the same finite team for time. This section exists so a full calendar is a deliberate decision, not an accumulation nobody added up.*

| | |
|---|---|
| **Committed items this window** | |
| **Team capacity this window** | *Realistic delivery capacity, not aspirational* |
| **Headroom or shortfall** | |

**Tightening the cadence has a real resourcing cost.** Treat any specific percentage figure for that cost with suspicion unless it comes from your own team's tracked data: this template does not cite one, because none of the numbers found in general industry sources could be traced to a disclosed methodology worth repeating here.

**Crunch is a documented problem class in game postmortems generally, and a tight live-ops cadence is a plausible way to produce it, though not one this template can cite a dedicated study for.** If a capacity shortfall in this section is being closed by unplanned overtime rather than by cutting scope, say so and flag it, using the same crunch category the [cycle retrospective](../production/cycle-retrospective.md) already tracks.

---

## 3. Change control

*How late an item can be added to or cut from the calendar, and who decides. Without a stated rule, the calendar drifts by whoever asks loudest closest to the date.*

| | |
|---|---|
| **Who can add an item** | |
| **Who can cut an item** | |
| **Latest an item can be added without displacing something else** | |
| **What happens to a cut item** | *Rescheduled, or dropped, stated explicitly rather than left ambiguous* |

---

## Notes on using this template

*Delete this section too.*

**List only what is scoped.** A calendar item with no estimate and no dependency named is a wish, not a plan. Keep wishes in a separate backlog, not on this document.

**State cadence tightening's cost honestly, in your own numbers.** Marketing and conference-talk figures on the resourcing cost of a faster cadence rarely disclose a methodology worth trusting. Track your own team's data instead of borrowing someone else's unverified figure.

**A full calendar is not automatically a healthy one.** Check section 2 before adding item ten, not after the team is already behind on item seven.

**Where this lives:** wiki or the tracker already holding the calendar, since this changes on a rolling basis and benefits from being where the team already looks for scheduling, not docs-as-code.

---

## Related documents

- [`deployment-plan.md`](deployment-plan.md). What must not collide with a scheduled release on this calendar
- [`../production/cycle-retrospective.md`](../production/cycle-retrospective.md). Where a capacity shortfall or crunch pattern flagged here gets analysed after the fact
- [`release-notes.md`](release-notes.md). How a shipped calendar item gets announced to players
