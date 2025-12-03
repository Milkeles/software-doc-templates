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

## What the board actually looks like

Since the board is where most of this documentation lives, here is what a board carrying it looks like. Every feature below exists to hold one part of the Definition of Workflow.

```
   OPTIONS   |        BUILD   3        |   REVIEW  2  |     DONE
             |   doing    |   ready    |              |
  -----------+------------+------------+--------------+------------
   [  ]      |   [ A ]    |   [ C ]    |   [ D ] (!)  |   [ E ]
   [  ]      |   [ B ]    |            |              |   [ F ]
   [  ]      |            |            |              |
  -----------+------------+------------+--------------+------------
   not       | STARTED    | exit: all  | exit: one    | FINISHED
   started;  | here       | tests pass,| approval,    | merged and
   age not   |            | PR open    | all comments | deployed
   counted   |            |            | resolved     |
```

**The numbers after column names are the WIP limits.** Three in build, two in review. Options and Done are unlimited, because neither holds work in progress.

**The doing and ready split inside Build is the important bit, and it is the one most boards omit.** Without it, a finished item and an item someone is actively working on look identical. With it, the "ready" sub-column is a visible queue: cards sitting there are done and waiting for someone downstream to pull them. That queue is where your cycle time is going, and you cannot see it on a board with single columns.

**Pull happens right to left.** Nobody assigns anything. A person with free capacity looks at the rightmost column with something in it and takes from there. This is what makes the limit bite: to start something new in Build you must first move something out, and to move something out someone must have space in Review.

**The `(!)` is a blocked marker.** Card D is stopped on something outside the team. It still counts against the Review limit, which is deliberate: a blocked item is occupying a slot and the board should say so.

**The text under each column is the explicit policy**, element 5 of the Definition of Workflow. It is written on the board because it is read at the moment someone decides whether a card may move. Two words matter more than the rest: STARTED and FINISHED. Those anchor element 2, and without them cycle time cannot be computed at all.

### Swimlanes carry classes of service

```
  EXPEDITE   1 |  [ X ]     |            |              |
  -------------+------------+------------+--------------+---------
  STANDARD     |  [ A ]     |  [ C ]     |  [ D ] (!)   |  [ E ]
               |  [ B ]     |            |              |  [ F ]
  -------------+------------+------------+--------------+---------
  INTANGIBLE   |            |            |              |  [ G ]
```

One expedite lane, limited to one item, with a written rule for what qualifies. That single row does more organisational work than any policy document: it converts "this is urgent" from a negotiation with whoever asked loudest into a rule with a cap on it. When the lane is full, the next urgent request has to displace the current one, and someone has to say so out loud.

### What goes on the card face

The board is read at a glance, so the card face is scarce space. Put on it only what changes a decision:

| On the face | Why |
|---|---|
| Title, in the language of the requester | So the person who asked can find it |
| Work item type, as a colour or tag | Because you measure types separately |
| Start date, or the age in days | The one number that tells you to act today |
| Blocked marker, and what on | Blocked items must be visible without opening them |
| Who is on it | Only if it is more than one person, otherwise it is noise |

Leave off estimates. Kanban forecasts from throughput and cycle time history, so a points field on the card is a habit carried over from a different method that adds an estimation meeting you no longer need.

### Definition of Done, and where it goes in Kanban

Teams arriving from Scrum look for the single Definition of Done and do not find one. That is not an omission.

Kanban splits it in two, and both halves are in the board diagram above.

**Per-transition exit criteria** are the working half. "All tests pass, PR open" is the exit criterion for the doing sub-column. Each one is small, checked constantly, and lives under the column it governs. A single global checklist read at the end of a two week Sprint is checked once, late, when the cost of failing it is highest.

**One definition of finished** is the other half, and it anchors the measurement. It is a single sentence saying what the last column means, and it is the thing your cycle time is measured to. "Merged and deployed to production" and "merged" are different sentences that produce different numbers from the same work.

If you want the Scrum-style single Definition of Done as well, keep it, but keep it as the definition of finished. Do not maintain both a global checklist and per-column criteria: they will disagree within a month, and everyone will follow the one printed on the board.

---

## Setting this up in Jira or Trello

Most of the boards in the world are in one of these two, and neither does everything the method assumes. Here is what each can actually hold, so you know which parts have to live elsewhere.

| Definition of Workflow element | Jira | Trello |
|---|---|---|
| 1. What a work item is | Issue types | Board scope, by convention only |
| 2. Started and finished points | Which columns count; must be written down separately | Convention only |
| 3. States | Columns, several statuses can map to one | Lists |
| 4. How WIP is controlled | Column constraints, per column | Power-Up only, not native |
| 5. Explicit policies | Not on the board face | Not on the board face |
| 6. Service Level Expectation | Nowhere native | Nowhere native |

