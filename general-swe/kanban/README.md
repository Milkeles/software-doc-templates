# Kanban

Documents for teams that pull work continuously against WIP limits instead of committing to iterations.

Support, platform, operations and any team whose work arrives unpredictably belongs here. So does a product team that found Sprint commitments were mostly fiction.

---

## First: there are two Kanbans, and they disagree

This trips up more teams than any practice in it. Two credible bodies of work both call themselves Kanban, and they are not the same thing.

**The Kanban Method**, from David Anderson's *Kanban: Successful Evolutionary Change for Your Technology Business* (2010), maintained by [Kanban University](https://kanban.university/). It is a management method applied on top of whatever you already do, with two sets of principles, six general practices, classes of service, STATIK for designing a system, and a set of cadences. Its metrics are lead time, delivery rate and WIP.

**The Kanban Guide**, by Daniel Vacanti and John Coleman, current edition [v2025.5](https://kanbanguides.org/english/). Shorter and stricter. Three practices, one required artefact called the Definition of Workflow with six mandatory elements, four flow metrics (WIP, throughput, work item age, cycle time), and a Service Level Expectation. No classes of service, no STATIK, no prescribed cadences.

They overlap on the essentials, visualise the work and limit WIP, and diverge on nearly everything a document would capture, including what to measure and what to call it.

**These templates use the Kanban Guide's vocabulary**, for three reasons: it names the required elements of a workflow explicitly, so a document can be checked against it; its metrics are defined precisely enough to compute the same way twice; and it is short enough that a team can read the source. Where the Kanban Method supplies something the Guide does not, classes of service, STATIK and the review cadences, it is used and attributed.

Pick one vocabulary and say which. A team using "lead time" from one source and "cycle time" from the other will produce numbers that cannot be compared with anything, including its own from last quarter.

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [Definition of Workflow](definition-of-workflow.md) | Always. It is the one required artefact | Never | On the board |
| [Work item types and classes of service](work-item-types.md) | Different kinds of work need different treatment, which is nearly always | One kind of work arrives | On the board |
| [Kanban system design](kanban-system-design.md) | Designing or redesigning the system, usually via STATIK | You inherited a board that works | Wiki, then archived |
| [Flow review](flow-review.md) | You have four weeks of data and want to act on it | You have not been measuring yet | Wiki, data from the tool |
| [Blocker log](blocker-log.md) | Work stalls on things outside the team | Nothing ever blocks | On the board, tallied in the flow review |

---

## Where Kanban documents live, and why it is different here

Every other group in this repository sends documents to a repository or a wiki. Kanban is the exception, and the reason is worth understanding.

**Kanban policies belong on the board.** Not in a wiki, not in the repo. A WIP limit is read at the moment someone decides whether to start something. A pull criterion is read at the moment someone moves a card. A policy stored anywhere else is a policy consulted after the decision, which is the same as no policy.

The Kanban Method makes this concrete: policies "should be placed in a clearly noticeable area, preferably right next to the board." That is a physical claim about attention, not a filing preference.

The practical version for a digital board: WIP limits are configured as limits, not written as prose. Column entry and exit criteria go in the column description. The Definition of Workflow lives on the board's front page. Anything you have to navigate away to read will not be read.

Two things do belong elsewhere. The system design record, which explains why the board looks like this, goes in a wiki, because it is history and nobody consults it while pulling work. And the flow review's conclusions go wherever your improvement actions live.

---

## The documents, one by one

### Definition of Workflow

**When.** Always. The Kanban Guide requires it, and it is the only thing it requires.

**Why.** A board without a written workflow definition means every person has a slightly different idea of what a column means. That difference is invisible until you measure something, at which point two people report different cycle times for the same work and neither is wrong.

Six elements are mandatory:

1. What a work item is
2. When items are considered started and finished
3. The states items flow through
4. How WIP is controlled
5. Explicit policies for moving between states
6. A Service Level Expectation

Elements 2 and 6 are the ones teams skip and the ones that carry the value. Without an agreed start point, cycle time is uncomputable. Without an SLE, you have measurements and no expectation to compare them against, so nothing ever counts as a problem.

**Where.** On the board.

### Work item types and classes of service

**When.** As soon as different work needs different handling, which is almost immediately for any team taking both planned work and interruptions.

**Why.** Two separate ideas, often confused.

**Work item types** classify work by its nature: feature, defect, support request, maintenance. They exist so you can measure separately. Cycle time across all types mixed together is an average of unlike things and tells you nothing actionable.

**Classes of service** come from the Kanban Method and classify by the shape of the cost of delay. The standard four are expedite, fixed date, standard and intangible. They exist so that "this is urgent" becomes a class with a policy and a limit, rather than a negotiation with whoever asked.

That is the psychological work being done here. Urgency is otherwise decided by the persistence of the requester. Naming an expedite class, capping it at one item, and writing down what qualifies converts a social contest into a rule. It also makes the cost visible: an expedite item that pre-empts other work is a decision someone made, not a thing that happened.

Note the disagreement. The Kanban Guide does not include classes of service at all, on the reasoning that they are one way to manage flow rather than part of the definition of Kanban. If you use them, you are using the Kanban Method's addition, which is fine as long as you know it.

**Where.** On the board, as row or tag definitions with their policies attached.

### Kanban system design

**When.** Designing a system, or redesigning one that stopped fitting.

**Why.** The usual failure is copying someone else's board. Columns get inherited from a template, then work sits in "In Review" for four days because nobody defined what pulls it out. STATIK, the Systems Thinking Approach to Introducing Kanban, exists to prevent this by deriving the board from your actual demand.

Its six steps, from the Kanban Method: identify sources of dissatisfaction, analyse demand, analyse system capability, model the workflow, identify classes of service, design the system. Note that it starts with dissatisfaction. The method is deliberate about this: an improvement effort with no felt problem has no motive force, and boards installed without one become tracking overhead.

The source is explicit that STATIK is iterative, not a one-pass sequence, and that it "should not be done in isolation" by a manager, coach or consultant. A system design derived without the people doing the work will describe a workflow that does not exist.

**Where.** A wiki. It is the reasoning behind the board, consulted when changing it, not while working.

### Flow review

**When.** Once you have four or more weeks of data. Monthly or biweekly after that.

**Why.** Kanban has no Sprint boundary, so nothing forces a team to look up. The flow review is that forcing function.

The four metrics are chosen to answer different questions, and only one of them is a leading indicator:

| Metric | Question | Lagging or leading |
|---|---|---|
| Work in progress | How much have we started and not finished? | Current |
| Cycle time | How long did finished items take? | Lagging |
| Throughput | How many items finish per period? | Lagging |
| **Work item age** | **How long has each unfinished item been going?** | **Leading** |

**Work item age is the metric that changes behaviour today.** Cycle time tells you about work that is already gone. Age tells you which item on the board right now is about to breach your Service Level Expectation, while you can still do something. Teams that review only cycle time are conducting a post-mortem every month; teams that watch age are managing.

The other reason to review flow rather than velocity: these metrics measure the system, not the people. Nothing here can be attributed to an individual, which is what makes it safe to look at honestly. The moment a flow metric becomes a personal target, it stops measuring and starts being managed.

**Where.** The numbers come from your tool, so do not retype them. The document holds what you decided.

### Blocker log

**When.** Work stalls on things outside the team's control, which for platform and support teams is constant.

**Why.** A blocked item is visible on the board today and forgotten next month. The log makes blockers countable, and counting is what turns "we're always waiting on the security review" from a complaint into a case with numbers attached.

This is the highest-leverage document in the group for teams whose problems are organisational rather than technical. Most flow problems in large companies are queueing at boundaries, and a boundary you can measure is a boundary you can argue about.

**Where.** Marked on the board while blocked, tallied into the flow review afterwards.

---

## Why WIP limits work, since someone will ask

Two mechanisms, one arithmetic and one psychological.

The arithmetic is Little's Law: for a stable system, average cycle time equals average work in progress divided by average throughput. Reduce WIP without reducing throughput and cycle time falls, proportionally. This is not an empirical claim about software, it is a queueing result, and it is why limiting WIP is the one Kanban practice that is not negotiable.

The psychological mechanism is that starting work feels free and finishing work does not. Nothing in an ordinary workflow makes the cost of a new start visible, so people start things, and each started item adds context-switching cost to everything else. A WIP limit makes starting cost something: to start, you must first finish, or explicitly break the limit in front of everyone. The Kanban Method's phrasing of the underlying trade-off is exact: effective systems "focus more on flow of work and less on worker utilization", because "when resources are fully utilized there is no slack in the system and the result is very poor flow."

Expect the limit to feel wrong for two weeks. That feeling is the problem becoming visible, which is what you wanted.

---

## What to write first

1. **Definition of Workflow.** One page on the board. Without it nothing you measure means anything.
2. **Work item types**, so your metrics separate unlike work.
3. **Flow review**, once four weeks of data exist.
4. The rest when you feel the absence.

---

## Sources

- Anderson, *Kanban: Successful Evolutionary Change for Your Technology Business*, Blue Hole Press, 2010
- Kanban University, [The Official Guide to the Kanban Method](https://kanban.university/kanban-guide/), 2022. Source of the six general practices, both sets of principles, STATIK, classes of service and the cadences quoted above
- Vacanti and Coleman, [The Kanban Guide](https://kanbanguides.org/english/), v2025.5, May 2025. Source of the three practices, the Definition of Workflow, the four flow metrics and the Service Level Expectation
- Vacanti, *Actionable Agile Metrics for Predictability*, 2015, on flow metrics and their misuse
- Little, [A Proof for the Queuing Formula L = λW](https://doi.org/10.1287/opre.9.3.383), *Operations Research* 9(3), 1961

Kanban University is the commercial home of the Kanban Method and its guide is promotional as well as descriptive; the Kanban Guide is released under Creative Commons and is the more neutral of the two. Both are stated positions rather than research findings. Little's Law is the only mathematically established claim on this page.
