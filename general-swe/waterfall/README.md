# Waterfall and plan-driven development

Documents for teams whose scope is fixed before work starts and who must prove, later, that they built what was specified.

Medical devices, avionics, automotive, rail, pharmaceutical systems, defence, and any fixed-price contract with an acceptance clause. Also anyone whose auditor, notified body or customer will read the documentation as evidence rather than as help.

---

## First: Royce did not propose the waterfall

Worth getting right, because the caricature makes teams either adopt this badly or dismiss it entirely.

Winston Royce's 1970 paper, *Managing the Development of Large Software Systems*, is the origin of the sequential diagram. **The word "waterfall" appears in it zero times.** The label was attached later; its first widely cited appearance in print is Bell and Thayer's 1976 ICSE paper.

More importantly, Royce drew the pure sequential model and then wrote, directly beneath it:

> "I believe in this concept, but the implementation described above is risky and invites failure."

His actual argument is that phased development is sound and that the single-pass version of it fails, because design iterations are never confined to adjacent phases. He then prescribes five additions:

| | |
|---|---|
| 1 | Program design comes first |
| 2 | Document the design |
| 3 | Do it twice |
| 4 | Plan, control and monitor testing |
| 5 | Involve the customer |

"Do it twice" means building the thing once as a pilot, at roughly a third of the schedule, and delivering the second version. Royce was arguing for prototyping in 1970. The model taught as "waterfall" is his Figure 2, the one he rejected, with the corrections stripped off.

He also scoped his own prescription honestly, in the summary:

> "If the relatively simpler process without the five complexities described here would work successfully, then of course the additional money is not well spent. In my experience, however, the simpler method has never worked on large software development efforts."

Both halves of that sentence matter. The documentation in this group is expensive. It pays for itself on large, critical, stable work and wastes money elsewhere.

---

## When plan-driven genuinely wins

The most useful answer is Boehm and Turner's, from *Balancing Agility and Discipline* (2003). They rate a project on five factors:

| Factor | Plan-driven fits when | Agile fits when |
|---|---|---|
| **Size** | Large products and teams | Small products and teams |
| **Criticality** | Failure costs lives or large sums | Failure costs comfort or discretionary money |
| **Dynamism** | Requirements are stable | Requirements change constantly |
| **Personnel** | Experts available at definition, fewer later | Experts available continuously |
| **Culture** | People are empowered by clear policies and procedures | People are empowered by many degrees of freedom |

Their conclusion is the part people skip, and it is the reason this group is not framed as the opposite of the other groups:

> "a project which is a good fit to agile or plan-driven for four of the factors, but not the fifth, is a project in need of risk assessment and likely some mix of agile and plan-driven methods."

Most real projects score mixed. A team building a medical device runs a regulated V-model for the device software and a Kanban board for its internal tooling, and both are correct. Boehm and Turner explicitly rebut the idea that the two are unmixable: "Agile and plan-driven methods have been successfully combined in a variety of situations."

So use this group where the evidence is needed, not everywhere in the same company.

---

## What actually enforces plan-driven work

Not the lifecycle diagram. The gates.

DOD-STD-2167A, the standard most blamed for imposing waterfall on the defence industry in the late 1980s, never mandated it. Its text left development methods to the contractor and named rapid prototyping as an acceptable example. What forced sequential development was the schedule of **formal reviews and audits**, each with required deliverables, which made it impossible to code before the design document had been approved. Its 1994 replacement, MIL-STD-498, listed removing the waterfall bias as an explicit change.

The lesson carries directly into how you use these templates. **A document that no gate consumes is not a plan-driven document, it is paperwork.** Every template here should be answerable to the question: which review approves it, and what may not start until it is approved? If nothing, delete it.

This is also the honest defence of the group against the accusation that it is bureaucracy. It usually is bureaucracy, right up to the point where a regulator asks how you know your software does what the requirement said. Then it is the only answer available.

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [Software requirements specification](software-requirements-specification.md) | Scope is agreed before build, or a standard requires one | Requirements will be discovered during build | eQMS or requirements tool if regulated, docs-as-code if not |
| [Software design description](software-design-description.md) | Design must be approved before implementation, or handed to another team to build | The team designing is the team building, continuously | Docs-as-code |
| [Requirements traceability matrix](requirements-traceability-matrix.md) | Anyone will ask "is every requirement built and tested" | Nobody will ask, and nothing is safety-related | Generated from tools, never hand-kept |
| [Master test plan](master-test-plan.md) | Testing spans several levels, teams or a contract | One team tests its own work continuously | Test management tool |
| [User acceptance test plan](user-acceptance-test-plan.md) | Acceptance triggers payment, warranty or go-live | You release continuously and roll back on failure | Contract repository or eQMS, signed |
| [Change request](change-request.md) | Changing scope after a baseline is approved | Nothing is baselined | ITSM or eQMS workflow |
| [Phase gate review](phase-gate-review.md) | A named authority must approve before the next phase starts | Nobody has the authority to stop the work | eQMS or project record, signed |