**Jira.** WIP limits are under Board, Configure, Columns. Set the constraint type to "Issue count" or "Issue count, excluding subtasks", then set a minimum and maximum per column. The column header turns red when the maximum is exceeded and yellow when the minimum is not met.

The thing to know before relying on it: **Jira does not enforce the limit.** It is a visual indicator, and no configuration will stop someone dragging a card into a full column. That is not necessarily wrong, since a limit you can break in public is closer to the intent than one you cannot break at all, but it means the limit is a social agreement with a colour attached. Treat the red header as the prompt for a conversation, not as a control.

Two more limitations worth knowing up front. Swimlanes do not carry their own WIP limits, so an expedite lane capped at one has to be enforced by people rather than by the tool. And there is no place on the board face for column policy text, so the usual workaround is a pinned card at the top of each column holding the policy, which is uglier than it should be and still better than a wiki page.

On metrics, Jira gives you a control chart and a cumulative flow diagram natively. Read the control chart's configuration carefully: its cycle time is whatever set of statuses you selected, so two teams in the same company will report numbers that cannot be compared. Fix the selection to match your written started and finished points and record what you chose. Work item age, the one leading indicator, is the gap: Jira has an average age report, but a per-item aging chart of the kind that tells you which card to worry about today needs a Marketplace app.

**Trello.** There are no native WIP limits. You need a Power-Up, of which List Limits is the common free one, and it highlights a list when the count exceeds the number you set. Automation can approximate policies, but it enforces nothing about pulling.

Trello has no native flow metrics at all. If you are on Trello and serious about measurement, plan on exporting or on a Power-Up, and decide that before you have six months of data you cannot analyse.

**The honest summary.** Both tools hold elements 3 and 4 and nothing else. Elements 1, 2, 5 and 6 need somewhere to live, and the only placement that survives contact with a working day is on the board face itself, as a pinned card, a column description where the tool has one, or a printed sheet next to a physical board. This is the single most common reason a team has a Definition of Workflow and does not follow it.

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

## Why these practices work, and how good the evidence is

Kanban's mechanics look arbitrary until you see what each is doing to the people using it. The reasoning below is why the documents in this group are worth keeping. It is also graded, because the four arguments are not equally well supported and pretending otherwise would be the same mistake the templates warn against.

### WIP limits: one proof and one behavioural argument

**The arithmetic is settled.** Little's Law: for a stable system, average cycle time equals average work in progress divided by average throughput. Reduce WIP without reducing throughput and cycle time falls, proportionally. This is a queueing result, not an empirical claim about software, which is why limiting WIP is the one Kanban practice that is not negotiable.

**The behavioural argument is that starting feels free and finishing does not.** Nothing in an ordinary workflow makes a new start cost anything, so people start things. A WIP limit is the only mechanism that prices it: to start, you must first finish, or break the limit where everyone can see. The Kanban Method's phrasing of the underlying trade-off is exact: effective systems "focus more on flow of work and less on worker utilization", because "when resources are fully utilized there is no slack in the system and the result is very poor flow."

**What high WIP actually costs is not what most people claim.** The intuitive story is that switching between items makes you slower. The best field evidence says something more uncomfortable. Mark, Gudith and Klocke measured interrupted against uninterrupted work and found interrupted tasks were completed *faster*, with no drop in quality, and that people paid for it in stress, frustration, time pressure and effort.

Read that carefully before using it. It does not say interruption is free. It says people absorb the cost personally instead of the work absorbing it, which is exactly why the cost is invisible on a delivery report and shows up in retention. If you argue for WIP limits on the grounds that they make delivery faster, someone will measure and contradict you. Argue instead that they stop the team paying for throughput out of its own capacity, which is what the evidence supports.

**One popular argument you should not use.** The Zeigarnik effect, that unfinished tasks stay in your head and nag at you, is the standard justification for limiting WIP, and it does not hold up. A 2025 meta-analysis of the Zeigarnik and Ovsiankina effects found no memory advantage for unfinished tasks and concluded that the Zeigarnik effect "lacks universal validity." What did survive is the related Ovsiankina effect, a general tendency to resume interrupted tasks. Drop the memory claim. The stress finding above is better sourced and makes the same point.

Expect a new limit to feel wrong for a fortnight. That feeling is the queue becoming visible, which is what you wanted.

### Pull instead of push, and why it changes motivation

Push means work is assigned to you. Pull means you take the next item when you have capacity. Mechanically the difference is small. In terms of what it does to people it is the largest single difference between a Kanban board and a task list.

