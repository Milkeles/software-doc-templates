# Shape Up

Documents for teams that fix time and vary scope, shape work before betting on it, and give a team six uninterrupted weeks to ship.

From Ryan Singer's *Shape Up: Stop Running in Circles and Ship Work that Matters* (Basecamp, 2019), free in full at [basecamp.com/shapeup](https://basecamp.com/shapeup).

---

## Shape Up barely uses documents, and that is the point

Most methods add artefacts. Shape Up removes them. The book prescribes exactly two written things: the **pitch**, which gets a chapter of its own, and the **kick-off message**, which gets a paragraph. Everything else people call a Shape Up document is tooling state: to-do lists, dots on a chart.

So this group is small, and two of its four templates come with a warning attached. That is deliberate. Padding it out would misrepresent the method.

**What is not in the book, so you do not attribute it to Singer:**

| Commonly claimed | Reality |
|---|---|
| A cycle retrospective | The words *retrospective*, *retro*, *lessons learned* and *post-mortem* appear nowhere in the book |
| Framing as a phase | Singer added it in 2025 and says so: "We didn't have a word for it when I wrote the book" |
| "A pitch is not a specification" | A fair reading, but he never writes it. Do not quote it |
| Projects that overrun are always cancelled | Cancellation is the default. Chapter 14 allows extension under two specific conditions |
| Teams keep no lists at all | Decentralised lists are explicitly endorsed. Only the central prioritised queue is rejected |

---

## The three ideas everything else follows from

### Appetite replaces estimation

This is the inversion, and Singer's sentence is exact:

> "An appetite is completely different from an estimate. Estimates start with a design and end with a number. Appetites start with a number and end with a design. We use the appetite as a creative constraint on the design process."

An estimate is a prediction you produce after designing. An appetite is a budget you set before designing, which then constrains what you are allowed to design. The question stops being "how long will this take" and becomes "what is worth building if we only care enough to spend two weeks."

The justification is that "good" has no absolute meaning:

> "There's no absolute definition of 'the best' solution. The best is relative to your constraints. Without a time limit, there's always a better version."

Two standard appetites: **small batch**, one or two weeks, several batched into a cycle, and **big batch**, a full six weeks. Do not over-harden this. The betting table negotiates appetites in chapter 9, and the appendix tells small teams their bets "might be different sizes each time: maybe two weeks here, three weeks there."

### Shaped work is rough, solved and bounded

Singer's three properties, in his order:

**Rough.** Unfinished on purpose, so the team can see where their judgement goes. "Work that's too fine, too early commits everyone to the wrong details."

**Solved.** "All the main elements of the solution are there at the macro level and they connect together. The work isn't specified down to individual tasks, but the overall solution is spelled out."

**Bounded.** It says what not to do, and where to stop.

The failure modes sit either side. Too abstract and a programmer told Singer: "You're solving a problem with no context. You have to be a mind reader." Too concrete and you get the opposite problem, in the words of a design lead he quotes: "I know you're looking at this, but that's not what I want you to design. I want you to re-think it!"

His argument against high-fidelity mockups is not aesthetic, it is about estimation:

> "Counterintuitive as it may seem, the more specific the work is, the harder it can be to estimate. That's because making the interface *just so* can require solving hidden complexities and implementation details that weren't visible in the mockup."

### The circuit breaker

Teams get uninterrupted time, and in exchange the deadline is real:

> "Teams have to ship the work within the amount of time that we bet. If they don't finish, by default the project doesn't get an extension. We intentionally create a risk that the project, as pitched, won't happen."

Three reasons he gives. It caps the downside, so no single project can overload the system. A miss is diagnostic: "if a project doesn't finish in the six weeks, it means we did something wrong in the shaping," which sends the work back to shaping rather than into more building. And it forces ownership, because "you can't ship without making hard decisions about where to stop."

