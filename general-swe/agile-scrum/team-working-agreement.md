# {Team} working agreement

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Agreed by** | *Everyone on the team, by name. An agreement written by one person is a policy.* |
| **Agreed on** | YYYY-MM-DD |
| **Next review** | *A date, not "as needed".* |

*How this team works together, written down so it can be argued with. Google's Project Aristotle found that how a team works together predicts effectiveness better than who is on it, and most of the "how" in any team is unwritten, inconsistently understood, and impossible to challenge.*

**Every line must be checkable.** *"We respect each other" changes no behaviour and cannot be broken. "We do not merge after 15:00 on Friday" can be. If someone could not tell whether the team followed a line yesterday, cut it or sharpen it.*

---

## Hours and availability

*When people are reachable, in which timezones, and what response time is expected on what channel.*

*The most common source of quiet friction on distributed teams, and the cheapest to fix. Say what is genuinely expected rather than what sounds accommodating.*

- *Core overlap: 10:00 to 15:00 CET*
- *Chat: same day. Mentions: within four hours during core overlap. Nothing is expected outside your working hours.*
- *We do not expect replies at weekends. If it is urgent, use the on-call path.*

---

## Meetings

*Which meetings this team holds, what each is for, and the rules that make them tolerable.*

- *Meeting, purpose, length, who must attend*
- *Declining a meeting with no agenda is fine and needs no explanation*
- *Cameras: state the actual expectation rather than leaving people to guess*
- *No-meeting blocks*

---

## How we work

*Concrete practices. Everything here should be visible in the repository or the tracker.*

- *Pairing: when we do it and when we do not*
- *Branching and pull request conventions, linking the [code review guidelines](../foundations/code-review-guidelines.md)*
- *Review response: within one working day*
- *A red build stops new merges, and whoever broke it fixes it or reverts within 20 minutes*
- *Nobody picks up a second item while a review of theirs is waiting*

---

## Being stuck

*How long before you ask for help, and how to ask.*

*Worth writing explicitly. New joiners consistently overestimate how long they should struggle alone, and everyone underestimates how much it costs.*

- *Stuck for more than 45 minutes: post in the team channel. This is expected, not a failure.*
- *Asking is never criticised here. Silently losing a day is.*

---

## Decisions and disagreement

*Who decides what, and how an argument ends.*

*Most team friction is not disagreement; it is not knowing who decides. Name it.*

- *Technical decisions inside our systems: the team, by consensus. If consensus fails after one discussion, ... decides and the reasoning is recorded in an [ADR](../foundations/architecture-decision-record.md).*
- *Product ordering: the Product Owner.*
- *Disagree and commit: once decided, we do not relitigate it in private.*
- *Disagreement lasting more than two rounds of comments moves to a call.*

---

## Definition of interrupt

*What may break a Sprint and what may not, agreed in advance so it is not negotiated under pressure by whoever is nearest.*

- *Production incidents interrupt anything.*
- *Anything else goes to the Product Owner, who decides against the [Sprint Goal](sprint-backlog.md).*
- *Support rotation: one person per Sprint absorbs the interruptions, so the rest are not sampled at random.*

---

## Quality

*Practices the team holds itself to that are not in the [Definition of Done](definition-of-done.md), because they are not per-item.*

- *We leave code better than we found it, within the change we are already making*
- *We do not merge with a failing test marked skipped without a ticket and a date*

---

## How we treat each other

*Keep this short and make it behavioural. Aspirational statements about respect belong on posters.*

- *We critique the work, not the person*
- *We assume competence and good intent, and ask before concluding*
- *Anyone may say "I do not understand" at any point, including in front of stakeholders*

---

## Changing this

*When and how. Any member may propose a change; the team agrees it at a retrospective.*

*Add a line when something goes wrong twice. Delete a line nobody has needed for three months. An agreement that only grows becomes a document nobody reads, which is worse than no document.*

---

## Notes on using this template

*Delete this section too.*

**The writing is the value.** Most of the benefit arrives during the conversation that produces this, when disagreements surface with nothing at stake. A working agreement handed to a team by someone else delivers none of that.

**Start with five lines.** Pick the frictions the team actually has. A twenty-point agreement written on day one is a guess, and nobody will remember it by day three.

**Review it when the team changes.** One person joining or leaving changes the norms whether or not the document changes. A new joiner reading it and asking "is this true?" is the best audit available.

**Where this lives:** the wiki, linked from the team's page and from onboarding. It is a social contract that changes without a pull request, and putting it behind code review adds friction exactly where you want none.
