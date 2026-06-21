# Non-Functional Requirements

> How well the system must work, stated so that someone can test it.
>
> **Also called:** NFRs, quality attributes, or quality requirements.
>
> **The problem this solves.** Functional requirements get written because someone asks for them. Quality attributes do not, so they arrive as adjectives in a meeting, get agreed by everyone, and mean something different to each person. "The system must be fast" has never failed a review and has never been testable.
>
> **Two sources do the work here.** ISO/IEC 25010:2023 tells you which qualities exist, so you check yourself against a list instead of remembering. The six-part quality attribute scenario from Bass, Clements and Kazman, *Software Architecture in Practice* (4th edition, Addison-Wesley, 2021), tells you how to state one so it can be verified.
>
> **Where it lives.** With the requirements it accompanies. A section of the [PRD](product-requirements-document.md) or [SRS](../waterfall/software-requirements-specification.md) for small work; a standalone document when the qualities are the hard part, which is common in platform, embedded and regulated work.
>
> **Delete this block before publishing.**

---

## 1. How to state one

Never as an adjective. Always as a scenario with a number in it.

The six-part scenario gives you the parts to fill in:

| Part | Question |
|---|---|
| **Source of stimulus** | Who or what causes it? |
| **Stimulus** | What happens? |
| **Environment** | Under what conditions? Normal load, peak, degraded, startup |
| **Artifact** | What part of the system is affected? |
| **Response** | What should the system do? |
| **Response measure** | How is that measured? |

**The response measure is the part that matters.** Everything else is context; the measure is what makes the requirement a requirement rather than an aspiration. If you cannot write a measure, you do not yet have a requirement, and the honest move is to record it as an open question rather than write something unfalsifiable.

Worked example:

> **NFR-07 Reset email latency.**
> A user (source) requests a password reset (stimulus) while the system is under peak load, defined as 500 concurrent reset requests (environment). The notification service (artifact) sends the reset email (response). 95% of emails are handed to the mail provider within 60 seconds, and 99% within 180 seconds (response measure).

Compare with the version this replaces: "password reset emails should arrive quickly." Both describe the same intent. Only one can be tested, and only one tells an engineer whether a queue is needed.

**State percentiles, not averages.** An average latency hides the tail, and the tail is what users complain about. This is the same reasoning behind Core Web Vitals being measured at the 75th percentile.

---

## 2. Which qualities to consider

Work through the ISO/IEC 25010:2023 characteristics and record a decision for each: a requirement, or an explicit "not a concern here, because...".

**Use the 2023 model, not the 2011 one.** The revision renamed characteristics, added one, and moved quality-in-use out to ISO/IEC 25019:2023. A document citing Usability and Portability as 25010 characteristics is citing a superseded model.

| Characteristic | Sub-characteristics |
|---|---|
| **Functional suitability** | Completeness, correctness, appropriateness |
| **Performance efficiency** | Time behaviour, resource utilization, capacity |
| **Compatibility** | Co-existence, interoperability |
| **Interaction capability** | Appropriateness recognizability, learnability, operability, user error protection, user engagement, inclusivity, user assistance, self-descriptiveness |
| **Reliability** | Faultlessness, availability, fault tolerance, recoverability |
| **Security** | Confidentiality, integrity, non-repudiation, accountability, authenticity, resistance |
| **Maintainability** | Modularity, reusability, analysability, modifiability, testability |
| **Flexibility** | Adaptability, scalability, installability, replaceability |
| **Safety** | Operational constraint, risk identification, fail safe, hazard warning, safe integration |

### What changed from the 2011 model

Worth knowing, because most existing documents and most search results still describe the old one.

- **Usability became Interaction capability.** User interface aesthetics was replaced by user engagement. Accessibility was split into inclusivity and user assistance. Self-descriptiveness was added.
- **Portability became Flexibility**, and gained scalability as a sub-characteristic. Scalability previously had no home in the model, which is why so many teams filed it under performance.
- **Safety is new**, taking the count from eight characteristics to nine.
- **Reliability's maturity became faultlessness.**
- **Security gained resistance.**

### Using the list properly

The list is a checklist against forgetting, not a template to fill. Nine characteristics do not mean nine requirements.

**Record the ones you decided not to specify, and why.** That line is the difference between a considered omission and an oversight, and it is what an auditor, a new architect or your future self will look for.

> **Co-existence:** not applicable. The service runs in a dedicated container with no other workloads.

---

## 3. Which ones usually need a number

The characteristics that most often need explicit requirements, and the trap in each.

**Availability.** State the target, the measurement window, and what counts as unavailable. "99.9%" alone is meaningless: over a year that is nearly nine hours, over a month it is 43 minutes, and the difference decides your architecture. Say whether scheduled maintenance is excluded, and define the failing condition precisely enough that two people would classify an incident the same way.

**Performance.** Separate throughput from latency; they trade against each other and a single number hides the trade. Always give a load condition. A latency figure with no stated load is not a requirement.