Seven documents is a lot. Only the specification and the traceability matrix are load-bearing in every plan-driven context. The rest earn their place from a specific gate, contract clause or regulation, and you should be able to name which one.

---

## The V-model, and what it is actually for

The V is a way of drawing the same lifecycle so that each specification level sits opposite the test level that verifies it.

| Specification | Verified by |
|---|---|
| User or stakeholder requirements | Acceptance testing |
| System requirements | System testing |
| Architectural design | Integration testing |
| Detailed design | Unit testing |

Its value is not the shape. It is that the shape makes an omission visible: a requirement level with nothing opposite it is a level nobody is verifying.

The pharmaceutical variant, from GAMP 5, is the most formalised: user requirements are verified by Performance Qualification, functional specification by Operational Qualification, design specification by Installation Qualification. The two arms are joined by a traceability matrix, and in GAMP 5 the matrix is what makes the V a V rather than two unrelated lists.

The V is used as the structural backbone of ISO 26262 and Automotive SPICE, maps onto IEC 62304, and appears in DO-178C, EN 50128 and the German V-Modell XT.

**Two honest limits.** The V says nothing about *when* phases happen, so it is fully compatible with iteration; each increment can traverse its own V, and hybrid models that do exactly this are common. And its real weakness is the one Royce named in 1970: the right-hand side is where timing, throughput and storage constraints are first *experienced* rather than *analysed*, so late discovery forces expensive rework on the left. That is precisely why his steps 1 and 3 exist.

---

## What the trace chain actually looks like

Kanban has a board. Scrum has a board. Plan-driven work has a trace chain, and it is just as much the working surface of the method. Everything in this group is either a node on it, a baseline across it, or a record of a change to it.

```
  BASELINE   SRS rev 3, approved 2026-02-14 by J. Okafor, design authority
  ==========================================================================

   URS-014  "the user can lock the device from the handset"
      |
      +--> SYS-031 -----> ARC-007 -----> MOD-042 -----> src/lock/handler.c
      |       |              |              |
      |       v              v              v
      |   SYS-TC-118     INT-TC-052     UT-lock-04
      |
      +--> ACC-TC-009        (acceptance runs against URS-014, not SYS-031)

   URS-015  ...
```

Read it two ways. Left to right is the V-model's left arm: each level of specification decomposes into the next. Vertical is the V's right arm: each level is verified by the test level opposite it. The traceability matrix is not a separate artefact you assemble later. It is this picture, exported.

**A requirement with nothing below it is unbuilt. Code with nothing above it is unrequested.** Those are the only two questions the chain exists to answer, and both directions matter, per Gotel and Finkelstein.

**What a baseline does.** Drawing a line across the chain and naming it freezes the reference. After that line, edits are not edits. They are change requests, and they arrive with an impact assessment attached, because the chain shows what the change touches.

**Suspect links are the mechanic that makes this work.** When a baselined item is edited, requirements tools flag everything linked downstream of it as suspect until a human reviews each one. IBM DOORS and Jama Connect both call it exactly that.

```
   SYS-031 edited under CR-221
      |
      +--> ARC-007       SUSPECT   design not yet reassessed
      +--> SYS-TC-118    SUSPECT   test may no longer verify the requirement
      +--> ACC-TC-009    SUSPECT
```

This is the plan-driven equivalent of a WIP limit: a small tool constraint that makes a principle physically hard to ignore. Without it, traceability degrades silently, because a link that was correct when it was drawn stays green forever.

### What each requirement record has to carry

The template asks for these because ISO/IEC/IEEE 29148 asks for them, not to fill a form.

