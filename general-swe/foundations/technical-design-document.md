# Design: {What you are building}

*Also called: design doc.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Author(s)** | |
| **Reviewers** | *Named people, not "the team". A doc with no named reviewer gets no review.* |
| **Status** | Draft \| In review \| Approved \| Implemented \| Abandoned |
| **Last updated** | YYYY-MM-DD |

*Length: one to three pages for most changes, ten to twenty for a project that will occupy several people for a quarter. If yours is longer than twenty, split it. Nobody reviews a forty-page design; they skim it and approve, which is worse than no review.*

*Write this before the code, while changing the approach is still cheap. A design doc produced after implementation is a status report.*

---

## Context and scope

*What a reader needs to know to follow the rest, and nothing more. Assume a competent engineer who does not work on your system.*

*Describe the situation as it is now, then the specific problem. Keep it factual: this is the shortest section that people most often bloat. Half a page.*

*Do not describe your solution here. If the reader can guess the design from this section, move that text down.*

> **Example.** The import pipeline processes one file at a time on a single worker. Volume has grown from 200 files a day to 9,000, and the daily run now finishes after the 06:00 reporting cutoff four days a week.

---

## Goals

*What success looks like, in terms someone could check. Numbers where numbers exist.*

- *Goal, measurable if possible: "daily import completes by 04:00 at 20,000 files"*

## Non-goals

*Things a reader might reasonably assume you are solving, that you are not. This is the highest-value section in the document and the one most often left out.*

*Scope arguments in review almost always turn out to be disagreements about non-goals. Naming them converts a late argument into an early one. "Not a goal" is different from "not possible" and different from "later"; say which.*

- *Non-goal, with one clause on why: "real-time import, because reporting is daily and streaming would double the operational surface"*

---

## The design

*The bulk of the document. Explain the approach as you would to a colleague at a whiteboard: what the pieces are, how data moves, what each part is responsible for.*

*Lead with a diagram or a numbered walkthrough of the main flow. Then the parts that are not obvious. Skip the parts that are.*

*Write the trade-offs inline, where they occur. "We batch in groups of 500 because the downstream API rate-limits at 2 req/s" belongs next to the batching, not in a separate discussion section.*

*Cover, as they apply:*

- *System context: what calls this, what it calls*
- *Data model and storage, including what is authoritative*
- *APIs and contracts you add or change, and whether the change is breaking*
- *Degradation: what happens when each dependency is slow or down*
- *State, idempotency, and what happens on retry*
- *Migration: how you get from the current system to this one without an outage*

*Include enough detail that a reviewer could find a design flaw. Exclude detail that only matters at implementation time. Function signatures and class names are usually the wrong altitude.*

---

## Alternatives considered

*The other approaches, each with why you rejected it. One paragraph each.*

*Reviewers who cannot see this section will propose the alternatives during review, and you will explain them one at a time in comment threads. Writing them down once is cheaper.*

*Be genuinely fair. An alternatives section where every option has an obvious fatal flaw signals that you evaluated nothing, and experienced reviewers read it that way.*

### {Alternative}

*What it is, in one sentence. Why not, in two or three. Name the condition that would change the answer if there is one.*

---

## Cross-cutting concerns

*Only the ones this design actually affects. Delete the headings that do not apply. A design doc that answers "N/A" eight times has trained its readers to skip the section.*

**Security and privacy.** *New attack surface, new data flows, what personal data is involved and where it lands. If the answer is more than a line, write a [threat model](threat-model.md) and link it.*

**Observability.** *What you will look at to know it works, and what alerts on failure. If you cannot say how you would detect this breaking in production, the design is not finished.*

**Testing.** *What is hard to test here and how you plan to handle it, not the full test plan.*

**Cost.** *Infrastructure, licence, or per-request cost changes worth a decision.*

**Compliance and data retention.** *Anything an auditor would ask about.*

**Operational load.** *What this adds to on-call: new alerts, new runbooks, new failure modes.*

---

## Rollout and rollback

*How this reaches production, in what order, behind what control. Feature flag, percentage rollout, dark launch, backfill then cutover.*

*Then the part people skip: what you do if it goes wrong after the point where a code revert is not enough. Once data has been written in a new format, "roll back the deploy" is not a plan.*

---

## Open questions

*What you have not resolved, with an owner and a date for each. Keep this section alive during review and empty it before the status becomes Approved.*

*An open question with no owner is a question nobody is answering.*

| Question | Owner | Needed by |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**The review is the product.** The artefact is a by-product. Send it to the named reviewers with a deadline, and treat unanswered comments as blocking. A design doc that nobody comments on either was not needed or was not read; both are worth knowing.

**Do not maintain it after ship.** Design docs describe a decision at a moment. Trying to keep one current turns it into a bad architecture overview. Once implemented, mark it Implemented, extract the durable decisions into [ADRs](architecture-decision-record.md), and update the [architecture overview](architecture-overview.md) instead.

**Skip the document entirely** when the approach is unambiguous, when the change is reversible in a day, or when writing it would take longer than building the thing. The test is whether there is a real trade-off to discuss. If not, you are writing an implementation manual.

**Where this lives:** a wiki or collaborative document tool during review, because the value is in the comment threads and the readers may not use pull requests. Link it from the repository. Move the outcomes into the repo when it ships.

---

## Related documents

- [`threat-model.md`](threat-model.md). Where security and privacy get a real analysis, once "cross-cutting concerns" needs more than a line
- [`architecture-decision-record.md`](architecture-decision-record.md). Where the durable decisions get extracted once the design is implemented
- [`architecture-overview.md`](architecture-overview.md). What gets updated instead of maintaining this document after ship
- [`rfc.md`](rfc.md). The other route to the same decision, when named approvers and a deadline matter more than expert review
- [`../../ai-assisted-development/specification/agent-task-specification.md`](../../ai-assisted-development/specification/agent-task-specification.md). The document to write instead, when the work is a bounded task for an agent to execute in one session rather than a judgment call about approach
- [`../waterfall/software-design-description.md`](../waterfall/software-design-description.md). The same job, done at gate weight: pick this one instead when a phase gate, regulator, or auditor has to sign off on the design before code starts
