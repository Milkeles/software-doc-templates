# {Item title}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Type** | *Feature \| Bug \| Technical \| Spike* |
| **Size** | *Whatever unit tells you it fits in a Sprint.* |
| **Product Goal** | *Which goal this serves. An item serving none is a question for the Product Owner.* |

*None of this is Scrum. The Guide requires a Product Backlog of ordered items with a description, order and size, and nothing else. The structure below exists because items written by one person and picked up by another lose information in transit. If your team is small enough to talk it through, use less of this.*

---

## What and why

*Pick the form that fits the work. Three are given below. Using the wrong one produces contortions that obscure rather than clarify, which is the main criticism of insisting on any single template.*

**User story**, for work with a clear actor:

> As a *{role}*, I want *{capability}*, so that *{benefit}*.

*The third clause is the one that matters. "So that" records why the item exists, and it is the clause teams drop first. An item whose benefit you cannot state is an item you cannot order against the Product Goal, and probably one you should not build.*

**Job story**, when the situation predicts behaviour better than the role:

> When *{situation}*, I want to *{motivation}*, so I can *{expected outcome}*.

*Useful where "as a user" would smuggle in an assumption about who is acting. The trigger is the point: "when my card is declined at checkout" tells you more about the design than "as a customer" does.*

**A plain sentence**, for work with no user-facing actor:

> *Rotate the signing keys quarterly without downtime, so a key compromise has a bounded blast radius.*

*Infrastructure, compliance, migrations and upgrades do not have users in the story sense. Forcing them into "as a developer, I want" is a well-known way to make a backlog unreadable. Write the change and the reason.*

---

## Context

*What a reader needs that is not in the sentence above. The current behaviour, the ticket that prompted it, the constraint, the screenshot.*

*Remember what the card is for. Ron Jeffries put it plainly in 2001: "the card does not contain all the information that makes up the requirement." It is a token for a conversation. Write enough that the conversation starts in the right place, not enough to replace it.*

---

## Acceptance criteria

*Per-item conditions that answer "does this do the right thing". Written so a passing or failing answer is obvious.*

*Distinct from the [Definition of Done](definition-of-done.md), which applies to every item and answers "is this releasable". An item can meet all its acceptance criteria and still not be done.*

*Given/When/Then is a useful shape where behaviour is conditional. A bulleted list is fine where it is not. Do not use a format that adds words without adding checks.*

- *Given a merchant with more than 10,000 transactions, when they request an export, then the file is delivered by email within 15 minutes.*
- *Empty result sets produce a file with headers, not an error.*

**Edge cases the team should decide now.** *Empty, maximum, concurrent, permission-denied, partial failure. The cases that get discovered mid-Sprint and blow up the size.*

---

## Out of scope

*What this item deliberately does not cover, and where it goes instead.*

*One line each. Prevents the slow expansion that turns a two-day item into a two-week one without anyone deciding to.*

---

## Dependencies

*What must exist before this can start, and who owns it. A blocked item in a Sprint is the most reliable way to miss a Sprint Goal.*

---

## Notes on using this template

*Delete this section too.*

**Run it through INVEST before it reaches Sprint Planning.** Bill Wake's 2003 checklist catches most defects while they are still cheap:

| | |
|---|---|
| **I**ndependent | *Can it be built without another item going first?* |
| **N**egotiable | *Does it state the need rather than dictate the implementation?* |
| **V**aluable | *Can you name who is better off? "Valuable to the developers" usually means it should be part of another item.* |
| **E**stimable | *Does the team know enough to size it? If not, write a spike instead.* |
| **S**mall | *Does it comfortably fit in a Sprint? The Guide's own readiness heuristic is exactly this.* |
| **T**estable | *Could you write the check before the code?* |

**The template is a prompt, not a grammar.** Every form above is contested, and the criticism is fair: a fixed sentence shape can hide the reasoning it was meant to expose. If the shape is making an item harder to understand, abandon it for that item. Consistency is worth something; clarity is worth more.

**Detail is proportional to distance.** An item three Sprints away needs a title and a rough size. An item entering Sprint Planning needs the detail above. Writing full acceptance criteria for the whole backlog is refinement done as busywork, and most of it will be rewritten or deleted.

**Refinement is an activity, not an event.** The Guide describes it as ongoing and prescribes no meeting, no attendees and no timebox. The often-quoted "no more than 10 percent of capacity" rule was in the 2017 Guide and was removed in 2020; anyone still citing it is citing a superseded document.

**Where this lives:** the tracker. Items are ordered, worked and closed there, and a copy anywhere else will disagree with it within a week.
