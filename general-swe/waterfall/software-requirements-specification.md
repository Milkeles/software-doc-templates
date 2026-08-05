# Software requirements specification: {System}

*Also called: SRS, Requirements Specification.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Document ID** | *Unique identifier. Required by ISO/IEC/IEEE 29148 clause 9.2.1.* |
| **Version** | |
| **Status** | *Draft / In review / Approved / Superseded* |
| **Author** | |
| **Approved by** | *Name and role. The person accountable, not the person who typed it.* |
| **Approval date** | YYYY-MM-DD |
| **Baseline** | *Which baseline this becomes on approval, and what change control applies after.* |

*Follows ISO/IEC/IEEE 29148:2018 clause 9.6. That standard replaced IEEE 830, which was withdrawn in October 2024. If your contract names IEEE 830, this structure still satisfies it, with more.*

*The one thing 29148 adds that IEEE 830 lacked: every requirement carries its verification method. That single column is what connects this document to the test plan and lets the [traceability matrix](requirements-traceability-matrix.md) be generated rather than invented later.*

---

## Change history

*Required for any controlled document. If this lives in a tool that keeps history, link it and delete the table.*

| Version | Date | Change | Author | Approved by |
|---|---|---|---|---|
| | | | | |

---

## 1. Purpose

*What this document specifies and who it is for. Two or three sentences.*

*Name the audience precisely. A specification written for a supplier, a test team and an auditor at once usually serves none of them.*

## 2. Scope

*The software being specified, what it does, what it does not do, and the benefit it delivers.*

**Out of scope.** *List explicitly. The out-of-scope list prevents more disputes than the in-scope list, because scope arguments are almost always about the boundary rather than the centre.*

## 3. Definitions, acronyms and references

*Terms whose meaning is contested or domain-specific. Link the [glossary](../foundations/glossary.md) rather than duplicating it.*

*References: the contract, the standards claimed, the stakeholder requirements this derives from, upstream specifications. Give each an identifier and a version. A reference to "the security policy" without a version is not traceable.*

---

## 4. Product perspective

*Where this system sits. What it replaces, what it integrates with, what constrains it.*

*A context diagram belongs here. One page showing the system, its external actors and its interfaces answers more questions than three pages of prose.*

## 5. Product functions

*A summary of what the system does, at a level a stakeholder can read. Not the requirements themselves.*

*This section exists so a reader can orient before reading section 9. Keep it to a page.*

## 6. User characteristics

*Who uses the system and what you are assuming about them: expertise, training, frequency of use, accessibility needs.*

*Assumptions about users become defects when wrong. Writing them down makes them challengeable.*

## 7. Limitations

*What the system may not do, and why. Regulatory prohibitions, hardware ceilings, licensing restrictions, deliberate exclusions.*

## 8. Assumptions and dependencies

*Things taken as true that are outside your control, and what breaks if they turn out false.*

*Give each one an owner and a date by which it will be confirmed. An unconfirmed assumption held for six months is a risk that nobody is watching.*

| Assumption or dependency | If it is wrong | Owner | Confirm by |
|---|---|---|---|
| | | | |

---

## 9. Specified requirements

*The substance. Everything above is context for this.*

*Group by whatever makes the set easiest to review: by feature, by user class, by mode, by external interface. 29148 does not mandate an order and IEEE 830's annex offered eight alternatives. Pick one and stay in it.*

### Requirement format
*Each requirement is one row. Every column is mandatory. A blank verification column means the requirement is not finished.*

| ID | Requirement | Rationale | Priority | Source | Verified by |
|---|---|---|---|---|---|
| *SRS-014* | *The system shall lock an account after 5 consecutive failed authentication attempts within 15 minutes.* | *Security policy SEC-3, brute-force mitigation* | *Shall* | *StRS-007* | *Test, TC-091* |

**ID.** *Stable and never reused. When a requirement is deleted, the identifier retires with it. Renumbering a specification destroys every trace pointing at it.*

**Requirement.** *One requirement per row. The 29148 characteristic is "singular": "includes only one requirement with no use of conjunctions." A requirement joined by "and" cannot be individually traced, tested, prioritised or changed.*

**Rationale.** *Why the requirement exists. This is pre-specification traceability and it is the half teams skip. Two years on, nobody can tell whether a requirement is load-bearing or a preference someone had, and so nothing can safely be removed.*

**Priority.** *Use "shall", "should", "may" consistently, or a ranked scheme. 29148 and IEEE 830 both expect requirements to be ranked for importance or stability. Everything being mandatory is the same as nothing being ranked.*

**Source.** *The stakeholder requirement, contract clause, regulation or hazard this derives from. Upward traceability.*

**Verified by.** *How you will know it is met: test, inspection, analysis, or demonstration. Downward traceability into the test plan.*

### Requirement characteristics to check before approval

*29148:2018 clause 5.2.5 gives nine characteristics for an individual requirement. Check each one before it is baselined, because after baselining every correction costs a [change request](change-request.md).*