**The rule has an exception, and summaries drop it.** Chapter 14 permits extending a project when both tests pass: every outstanding item is a genuine must-have that survived hammering, and all remaining work is downhill with no open questions. Uphill work at the end of a cycle means the shaping was wrong, and no amount of extra time fixes that. The two-week cool-down absorbs small overruns, but Singer adds that habitual overrun "points back to a problem in the shaping process or a performance problem with the team."

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [Pitch](pitch.md) | Always. The one artefact the book specifies in full | Never, if you are doing Shape Up at all | Wiki or doc tool, frozen after the bet |
| [Kick-off message](kick-off-message.md) | Every cycle, when the bets are placed | Never | Wherever the team talks, linked to the pitch |
| [Scope map](scope-map.md) | End of week one, once scopes are discovered | Before the cycle starts. Writing it early is planning, which is the thing it is not | Your tracker, as list names |
| [Cool-down guide](cool-down-guide.md) | Once, as a team agreement | You have no cool-down, in which case fix that first | Wiki |

**The hill chart is not on this list**, and that is a considered call. Its entire argued value is comparison over time: seeing that a dot has not moved in three days. That requires stored, timestamped, low-friction updates. A Markdown file is a snapshot pretending to be a time series. Use a tool with history, and see the section below on tooling.

---

## The documents, one by one

### Pitch

**When.** For any work you want considered at the betting table.

**Why.** The pitch is where shaping output becomes a decision someone can make. Five ingredients, in Singer's order and wording:

| Ingredient | What it holds |
|---|---|
| **Problem** | "The raw idea, a use case, or something we've seen that motivates us to work on this" |
| **Appetite** | "How much time we want to spend and how that constrains the solution" |
| **Solution** | "The core elements we came up with, presented in a form that's easy for people to immediately understand" |
| **Rabbit holes** | "Details about the solution worth calling out to avoid problems" |
| **No-gos** | "Anything specifically excluded from the concept" |

Problem and solution must arrive together, and Singer is firm in both directions. Solution first: "Diving straight into 'what to build' is dangerous. You don't establish any basis for discussing whether this solution is good or bad without a problem." Problem alone: "A problem without a solution is unshaped work. Giving it to a team means pushing research and exploration down to the wrong level."

**The rabbit holes ingredient is misunderstood most often.** It is not a list of risks you are flagging for the team. It is a record of holes you already patched during shaping, sometimes by dictating a solution:

> "It's not responsible to give the team a tangled knot of interdependencies and then ask them to untangle it within a short fixed time window."

That is also why the pitch is circulated asynchronously and commented on before the betting table: "Not to say yes or no, that happens at the betting table, but to poke holes or contribute missing information."

**Where.** A wiki or document tool. It contains sketches, it is read by non-engineers, and it is frozen once the bet is made. Nothing about it versions with code.

### Kick-off message

**When.** Once per cycle, when the bets are placed.

**Why.** It is the only other thing the book asks you to write, and it does a job nothing else does: it tells a team the cycle has started, what they are on, and that nothing else is coming.

The pitch gets reused here. Singer: "If the project gets chosen, the pitch can be re-used at kick-off to explain the project to the team."

This template adds one section the book does not have: what was passed on. That is an addition, labelled as one in the template. The reasoning is that "no backlog" only works if people can see their idea was considered, and a bare list of winners looks identical to a list of ideas nobody read.

**Where.** Wherever the team communicates. Link it to the frozen pitch rather than copying it.

### Scope map

**When.** End of week one or start of week two. Not before.

**Why.** Scopes are the parts of a project that can be finished independently, sized at a few days or less. They are not a work breakdown, and the difference is the entire point:

> "Scope mapping isn't planning. You need to walk the territory before you can draw the map."

Scopes come from real interdependencies, which you cannot see until you are in the work. Singer expects them to be wrong at first: "at the start of a project, we don't expect to see accurate scopes." Instability in week one is the process working.

The reason to write them down is language. "Scopes become the language of the project at the macro level," which is what lets a team discuss progress without enumerating tasks. And they are where scope hammering happens, through one concrete act: marking a task with a tilde makes it a nice-to-have. "The act of marking them as a nice-to-have is the scope hammering."

**Where.** Your tracker, as list names. The template is a scaffold for the conversation, not a document to maintain.