| Field | Why it is there |
|---|---|
| **Identifier** | Stable, never reused. Everything else links to it |
| **The requirement, singular** | No conjunctions. Two requirements joined by "and" cannot be traced, tested or changed separately |
| **Verification approach** | Inspection, analysis, demonstration or test. The field 29148 added and IEEE 830 lacked, and the one that makes the chain generatable |
| **Source and rationale** | Who asked and why. The pre-specification half, and the half everyone drops |
| **Status and baseline** | Which approved revision this belongs to |
| **Links, up and down** | The chain itself |

Leave the estimate and the assignee off. Those belong in the schedule, and putting them here makes the requirement record change for reasons that have nothing to do with the requirement.

### Setting this up in a tool

| What the method needs | Requirements tool (DOORS, Jama, Polarion) | Jira plus Confluence |
|---|---|---|
| Typed trace links | Native, with link types | Issue links, untyped by default |
| Baseline | Native, immutable snapshot | No equivalent. Fixed versions are the nearest thing and are editable |
| Suspect links on change | Native and automatic | Nothing native |
| Trace matrix | Generated view | Plugin, or exported and assembled by hand |
| Approval of record | Electronic signature with reauthentication, meaning of signing recorded | A comment. Not a signature |
| Non-rewritable history | Native | Admins can edit issue history |

The right-hand column is why the split in the next section is not a preference. If the four questions there come back yes, an issue tracker cannot answer them, and no amount of workflow configuration will change that.

For unregulated plan-driven work the right-hand column is fine, with one addition: write the started and finished definitions and the trace conventions somewhere, because the tool will not enforce them and nobody will infer them.

---

## Where these documents live, and why the answer is different here

Every other group in this repository chooses between a wiki and the repository on grounds of convenience. Here the constraint is evidential, and it is legal rather than stylistic.

**Ask four questions of each document:**

1. Does it need an **approval of record**, with a named approver and a recorded meaning of the signing?
2. Must its history be **non-rewritable**?
3. Must the **current approved revision** be provably the one in use at the point of use?
4. Will an **auditor, a notified body or a court** read it?

Any yes pushes the document toward a controlled document management system or eQMS. All no, and it belongs next to the code, where it will actually be maintained.

**Why git alone is not enough when the answer is yes.** ISO 9001 clause 7.5.3 requires that documented information be reviewed and approved, that revision status be identifiable, that it be available at the point of use, and that obsolete versions be prevented from unintended use. Git handles change history and version identity well. It does not supply an approval of record, controlled distribution, or a guarantee that the approved revision is the one someone is working from.

21 CFR Part 11 is stricter still. An electronic signature must be unique to one individual, and the signed record must carry the printed name of the signer, the date and time, and **the meaning of the signing**: review, approval, responsibility or authorship. A git commit has none of that. Its author field is a configurable string, and history is rewritable with `--amend`, `rebase` or a force push. The two properties git lacks are non-repudiation and non-obscuring: Part 11 audit trails must not obscure previously recorded information, which is the opposite of a rebase.

So the split, per document:

| Document | Regulated context | Unregulated context |
|---|---|---|
| Requirements | Requirements tool or eQMS with Part 11 signatures | Docs-as-code, versioned with the code |
| Design description | eQMS, or docs-as-code with signed release records | Docs-as-code; it describes the code and drifts fastest when separated from it |
| Traceability matrix | Generated from the requirements and test tools | Generated, or a linked report; never a hand-kept spreadsheet |
| Test plans and cases | Test management tool linked to the matrix; test code in the repo | Test management tool or docs-as-code |
| Change requests | ITSM or eQMS workflow with immutable approval records | Issue tracker |
| Acceptance sign-off | Signed record in the eQMS or contract repository | Wherever the contract lives |
| Phase gate records | eQMS or project record, signed | Wiki |

One useful precedent for the unregulated case: ISO/IEC/IEEE 42010, the architecture description standard, explicitly declines to prescribe a form. A conforming architecture description can be a document, a wiki, hypertext, a model collection or a repository. The standard cares about content and coverage, not storage. Most standards that seem to demand a Word file actually demand properties, and properties can be met in more than one place.

---

## The documents, one by one

### Software requirements specification

**When.** Scope is agreed before build, or a standard requires one. In regulated work you do not get a choice.

**Why.** The specification is the baseline everything else is measured against. Without a fixed reference, "is it done" has no answer, acceptance has nothing to test against, and change control has no baseline to control changes to.

The current standard is **ISO/IEC/IEEE 29148:2018**, which replaced IEEE 830, IEEE 1233 and IEEE 1362. IEEE 830 was formally withdrawn in October 2024, which is worth knowing because most SRS templates circulating online are still IEEE 830's Figure 1 outline.

