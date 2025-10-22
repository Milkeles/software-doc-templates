# User acceptance test plan: {System or release}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Document ID** | |
| **Version** | |
| **Accepting party** | *The organisation or business unit accepting. Not the project team.* |
| **Business owner** | *The named individual who signs. One person, not a committee.* |
| **Acceptance baseline** | *The [specification](software-requirements-specification.md) version and contract schedule being accepted against.* |
| **Acceptance period** | *Start and end dates, from the contract.* |

*Acceptance is where a project's remaining ambiguities are converted into money. Everything vague in the specification gets settled here, under time pressure, in front of the person who pays.*

*Write this plan against the contract's acceptance schedule, before testing begins. A plan written from a fresh reading of the requirements will not match what the contract says was promised, and the difference is the dispute.*

---

## 1. Purpose and what acceptance triggers

*What signing this acceptance actually does. Be explicit, because the consequences are usually larger than the participants realise.*

*Typically some combination of: releases a payment milestone, starts the warranty or support period, transfers risk of loss, ends the supplier's obligation to fix free of charge, permits go-live.*

> **Example.** Acceptance releases milestone payment 3, starts the 12-month warranty, and transfers operational responsibility to the customer's service desk.

**Deemed acceptance.** *State the clause if the contract has one, and state the deadline. Deemed acceptance means that if the accepting party neither accepts nor rejects in writing within the period, acceptance happens automatically. It makes the customer's sign-off discipline as commercially significant as the supplier's delivery, and customers routinely do not know it is there.*

---

## 2. Scope of acceptance

**Being accepted.** *Which functions, which interfaces, which environments.*

**Not being accepted here.** *Deferred scope, later phases, items covered by a separate acceptance.*

*Cross-reference the deferrals in the [traceability matrix](requirements-traceability-matrix.md). A requirement deferred by an approved [change request](change-request.md) is a decision. The same requirement missing without one is a defect, and the distinction is worth several weeks of argument.*

---

## 3. Participants and roles

*Named people. Roles without names produce a test with no one accountable for finishing it.*

| Role | Name | Responsibility |
|---|---|---|
| *Business owner* | | *Signs acceptance or rejection* |
| *UAT lead* | | *Runs the test, reports daily* |
| *Business testers* | | *Execute scenarios, raise defects* |
| *Supplier contact* | | *Triages and fixes* |
| *Technical support* | | *Environment and data* |

*Business testers must be people who do the work, not their managers. A manager tests the process as documented; a user tests the process as performed, and the difference is where acceptance defects come from.*

**Availability.** *Confirmed dates and hours per tester, agreed with their line manager in writing. The most common cause of a UAT overrun is that the testers had day jobs and nobody negotiated the release.*

---

## 4. Environment and data

*Which environment, how it differs from production, and who guarantees it is stable for the acceptance period.*

*Acceptance testing on a shared environment that is being deployed to during the test is not acceptance testing. Freeze it, and say who may authorise a deployment during the window.*

**Data.** *Production-like data is what makes UAT find real defects, and it is also where the privacy problem lives. State the source, the masking approach, who verified the masking, and the retention and destruction rules for the data after the test.*

---

## 5. Entry criteria

*What must be true before UAT starts. Every one of these will be pressed at the moment it bites, which is why they are agreed now.*

| Criterion | Evidence | Met? |
|---|---|---|
| *System testing complete and signed off* | *Test completion report* | |
| *No open severity 1 or 2 defects* | *Defect report* | |
| *Environment provisioned and frozen* | *Change freeze notice* | |
| *Test data loaded and verified* | *Data validation sign-off* | |
| *Testers trained and available* | *Attendance record* | |
| *Acceptance scenarios reviewed and agreed by both parties* | *This document, approved* | |

*Starting UAT with entry criteria unmet is the most reliable way to lose the schedule. Testers hit environment problems, log them as defects, lose confidence, and the calendar time is spent without producing evidence.*

---

## 6. Acceptance scenarios

*What will be tested, in business terms, traced to the baseline.*

*Write scenarios as business processes end to end, not as feature checks. A feature checklist re-runs system testing with less skilled testers. A process scenario tests something system testing structurally cannot: whether the pieces work together in the sequence a real person performs them.*

| ID | Business scenario | Traces to | Priority | Tester | Result |
|---|---|---|---|---|---|
| *UAT-012* | *Register a new supplier, raise a purchase order against them, receive partial delivery, reconcile the invoice* | *SRS-041, SRS-044, SRS-052* | *Critical* | | |

**Priority.** *Critical scenarios must pass for acceptance. Others may fail into an agreed defect schedule. Deciding this in advance is what makes the exit criteria enforceable.*