| Characteristic | The check |
|---|---|
| *Necessary* | *Removing it would leave a deficiency* |
| *Appropriate* | *Stated at the right level of abstraction for this document* |
| *Unambiguous* | *"can be interpreted in only one way"* |
| *Complete* | *Needs no further information to be actioned* |
| *Singular* | *One requirement, no conjunctions* |
| *Feasible* | *Achievable within known constraints* |
| *Verifiable* | *A method exists to prove it was met* |
| *Correct* | *An accurate statement of the actual need* |
| *Conforming* | *Follows the agreed template and style* |

*The set as a whole must also be complete, consistent, feasible, comprehensible and able to be validated. "Complete" for a set has a specific meaning worth quoting to anyone tempted to approve early: the set "contains no To Be Defined (TBD), To Be Specified (TBS), or To Be Resolved (TBR) clauses."*

*Ambiguity has known offenders. Search the document for these before review: "user-friendly", "fast", "efficient", "as appropriate", "etc.", "if possible", "and/or", "support", "handle", "process". Each one is a dispute deferred to acceptance testing.*

---

## 10. External interfaces

*Every interface across the system boundary: user, hardware, software, communications.*

*For each: name, purpose, protocol, data format, error behaviour, and the document that governs it. Where an interface control document exists, reference it rather than restating it, and say which version.*

| Interface | Type | Governed by | Version |
|---|---|---|---|
| | | | |

---

## 11. Quality and performance requirements

*Requirements about how well the system does things, not what it does. Same table format as section 9. They are requirements, not aspirations, and they carry verification methods like everything else.*

*Cover the ones that apply, and say when one does not so a reviewer knows it was considered rather than forgotten.*

- **Performance.** *Throughput, latency, capacity, concurrency. Each with a number and the load condition it holds under. "The system shall be fast" is not a requirement; "95% of search requests complete within 300ms at 500 concurrent users" is.*
- **Usability.** *Task completion, error rates, training time, accessibility conformance level.*
- **Reliability and availability.** *Uptime target, mean time between failures, degraded-mode behaviour.*
- **Security.** *Authentication, authorisation, encryption, audit, retention. Link the [threat model](../foundations/threat-model.md) rather than reproducing its analysis.*
- **Maintainability and portability.** *Where a change is expected, and how hard it must be.*
- **Data.** *Retention, integrity, residency, backup and recovery objectives.*

## 12. Design and implementation constraints

*Things the design must obey that are not derived from a need: mandated platforms, standards to comply with, existing systems to fit, regulatory obligations.*

*Constraints are worth separating from requirements because they have no rationale you can argue with. Mixing them in makes the requirement set look more negotiable than it is.*

---

## 13. Apportioning of requirements

*Requirements deferred to a later release or a later system. Say which, and to what.*

*Named deferral is what stops a scope negotiation reopening as a defect report. Leaving something out silently means it will be raised at acceptance.*

---

## 14. Verification

*How the requirement set as a whole will be verified, and by whom. Individual methods are in the tables above; this is the strategy connecting them.*

*Reference the [master test plan](master-test-plan.md) and state how the [traceability matrix](requirements-traceability-matrix.md) will be produced and kept current. If your answer is "manually", expect it to be wrong within a month.*

---

## 15. Supporting information

*Anything a reader needs that is not a requirement: background, analysis, worked examples, models, calculations. Appendices.*

*Keep it out of section 9. Requirements mixed with explanation cannot be extracted, reviewed or traced as a set.*

---

## Notes on using this template

*Delete this section too.*

**Requirements are not design.** If a row says how rather than what, it has removed a choice from the designer without being accountable for the consequence. The exception is a genuine constraint, which belongs in section 12 where it is visible as one.

**Write the verification column first when you are stuck.** If you cannot say how you would prove a requirement was met, the requirement is not yet a requirement. This test catches more bad requirements than any review checklist.

**Do not aim for completeness on the first pass.** Aim for a reviewable set with the gaps marked. A specification with fifteen honest TBDs is workable; one with fifteen guesses presented as decisions is not, and you will not be able to tell which rows to trust.

**Approval is the expensive moment.** Once baselined, every correction costs a change request, an impact assessment and an approval. Spend the review time before that line, not after it.

**Where this lives:** a requirements management tool or eQMS if the work is regulated, because approval of record, revision status and a non-obscuring audit trail are required and plain version control does not provide them. Docs-as-code otherwise, where pull request review is the approval record and the diff is the change history.

---

## Related documents

- [`../requirements/vision-and-scope.md`](../requirements/vision-and-scope.md). The document that comes before this one: vision and scope answers why the project exists, this document answers what the software must do
- [`../requirements/non-functional-requirements.md`](../requirements/non-functional-requirements.md). Fuller treatment of section 11's quality and performance requirements, worth splitting out when the qualities are the hard part
- [`requirements-traceability-matrix.md`](requirements-traceability-matrix.md). Generated from this document's verification column, never invented afterwards
- [`master-test-plan.md`](master-test-plan.md). The verification strategy this specification's requirements feed into
- [`change-request.md`](change-request.md). What every correction costs once this specification is baselined
