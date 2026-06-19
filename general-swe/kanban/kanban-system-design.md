# Kanban system design: {Service}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Service** | *The service this system delivers. One system per service.* |
| **Participants** | *Everyone in the session. This may not be done by a manager, coach or consultant alone.* |
| **Date** | YYYY-MM-DD |

*The record of why your board looks the way it does. Follows STATIK, the Systems Thinking Approach to Introducing Kanban, from the Kanban Method.*

*Six steps below. They are iterative, not sequential: a later step regularly sends you back to an earlier one. Expect four hours to four days, and expect the workflow model to change twice during it.*

---

## 1. Sources of dissatisfaction

*What is bad now, from both sides. What the people doing the work are unhappy with, and what customers are unhappy with.*

*This comes first deliberately. A Kanban system installed where nobody is dissatisfied becomes tracking overhead, because there is no force pulling anyone to use it. If this section is thin, stop and ask whether you should be doing this at all.*

*Ask both groups separately. They rarely name the same things, and the gap between the two lists is itself a finding.*

**Internal**

- *"We start five things and finish none."*
- *"Every week something urgent lands and the plan is gone."*

**Customer**

- *"I never know when I will get it."* (More often the complaint than "it is too slow.")

---

## 2. Demand

*What arrives, how much, through which channels. Measured over a real period, not recalled.*

*Count from your ticketing system, your inbox, your chat channels. Include the demand that arrives informally: the tap on the shoulder, the direct message. That channel is usually invisible and frequently the largest.*

| Type of demand | Volume per week | Arrives via | Who requests it |
|---|---|---|---|
| | | | |

**Patterns.** *Seasonality, spikes, what correlates with what. A support team whose demand triples after every release has a design problem upstream, and this is where it becomes visible.*

**Unplanned share.** *What proportion arrives without notice. Decides whether iterations were ever viable here.*

---

## 3. Current capability

*What the system actually delivers today. Historical data, not opinion.*

*You may not have this data. Say so and collect it for a month rather than estimating it. A capability figure produced from memory is systematically optimistic, and every downstream decision inherits the error.*

| Measure | Today |
|---|---|
| *Throughput* | *items per week, by type* |
| *Cycle time, 50th percentile* | |
| *Cycle time, 85th percentile* | |
| *Cycle time, 95th percentile* | |
| *Current WIP* | |
| *Where items spend the most time* | |

**Read the spread, not the average.** *The gap between the 50th and 95th percentile is what makes a service feel unreliable. Customers do not experience your median; they experience the variation, and a system with a tight spread at eight days is preferred to one averaging five with a long tail.*

---

## 4. Workflow model

*The activities each type of work actually passes through. Observed, not designed.*

*Trace three or four recently completed items end to end and write down what really happened, including the waiting. Waiting states are usually where most of the elapsed time is, and they are the ones missing from every board drawn from imagination.*

*Different types may follow different paths. Model them separately before deciding whether one board can hold both.*

| Activity | Active or waiting | Typical duration | Who does it |
|---|---|---|---|
| | | | |

**Where work waits longest.** *Name it. This is the finding that justifies the whole exercise, and it is usually a handoff rather than a task.*

---

## 5. Classes of service

*How different work is treated, and by what rule. See [work item types](work-item-types.md).*

*Derive them from the demand and dissatisfaction above rather than adopting the standard four by default. If nothing in your demand has a sharply rising cost of delay, you do not need an expedite class, and having one will only teach people to ask for it.*

---

## 6. The system design

*What you are going to build, from everything above.*

- **Board.** *Columns, rows, what each state means. Link the [Definition of Workflow](definition-of-workflow.md).*
- **WIP limits.** *Starting numbers, and how you chose them. Just below current WIP is the usual answer.*
- **Policies.** *Pull criteria, replenishment, blockers, escalation.*
- **Metrics.** *What you will track and where it comes from.*
- **Cadences.** *Which meetings, how often, for what. The Kanban Method's team-level set is a daily meeting to track flow, a replenishment meeting weekly or as needed, and a retrospective every two to four weeks. Add cadences as you need them rather than adopting all seven on day one.*
- **Service Level Expectation.** *The starting figure and when you will recalculate it.*

---

## What we expect to change

*Predictions, with what would confirm them. Written now so you cannot rewrite history later.*

| We expect | Measured by | Check on |
|---|---|---|
| *Cycle time 85th percentile drops below 10 days* | *Board data* | *In 8 weeks* |
| *Fewer than 2 expedites per month* | *Expedite tally* | *In 8 weeks* |

*This is the difference between an evolutionary change and a reorganisation. If you cannot say what should improve, you cannot tell whether it did, and the board will be judged on whether people like it.*

---

## Notes on using this template

*Delete this section too.*

**Do it with the people who do the work.** The Kanban Method is explicit that this "should not be done in isolation" by a project manager, team lead, coach or consultant. Everyone carries a private picture of how work flows, and those pictures rarely match. Reconciling them is most of the value here, and it cannot be done by proxy.

**Expect to iterate.** Step 5 will send you back to step 2. That is the process working, not a sign you did step 2 badly.

**Redo it when the service changes**, not on a schedule. New demand, a new team boundary, or a persistent flow problem the reviews cannot fix.

**Where this lives:** a wiki. It explains the board rather than operating it, and it is consulted when changing the system, not while pulling work. Archive old versions; the comparison is the useful part.

---

## Related documents

- [`definition-of-workflow.md`](definition-of-workflow.md). The board document that step 6 produces, describing what this session designed
- [`work-item-types.md`](work-item-types.md). Where the classes of service named in step 5 get their full policy and limits written down
- [`flow-review.md`](flow-review.md). Supplies the current capability data this session starts from, and is where a persistent problem this design cannot fix gets raised