**Coverage.** *Every critical and high requirement in the baseline appears in at least one scenario. Generate this check from the traceability matrix rather than asserting it.*

---

## 7. Defect handling

**Severity definitions.** *Agreed with the accepting party in advance, and written here. If severity is defined during the test, it is negotiated by whoever is most frustrated.*

| Severity | Definition | Blocks acceptance? |
|---|---|---|
| *1 Critical* | *Core business process cannot be completed, no workaround* | *Yes* |
| *2 High* | *Business process impaired, workaround exists but is costly* | *Yes unless formally accepted with a remediation date* |
| *3 Medium* | *Inconvenience, acceptable workaround* | *No, listed in the defect schedule* |
| *4 Low* | *Cosmetic* | *No* |

**Triage.** *Joint, daily, both parties present. Same-day triage keeps disagreements small. Weekly triage produces a backlog of contested severities that gets settled in one meeting nobody enjoys.*

**When the defect is in the requirement.** *Route it to a [change request](change-request.md), not to the defect log. A system that correctly implements a requirement the business no longer wants is not defective, and letting that argument run through the defect process is how acceptance periods double.*

**Remediation cycles.** *How many fix-and-retest rounds the contract allows, and what happens when they are exhausted. This is usually specified and usually forgotten until the third round.*

---

## 8. Exit criteria

*What acceptance requires. Numbers, agreed in advance, from the contract where it specifies them.*

| Criterion | Threshold |
|---|---|
| *Critical scenarios executed* | *100%* |
| *Critical scenarios passed* | *100%* |
| *Open severity 1 defects* | *0* |
| *Open severity 2 defects* | *0, or formally accepted with a documented workaround and remediation date* |
| *Residual defects* | *Listed and explicitly accepted in the defect schedule* |

*A caution on thresholds. Unlike the rest of this group, acceptance testing has no governing standard, and the commonly quoted figures, 95 to 98 percent pass rates, are convention rather than a rule. Set yours deliberately and against this system's risk, and do not let a number arrive from a template.*

---

## 9. Acceptance decision

*The three possible outcomes. Naming all three in advance is what makes conditional acceptance a normal option instead of a concession made under pressure.*

| Outcome | Means |
|---|---|
| **Accepted** | *All exit criteria met. The triggers in section 1 fire.* |
| **Accepted with conditions** | *Accepted against a listed defect schedule with agreed remediation dates and an agreed retention or holdback. The normal outcome on real projects.* |
| **Rejected** | *Exit criteria not met. State what happens next: remediation cycle, revised delivery date, or the contractual remedy.* |

**Defect schedule for conditional acceptance.**

| Defect | Severity | Workaround | Fix by | Verified by |
|---|---|---|---|---|
| | | | | |

---

## 10. Sign-off

*The evidential record. This is the part that has legal weight, and the part that gets emailed as an unsigned attachment if you do not provide a place for it.*

| | |
|---|---|
| **Decision** | *Accepted / Accepted with conditions / Rejected* |
| **Signed** | *Name, role, signature* |
| **Date** | |
| **Attachments** | *Test results, defect schedule, coverage report from the traceability matrix* |

*The signature needs to carry a meaning, not just a mark. Where 21 CFR Part 11 or an equivalent applies, an electronic signature must record the printed name, the date and time, and the meaning of signing. Where it does not apply, the same three things are still what makes the record useful in a dispute two years later.*

---

## Notes on using this template

*Delete this section too.*

**UAT is not a second system test.** If the business is finding functional defects, system testing did not finish, and running UAT anyway spends the customer's goodwill on work the supplier owed. Acceptance tests whether the system supports the business process. That is a question only the business can answer and one no amount of system testing reaches.

**Agree the scenarios before you build, not before you test.** Acceptance scenarios written at the start are a second, independent reading of the requirements, and the places where they disagree with the specification are the ambiguities, found while they are still cheap. Written at the end, they are just a test script.

**Conditional acceptance is a normal outcome.** Treating it as failure pushes both parties toward the two bad options: accepting defects silently to keep the milestone, or rejecting outright over things a defect schedule would have covered. Plan for it and it becomes a negotiation over dates rather than over blame.

**Watch the calendar, not just the results.** Deemed acceptance clauses and fixed acceptance periods mean that time passing is itself a decision. Track the days remaining as visibly as the pass rate.

**Where this lives:** the plan can live in the test management tool with the scenarios. The signed acceptance record belongs in the contract repository or the eQMS, because it is evidence rather than working material, and it must be findable by someone who has never heard of your test tool.