The substantive difference between them is worth the upgrade. 29148 requires each requirement to carry its **verification approach**, which IEEE 830 did not. The 2011 text says so explicitly. That single addition is what connects the specification to the test plan and makes the traceability matrix generatable rather than invented afterwards.

29148 also gives characteristics that individual requirements must have. The 2011 list is necessary, implementation free, unambiguous, consistent, complete, singular, feasible, traceable, verifiable. The 2018 revision replaced it with nine characteristics aligned to the INCOSE guide: necessary, appropriate, unambiguous, complete, singular, feasible, verifiable, correct, conforming. Note the delta if you cite it: implementation free, consistent and traceable left the individual list, and traceability moved into requirements attributes and requirements management rather than disappearing.

The two characteristics that do the most work in practice are **singular** ("includes only one requirement with no use of conjunctions") and **verifiable**. A requirement joined by "and" cannot be individually traced, tested or changed, and a requirement with no verification method is an opinion.

**Where.** Requirements tool or eQMS if regulated. Docs-as-code if not.

### Software design description

**When.** Design must be approved before implementation begins, or is handed to a separate team, or a standard requires a design that requirements trace into.

**Why.** In a plan-driven lifecycle the design document is a gate artefact: it is what the design review approves, and implementation is not authorised until it is approved. That is a different job from the architecture overview in [`foundations/`](../foundations/architecture-overview.md), which exists to orient a reader. Use the foundations document if you want people to understand the system. Use this one if someone must sign that the design satisfies the requirements.

**IEEE 1016-2009** is the standard, and it borrows its structure from IEEE 1471, now ISO/IEC/IEEE 42010: a design is described through **viewpoints** chosen to address identified **stakeholder concerns**. It offers twelve standard viewpoints, including context, composition, logical, dependency, information, interface, structure, interaction, state dynamics and resource, and expects you to select the ones your concerns require rather than fill in all twelve.

That selection rule is the design's whole defence against bloat. A viewpoint with no stakeholder concern behind it is pages nobody will read or maintain.

IEEE 1016-2009 is old and, as far as we can determine, has not been superseded. Treat it as current but aging.

**Where.** Docs-as-code. It describes the code and rots faster than any other document when kept apart from it.

### Requirements traceability matrix

**When.** Anyone will ask whether every requirement was built and tested, or whether every line of code exists for a reason.

**Why.** This is the spine of the whole group. The canonical definition is Gotel and Finkelstein's (1994): "the ability to describe and follow the life of a requirement, in both a forward and backward direction."

The two directions answer different questions and catch different faults:

| Direction | Question | Finds |
|---|---|---|
| **Forward**, source to requirement to design to code to test | Is this requirement implemented and verified? | Gaps |
| **Backward**, artefact back to requirement to source | Why does this code or test exist? | Scope creep, gold-plating, orphaned code |

Gotel and Finkelstein add a second, orthogonal axis that most teams miss: **pre-specification** traceability, back to a requirement's origin, rationale and stakeholder, versus **post-specification** traceability forward into design and code. Teams almost always build the post half and skip the pre half, then cannot answer why a requirement exists once its author has left. That is the more expensive omission.

Where it is genuinely mandatory, with the actual clause rather than folklore:

- **IEC 62304** (medical device software) requires traceability between software requirements and their verification for **all** safety classes including Class A (clause 5.7.4), hazard traceability through to risk control verification for Classes B and C (7.3.3), and records linking change request to problem report to approval for all classes (8.2.4).
- **DO-178C** (airborne software) requires bidirectional traceability across system requirements, high-level requirements, low-level requirements, source code and verification, and made **trace data an explicit life cycle data item** that must itself be verified, which DO-178B did not.
- **ISO 26262** (automotive) manages safety requirements and their traceability in Part 8 Clause 6, with bidirectional traceability from software safety requirement to test case in Part 6. Rigour scales with ASIL.
- **FDA** expectations for medical software run through the 2002 *General Principles of Software Validation*, which asks for traceability analysis in every phase and phrases it as "software requirements to system requirements (and vice versa)". Note that Part 820 became the Quality Management System Regulation on 2 February 2026 and now incorporates ISO 13485:2016 by reference, so the 2002 guidance is the reference for method rather than the current regulation.