### Cool-down guide

**When.** Once, as a team agreement.

**Why.** Cool-down is two weeks after each cycle with no scheduled work, where people fix bugs, explore, and hold the betting table. It exists because "the end of a cycle is the worst time to meet and plan because everybody is too busy finishing projects."

It needs a written agreement for one reason: it is the first thing that gets eaten. Practitioner accounts converge on this, and one team that abandoned Shape Up described exactly the decay: "We started treating it as a parking lot for everything that wasn't a main project." Cool-down with no protection is just an unplanned sprint with lower morale.

**This template is partly an addition, and the README says so rather than hiding it.** Singer prescribes no meeting, no record and no retrospective for cool-down. The template covers what the book does define, and offers an optional shaping review, clearly labelled as not part of the method. The grounds for offering it are Singer's own: a project that misses its cycle "means we did something wrong in the shaping," and a claim like that with no venue to examine it is a diagnosis nobody makes.

**Where.** A wiki. It is an agreement about how you work.

---

## Two things about the betting table

**It is not a prioritisation meeting.** Singer frames it as the opposite: a place "to exercise control over the direction of the product instead of a battle for resources or a plea for prioritization." Attendees at Basecamp are the CEO, CTO, a senior programmer and a product strategist, it lasts an hour or two, and everyone has read the pitches beforehand. There is no second meeting to approve the outcome.

Five questions decide each bet: does the problem matter, is the appetite right, is the solution attractive, is this the right time, are the right people available.

**"No backlog" does not mean no lists.** This is the most misquoted idea in the book. Singer rejects the central prioritised queue, on two grounds: it creates a permanent feeling of being behind, and "the time spent constantly reviewing, grooming and organizing old ideas prevents everyone from moving forward on the timely projects that really matter right now."

But he explicitly endorses decentralised lists:

> "Support can keep a list of requests or issues that come up more often than others. Product tracks ideas they hope to be able to shape in a future cycle. Programmers maintain a list of bugs they'd like to fix when they have some time. There's no one backlog or central list and none of these lists are direct inputs to the betting process."

The claim is narrow and defensible: no single queue feeds scheduling. Anyone telling you Shape Up forbids writing things down is describing a method Singer did not write.

The load-bearing assumption underneath is: "Really important ideas will come back to you." That is an empirical claim about your organisation, and it is worth checking against yours before you delete anything.

---

## Six weeks, and the tooling assumption

**Why six.** Two weeks is rejected as "too short to get anything meaningful done" and "extremely costly due to the planning overhead." Longer is rejected because the deadline stops being felt: "If the deadline is too distant and abstract at the start, teams will naturally wander and use time inefficiently until the deadline starts to get closer and feel real."

The evidence is experiential. "After years of experimentation we arrived at six weeks," from one company, with no published comparison. Singer relativises it himself in the appendix: "Six weeks might not be the exact time frame for your team."

**On tooling.** Every chapter of the book ends with an advertisement for Basecamp, the pitch is a Basecamp Message, scopes are Basecamp to-do lists, and the hill chart is "a feature exclusive to Basecamp." An appendix is a product tutorial.

That does not make the advice wrong, but it means you should read the requirement rather than the product. The hill chart genuinely needs stored update history and a single place that designers, programmers, QA and managers all read, whoever sells it. A spreadsheet with dated rows meets that requirement. A Markdown file in a repository does not, and no amount of discipline will fix that, because the value is in comparing today's position to last Tuesday's.

---

## Where this breaks, including according to its author

Shape Up is documented practice from one company of roughly fifty people, published by that company. There is no independent controlled evaluation of it. The academic footprint is a handful of student theses and one peer-reviewed conference paper where it appears as a case rather than as the subject. That is an absence of evidence rather than evidence against, but do not repeat claims that it is proven.

**Singer's own limits, from the book.** The scope of the whole method, stated in chapter 1:

> "At every step of the process we target a specific risk: the risk of not shipping on time. This book isn't about the risk of building the wrong thing."

Shape Up is a delivery method, not a discovery method, by its author's explicit statement. If your problem is that you keep building things nobody wants, this is not the fix.