**Capacity and scalability.** The load you must handle today, the growth you must absorb, and over what period. Without a horizon, "scalable" means whatever the reader hopes.

**Security.** Mostly expressed as constraints and standards to conform to rather than as measures. Name them: which authentication requirements, which data classification, which controls. See [`../foundations/threat-model.md`](../foundations/threat-model.md) for deriving these rather than guessing.

**Inclusivity and accessibility.** Name the standard and level: WCAG 2.2 Level AA is the usual target and is what most regulation now points at. "Accessible" is not a requirement; a named conformance target is. See [`../../web-development/accessibility/`](../../web-development/accessibility/).

**Recoverability.** Recovery time objective and recovery point objective, both as numbers. These two determine backup architecture more than any other requirement, and they are routinely left to be discovered during the first real outage.

**Maintainability and testability.** Hardest to measure honestly. Proxy metrics like coverage percentages are gameable and weakly connected to what you want. Often better stated as constraints, "no module may exceed X", or as a scenario about change: "a new payment provider can be added by implementing one interface, with no changes to the checkout flow."

---

## 4. Conflicts

Quality attributes trade against each other. A document that lists them without acknowledging the trades is describing an impossible system.

Common tensions: security against usability, performance against maintainability, availability against consistency, flexibility against performance.

**Where two requirements pull against each other, say which wins.**

> NFR-07 (reset email within 60 seconds) conflicts with NFR-12 (uniform response timing regardless of whether an address is registered). NFR-12 wins. The security property is not negotiable; the latency target is a goal.

This is the same discipline as the driver, constraint and degree-of-freedom table in [vision and scope](vision-and-scope.md), applied at the level of individual qualities. Resolving it here means it is not resolved at 2am by whoever is on call.

---

## 5. Verification

Every requirement gets a verification method, stated when the requirement is written.

| Method | Fits |
|---|---|
| Test | Anything with a measurable response |
| Analysis | Capacity models, failure mode analysis |
| Inspection | Conformance to a standard, presence of a control |
| Demonstration | Operational procedures, recovery drills |

ISO/IEC/IEEE 29148:2018 lists **verifiable** among its characteristics of a well-formed requirement, alongside necessary, appropriate, unambiguous, complete, singular, feasible, correct and conforming. A requirement with no method is not verifiable, and writing the method at the same time as the requirement is what catches that immediately rather than at acceptance.

**A requirement whose verification is "review the design" is not verified.** Either find a real method or downgrade it to a design guideline and stop calling it a requirement.

---

## 6. Format

Table or list, one identifier each, traceable to a business objective or a stakeholder need.

| ID | Characteristic | Requirement | Verification | Priority |
|---|---|---|---|---|
| NFR-07 | Performance efficiency | 95% of reset emails handed to the provider within 60s at 500 concurrent requests | Load test | Must |
| NFR-08 | Reliability | Availability 99.9% monthly, excluding announced maintenance; unavailable means the sign-in endpoint returns 5xx or exceeds 10s | Monitoring, monthly report | Must |
| NFR-09 | Interaction capability | Conforms to WCAG 2.2 Level AA on all authenticated pages | Audit per [test plan](../../web-development/accessibility/accessibility-test-plan.md) | Must |
| NFR-12 | Security | Reset response is identical in content and timing for registered and unregistered addresses | Penetration test | Must |

**Every row traces to something.** A quality requirement that traces to no objective and no stakeholder is usually an engineer's preference, and it will be the first thing dropped under pressure. Tracing it either justifies it or reveals that it should not be there.

---

## Common failures in this document

- **Adjectives.** Fast, secure, reliable, scalable, user-friendly. None testable, all agreed by everyone.
- **Numbers with no conditions.** "Response under 200ms" without a load figure is unfalsifiable and unbuildable.
- **Averages instead of percentiles.** Hides exactly the behaviour users notice.
- **Availability without a definition of unavailable.** Two people classify the same outage differently, and the number becomes an argument.
- **Copied from a previous project.** Produces requirements nobody chose, which either constrain the design pointlessly or are quietly ignored.
- **Conflicts unresolved.** The trade-off is made under pressure by whoever is present.
- **Citing the 2011 quality model.** Superseded in 2023, with real renames.

---

## Related documents

- [`product-requirements-document.md`](product-requirements-document.md). Where these usually live for smaller work
- [`../waterfall/software-requirements-specification.md`](../waterfall/software-requirements-specification.md). Formal specification, with verification approach per requirement
- [`../foundations/threat-model.md`](../foundations/threat-model.md). Where security requirements should come from
- [`../foundations/architecture-decision-record.md`](../foundations/architecture-decision-record.md). Quality attribute conflicts and their resolutions are ADR material
- [`../../web-development/performance/performance-budget.md`](../../web-development/performance/performance-budget.md). Performance requirements enforced automatically