**The honest counterweight.** None of these mandates a spreadsheet. They mandate recorded, maintainable, bidirectional trace relationships. A hand-maintained matrix goes stale within one sprint of real change, and a stale matrix is itself an audit finding. Generate it from typed links in your requirements and test tools, or do not claim to have one.

**Where.** Generated. Never hand-kept.

### Master test plan

**When.** Testing spans multiple levels, several teams, or a contract that says what testing will happen.

**Why.** The plan exists so that coverage is a decision rather than an accident, and so that the levels do not each assume another level covered something.

The lineage matters if you cite standards. IEEE 829-1998 was a single flat sixteen-clause test plan. IEEE 829-2008 restructured it into a **master test plan** plus **level test plans**, and added an integrity level scheme that determines which documents are required at all. 829 is now superseded by **ISO/IEC/IEEE 29119-3**, currently the 2021 second edition.

29119-3 changed the substance, not just the numbering:

- **Risk moved to the centre.** The test plan now contains a risk register and a test strategy, and the completion report contains residual risks. Testing is framed as risk management rather than as coverage accounting.
- **Stakeholders and context of testing became explicit plan content.** 829 had neither.
- **Organisational-level documents were added** above project level: a test policy and organisational test practices, so a project plan does not have to restate the company's position from scratch each time.
- **Common content applies to every test document**: identifier, issuing organisation, approval authority, change history, status. Much of the document-control burden now sits inside the standard.

Annex S of 29119-3 maps its content back to IEEE 829-2008, which is the practical route if your contract names 829 and your tooling produces 29119.

**Where.** A test management tool linked to the traceability matrix. Test code in the repository.

### User acceptance test plan

**When.** Acceptance is a formal event: it triggers payment, starts a warranty period, transfers risk, or gates go-live.

**Why.** Acceptance testing is where a project's ambiguities are converted into money. If the acceptance criteria are not written against the requirements baseline before testing starts, the test becomes a negotiation about what was meant, held at the worst possible moment.

The mechanics that catch people out are contractual rather than technical:

- The contract usually defines the acceptance criteria and procedure as a schedule referencing the requirements baseline. Write the plan against that schedule, not against a fresh interpretation.
- A **fixed acceptance period** runs from delivery, with a defined number of remediation cycles.
- **Deemed acceptance** clauses are common: if the customer neither accepts nor rejects in writing within the period, acceptance is deemed to have happened. This makes the customer's sign-off discipline as commercially significant as the supplier's.
- Acceptance is evidenced by a signed certificate. Conditional acceptance, against a listed defect schedule with agreed remediation dates, is normal and is better than an argument.

For structure, use ISO/IEC/IEEE 29119-3 clause 7.2 applied at acceptance level, or IEEE 829-2008's level test plan, in which acceptance is one of the named levels. Inventing a structure is unnecessary.

**A caution.** Unlike everything else in this group, acceptance testing has no governing standard of its own, and most published guidance is vendor material. The commonly quoted exit thresholds, 95 to 98 percent pass rates and zero open severity-1 defects, are convention rather than a rule. Set yours deliberately.

**Where.** The signed record goes wherever contracts live, or the eQMS. The test execution lives in the test tool.

### Change request

**When.** Anything baselined needs to change. If nothing is baselined, you do not need this document; you need a backlog.

**Why.** Change control gets a bad reputation because it is usually implemented as delay. Its actual purpose is narrower and defensible: to make sure the impact of a change is assessed by someone competent to assess it, and that the assessment is recorded next to the decision.

**IEC 62304 clause 8.2.4** is the tightest sourced statement of the minimum, and it applies to all safety classes: records of the relationships and dependencies between the change request, the relevant problem report, and the approval of the change request. That triangle, problem to request to approval, is the requirement. Everything else your form asks for is local policy.

Two things modern practice gets right that older templates do not:

**ITIL 4 does not require a CAB.** The practice was renamed from change management to change enablement, and the monolithic change advisory board was replaced by a **change authority** with delegated authority, deliberately decentralised. Routing low-risk changes through a full board is treated as an anti-pattern that creates a bottleneck without improving change quality. Many plan-driven templates still assume a weekly CAB reviewing everything; that assumption is no longer even ITIL's position.

**Standard changes are pre-authorised.** ITIL 4's three types are standard (pre-approved, low risk, repeatable, no per-instance authorisation), normal (assessed and authorised, escalating with risk) and emergency (expedited, often a separate authority, documentation may follow execution). Getting your repeatable changes classified as standard is the single highest-value change-control improvement available to most teams.

