# Scrum

Documents for teams working in Sprints with a Product Owner, a Scrum Master and Developers.

Start with one fact that decides how you should read everything below: **Scrum requires no documents.** The 2020 Scrum Guide never uses the word "documentation". It defines three artifacts, and an artifact is a thing the team maintains, not a page it writes. Everything in this folder is either one of those three artifacts given a usable shape, or a practice that grew up around Scrum and is not part of it.

That distinction matters because most Scrum paperwork is inherited rather than chosen. Knowing which parts are the framework and which are convention tells you what you are free to drop.

---

## What Scrum actually defines

Three artifacts, each with a commitment attached:

| Artifact | Commitment | What the commitment is for |
|---|---|---|
| Product Backlog | Product Goal | Gives the backlog a direction, so ordering has a criterion |
| Sprint Backlog | Sprint Goal | Gives the Sprint one objective, so scope can flex without the Sprint failing |
| Increment | Definition of Done | Gives "finished" a fixed meaning, so progress is real |

Five events: the Sprint, Sprint Planning, the Daily Scrum, the Sprint Review, the Sprint Retrospective.

Notably absent from the Guide: user stories, story points, velocity, epics, acceptance criteria, and the Definition of Ready. Those words appear zero times in both the 2017 and 2020 editions. They may still be good ideas. They are not Scrum, and treating them as mandatory is how teams end up defending practices nobody chose.

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [Definition of Done](definition-of-done.md) | Always. It is a Scrum commitment, and without it "done" is negotiable | Never | Repo |
| [Product Goal](product-goal.md) | Always. Also a Scrum commitment | Never | Tracker or wiki, at the top of the backlog |
| [Sprint Backlog](sprint-backlog.md) | Every Sprint. Holds the Sprint Goal | Never | Tracker |
| [Product Backlog item](product-backlog-item.md) | Items need consistent shape across a team larger than about five | Two people who talk all day | Tracker |
| [Sprint Review notes](sprint-review-notes.md) | Stakeholders who cannot attend need the outcome, or decisions need a record | Everyone who matters was in the room and nothing was decided | Wiki |
| [Sprint Retrospective](sprint-retrospective.md) | Every Sprint. The event is mandatory; recording it is not, but the actions are | Never for the event. Skip the write-up if actions go straight to the tracker | Wiki, actions in the tracker |
| [Team working agreement](team-working-agreement.md) | The team is new, has changed, or keeps relitigating the same friction | Norms are stable and nobody is confused | Wiki |

Two of these, the Definition of Done and the Product Goal, are framework commitments. The rest are conveniences. Drop any of them the moment it stops changing a decision.

---

## The documents, one by one

### Definition of Done

**When.** From the first Sprint. It is not optional: the Guide makes it the Increment's commitment.

**Why.** Without a fixed meaning of finished, every progress signal is a guess. The Guide is blunt about the consequence: an item that does not meet the Definition of Done "cannot be released or even presented at the Sprint Review. Instead, it returns to the Product Backlog for future consideration." That is the mechanism. The Definition of Done converts "nearly done" from a status into a non-status, which is the only reliable defence against work that is 90 percent complete for three Sprints.

The psychological function is worth naming. Progress is over-reported almost everywhere, not from dishonesty but because people report on the part they can see. An externally fixed completion standard removes the judgement call from the person least able to make it objectively.

**Ownership.** The Guide sets a specific rule: if the organisation has a standard, every team "must follow it as a minimum" and may add to it. If not, the team writes its own. Teams working on the same product must share one.

