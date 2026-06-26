# Software design description: {System}

*Also called: SDD, Software Design Document.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Document ID** | |
| **Version** | |
| **Status** | *Draft / In review / Approved / Superseded* |
| **Specification** | *The [requirements specification](software-requirements-specification.md) and version this design satisfies.* |
| **Approved by** | *The design authority. Implementation is not authorised until this is signed.* |
| **Approval date** | YYYY-MM-DD |

*Follows IEEE 1016-2009, which describes a design through **viewpoints** selected to address identified **stakeholder concerns**. That selection rule is what keeps the document finite.*

*This is a gate artefact. It exists so someone can approve that the design satisfies the requirements, before code is written. If you want a document that helps a reader understand the system, write an [architecture overview](../foundations/architecture-overview.md) instead. The two have different jobs and trying to make one document do both produces a document that is too formal to read and too vague to approve.*

---

## Change history

| Version | Date | Change | Author | Approved by |
|---|---|---|---|---|
| | | | | |

---

## 1. Introduction

*What this design covers, what it does not, and which requirements it addresses. Half a page.*

*State the scope boundary explicitly. A design description that quietly covers three subsystems is unreviewable, because no single reviewer is competent across all of it.*

---

## 2. Design stakeholders and their concerns

*Who has a stake in this design and what each one needs to get out of it. Fill this in before choosing viewpoints, because the concerns decide which viewpoints you need.*

*Do this properly and the rest of the document writes itself. Skip it and you will produce every diagram you know how to draw.*

| Stakeholder | Concern | Addressed by viewpoint |
|---|---|---|
| *Implementers* | *What to build, and what the interfaces are* | *Composition, interface* |
| *Test lead* | *What can be tested at which level* | *Composition, interaction* |
| *Security reviewer* | *Trust boundaries and data at rest* | *Context, information* |
| *Operations* | *Failure modes and recovery* | *State dynamics, resource* |
| *Auditor or assessor* | *That every requirement has a design element* | *Traceability, section 5* |

**Every concern must be framed by at least one viewpoint.** *That is the coverage rule, borrowed from ISO/IEC/IEEE 42010. A concern with no viewpoint is a stakeholder who will not be able to review this document.*

**The converse rule matters more.** *A viewpoint with no concern behind it is pages nobody reads and nobody maintains. Delete it.*

---

## 3. Design viewpoints in use

*Which of the standard viewpoints you are using, and why. IEEE 1016 defines twelve; a typical design needs four to six.*

| Viewpoint | What it shows | Using it? | Why or why not |
|---|---|---|---|
| *Context* | *The system boundary and external actors* | *Yes* | *Trust boundaries are a concern* |
| *Composition* | *Decomposition into parts* | *Yes* | *Drives work allocation and test levels* |
| *Logical* | *Static structure, types, relationships* | | |
| *Dependency* | *What relies on what; coupling* | | |
| *Information* | *Persistent data, structure, lifecycle* | | |
| *Patterns use* | *Design patterns applied* | | |
| *Interface* | *Services offered and required* | | |
| *Structure* | *Internal construction of each element* | | |
| *Interaction* | *How elements collaborate at runtime* | | |
| *State dynamics* | *States, transitions, failure modes* | | |
| *Algorithm* | *Procedural logic where it is not obvious* | | |
| *Resource* | *Use of memory, threads, connections, budget* | | |

*Filling in the "why not" column is the point of this table. It shows a reviewer that an absent viewpoint was a decision.*

---

## 4. Design views

*One section per viewpoint selected above. Each contains models covering the whole system from that viewpoint.*

*Write these as sections 4.1, 4.2 and so on, named after the viewpoint. For each:*

- *the models: diagrams, tables, schemas, with a notation stated;*
- *what the models do not show, so nobody reads an omission as an assertion;*
- *known issues and open points in this view.*

*Recording known issues in the view is required by the standard and is the honest alternative to a document that looks finished. An approved design with three recorded open points is safer than one with three unrecorded ones.*

### 4.x {Viewpoint name}

**Concerns addressed.** *From section 2.*

