# Product Requirements Document

> What to build and why, for the team building it.
>
> **Also called:** PRD, or product spec.
>
> **Read this before you use it.** The PRD is the least standardised document in this repository. There is no ISO standard, no IEEE standard, no PMI or IIBA definition. Every published PRD template is somebody's house style, including this one. Anyone who tells you there is a correct PRD structure is describing their previous employer.
>
> **A respected objection exists and you should hear it.** Marty Cagan has argued against the document form for twenty years. In "Revisiting the Product Spec" (2006) he wrote that "most specs take too long to write, they are seldom read, they don't provide the necessary detail", and that "it is all too easy for the mere existence of the spec to serve as a false indicator to management and the product team". His alternative is direct: "there's only one form of spec that can deliver on these requirements, and that is the high-fidelity prototype." In "The End of Requirements" (2013) he went further: "Most requirements are not actually requirements, and the rest are better thought of as constraints."
>
> **When Cagan is right, do not write this.** If you can build a prototype people can use, and your team sits close enough to talk daily, the prototype plus a one-page brief carries more information than this document and carries it more accurately.
>
> **When to write it anyway.** When the people who must agree cannot all be in the room: a distributed team, an external supplier, a regulated context needing a record, or a decision that must survive the departure of the person who made it. The document is a coordination device for exactly those conditions. Outside them it is overhead.
>
> **Where it lives.** Wiki. It changes through discussion, it is co-authored with non-engineers, and it is superseded rather than versioned.
>
> **Delete this block before publishing.**

---

## 1. Summary

Three sentences. What is being built, for whom, and why now.

If a reader stops here, they should be able to describe the work correctly to somebody else. Most readers do stop here.

> Self-service password reset for the customer portal. Replaces a support-mediated flow costing 1.8 FTE-days a week. Shipping before the September regulatory deadline that requires audit logging on all credential changes.

---

## 2. Problem

The user problem, evidenced.

State what people do today, what it costs them, and how you know. **Cite the evidence rather than describing it**: the ticket count, the research session, the funnel drop-off, the recorded complaint. A problem statement with no evidence is a solution someone already picked, working backwards.

Say what you do not know. A stated uncertainty gets tested; an unstated one gets built.

> 63% of support contacts in Q1 were account access. Of 12 interviewed users, 9 had tried and failed to find a self-service option before contacting support. We do not know how many users abandon before contacting support at all.

---

## 3. Goals and non-goals

**Goals.** What this work achieves, each with a measure. Three to five. If [vision and scope](vision-and-scope.md) exists, these are narrower and must trace to its objectives.

**Non-goals.** What this work deliberately does not do, and why.

The non-goals list is the most valuable part of the whole document, and the first thing cut when someone is in a hurry. It is where you record the ideas that were raised and rejected, so they do not return every fortnight.

> **Non-goal: passwordless login.** Worth doing, out of scope here. It would change the authentication architecture and cannot ship before the September deadline.

Naming the reason matters. "Out of scope" invites reopening. "Would change the authentication architecture and cannot ship before September" does not.

---

## 4. Users

Who this is for, at the level of detail your team lacks.

If you have real research, reference it and link the findings. If you have personas, link them rather than restating. **If you have neither, say so.** A PRD that invents a user is worse than one that admits the audience is assumed, because the invention gets treated as evidence by everyone downstream.

Include the users you are not designing for. A product optimised for the frequent expert user fails the occasional novice, and stating which you chose prevents a design review discovering it late.

---

## 5. Requirements

The substance. How you write these is the biggest decision in the document.

### Choosing a form

| Form | Fits | Costs |
|---|---|---|
| User stories | Iterative delivery, co-located team, ongoing conversation | Deliberately incomplete. A story is a placeholder for a discussion, not a specification |
| Use cases | Interaction-heavy flows, many alternate paths, external supplier | Verbose. Overkill for simple CRUD. See [`use-case-specification.md`](use-case-specification.md) |
| Shall-statements | Regulated work, contractual delivery, formal verification | Slow to write and read. See [`../waterfall/software-requirements-specification.md`](../waterfall/software-requirements-specification.md) |
| Job stories | The situation matters more than the role | Less familiar, so needs explaining once |

**Pick one and use it throughout.** Mixing forms in one document means no reader knows the level of commitment any given line carries.

### Whatever the form

Every requirement needs three things:

