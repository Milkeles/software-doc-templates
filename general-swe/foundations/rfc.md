# RFC-NNNN: {Title}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Author(s)** | |
| **Approvers** | *The named people whose agreement makes this decided. Not "engineering". If you cannot list them, you do not have an RFC.* |
| **Affected** | *Teams or systems that must change if this is accepted.* |
| **Status** | Draft \| Discussion \| Final comment period \| Accepted \| Rejected \| Withdrawn \| Superseded |
| **Comment period ends** | YYYY-MM-DD |
| **Tracking issue** | *Link, added on acceptance.* |

*An RFC is a design document with two things a design document lacks: named approvers and a deadline. Everything else about the format is negotiable. Those two are not, and without them the proposal will sit in Discussion until it is irrelevant.*

---

## Summary

*One paragraph. What you are proposing and what changes for people if it is accepted. Someone should be able to read only this and decide whether the rest concerns them.*

*Write it last.*

---

## Motivation

*Why do this at all, and why now. What is broken or blocked today, with evidence: an incident, a support volume, a measurement, a customer commitment.*

*Answer the question a reader is actually asking: what happens if we do nothing? If the honest answer is "not much", expect the RFC to be rejected, and consider withdrawing it yourself.*

---

## Guide-level explanation

*Explain the proposal as though it already exists and you are teaching it to someone who will use it.*

*Use the vocabulary you expect people to use afterwards. Show examples. Cover what changes for existing users, and what they must do about it.*

*This section exists to catch a specific failure: proposals that are coherent to their author and incomprehensible to everyone else. If you cannot teach it, it is not ready, regardless of how sound the internals are.*

*For a change with no user-facing surface, keep this short and spend the length below.*

---

## Detailed design

*The part reviewers will argue about. Precise enough that someone else could implement it, and that a reader can find a flaw.*

*Cover interactions with what already exists, edge cases, failure behaviour, and how the transition works for things already running. Corner cases go in detail here rather than being left to implementation.*

*If parts are genuinely undecided, say so and move them to Unresolved questions rather than writing vaguely.*

---

## Drawbacks

*Why we might not want to do this. Written by you, in your own words.*

*Every proposal has real costs. A reviewer who finds one you did not list starts discounting the rest of the document, and rightly. Naming them yourself is both more honest and more persuasive.*

---

## Rationale and alternatives

*Why this design rather than the others.*

- *What other approaches were considered, and why each was rejected*
- *What the impact is of not doing this*
- *Whether prior art or an existing tool solves it, and why that was not used*

---

## Prior art

*How other projects, teams, or systems solved this, and what happened to them. Papers, other languages or frameworks, an internal system that tried it before.*

*This is where an RFC beats a design doc: it forces the author to check whether the problem is already solved. Include failures. A precedent that went badly is more informative than one that went well.*

*Write "none found" if you looked and found nothing. Leaving the section blank looks like you did not look.*

---

## Unresolved questions

*What must be settled before acceptance, and what is deliberately left to implementation. Separate the two, so approvers know what they are approving.*

- *Before acceptance: ...*
- *During implementation: ...*
- *Out of scope for this RFC: ...*

---

## Future possibilities

*What this makes possible later, and what it deliberately leaves room for. Also what it forecloses.*

*Keeps speculation out of the sections that decide the outcome, while giving reviewers somewhere to put "but what about ..." that does not block the decision.*

---

## Decision record

*Filled in by an approver when the comment period closes. Do not delete it afterwards; a rejected RFC with a stated reason is one of the most useful documents a team can keep, because it stops the same proposal returning every year.*

| | |
|---|---|
| **Outcome** | Accepted \| Rejected \| Withdrawn |
| **Date** | YYYY-MM-DD |
| **Approved by** | |
| **Reason** | *One or two sentences. Mandatory on rejection.* |

---

## Notes on using this template

*Delete this section too.*

**Run a real comment period.** Announce that the RFC is entering final comment, give a fixed window (ten days is the Rust convention and works well), and decide at the end. Objections raised after the period closes do not reopen it; they start a new RFC. Without the deadline, silence is indistinguishable from stalling.

**Decide who decides before you write.** An RFC whose approvers are chosen after the argument starts will be decided by whoever argues longest.

**RFC or design doc?** Many organisations use the words interchangeably, and that is fine as long as yours picks one meaning and states it. The distinction worth keeping: use this template when the decision needs a record that specific people agreed, by a date. Use the [design document](technical-design-document.md) when you want expert eyes on an approach your own team will decide.

**Where this lives:** in the repository as a pull request when every required approver reviews code, which gives you line comments, version history, and an auditable approval trail with no extra tooling. Use a wiki when product, legal, design or leadership must sign off, because a pull request excludes them. The tooling does not supply the approvers or the deadline; you do.
