# Onboarding: {Team or system}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | |
| **Last used** | *Date and by whom. If nobody has followed this in six months, assume it is broken.* |

*Written for someone who starts on Monday and knows nothing about your systems. Assume competence, assume no context.*

*The evidence says the tasks a newcomer is given drive their learning, confidence and integration far more than what they are asked to read. So this document is organised around what they do, week by week, and reading material is attached to tasks rather than piled at the front.*

---

## Day one

*Only what is needed to be functional. Accounts, access, machine, where to be and when.*

*Keep this to a checklist and put the requests in ahead of the start date. Access delays are the single largest source of a wasted first week, and they are entirely avoidable.*

| Access | Requested by | Who grants it | Needed by |
|---|---|---|---|
| *Repository* | | | *Day 1* |
| *Cloud account, read-only* | | | *Day 1* |
| *CI, deploy pipeline* | | | *Day 3* |
| *Production, scoped* | | | *Week 2* |

**People to meet.** *Three or four names with what each does and why the new joiner will need them.*

**Your onboarding buddy.** *Name. Deliberately not the new joiner's manager: a question costs nothing to ask a peer and feels expensive to ask the person who writes your review. State that this person is there to be interrupted.*

---

## First change

*A prepared, real, small change that reaches production in the first week, with the steps to make it happen.*

*This is the most valuable section in the document, for two reasons. It converts abstract system knowledge into a concrete path a person has walked. And it tests every link in your toolchain while someone is watching, so a broken step is discovered in week one instead of month three.*

*Pick something genuinely useful and genuinely small. Keep two or three candidates ready so this does not need inventing on the day.*

1. *Set up your environment: link to the service README.*
2. *Make the change: what and where.*
3. *Get it reviewed: link to the review guidelines.*
4. *Watch it deploy: what the pipeline does and how long it takes.*
5. *Confirm it worked in production: the dashboard or query to look at.*

**When something in this list does not work, fix the document.** *Say this explicitly and treat the fix as part of the task. The new joiner is the only person who can still see the gaps.*

---

## What we build and why

*The business, the users, the problem. Then the system shape, briefly, with a link to the [architecture overview](architecture-overview.md).*

*Lead with the domain, not the technology. An engineer who understands what an order is can work out what `OrderService` does. The reverse does not hold.*

*Point at the [ADR log](architecture-decision-record.md) and suggest reading the last ten in order. It teaches more than any diagram, because it teaches the constraints.*

---

## How we work

*The team's operating rhythm and its unwritten rules, written down.*

- *Meetings that exist, what each is for, which are optional*
- *How work is chosen and tracked*
- *Branching, review and release conventions, with links*
- *Working hours, timezones, and what "responsive" means here*
- *How decisions get made and where they get recorded*

*Include the norms that are obvious to you and invisible to a new joiner: whether it is fine to decline a meeting, how to signal being stuck, whether direct messages or channels are preferred, what a red build obliges you to do.*

---

## On-call

*When a new joiner joins the rota, and what has to be true first.*

*The usual sequence is shadowing, then a reverse shadow where the newcomer leads and the experienced engineer observes, then the real rota. Say how many of each.*

*Link the [runbooks](runbook.md) and the escalation policy. State plainly that escalating early is correct and that nobody is judged for it.*

---

## Where things are

*A short, curated map. Repositories, dashboards, the wiki, the tracker, the incident channel.*

*Curated is the operative word. A list of forty links is not orientation. Name the five things used weekly and let the rest be found by asking.*

| What | Where | When you need it |
|---|---|---|
| | | |

---

## First 30, 60, 90 days

*What the new joiner should be able to do by each point, so both they and their manager can tell whether it is going well.*

*Write these as capabilities, not as a task list. "Can pick up a ticket in the payments area without help" is checkable. "Understands the payments domain" is not.*

| By | You should be able to |
|---|---|
| *30 days* | *Ship a small change unaided; know who to ask about each area* |
| *60 days* | *Take a normal ticket end to end; shadow an on-call shift* |
| *90 days* | *Own a piece of work with an external dependency; join the rota* |

---

## Notes on using this template

*Delete this section too.*

**Update it every time it is used.** Ask each new joiner to submit one pull request improving it, before their memory of being confused fades. Nothing else keeps this document alive, because everyone else who reads it already knows the answers.

**Split it by what breaks it.** Environment setup, the first change and the architecture tour belong in the repository: they are invalidated by code changes and should break loudly in review. Team norms, people and organisational context belong in the wiki, where they change without a pull request. Link one from the other.

**Do not link the entire wiki.** A newcomer given fifty documents reads none of them. Attach reading to the task that needs it.

**Measure it.** Time to first merged change, and time to first production deploy. Both are easy to get from your existing tools, and both tell you more about onboarding than anyone's recollection of how it went.

---

## Related documents

- [`architecture-overview.md`](architecture-overview.md). Where "what we build and why" sends the reader for the shape of the system
- [`architecture-decision-record.md`](architecture-decision-record.md). The reading list this guide recommends before anything else, the last ten decisions in order
- [`runbook.md`](runbook.md). What a new joiner shadows before joining the on-call rota
- [`service-readme.md`](service-readme.md). Where the first change actually begins, environment setup
- [`code-review-guidelines.md`](code-review-guidelines.md). What the first change is measured against before it merges