**Log rejections too.** PMBOK's change log records accepted changes and rejected ones with reasons. The rejected half is what auditors and future maintainers actually want, and it is the half everyone drops.

**Where.** ITSM or eQMS workflow. The approval must be an immutable record, not a comment.

### Phase gate review

**When.** A named authority must approve before the next phase may start.

**Why.** This is the document that makes the rest of the group real, for the reason DOD-STD-2167A demonstrates: sequential development is enforced by review gates and their required deliverables, not by a diagram.

A gate does three things worth writing down. It fixes a baseline, so change control has something to control. It transfers accountability, from the people who produced the artefacts to the person who approved them. And it creates a decision point where cancelling is a legitimate outcome, which is the only structural defence a plan-driven project has against sunk-cost continuation.

Gates fail in one specific way, and the template is built to resist it: they become attendance rituals where everything is approved with conditions and nothing is ever stopped. A gate that has never held anything back is not a control, and you should either give it teeth or stop holding it.

**Where.** The signed record in the eQMS or project record. Not in a slide deck.

---

## Why these documents work, and how good the evidence is

The case for plan-driven documentation is usually made as compliance, which is true and boring. The more interesting case is that gates and baselines are countermeasures against two failure modes that are well documented in people, and the research quality varies a lot between the claims below.

### Gates exist because projects do not stop themselves. Evidence: good, and some of it is about software

Barry Staw's 1976 experiment gave 240 business students an investment decision, then bad news, then the chance to invest again. People committed the **most** additional money to a failing course of action when they had personally chosen it. Being responsible for the earlier decision made them worse at judging whether to continue, not better.

Mark Keil took this to software directly. His 1995 MIS Quarterly study of runaway IT projects found escalation driven by project, psychological, social and organisational factors together, not by any single bias. Keil and Robey then looked at what actually stops it: interviews with 42 IS auditors covering twelve de-escalation factors, and in the majority of cases the turnaround was triggered by **senior managers, internal auditors or external consultants**. Somebody from outside the project.

That is the design argument for the phase gate, stated precisely. The value is not the meeting or the slides. It is that the authority to continue sits with someone who did not choose the course, at a scheduled moment they cannot skip. A gate chaired by the project manager reproduces exactly the condition Staw showed is worst.

It also explains the one failure mode worth guarding: a gate that has approved everything it has ever seen has been captured, and provides no protection at all. The [phase gate review](phase-gate-review.md) template asks what may not start until this is approved, and asks for the conditions of a no, for this reason.

### Baselines work because agreement decays and nobody notices. Evidence: design reasoning, not research

We could not find a study demonstrating that a written, approved baseline reduces disputes about scope. The argument is mechanical rather than empirical: acceptance testing, change control and traceability all require a fixed reference, and without one, "is it done" has no answer that two parties will give the same way. Treat that as a reason the documents cohere, not as proof they pay off.

The related claim, that writing requirements down early prevents expensive late rework, is the one with a contested evidence base. See below.

### Traceability answers "why does this exist", and the backward direction is the neglected half

Covered above under the matrix. The point worth repeating here is psychological rather than procedural: the person who knows why a requirement exists leaves, and the rationale leaves with them. Gotel and Finkelstein's pre-specification traceability is the fix, and it is the half teams reliably skip because it produces no immediate benefit to the people recording it.

### One argument you should not use: the exponential cost-of-change curve

This is the most quoted justification for doing requirements and design up front. A defect found in requirements costs one unit, in design ten, in production a hundred, so front-load the work.

Menzies, Nichols, Shull and Layman tested it. They examined 171 software projects from 2006 to 2014, looking for the delayed issue effect, and found no evidence for it: effort to resolve an issue in a later phase was not consistently or substantially greater than resolving it soon after introduction. The original curve comes from Boehm's 1981 data on projects with release cycles measured in years, and does not survive transplantation into continuous integration.

If you need to justify plan-driven documentation, use the reasons that hold: a regulator will ask for evidence, a contract defines acceptance against a baseline, and a system that can kill people needs verification traceable to every requirement. Those are sufficient. The cost curve is not, and quoting it in front of anyone who has read the 2017 paper will cost you the rest of the argument.

---

## What to write first

