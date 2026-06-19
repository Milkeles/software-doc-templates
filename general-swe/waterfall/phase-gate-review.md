# Phase gate review: {Gate name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Gate** | *Which one. Requirements, design, test readiness, release.* |
| **Project** | |
| **Date** | YYYY-MM-DD |
| **Chair** | *The person with authority to hold the work.* |
| **Attendees** | *Name and role. Note anyone required who did not attend.* |
| **Decision** | *Pass / Pass with conditions / Hold / Cancel* |

*The gate is what makes plan-driven development actually sequential. It is worth knowing that DOD-STD-2167A, the standard blamed for imposing waterfall on the defence industry, never mandated it in its text; what forced the sequence was the schedule of formal reviews and their required deliverables. Gates enforce phases, diagrams do not.*

*A gate does three things. It fixes a baseline, so [change control](change-request.md) has something to control. It transfers accountability from the people who produced the artefacts to the person who approved them. And it creates a point where stopping is a legitimate outcome, which is the only structural defence a plan-driven project has against continuing out of sunk cost.*

---

## 1. What this gate authorises

*What may start once this is passed, and what may not start until then. One sentence each.*

> **Example.** Passing the design gate baselines the software design description and authorises implementation. Until it passes, no production code is written against these requirements.

*If nothing is actually blocked by this gate, it is a status meeting. Either give it authority or stop holding it.*

---

## 2. Required deliverables

*What had to exist and be approved for this review to happen. The list is fixed in advance, per gate.*

| Deliverable | Version | Status | Approved by |
|---|---|---|---|
| | | | |

**Entry check.** *Whether the review should proceed at all. Reviewing incomplete deliverables produces a conditional pass with a long list, which is a hold that nobody had to say out loud.*

*Scale the required list to the risk. IEEE 829-2008 used an integrity level scheme, catastrophic through negligible, to decide which documents were required at all, and that idea generalises: a gate on a low-criticality component should demand less than the same gate on a safety-related one. Uniform gates across unequal work is how gate processes earn their reputation.*

---

## 3. Review criteria

*What is being checked. Written per gate, in advance, so the review is an assessment rather than an opinion poll.*

*Each criterion needs evidence, not assertion. "Requirements are complete" is a claim; "no TBD, TBS or TBR clauses remain, per the traceability report" is a check.*

| Criterion | Evidence | Met? | Note |
|---|---|---|---|
| | | | |

*Criteria that usually belong, by gate:*

**Requirements gate.** *Baseline approved. Every requirement is singular, verifiable and has a stated verification method. No unresolved TBDs. Every stakeholder requirement traces down. Assumptions have owners and confirmation dates.*

**Design gate.** *Design satisfies every requirement, shown by the [traceability matrix](requirements-traceability-matrix.md), not asserted. Every design element traces back to a requirement. Every identified stakeholder concern is framed by a viewpoint. Interfaces agreed with the parties on the other side of them.*

**Test readiness gate.** *Test plan approved. Coverage against the baseline demonstrated. Environments provisioned. Entry criteria for the level met. Test data available and validated.*

**Release gate.** *Exit criteria met. Open defects listed with severity and a disposition for each. Residual risks stated and accepted by a named person. Rollback tested, not just written.*

---

## 4. Traceability status

*The coverage numbers from the [traceability matrix](requirements-traceability-matrix.md), generated for this gate.*

| Measure | Count | Target | Met? |
|---|---|---|---|
| *Requirements in baseline* | | | |
| *Traced to design* | | | |
| *Traced to a test case* | | | |
| *Verified* | | | |
| *Open, with an approved deferral* | | | |

*Generate these. A gate that accepts a hand-typed coverage figure is accepting a claim, and the claim is the thing the gate exists to check.*

---

## 5. Open items

*Everything unresolved, each with a disposition. This is the section that decides the outcome, so fill it in before the decision, not after.*

| Item | Severity | Disposition | Owner | Due |
|---|---|---|---|---|
| | *Blocking / Condition / Accepted risk* | | | |

*Three dispositions, and the discipline is in keeping them distinct:*

- **Blocking.** *The gate cannot pass. Say so.*
- **Condition.** *The gate passes and this must be closed by a stated date, with a named owner. A condition with no date is a blocking item that someone declined to call one.*
- **Accepted risk.** *Not being fixed. Someone accepts the consequence, by name. This is the honest option and it is used far too rarely.*

---

## 6. Decision

| | |
|---|---|
| **Decision** | *Pass / Pass with conditions / Hold / Cancel* |
| **Baseline established** | *What is now under change control, at which version.* |
| **Authorised to start** | *What may now proceed.* |
| **Conditions** | *Each with an owner and a date. Listed here, not only in the minutes.* |
| **Next gate** | *Which, and the planned date.* |

**Signature.**

| Role | Name | Signature | Date |
|---|---|---|---|
| *Chair / design authority* | | | |
| *Quality* | | | |
| *Customer or sponsor* | | | |

*The signature carries the accountability transfer. Where an electronic signature standard applies, it must record the name, the date and time, and the meaning of the signing, and it must be bound to the record so it cannot be moved to another one.*

---

## Notes on using this template

*Delete this section too.*

**A gate that has never held anything back is not a control.** This is the failure mode, and it is nearly universal. Gates decay into attendance rituals where everything passes with conditions, the conditions are tracked in a spreadsheet nobody reads, and the phase after starts regardless. If your gates have a hundred percent pass rate, you are not gating, you are reporting, and the honest move is to say so and stop spending the meeting.

The countermeasure is the disposition vocabulary in section 5. Forcing every open item into blocking, condition or accepted risk makes the soft pass visible, because a conditional pass with nine conditions and no dates is obviously a hold.

**Review the evidence, not the presentation.** Deliverables circulate before the meeting and the meeting resolves disagreements about them. A gate where the artefacts are first seen on a slide is a gate where nothing was checked, and the format quietly guarantees this: nobody objects to a slide.

**Cancel is a legitimate outcome.** It is the one the structure exists to make possible, and it is the one no template ever lists, which is why it never happens. A project that cannot be stopped at a gate will be stopped later, by running out of money, having spent everything in between.

**Scale the gate to the risk.** Same gates, same evidence, same attendees for every project is what makes people route work around the process. Vary the required deliverables by criticality and say what the scheme is, so a light gate looks like a decision rather than an exception.

**Where this lives:** the signed record in the eQMS or the project record, because it is evidence of an approval and needs to be findable years later by someone who was not there. Not in a slide deck, and not only in meeting minutes. The working deliverables stay wherever they normally live; the gate record points at them by version.

---

## Related documents

- [`software-requirements-specification.md`](software-requirements-specification.md). What the requirements gate baselines before design may start
- [`software-design-description.md`](software-design-description.md). What the design gate baselines before implementation is authorised
- [`requirements-traceability-matrix.md`](requirements-traceability-matrix.md). Source of the coverage numbers a gate reviews as evidence, not as a claim
- [`change-request.md`](change-request.md). What change control protects once this gate fixes a baseline