**Notation.** *UML, C4, ERD, a house convention. Say which, and where the reader can learn it. A diagram in an unstated notation is a picture.*

**Models.**

**What this view does not cover.**

**Known issues in this view.**

---

## 5. Design elements

*The named parts the design is made of, and what each is responsible for. This is the table the traceability matrix points at.*

*IEEE 1016 recognises design entities, relationships, attributes and constraints. In practice, one table of elements with their responsibilities and their requirement links carries most of the value.*

| Element ID | Element | Responsibility | Satisfies requirements | Verified at |
|---|---|---|---|---|
| *DE-07* | *Session store* | *Issues, validates and revokes session tokens* | *SRS-014, SRS-015* | *Unit, integration* |

*Two checks before approval, both of which the [traceability matrix](requirements-traceability-matrix.md) should perform automatically:*

- *Every requirement appears in at least one element's row. A requirement with no design element is unimplemented.*
- *Every element traces back to at least one requirement. An element with no requirement is either gold-plating or a requirement nobody wrote down, and both are worth finding before it is built.*

---

## 6. Design rationale

*Why this design and not the alternatives. The section most often left out, and the one that costs most when it is.*

*Without rationale, the next team either preserves a constraint that has expired or removes one that is load-bearing, and cannot tell which they are doing.*

*For decisions with consequences beyond this document, write an [architecture decision record](../foundations/architecture-decision-record.md) and link it. Keep the rationale here for choices local to this design.*

| Decision | Alternatives considered | Chosen because | Reversible? |
|---|---|---|---|
| | | | |

---

## 7. Design constraints and their sources

*What the design was not free to choose, and where each constraint came from: a requirement, a standard, an existing system, a contract, a hardware limit.*

*Separating imposed constraints from chosen design is what lets a future reviewer tell which parts are open to change.*

---

## 8. Verification approach

*How the design will be shown to satisfy the requirements: review, analysis, prototype, or a combination. Who performs it and what evidence it produces.*

*In a regulated context this section is the input to the design review gate. Name the [phase gate](phase-gate-review.md) that consumes it.*

---

## Notes on using this template

*Delete this section too.*

**Select viewpoints, do not complete them.** IEEE 1016 offers twelve and expects you to use the ones your stakeholders' concerns require. A design description covering all twelve is a sign that nobody identified the concerns, and it will be approved without being read.

**Design to the level where the next decision is safe, and stop.** The purpose is to authorise implementation, not to pre-specify it. Detail beyond that point is a guess about the future that someone will have to maintain.

**Record what the design does not decide.** Deliberately deferred choices, and where they will be made. This is what stops an implementer treating a gap as permission and a reviewer treating it as an oversight.

**IEEE 1016-2009 is aging.** It has no successor we can find, so it remains the current reference, but its viewpoint list predates most cloud and distributed system practice. Add a deployment or resource view where the standard's list falls short; conformance is about addressing the concerns, not about the twelve names.

**Where this lives:** docs-as-code, versioned with the code it describes. This is the document that drifts fastest when separated from the implementation, because every refactor invalidates a little of it. Where a signed approval of record is required, keep the signed release in the eQMS and the working document in the repository, and make the signed version reference a commit.

---

## Related documents

- [`software-requirements-specification.md`](software-requirements-specification.md). What this design must satisfy before the design authority signs it
- [`requirements-traceability-matrix.md`](requirements-traceability-matrix.md). Checks automatically that every requirement has an element and every element a requirement
- [`../foundations/architecture-overview.md`](../foundations/architecture-overview.md). The document to write instead if the goal is helping a reader understand the system, not securing a design approval
- [`../foundations/architecture-decision-record.md`](../foundations/architecture-decision-record.md). Where to record a decision whose consequences reach beyond this design
- [`phase-gate-review.md`](phase-gate-review.md). The gate that consumes this document's verification approach and authorises implementation
- [`../foundations/technical-design-document.md`](../foundations/technical-design-document.md). The same job, done at ordinary weight: pick this one instead when there is no phase gate, regulator, or auditor requiring a signed baseline before code starts