1. **The specification.** Nothing else in this group means anything without a baseline.
2. **The traceability matrix**, set up as generated output at the same time. Retrofitting traces onto an existing project is the single most expensive mistake available here.
3. **The master test plan**, because it is what the matrix traces into.
4. **Change request and phase gate**, once there is a baseline worth protecting.
5. The rest when a contract or a regulation names them.

---

## Sources

- Royce, [Managing the Development of Large Software Systems](https://www.praxisframework.org/files/royce1970.pdf), *Proceedings of IEEE WESCON*, August 1970. Source of the five steps and both quotations above. Verified against the full text; the word "waterfall" does not appear in it
- Bell and Thayer, "Software requirements: Are they really a problem?", *Proceedings of ICSE '76*, pp. 61 to 68. The first widely cited appearance of the label. We could not obtain the full text, so the claim here is "first cited in print", not "coined by"
- Saravanos, [A Brief History of the Waterfall Model: Past, Present, and Future](https://arxiv.org/pdf/2510.03894), ICCSIT 2025. Peer-reviewed, confirms the Royce misattribution and surveys hybrid models
- Boehm and Turner, *Balancing Agility and Discipline*, Addison-Wesley, 2003. Source of the five factors, the home-ground tables and the four-of-five rule
- ISO/IEC/IEEE 29148:2018, *Requirements engineering*. Supersedes IEEE 830, 1233 and 1362
- IEEE 1016-2009, *Software Design Descriptions*
- ISO/IEC/IEEE 42010:2022, *Architecture description*. Second edition, November 2022
- ISO/IEC/IEEE 29119-3:2021, *Test documentation*. Supersedes IEEE 829-2008
- Gotel and Finkelstein, "An analysis of the requirements traceability problem", *ICRE '94*. Source of the traceability definition and the pre/post specification distinction
- IEC 62304:2006+AMD1:2015, *Medical device software life cycle processes*. Clauses 5.7.4, 7.3.3 and 8.2.4 quoted above are verified against the consolidated text
- FDA, [General Principles of Software Validation](https://www.fda.gov/media/73141/download), January 2002, and the [Quality Management System Regulation](https://www.fda.gov/medical-devices/postmarket-requirements-devices/quality-management-system-regulation-qmsr), effective 2 February 2026
- ISO 9001:2015 clause 7.5, and 21 CFR Part 11, on document control and electronic signatures
- DOD-STD-2167A and its successor MIL-STD-498, whose published change summary lists removing the waterfall bias
- Staw, "Knee-deep in the Big Muddy: A study of escalating commitment to a chosen course of action", *Organizational Behavior and Human Performance* 16(1), 1976, pp. 27 to 44. DOI [10.1016/0030-5073(76)90005-2](https://doi.org/10.1016/0030-5073(76)90005-2). 240 participants, laboratory
- Keil, "Pulling the Plug: Software Project Management and the Problem of Project Escalation", *MIS Quarterly* 19(4), 1995, pp. 421 to 447. DOI [10.2307/249627](https://doi.org/10.2307/249627)
- Keil and Robey, "Turning Around Troubled Software Projects: An Exploratory Study of the Deescalation of Commitment to Failing Courses of Action", *Journal of Management Information Systems* 15(4), 1999, pp. 63 to 87. Source of the finding that de-escalation is usually triggered from outside the project
- Menzies, Nichols, Shull and Layman, [Are Delayed Issues Harder to Resolve?](https://arxiv.org/abs/1609.04886), *Empirical Software Engineering* 22(4), 2017, pp. 1903 to 1935. 171 projects, no evidence for the delayed issue effect
- [Suspect links in Rational DOORS](https://www.ibm.com/docs/en/engineering-lifecycle-management-suite/doors/9.7.2?topic=data-suspect-links-changed-objects) and [Jama Connect and FDA 21 CFR Part 11](https://www.jamasoftware.com/datasheet/jama-connect-and-fda-21-cfr-part-11/). Vendor documentation, used only for what the tools do

**On sourcing.** The standards above are paywalled; clause numbers and titles here come from official previews and tables of contents, and quoted normative text is limited to what we could verify against a full copy. DO-178C and ISO 26262 clause references are corroborated across independent industry sources but not against the standards themselves, so treat them as pointers and check before citing in a submission.

**One thing not to cite.** The Standish CHAOS Report is the most quoted evidence that waterfall fails. Its methodology has been criticised in the peer-reviewed literature, notably by Jørgensen and Moløkken-Østvold. If you use its figures, cite the criticism in the same sentence, or use something else.
