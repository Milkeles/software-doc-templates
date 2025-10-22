# Master test plan: {System or project}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Document ID** | |
| **Version** | |
| **Status** | *Draft / In review / Approved* |
| **Approval authority** | *Who approves this plan. Required content under ISO/IEC/IEEE 29119-3 clause 5.2.3.* |
| **Approval date** | YYYY-MM-DD |
| **Baseline tested** | *Which [requirements](software-requirements-specification.md) version.* |

*Follows ISO/IEC/IEEE 29119-3:2021 clause 7.2, which superseded IEEE 829. If your contract names IEEE 829-2008, Annex S of 29119-3 maps between them, and this structure satisfies both.*

*One master plan sets the strategy across all levels. Each level, component through acceptance, gets its own plan only when the levels are run by different people or against different schedules. Two plans that repeat each other are one plan and a maintenance burden.*

---

## Change history

| Version | Date | Change | Author | Approved by |
|---|---|---|---|---|
| | | | | |

---

## 1. Context of testing

*What is being tested, in what environment, under what constraints. New in 29119-3; IEEE 829 had no equivalent, and its absence is why old test plans read as if written in a vacuum.*

*Cover the project or organisational context, the standards or regulations that apply, and anything about this system that makes testing it unusual: hardware in the loop, third-party dependencies you cannot control, data you cannot generate.*

## 2. Scope

**In scope.** *Which components, which levels, which quality characteristics.*

**Out of scope, and who covers it instead.** *Testing you are deliberately not doing. Name the party who is doing it, or state that nobody is and that this is accepted. An unstated gap becomes an assumption that someone else has it covered, and that assumption is usually wrong on both sides.*

## 3. Stakeholders

*Who has an interest in the outcome and what each needs from testing. Also new in 29119-3.*

| Stakeholder | Interest | What they need from this plan |
|---|---|---|
| *Business owner* | *Acceptance decision* | *Evidence against the requirements baseline* |
| *Regulator or assessor* | *Compliance evidence* | *Coverage, traceability, verified risk controls* |
| *Development lead* | *Defect feedback speed* | *Level definitions and entry criteria* |

## 4. Assumptions and constraints

*What must be true for this plan to hold, and what limits it. Environments, licences, data availability, staff, hardware, dates fixed by others.*

*Each constraint should have a consequence attached. "Only one test environment" is a fact; "only one test environment, so integration and system testing cannot run in parallel and the schedule assumes serial execution" is a plan.*

---

## 5. Risk register

*29119-3 puts risk at the centre of the plan, and this is the change that matters most from IEEE 829. Testing is framed as risk management, not coverage accounting.*

*Two kinds, kept separate because they are managed differently.*

**Product risks.** *What could go wrong with the system, and what testing you are doing about it. This is what decides where the effort goes.*

| Risk | Likelihood | Impact | Mitigating tests | Owner |
|---|---|---|---|---|
| *Payment reconciliation drifts under concurrent settlement* | *Medium* | *High* | *TC-200 to TC-214, load profile B* | |

**Project risks.** *What could stop you testing: environment unavailable, data not ready, dependency late, staff unavailable.*

| Risk | Likelihood | Impact | Contingency | Owner |
|---|---|---|---|---|
| | | | | |

*Risk-based testing is the only defensible way to allocate finite test effort. Uniform coverage across a system whose components carry wildly different consequences spends the same money on the payment engine and the preferences page.*

---

## 6. Test strategy

*How you will test, given the risks above. The core of the plan.*

*If your organisation has a standing [test strategy](../foundations/test-strategy.md), reference it and record only the deviations here. 29119-3 added organisational-level test documentation precisely so project plans stop restating company policy from scratch.*

### Test levels

*What each level tests, who runs it, and what it may assume the level below has covered.*

| Level | Tests | Run by | Entry criteria | Exit criteria |
|---|---|---|---|---|
| *Component* | *Units against detailed design* | *Developers* | *Code complete, review passed* | *Coverage target met, no open blockers* |
| *Integration* | *Interfaces between components* | *Developers* | *Components passed* | *All interfaces exercised* |
| *System* | *The whole system against the specification* | *Test team* | *Integration passed, environment ready* | *All planned cases run, exit thresholds met* |
| *Acceptance* | *Against the business need and the contract* | *Business* | *System testing signed off* | *See the [UAT plan](user-acceptance-test-plan.md)* |

*The overlap question is the one worth spending time on. Where two levels both test something, decide which owns it. Where neither does, you have found a gap while it is still cheap.*