**The evidence, including the bad news.** Kopczyńska, Piechowiak, Ochodek and Nawrocki surveyed 137 practitioners ([Journal of Systems and Software, 2022](https://doi.org/10.1016/j.jss.2022.111479)): 93 percent found the Definition of Done at least valuable, and "every second project struggles with infeasible, incorrect, unavailable, or creeping" definitions. The two most common problems were both about verification. Over 70 percent of projects found items hard or slow to verify, and over 60 percent had items that were impossible to verify at all. That is the single most useful finding for anyone writing one: **an item you cannot check is not a criterion, it is a sentiment**, and it is the most likely thing to go wrong.

**Where.** In the repository. Most of a good Definition of Done is enforced by CI, and the two must change together.

### Product Goal

**When.** Always, as the Guide's commitment for the Product Backlog. Written and communicated by the Product Owner.

**Why.** A backlog without a goal can be ordered by anything: loudest stakeholder, easiest item, oldest ticket. The Product Goal supplies the criterion that makes ordering an argument about evidence rather than about status. The Guide adds a constraint that gives it teeth: a team "must fulfill (or abandon) one objective before taking on the next." One goal at a time is the whole point, and a list of five parallel goals is a backlog with extra formatting.

**Where.** At the top of the backlog in your tracker, visible whenever anyone orders anything. Duplicating it into a wiki page nobody opens defeats it.

### Sprint Backlog and the Sprint Goal

**When.** Every Sprint, produced in Sprint Planning.

**Why.** The Guide defines the Sprint Backlog as three things: "the Sprint Goal (why), the set of Product Backlog items selected for the Sprint (what), as well as an actionable plan for delivering the Increment (how)." Most teams produce the second and skip the first, which costs them the mechanism that makes Scrum tolerate uncertainty.

Here is that mechanism, stated in the Guide: if the work turns out to be different from expected, Developers "collaborate with the Product Owner to negotiate the scope of the Sprint Backlog within the Sprint without affecting the Sprint Goal." The Goal is fixed; the item list is not. A team whose Sprint Goal is a summary of its selected items has nothing left to negotiate, so every surprise becomes a failed Sprint. That is the most common and most expensive Scrum mistake, and it is a documentation mistake.

**On task breakdown.** The Guide does not require it. Topic Three says decomposition into items of a day or less is what teams "often" do, and then that "how this is done is at the sole discretion of the Developers." The word "task" does not appear in the 2020 Guide. If your tooling forces a task breakdown, that is your tooling's opinion.

**Where.** The tracker. It changes daily and belongs to the Developers, who are the only people who should be updating it.

### Product Backlog item

**When.** Once the team is large enough that items are written by one person and picked up by another. Below that, conversation outperforms format.

**Why.** The value of a consistent item shape is that it makes missing information visible. The familiar "As a role, I want a capability, so that a benefit" form came from the XP team at Connextra in 2001, is usually credited through Rachel Davies, who credits the team, and spread through Mike Cohn's *User Stories Applied* (2004). Its real contribution is the third clause. Teams that drop "so that" lose the only part that records why the item exists, and that is the part which decides whether to build it at all.

Two things worth keeping alongside it. Ron Jeffries' Three Cs, written in 2001, states the point most people miss: "the card does not contain all the information that makes up the requirement." The card is a token for a conversation, and the confirmation is the acceptance test. And Bill Wake's INVEST checklist (2003) gives six checks (Independent, Negotiable, Valuable, Estimable, Small, Testable) that catch the usual defects in an item before it wastes a planning session.

**The disagreement.** The template is contested and the criticism is fair. Alan Klement's job story form, "When *situation*, I want to *motivation*, so I can *expected outcome*", drops the persona on the argument that "as a user" smuggles in an assumption about who is acting and why, while the situation is the thing that actually predicts behaviour. For work with no clear user role, infrastructure, compliance, migrations, both forms are contortions and a plain sentence is better. The template is a prompt, not a grammar. The template in this folder shows all three and says when each fits.

**Where.** The tracker, because items are worked and closed there.

### Sprint Review notes

**When.** Stakeholders who could not attend need the outcome, or the session changed the plan and the change needs a record.

**Why.** The Guide is careful here and most teams miss it: "The Sprint Review is a working session and the Scrum Team should avoid limiting it to a presentation." It is timeboxed to four hours for a one-month Sprint, and the Increment section adds that it "should never be considered a gate to releasing value." So the output is not an approval. It is what the team learned from stakeholders and what changed in the backlog as a result.

Write the notes accordingly. A document listing what was demonstrated records the wrong half of the meeting. What matters is the feedback and the decisions.

Note also that Scrum has no Product Owner sign-off step. Acceptance is the Definition of Done, applied continuously. A review that functions as an approval gate has quietly reintroduced a stage gate, and the notes are usually where you can see it happening.

**Where.** The wiki, linked from the tracker. It is a dated record for an audience wider than the team.

### Sprint Retrospective

**When.** Every Sprint. The event is one of the five and is not optional. The write-up is.

**Why.** The Guide prescribes no format, so teams invent one, and the invented ones tend to collect complaints without producing change. Esther Derby and Diana Larsen's five stages, from *Agile Retrospectives: Making Good Teams Great* (2006), remain the most useful structure: set the stage, gather data, generate insights, decide what to do, close the retrospective. Each stage exists to prevent a specific failure. Gathering data before generating insights stops the loudest memory from becoming the team's history. Deciding what to do as a separate stage stops the meeting ending in agreement and nothing else.

**What makes it work or fail.** Norm Kerth's Prime Directive, from *Project Retrospectives* (2001), is the standard opening and is worth reading aloud rather than linking: "Regardless of what we discover, we understand and truly believe that everyone did the best job they could, given what they knew at the time, their skills and abilities, the resources available, and the situation at hand."

The reason it works is now reasonably well evidenced. Google's Project Aristotle, across more than 180 teams, found psychological safety the strongest of five dynamics separating effective teams from ineffective ones. Within software specifically, Alami, Zahedi and Krancher ([Empirical Software Engineering 29(5), 2024](https://doi.org/10.1007/s10664-024-10512-1)) traced how psychological safety shapes the quality behaviours a team is willing to perform. A retrospective is where a team finds out how safe it actually is. If nobody names a real problem, that is the finding.

**Where.** The wiki. Actions go to the tracker with an owner, because an action item living in meeting notes is not scheduled, and unscheduled work does not happen. This is the most common way retrospectives decay: not from bad discussion, but from good discussion with no follow-through, which teaches everyone that the meeting is theatre.

### Team working agreement

**When.** A new team, a changed team, or a team relitigating the same friction every Sprint.

**Why.** Project Aristotle's finding was that how a team works together predicts effectiveness better than who is on it. A working agreement is the cheapest way to make "how" explicit. Its value is not the document; it is that writing it forces disagreements into the open at a moment when nothing is at stake, rather than during an incident.

The failure mode is platitudes. "We respect each other" changes no behaviour and is not checkable. "We do not merge on Fridays after 15:00" does. The template pushes for the second kind.

**Where.** The wiki, revisited in a retrospective every few months. It is a living social contract, not a versioned artifact.

---

## Two arguments worth having openly

### Definition of Ready

Not in Scrum. Zero occurrences in either Guide. The disagreement runs through Scrum's own authors, which is why it is worth stating rather than resolving.

**Against:** Mike Cohn recommends against it for most teams, calling it "often unnecessary process overhead" and warning that a rule saying something must be finished before the next thing can start "moves the team dangerously close to stage-gate process." His deeper argument is concurrent engineering: an agile team should always be doing a little analysis, design, coding and testing at once, and a readiness gate breaks that.

**For:** Jeff Sutherland, co-author of the Guide, promotes it. The citable version is Jakobsen and Sutherland, [*Scrum and CMMI: Going from Good to Great*](http://jeffsutherland.com/scrum/JakobsenScrumCMMIGoingfromGoodtoGreatAgile2009.pdf), Agile 2009 Conference, reporting large productivity gains at Systematic from tightening both ready and done states. Wider claims that a Definition of Ready doubles velocity circulate without a traceable source; treat them as assertion.

**Between:** Roman Pichler finds it useful mainly for new teams, and reframes the risk: if a team routinely rejects items at Sprint Planning, the problem is the collaboration between Product Owner and Developers, not the absence of a checklist.

**What the Guide offers instead** is a sizing heuristic rather than a gate: items "that can be Done by the Scrum Team within one Sprint are deemed ready for selection." Small enough to finish, not complete enough to pass an inspection.

Our position: if you adopt one, write it as guidelines rather than entry criteria, and check after two months whether items are being rejected. Rejection rate is the measurement that tells you which of Cohn and Sutherland is right about your team.

### Story points and velocity

Also not in Scrum. The 2020 Guide removed the word "estimate" entirely in favour of "size", and assigns sizing to "the Developers who will be doing the work."

Ron Jeffries, in [Story Points Revisited](https://ronjeffries.com/articles/019-01ff/story-points/Index.html) (2019), wrote: "I like to say that I may have invented story points, and if I did, I'm sorry now." His three specific objections are that using points to predict a completion date is "at best a weak idea", that comparing actuals against estimates is "at best wasteful", and that comparing teams on velocity is "harmful". His alternative is slicing work small enough that estimation stops mattering.

The counter-position is that a coarse relative size is cheap and helps a Product Owner make trade-offs, which is true, and it is not what velocity is usually used for. The practical test: if your points feed a forecast that someone treats as a commitment, or feed a comparison between teams, they have stopped measuring and started incentivising, and the numbers will adjust to fit.

None of this belongs in a template, which is why there is no estimation document in this folder.

---

## What to write first

1. **Definition of Done.** Nothing else works without it, and it is a framework commitment.
2. **Product Goal.** One sentence, and it makes backlog ordering decidable.
3. **Team working agreement**, if the team is new.
4. Everything else when you feel its absence.

A Scrum team that maintains three artifacts and holds five events is doing Scrum. Documents beyond that are yours to justify.

---

## Sources

- [The 2020 Scrum Guide](https://scrumguides.org/scrum-guide.html), Schwaber and Sutherland, CC BY-SA 4.0. All quoted text above is from this edition. Where the 2017 edition differs, it is noted.
- Kopczyńska, Piechowiak, Ochodek and Nawrocki, [On the benefits and problems related to using Definition of Done](https://doi.org/10.1016/j.jss.2022.111479), *Journal of Systems and Software*, 2022
- Silva et al., [A systematic review on the use of Definition of Done on agile software development projects](https://dl.acm.org/doi/10.1145/3084226.3084262), EASE 2017
- Jakobsen and Sutherland, [Scrum and CMMI: Going from Good to Great](http://jeffsutherland.com/scrum/JakobsenScrumCMMIGoingfromGoodtoGreatAgile2009.pdf), Agile 2009 Conference
- Alami, Zahedi and Krancher, [The role of psychological safety in promoting software quality in agile teams](https://doi.org/10.1007/s10664-024-10512-1), *Empirical Software Engineering* 29(5), 2024
- Derby and Larsen, *Agile Retrospectives: Making Good Teams Great*, Pragmatic Bookshelf, 2006
- Kerth, *Project Retrospectives: A Handbook for Team Review*, Dorset House, 2001
- Cohn, *User Stories Applied*, Addison-Wesley, 2004; and [The Definition of Ready and Its Dangers](https://www.mountaingoatsoftware.com/blog/the-dangers-of-a-definition-of-ready)
- Jeffries, [Essential XP: Card, Conversation, Confirmation](https://ronjeffries.com/xprog/articles/expcardconversationconfirmation/) (2001) and [Story Points Revisited](https://ronjeffries.com/articles/019-01ff/story-points/Index.html) (2019)
- Wake, [INVEST in Good Stories, and SMART Tasks](https://xp123.com/invest-in-good-stories-and-smart-tasks/) (2003)
- Klement, [Replacing the User Story with the Job Story](https://jtbd.info/replacing-the-user-story-with-the-job-story-af7cdee10c27)
- Pichler, [The Definition of Ready in Scrum](https://www.romanpichler.com/blog/the-definition-of-ready/)
- Google re:Work, [Understand team effectiveness](https://rework.withgoogle.com/intl/en/guides/understand-team-effectiveness), on Project Aristotle

Mountain Goat Software, romanpichler.com and jtbd.info are consultancy or practitioner sites, flagged as such. The Scrum Guide is normative. The four papers are peer-reviewed.
