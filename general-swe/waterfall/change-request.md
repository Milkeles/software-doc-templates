# Change request: {CR-ID}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **CR ID** | |
| **Raised by** | *Name and role.* |
| **Date raised** | YYYY-MM-DD |
| **Type** | *Standard (pre-authorised) / Normal / Emergency* |
| **Related problem report** | *The defect, incident or finding that prompted this, if any.* |
| **Status** | *Draft / Assessed / Approved / Rejected / Implemented / Closed* |

*Used when something baselined must change. If nothing is baselined, you do not need this document; you need a backlog item.*

*The minimum a standard actually requires is smaller than most forms. IEC 62304 clause 8.2.4 asks for records of the relationships between the change request, the relevant problem report, and the approval, and it asks for this at all safety classes. That triangle is the requirement. Everything else on this page is local policy, and you should be able to say what each field is for.*

---

## 1. What is changing

*The change in plain language, in the terms of the baseline it affects. One paragraph.*

*Write what the state will be after, not just what you are doing. "Change the lockout threshold from 5 attempts to 3" is reviewable. "Improve account security" is not.*

**Baseline affected.** *Which document and version: [specification](software-requirements-specification.md), [design](software-design-description.md), interface control document, configuration item.*

**Items affected.** *Specific identifiers. SRS-014, DE-07, TC-091. Vague scope is what makes impact assessment guesswork.*

---

## 2. Why

*The reason, and the consequence of not doing it.*

*Both halves. A justification with no stated cost of inaction gives the approver nothing to weigh, and every change then looks equally worth doing.*

**Category.** *A small fixed set so changes group and can be counted: defect correction, requirement error, scope addition, regulatory change, technical constraint discovered, obsolescence, performance shortfall.*

*Counting these is how you find out whether your requirements process is working. A quarter dominated by "requirement error" is a finding about the specification phase, not about the changes.*

---

## 3. Impact assessment

*Completed by someone competent to assess it, not by the requester. This is the section the whole process exists for.*

| Dimension | Impact | Assessed by |
|---|---|---|
| *Requirements* | *Which change, which are added or removed* | |
| *Design* | *Which elements* | |
| *Code* | *Which components* | |
| *Tests* | *Which cases change, which must be re-run* | |
| *Documents* | *Which need reissue and re-approval* | |
| *Interfaces* | *Anything crossing a boundary another party owns* | |
| *Schedule* | *Days, and whether the critical path moves* | |
| *Cost* | | |
| *Risk* | *New risks introduced, existing risks changed* | |
| *Safety* | *Any hazard analysis affected. If yes, this is not a routine change* | |
| *Security* | *Any trust boundary or control affected* | |
| *Regulatory* | *Whether this affects a submission, certification or validated state* | |

**Regression scope.** *What must be retested, and why that set and not a larger one. Under-scoping regression is the most common way a well-controlled change causes an incident.*

**Second-order effects.** *What else assumes the current behaviour. Downstream consumers, saved reports, integrations, trained users, documentation you do not own.*

*This row is where the value is. Most changes fail through something nobody thought to ask about, and the question that finds it is "who depends on this being the way it is now?"*

---

## 4. Implementation approach

*How the change will be made, in steps. Enough detail that the approver knows what they are authorising and the implementer knows what was agreed.*

**Verification.** *How you will confirm the change worked. Which tests, which acceptance criteria.*

**Rollback.** *How to undo it, how long that takes, and the point after which it stops being possible.*

*A change with no rollback is not forbidden, but it is a different decision and the approver must know they are making it. State the point of no return explicitly: after a data migration, after an external party consumes the new interface, after a release to production.*

**Timing.** *Proposed window, and why. Dependencies, freeze periods, business calendar.*

---

## 5. Decision

| | |
|---|---|
| **Change authority** | *The named person or role with authority for this change at this risk level.* |
| **Decision** | *Approved / Approved with conditions / Rejected / Deferred* |
| **Date** | |
| **Conditions or reasons** | |

*Record rejections and their reasons with the same care as approvals. PMBOK's change log includes both, and the rejected half is the half everyone drops. It is also the half that answers the question a future team will actually ask: was this considered and turned down, or did nobody think of it?*

---

## 6. Closure

*Completed after implementation. A change request left open after the work is done is the reason nobody trusts the change log.*

| | |
|---|---|
| **Implemented on** | |
| **Verified by** | *Name, and the evidence.* |
| **Documents reissued** | *Which, and at which version.* |
| **Traceability updated** | *Confirm the [matrix](requirements-traceability-matrix.md) reflects the change.* |
| **Post-implementation review** | *Did it do what it was supposed to, and did anything unexpected follow?* |

---

## Notes on using this template

*Delete this section too.*

**Pre-authorise your repeatable changes.** ITIL 4 defines three change types: standard, pre-approved and repeatable with no per-instance authorisation; normal, assessed and authorised with escalation by risk; and emergency, expedited with documentation sometimes following execution. Getting your routine low-risk changes classified as standard is the single highest-value improvement available to most change processes, because it removes the queue from the changes that make up most of the volume and none of the risk.

**You do not need a CAB.** ITIL 4 replaced the monolithic change advisory board with a **change authority** and explicit delegated authority, deliberately decentralised. Routing low-risk changes through a weekly board is treated as an anti-pattern: it adds delay without improving change quality, and it teaches people to batch changes to hit the meeting, which makes each one larger and riskier. Many plan-driven templates still assume a CAB reviewing everything. That assumption is no longer even ITIL's position.

**The emergency route needs to exist before the emergency.** If there is no defined expedited path, people will bypass the process entirely and you will lose the record, which is worse than a fast approval. Define who may authorise an emergency change, and require the documentation to follow within a stated period.

**Approval must be an immutable record.** A comment on a ticket that anyone can edit is not an approval. Where 21 CFR Part 11 or an equivalent applies, the signature must carry the name, the date and time and the meaning of signing, and the audit trail must not obscure what was previously recorded. That last property is why a git history alone does not serve here: it is rewritable by design.

**Count what comes through.** The change log is data about your process, not just about the changes. High volume in one category points at the phase that produced it, and that is a fixable problem rather than a permanent cost.

**Where this lives:** an ITSM or eQMS workflow tool where approvals are immutable and linked to the problem report, per IEC 62304 §8.2.4. An issue tracker is sufficient where nothing is regulated, provided the approval is recorded as a state transition and not as a comment.

---

## Related documents

- [`software-requirements-specification.md`](software-requirements-specification.md). One of the baselines a change request amends once it is approved
- [`software-design-description.md`](software-design-description.md). The other baseline a change request amends; the impact assessment names which design elements move
- [`requirements-traceability-matrix.md`](requirements-traceability-matrix.md). Updated on closure so the chain reflects what actually changed
- [`phase-gate-review.md`](phase-gate-review.md). Fixes the baseline that change control then protects
- [`../foundations/bug-report.md`](../foundations/bug-report.md). The problem report IEC 62304 §8.2.4 expects a change request to link back to