**An identifier.** `PR-14`. Tests, tickets and design decisions reference it. Without identifiers, traceability is impossible and every conversation re-describes the requirement from scratch.

**A priority, from a scale that forces choices.** MoSCoW works only if "Must" is capped: a list where everything is a Must is a list with no priorities. Numbered priority with a stated cap ("no more than 8 P0 items") is harder to game.

**Acceptance criteria.** The condition under which someone agrees it is done. Written before implementation, not after. **This is the single highest-value habit in requirements work**, because it converts "the reset flow should be secure" into something a tester can pass or fail.

> **PR-14** A user can request a password reset using their registered email address. *(P0)*
>
> Accepted when:
> - Submitting a registered address sends a reset link within 60 seconds.
> - Submitting an unregistered address returns the same message and timing, so the response does not reveal whether an account exists.
> - The link expires after 30 minutes and is single-use.
> - Every request and use is written to the audit log.

Note what the second criterion does: it captures a security property that "can request a password reset" does not imply, and that would otherwise be discovered in a penetration test.

### What does not belong here

Implementation. If the requirement names a database, a library or a class, it is a design decision wearing a requirement's clothes. Move it to the [technical design document](../foundations/technical-design-document.md), or to a constraints section if it genuinely is imposed from outside.

The exception is a real constraint, and it should be labelled as one: "must use the existing identity provider, because replacing it is a separate programme."

---

## 6. Non-functional requirements

Performance, security, availability, accessibility, operability.

Do not list adjectives. "Fast", "secure" and "reliable" fail as requirements because nobody can disagree with them and nobody can test them. State each as a measurable scenario, and see [`non-functional-requirements.md`](non-functional-requirements.md) for the form and for the ISO/IEC 25010 characteristics to check yourself against.

The short version: name the stimulus, the condition, and the measurable response.

> Under 500 concurrent reset requests, 95% of reset emails are sent within 60 seconds.

---

## 7. Design

Link, do not embed.

Point to the mockups or prototype. If the design is not ready, say what is unresolved and who is deciding.

**Where a prototype exists, it is authoritative over any description in this document.** Say so explicitly. Otherwise a stale sentence here will be built instead of the design, and nobody will know which was intended.

---

## 8. Open questions

Number them, give each an owner and a date needed.

| # | Question | Owner | Needed by |
|---|---|---|---|
| 1 | Do we notify users by SMS when no email is on file? | [name] | 2026-04-10 |
| 2 | What is the legal retention period for reset audit records? | [name] | 2026-04-03 |

A PRD with no open questions is either finished or dishonest, and at the point it is written it is rarely finished. **This section is what stops the document pretending to a certainty it does not have.**

Move each question to a decision when it closes. Do not delete it; the record of what was uncertain is useful when someone later asks why a choice was made.

---

## 9. Release and rollout

How this reaches users. What is behind a flag, who sees it first, what has to be true before it goes wider.

Keep it to a paragraph and link a [rollout plan](../../web-development/foundations/rollout-plan.md) if the change warrants one.

---

## 10. Out of scope

Distinct from non-goals. Non-goals are things you decided not to do; out of scope is work someone else owns or that follows later.

> Migrating existing users to the new identity provider. Owned by the platform team, tracked separately, not a dependency of this work.

---

## Common failures in this document

- **Written to be approved rather than to be built from.** Optimising for a sign-off meeting produces a document nobody consults afterwards.
- **No non-goals.** Guarantees the same suggestions return every two weeks.
- **Requirements without acceptance criteria.** Every one becomes a negotiation at the end of the work, when it is most expensive.
- **Implementation disguised as requirements.** Constrains the designers who were supposed to solve the problem.
- **Never updated after the first sprint.** Becomes a historical artefact that people still cite as current.
- **Written when a prototype would do.** Cagan's objection is correct in the situations it describes. Recognise them.
- **Everything is P0.** No prioritisation happened; it was deferred to whoever runs out of time first.

---

## Related documents

- [`vision-and-scope.md`](vision-and-scope.md). Why the project exists. This document assumes that is settled
- [`use-case-specification.md`](use-case-specification.md). For flows with many alternate paths
- [`non-functional-requirements.md`](non-functional-requirements.md). Quality attributes, stated testably
- [`../foundations/technical-design-document.md`](../foundations/technical-design-document.md). How it will be built. Different document, different author, different review