### Test types

*Which of these apply, and at which level. State the ones you are not doing and why.*

*Functional, performance, security, usability, accessibility, compatibility, installation, recovery, data migration, regression, and any regulated verification your standard names.*

### Test design techniques

*How cases are derived, so coverage is arguable rather than intuitive: equivalence partitioning, boundary values, decision tables, state transition, use case, risk-based exploratory.*

*Naming the technique is what lets a reviewer challenge coverage. "We tested it thoroughly" cannot be challenged, which is the same as saying it cannot be checked.*

### Entry and exit criteria

*Measurable, decided now. Criteria written during the crisis they were meant to prevent are negotiated, not applied.*

**Suspension and resumption.** *When testing stops before it is finished, and what must be true to restart. Usually a blocker rate or an environment failure. Without this, a broken build burns a week of tester time before anyone calls it.*

### Regression approach

*What is re-run after a change, how it is selected, and how much of it is automated. This is where most long-lived test effort goes, and plans that omit it underestimate the schedule by a wide margin.*

---

## 7. Traceability

*How test cases link to requirements, and how the [traceability matrix](requirements-traceability-matrix.md) is produced.*

*IEEE 829-2008 required a test traceability matrix in every level test plan, which remains a good rule outside regulated work. State the mechanism, not the intention: requirement identifiers as metadata in the test management tool, reported at each gate.*

---

## 8. Test environments and data

**Environments.** *Each one, what it represents, who owns it, how it is provisioned and refreshed, and how it differs from production. Differences are where late defects hide, so list them rather than claiming parity.*

**Test data.** *Where it comes from, how much, how it is refreshed, and how personal data is handled. Production data copied into a test environment is a compliance incident waiting for an audit. If you mask, say how, and say who verified the masking works.*

---

## 9. Defect management

**Severity and priority.** *Two different scales. Severity is technical impact; priority is fixing order. Define both, because a system that conflates them lets the loudest stakeholder set severity.*

| Severity | Definition | Response |
|---|---|---|
| *1 Critical* | *No workaround, blocks a core business function* | *Fix before release, always* |
| *2 High* | *Major function impaired, workaround exists* | *Fix before release unless waived* |
| *3 Medium* | *Minor function impaired* | *Fix or defer with agreement* |
| *4 Low* | *Cosmetic or trivial* | *Backlog* |

**Workflow.** *Raise, triage, assign, fix, retest, close. Who does each step, and the target time for triage.*

**Anomaly resolution.** *What happens when the defect is in the requirement rather than the code. This route ends in a [change request](change-request.md), and a plan without it turns specification errors into unfixable defects that sit open forever.*

---

## 10. Activities, schedule and resources

*Test activities in sequence, with dependencies and dates. Staff, skills, training, tools, licences, environments.*

*State the critical path through testing explicitly. Test schedules compress under delivery pressure and the compression is applied to whatever is at the end, which is usually regression and non-functional testing.*

---

## 11. Reporting

*What is reported, to whom, how often, and in what form.*

*Progress reporting during execution: cases run, passed, failed, blocked, defects by severity, coverage against the matrix.*

*29119-3 also defines a **test completion report** at the end, whose two most useful sections are the ones teams skip: **residual risks**, meaning what was not tested and what could therefore still be wrong, and **lessons learned**. Write the residual risk section before the release decision, not after it, because it is the input to that decision.*

---

## Notes on using this template

*Delete this section too.*

**Plan by risk, not by symmetry.** Equal test effort across unequal components is the default outcome of planning by structure, and it is always wrong. The risk register in section 5 is what makes the allocation defensible when someone asks why you spent three weeks on one module.

**Exit criteria set before execution are the whole point.** Every criterion here will be argued against at the moment it bites, by people under delivery pressure. That is expected. The value is that the argument is explicit and someone has to sign the waiver.

**Do not write a level test plan that repeats this one.** Separate plans are worth it only when levels are run by different organisations or on different schedules. Otherwise put the level detail in section 6 and keep one document that stays current.

**Residual risk is the deliverable.** A test report saying everything passed tells the release decision nothing it did not assume. A report saying what was not covered, and what could therefore be wrong, is the only part of testing that informs a decision someone is accountable for.

**Where this lives:** a test management tool, linked to the requirements. 29119-3 requires identifier, approval authority, change history and status on every test document, which tools supply natively and a wiki page does not. Test code belongs in the repository with the code it tests.