The grounding is self-determination theory, which holds that intrinsic motivation depends on three needs: autonomy, competence and relatedness. Its application to work is well studied, and the workplace literature consistently finds that people whose autonomy is supported show higher engagement and lower burnout.

**Be honest about the size of the step being taken here.** SDT's workplace evidence concerns meaningful input into how work is done. Extending it to "choosing which card to pull next" is a plausible extrapolation, not a demonstrated finding, and nobody has tested it on kanban teams specifically. State it that way rather than dressing an argument about board mechanics in psychology it has not earned.

What is not an extrapolation is the second-order effect, which is visible on any board that runs this way. Under push, the interesting work is allocated, and allocation is a relationship with your manager. Under pull, it is available, and taking it is a decision you make. The same work arrives either way. Only one version makes the person a participant in what they do next.

### Why limits produce collaboration without anyone asking for it

This is the effect people notice first and expect least.

When the limit is reached, a person who finishes something cannot start anything new. Their only useful move is to help finish something already in flight. So they pick up a review, pair on the blocked item, or take the piece of someone else's work that is queueing. Swarming happens because the alternative is doing nothing, not because anyone ran a workshop on collaboration.

The same constraint spreads knowledge as a side effect. If you cannot start a new thing, you end up inside work you did not begin, which is the cheapest cross-training any team gets.

Treat this as a practitioner argument rather than a research finding. The mechanism is easy to state and I found no study testing it. It is included because it is the most common reason teams report that a limit they resisted turned out to be worth keeping, and because it explains something the arithmetic does not.

### Visualisation, and one strong caution about it

A board makes work visible, and visible work is discussable. The board is a shared object several people can point at, which is why standing in front of one produces different conversations than reading the same information in a list.

The caution is sharper than the benefit. **Visible work is measurable work, and measurable work invites targets.** Robert Austin's analysis of measurement dysfunction is the right frame: measurement systems work only if you can measure everything a person should be doing, which is essentially never, and under partial measurement people rationally optimise the measured dimension at the expense of the unmeasured ones. The behaviour is not cheating. It is the predictable response to being partially measured.

That is why the flow review measures the system and not the person, and why nothing in these four metrics can be attributed to an individual. Cycle time per developer is the exact failure Austin describes, and the first thing it will produce is smaller tickets rather than faster delivery.

The rule that follows: put the work on the board, keep the people off the report.

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

On the reasoning behind the practices:

- Mark, Gudith and Klocke, [The Cost of Interrupted Work: More Speed and Stress](https://doi.org/10.1145/1357054.1357072), CHI 2008. Interrupted work finished faster, at a cost in stress and effort
- Bornemann, Foroughi and Hüffmeier, [Interruption, recall and resumption: a meta-analysis of the Zeigarnik and Ovsiankina effects](https://doi.org/10.1057/s41599-025-05000-w), *Humanities and Social Sciences Communications* 12, 2025. Why the Zeigarnik argument for limiting WIP does not hold
- Ryan and Deci, "Self-determination theory and the facilitation of intrinsic motivation, social development, and well-being," *American Psychologist* 55(1), 2000, and Deci, Olafsen and Ryan, ["Self-Determination Theory in Work Organizations: The State of a Science"](https://doi.org/10.1146/annurev-orgpsych-032516-113108), *Annual Review of Organizational Psychology and Organizational Behavior* 4, 2017
- Austin, *Measuring and Managing Performance in Organizations*, Dorset House, 1996. Measurement dysfunction under partial measurement
- Atlassian, [Configure columns](https://support.atlassian.com/jira-software-cloud/docs/configure-columns/) and [View and understand the control chart](https://support.atlassian.com/jira-software-cloud/docs/view-and-understand-the-control-chart/). Jira column constraints and metric definitions

**On sourcing.** Kanban University is the commercial home of the Kanban Method and its guide is promotional as well as descriptive; the Kanban Guide is released under Creative Commons and is the more neutral of the two. Both are stated positions rather than research findings. Little's Law is the only mathematically established claim on this page.

The psychology is graded deliberately. Mark's interruption finding and Austin's dysfunction argument are solid and directly on point. The self-determination link to pulling a card is an extrapolation from workplace autonomy research and is labelled as one. The claim that WIP limits produce collaboration is a practitioner argument with no study behind it. And the Zeigarnik effect, which is the most commonly cited justification for limiting WIP, is on this page only so you know not to use it.

Tool behaviour changes. The Jira and Trello details were checked against current documentation, but Atlassian renames and moves features regularly, so verify before quoting any of it in an argument.
