# Work item types and classes of service

*Also called: issue types, ticket types.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | *The board.* |
| **Agreed** | YYYY-MM-DD |

*Two separate classifications, routinely confused. **Type** is what the work is. **Class of service** is how urgently it must be handled and why. A production defect and a feature are different types; either can be expedited.*

---

## Work item types

*The kinds of work that arrive here. Keep the list short: four or five types that genuinely behave differently.*

*They exist so metrics separate. A cycle time averaged across a two-hour support request and a three-week feature describes neither, and acting on it produces changes that help nobody.*

| Type | What it is | Typical size | Arrives via | Separate SLE |
|---|---|---|---|---|
| *Feature* | *New customer-visible capability* | *3 to 8 days* | *Replenishment from the roadmap* | *Yes* |
| *Defect* | *Something works incorrectly in production* | *Hours to 2 days* | *Support, alerts* | *Yes* |
| *Maintenance* | *Upgrades, patching, dependency work* | *1 to 3 days* | *Planned* | *No* |
| *Spike* | *Timeboxed investigation producing a decision* | *1 to 2 days* | *Any* | *No* |

*Split a type when the two halves have visibly different cycle time distributions. Merge two types when they do not. The distribution decides, not the org chart.*

**Unplanned demand.** *What proportion of your throughput arrives unplanned, measured rather than guessed. It is the number that tells you whether iteration-based planning could ever have worked here, and it belongs in this document because people will dispute it.*

---

## Classes of service

*How work is treated, based on how the cost of delay behaves. From the Kanban Method. The Kanban Guide does not include classes of service, so if you use them, know that you are adding to the Guide rather than following it.*

*The point is to make urgency a rule instead of a negotiation. Without a class, "this is urgent" is decided by whoever pushes hardest, and the cost of that decision falls on work nobody is defending.*

| Class | Use it when | Policy | Limit |
|---|---|---|---|
| **Expedite** | *Cost of delay is immediate and severe. Production down, money leaking, legal exposure.* | *Pre-empts other work. May exceed WIP limits. Requires a named approver.* | *1 at a time* |
| **Fixed date** | *Cost of delay jumps sharply after a specific date. Regulation, contract, external launch.* | *Started early enough to finish before the date, scheduled from cycle time history, not optimism.* | *Set one* |
| **Standard** | *Cost of delay grows steadily. Most work.* | *First in, first out within the class.* | *Most of the board* |
| **Intangible** | *No immediate cost of delay, real cost later. Debt, upgrades, tooling.* | *A reserved share of capacity, so it is never simply outcompeted.* | *Reserve a percentage* |

**Who may declare each class, and by what test.** *Name a person or role for expedite and fixed date. Write the test as an observable condition, not a feeling.*

> **Example.** Expedite requires either an active incident at severity 2 or above, or written agreement from the head of product. Being asked urgently by a stakeholder does not qualify.

**Expedite budget.** *Track how many expedites you accept per month. If it exceeds roughly one in ten items, the class has stopped meaning anything, and the real finding is that your planned work is not planned.*

---

## Reserved capacity

*If you reserve capacity for a class, say how much and how it is enforced on the board.*

*Intangible work loses every direct contest with visible customer work, which is why it needs protection rather than prioritisation. A reserved lane or a standing WIP allocation enforces it; good intentions at replenishment do not.*

> **Example.** One of the three in-progress slots is reserved for intangible work. It may sit empty; it may not be reassigned.

---

## Notes on using this template

*Delete this section too.*

**Start with types, add classes only when you need them.** Most teams get most of the benefit from separating types and measuring them apart. Classes of service earn their place when urgency is being decided socially and it is costing you.

**Watch for class inflation.** Every expedite lane eventually fills up. The countermeasures are a hard limit, a named approver, and a monthly count that everyone sees. Without those three, expedite becomes the default class within a year and you are back to negotiation.

**Where this lives:** on the board. Types as card types or colours; classes as lanes or tags with their policy written where the card sits. Both must be legible at the moment someone decides what to pull.

---

## Related documents

- [`definition-of-workflow.md`](definition-of-workflow.md). Element 1 asks for the work item unit to be defined, and links back to the types listed here
- [`kanban-system-design.md`](kanban-system-design.md). Where classes of service are derived from measured demand rather than adopted by default
- [`flow-review.md`](flow-review.md). Reports metrics per type, so a problem in one type is not hidden inside an average of unlike work