The appendix separates "basic truths" from "specific practices" and calls the practices scale-dependent. For a team of two or three, it says to throw out most of the structure: no six-week cycles, no cool-down, no formal pitches, no betting table.

**The precondition most adopters do not have.** Basecamp ran a separate team for security, infrastructure and performance, an operations team, and technically skilled support staff. Singer's summary: "All this means that we don't need to interrupt the designers and programmers on our Core Product team." Six uninterrupted weeks is not a policy you can declare. It is something an organisational structure buys you, and if nothing absorbs the interruptions, the cycle absorbs them.

**Singer's own carve-outs, from a 2021 post.** He excludes two categories by name and recommends the opposite approach for both. On reactive work: "Reactive work is too small to put into a pitch. And there's too much urgency to wait six weeks for a future cycle." His recommendation is blunt: "A regularly prioritized backlog + kanban setup is much closer to the right approach than pitches and cycles." On work depending on another party: "No matter what agreements you make, at the end of the day, their schedule isn't yours."

So if your team is on-call, interrupt-driven, or gated by an external party, the author of Shape Up is telling you to use [`kanban/`](../kanban/) for that work. Many teams need both, split by work type rather than by team.

**Published criticism worth knowing.** Two accounts are specific enough to be useful. A team that ran Shape Up for two years and reverted reported that appetite cut the wrong way for them: "when we assigned a 3-week appetite, the work naturally expanded to fill that time which may actually encourage gold-plating." That is a direct inversion of Singer's own argument, and it is worth watching for. The same account reported cool-down decay and a loss of the ability to re-prioritise mid-cycle, and concluded that their real problem was unclear product direction, which no scheduling method fixes.

A second review names small teams (not enough people for parallel shaping and building tracks), critical bugs (waiting six weeks is risky), and cross-team dependencies (no regular synchronisation points) as the recurring failure cases.

**Note that the criticism and the author converge.** Cool-down erosion, interrupt work and external dependencies are exactly what Singer addresses in his post-book writing. The method's known weak points are known to both sides, which is more than can be said for most methods.

---

## What to write first

1. **A pitch.** One, for something real, before adopting anything else. If shaping something to a fixed appetite feels impossible, that finding is worth more than a rollout plan.
2. **The cool-down agreement**, early, because cool-down is what gets taken first and it is easier to defend something written down.
3. **Kick-off messages**, once you are running cycles.
4. **Scope maps** only once a team is mid-cycle and needs the language.

---

## Sources

- Singer, [*Shape Up: Stop Running in Circles and Ship Work that Matters*](https://basecamp.com/shapeup), Basecamp, 2019. Every quotation above is from the book text
- Singer, [Shape Up is for features, not all development work](https://www.ryansinger.co/shape-up-is-for-features-not-all-development-work/), 2021. The reactive-work and external-dependency carve-outs
- Singer, [Common Pitfalls When Adopting Shape Up](https://www.ryansinger.co/pitfalls-when-adopting-shape-up/), 2025. Introduces framing as distinct from shaping, and names Basecamp's unstated precondition that everyone there was highly technical
- Hallgren, *Understanding modern project management frameworks' impact on trust in distributed teams*, Stockholm University, 2023. A master's thesis, single company, qualitative
- Wauters, [2 years with Shape-Up, and why we switched back](https://scalex.dev/blog/2-years-with-shape-up/), 2025
- Chazoule, [Shape Up: Should You Change Your Agile Methodology?](https://marmelab.com/blog/2024/09/26/shape-up.html), Marmelab, 2024

**On sourcing.** The book is the only authoritative source and it is a single company's account of its own practice, published by that company and used to sell its product. The criticism above is practitioner writing, not research. We found no peer-reviewed study evaluating Shape Up, and none evaluating fixed time with variable scope as an isolated practice. Treat everything on this page as a well-argued position rather than a measured result, which is also how its author presents it.

One thing we could not establish: whether Basecamp still runs Shape Up. The book's page is maintained, which proves the page is maintained. Do not write that they use it in the present tense.
