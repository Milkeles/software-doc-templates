# Test cases: {Feature or area}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *Feature, requirement IDs, or area under test.* |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |
| **Where these run** | *CI job, test management tool, or manual.* |

*Write this only for the cases a person executes or a person must audit. Automated tests are their own specification: the code is the document, and a second copy in prose will drift within a month. See [`test-strategy.md`](test-strategy.md) for what gets tested where.*

---

## Before you write any of these

*Predesigned test cases are not free and are not always better. The strongest evidence available compares them directly against exploratory testing, where design and execution happen at once.*

*Itkonen and Mantyla replicated an earlier experiment with 51 participants on the jEdit editor, removing the original time limit. Their result, in their words: "there is no difference in the defect detection effectiveness between ET and TCT", exploratory testing "is more efficient by requiring less design effort", and test-case-based testing "produces more false-positive defect reports than ET". The original study used 79 participants and reached the same place.*

*So do not write test cases to find more defects. On that measure they do not. The same authors give the honest reason to write them anyway: "we recognize that TCT has other benefits over ET in managing and controlling testing in large organizations."*

**Write a test case when at least one is true.**

| Reason | Example |
|---|---|
| Someone outside the team must see what was checked | Regulated release, customer acceptance, audit |
| The same check must run identically on a schedule | Quarterly disaster recovery drill |
| The steps are long enough that a person will get them wrong | 14-step billing reconciliation |
| It is the specification for an automated test not yet written | Backlog of cases waiting for automation |
| Losing the knowledge would be expensive | One person knows how to test the payment gateway |

**Otherwise, charter a session instead.** Give the tester a mission and let them design as they go. Record it with a session sheet in the [test summary report](test-summary-report.md). It costs less design effort for the same defects.

---

## The case list

*One row per case. Keep the summary short enough to scan, because this table is how people find a case, not how they run it.*

| ID | Summary | Verifies | Priority | Type | Status |
|---|---|---|---|---|---|
| *TC-104* | *Refund exceeding original charge is rejected* | *REQ-31* | *High* | *Manual* | *Active* |
| *TC-105* | *Refund in a closed accounting period is rejected* | *REQ-31* | *High* | *Automated* | *Active* |
| *TC-106* | *Partial refund updates the ledger twice* | *REQ-33* | *Medium* | *Manual* | *Retired 2026-02* |

*The **Verifies** column is the one that earns the table. A case that verifies nothing is a case nobody can decide to delete. If you keep a [requirements traceability matrix](../waterfall/requirements-traceability-matrix.md), this column is its other half.*

*Retire cases in place, with a date. Deleting them silently loses the answer to "did we ever test this".*

---

## Each case

*ISO/IEC/IEEE 29119-3:2021 defines a test case specification as, in full, "documentation of a set of one or more test cases". It sets no field list you are obliged to copy, and it says explicitly that "test documentation titles, headings and layout described in this document may be modified". What follows is the smallest set that survives being handed to someone else.*

### TC-104 Refund exceeding original charge is rejected

| | |
|---|---|
| **Verifies** | REQ-31 |
| **Priority** | High |
| **Preconditions** | *A settled order exists with a single charge of 40.00 EUR. Operator has the `refund` role.* |
| **Test data** | *Order `ORD-88213` on the seed dataset, or any settled single-charge order.* |
| **Environment** | *Staging, with the payment provider in sandbox mode.* |

**Steps**

| # | Action | Expected result |
|---|---|---|
| 1 | *Open the order in the operations console* | *Order shows status Settled, charged 40.00 EUR* |
| 2 | *Enter a refund of 45.00 EUR and submit* | *Refund is rejected. Message names the maximum refundable amount. No provider call is made* |
| 3 | *Reload the order* | *Order still shows Settled, refunded 0.00 EUR* |

**Postconditions.** *State what is left behind and what needs cleaning up. A case that leaves the account in a changed state and does not say so will break the next case that runs.*

---

## Pick the right abstraction level

*This is the failure the experiment above identified by name. In test-case-based testing, "the problems were related to correct abstraction levels of test cases".*

*Too concrete and the case breaks every time a button moves, so people stop trusting it and stop running it. Too abstract and two testers execute it differently, so a pass means nothing.*

| Too concrete | Too abstract | About right |
|---|---|---|
| *Click the blue Submit button at the bottom right* | *Try an invalid refund* | *Submit a refund larger than the original charge* |
| *Expect the toast reading "Error 4021"* | *Expect it to fail* | *Expect rejection, with the maximum refundable amount shown* |

**The test.** *Could a competent new joiner execute this without asking you a question, and would it still pass after a redesign that did not change behaviour? If yes to both, the level is right.*

---

## Guard against false positives

*The other measured weakness of predesigned cases: they produce more false-positive defect reports than exploratory testing. A case written six months ago against behaviour that has legitimately changed still fails, and the tester dutifully files a bug against a working product.*

*Every false positive costs a developer an investigation and costs the test suite some of its authority.*

- **Date the expectation, not just the case.** When a case fails, the first question is whether the product changed on purpose.
- **Say which requirement the expected result comes from.** If the requirement changed and the case did not, that is visible in one step.
- **Make failure reporting go through a person who knows the feature**, or through the [bug report](bug-report.md) checklist, before it reaches the backlog.

---

## What these cases do not cover

*Name it. A case list read as complete is more dangerous than no case list, because it converts an unknown into a false assurance.*

*Coverage figures do not fix this. Inozemtseva and Holmes generated 31,000 test suites across five systems of up to 724,000 lines and concluded that coverage "should not be used as a quality target because it is not a good indicator of test suite effectiveness". Use it to find untested areas. Do not use it to certify tested ones.*

---

## Notes on using this template

*Delete this section too.*

**Fewer cases, better maintained.** A hundred stale cases are worse than fifteen current ones, because someone has to execute all hundred to find out which fifteen mattered. Retire aggressively.

**Do not write cases for automated tests.** Name the test file in the case list and stop. The moment the prose and the code disagree, both become untrustworthy and nobody can tell which one is wrong.

**Number them once and never renumber.** IDs appear in bug reports, release notes and audit records that you do not control. A renumbering breaks all of them silently.

**Where this lives:** in the repository beside the tests, if the cases are executable or destined for automation. In a test management tool if execution results must be recorded per run, per build, and shown to someone outside the team. Splitting them across both is the common failure, and it ends with two lists that disagree.

---

## Related documents

- [`test-strategy.md`](test-strategy.md). What gets tested at which level, which decides whether a case belongs here at all
- [`bug-report.md`](bug-report.md). What a failing case turns into
- [`test-summary-report.md`](test-summary-report.md). What the run of these cases is reported as
- [`../waterfall/master-test-plan.md`](../waterfall/master-test-plan.md). The project-scoped plan with a schedule, where fixed-scope work needs one
- [`../waterfall/requirements-traceability-matrix.md`](../waterfall/requirements-traceability-matrix.md). Where the **Verifies** column is reconciled against the requirements
