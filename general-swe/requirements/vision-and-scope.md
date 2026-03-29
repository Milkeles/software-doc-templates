# Vision and Scope

> Why this project exists, what success looks like, and what it will not do.
>
> **Written before requirements, not alongside them.** Every later argument about whether a feature belongs is settled here or nowhere. A team that skips this document does not avoid the decisions; it makes them one feature at a time, inconsistently, in review meetings.
>
> **The structure below follows Karl Wiegers.** *Software Requirements*, 3rd edition (Wiegers and Beatty, Microsoft Press, 2013), and its published Vision and Scope template. It is the most widely used structure for this document and the section order is his. The guidance under each heading is not.
>
> **Where it lives.** Wiki. It is a living document with business stakeholders as co-authors, it changes through discussion rather than through commits, and its readers include people who will never clone the repository. See the group [README](README.md).
>
> **Length.** Under ten pages. This document is read by executives who will read the first page and skim the rest, so put the decisions early.
>
> **Delete this block before publishing.**

---

## 1. Business requirements

Why the organisation is funding this. Not what the software does.

### 1.1 Background

Enough context for a reader who has just joined. What exists today, how the situation arose, and what has already been tried.

Keep it to three paragraphs. Background sections grow because they are easy to write, and length here delays the reader from reaching anything they can act on.

### 1.2 Business opportunity

The problem or opportunity, stated in terms of the business rather than the software.

Include the market or operational situation, what competitors or comparable organisations do, and what it currently costs to leave this unsolved. **The cost of doing nothing is the most persuasive sentence in the document and the one most often left out.**

> Support handles roughly 400 password reset requests a month at an average of 11 minutes each. That is 1.8 full-time days a week spent on a task users could complete themselves.

### 1.3 Business objectives

What the organisation gets, in numbers, with dates.

| Bad | Good |
|---|---|
| Improve customer satisfaction | Reduce support contacts for account access by 60% within two quarters of launch |
| Modernise the platform | Cut deployment time from 4 hours to under 30 minutes by Q3 |

Every objective must be something a person outside the team could verify without asking you. If you cannot state it that way, you do not yet know why you are building this.

Keep it to three to five. A list of twelve objectives is a list of no priorities.

### 1.4 Success metrics

How you will know, and when you will look.

For each objective, give the metric, its current value, its target, and the date you will measure. **The current value is the part people skip, and without it a target is unfalsifiable.**

> Support contacts for account access: currently 400/month. Target under 160/month. Measured monthly from launch, assessed at launch plus 6 months.

Say who owns the measurement. A metric with no owner is not measured.

### 1.5 Vision statement

One or two sentences describing the product at a point in the future. It sits inside business requirements deliberately: the vision serves the business objectives above, and is not a separate act of imagination.

Wiegers offers a keyword template that constrains it usefully:

> For [target customer]
> who [statement of need or opportunity],
> the [product name]
> is a [product category]
> that [key benefit, compelling reason to buy or use].
> Unlike [primary competitive alternative],
> our product [statement of primary differentiation].

The value of the form is that it forces you to name the alternative. A vision statement with no "unlike" clause usually means nobody has asked why the status quo is not good enough.

### 1.6 Business risks

Risks to the business case: market, financial, legal, organisational, timing.

**Not technical risks.** Those belong in the technical design or the [risk register](../project-management/risk-register.md). Keeping business risk here and delivery risk there stops both documents from becoming a general anxiety list.

For each: the risk, its likely impact, and what you would do about it. A risk with no response is a worry.

### 1.7 Business assumptions and dependencies

**Assumptions** are things you believe true that you have not verified, and that would change the plan if false. State them so someone can challenge them cheaply now rather than expensively later.

> We assume the finance team will continue to own reconciliation. If that changes, the scope grows by an integration we have not estimated.

**Dependencies** are things outside your control that you need. Another team, a vendor, a contract, a regulatory approval. Name the owner and the date you need it.

**Business assumptions belong here and not in the software requirements specification.** The SRS carries technical assumptions. Splitting them keeps each document readable by its own audience and stops both from drifting.

---

## 2. Scope and limitations

The section people actually return to.

### 2.1 Major features

The handful of capabilities that deliver the objectives, at the level of a bullet each. Label them so later documents can reference them: FE-1, FE-2.

Not a feature list. If you have more than about fifteen, you are writing requirements, and they belong in the [SRS](../waterfall/software-requirements-specification.md), a [PRD](product-requirements-document.md) or a backlog.

Trace each feature to an objective. **A feature that traces to nothing is the first thing to cut**, and this table is how you find it.

| Feature | Serves objective |
|---|---|
| FE-1 Self-service password reset | Reduce account access support contacts |
| FE-2 Session management dashboard | Reduce account access support contacts |

### 2.2 Scope of initial release

What ships first, and the quality and performance characteristics it must have. Be concrete about what "done" means for each feature, because a feature name alone can describe a week or a quarter of work.

### 2.3 Scope of subsequent releases

What is planned later, in decreasing detail. Release 2 gets a paragraph, release 3 gets a sentence.

This section protects the initial release. "Not now" is a far easier answer to defend than "no", and having somewhere to write it down is what makes deferral possible.

### 2.4 Limitations and exclusions

**Write this section first, and make it long.**

What the product will explicitly not do, and what it will not support. Every item here is an argument you will not have to have twice.

> - No migration of records created before 2019.
> - No mobile application. The web interface is responsive; a native app is out of scope for all planned releases.
> - No offline mode.
> - Does not replace the existing reporting tool.

The test of a good exclusion is that somebody was expecting it. Excluding things nobody wanted is filler. Exclusions that surprise a reader are exactly the ones that needed writing down, and a mild objection now is much cheaper than a discovery at acceptance.

---

## 3. Business context

### 3.1 Stakeholder profiles

Who is affected, what they want, and what they will resist.

| Stakeholder | Major value | Attitudes | Major interests | Constraints |
|---|---|---|---|---|
| Support agents | Fewer repetitive tickets | Sceptical; a previous tool was withdrawn | Must keep manual override for edge cases | Cannot retrain during peak season |

**The "attitudes" column earns the table.** A stakeholder who has been burned before behaves differently from one who has not, and that is a project fact, not gossip. Write it factually and without judgement: this document is often read by the people described in it.

For a fuller treatment, see [`stakeholder-register.md`](../project-management/stakeholder-register.md). This section is a summary; do not duplicate the whole analysis here.

### 3.2 Project priorities

The most useful table in the document, and Wiegers' distinctive contribution. It comes from his *Creating a Software Engineering Culture* (Dorset House, 1996).

Classify each dimension as a **driver** (a top-priority objective), a **constraint** (a limit you must work within), or a **degree of freedom** (something that can flex).

| Dimension | Driver | Constraint | Degree of freedom |
|---|---|---|---|
| Schedule | Must ship before the regulatory deadline of 2026-09-30 | | |
| Features | | | 3 of 5 major features acceptable at launch |
| Quality | | Zero critical defects in payment paths | |
| Staff | | Team of 4, no additions approved | |
| Cost | | | Up to 15% over budget acceptable if schedule holds |

Two rules make it work:

**Not everything can be a driver.** If three of five rows are drivers, the exercise has failed and the trade-offs will be made later by whoever is in the room, without anyone noticing a decision was taken.

**At least one degree of freedom.** A project with no flex will breach something. This table decides in advance what breaks, while everyone is calm.

### 3.3 Deployment considerations

The operating environment: where it runs, who installs it, what data has to move, what training is needed, what has to be true on day one.

This section catches the work nobody costed. Data migration, user training, support readiness and decommissioning the old system routinely cost more than the feature work and routinely appear in no plan.

---

## Common failures in this document

- **Objectives with no numbers.** Nothing to measure at the end, so the project cannot succeed or fail, only continue.
- **Empty exclusions section.** The single most reliable predictor of scope disputes.
- **Written after development started.** Becomes a description of what was built, and loses its only function.
- **Every priority is a driver.** The trade-off table shows no trade-offs, so it settles nothing.
- **Technical detail leaking in.** Architecture and design belong in the [technical design document](../foundations/technical-design-document.md). This document is read by people who do not want it.
- **Never revisited.** Objectives change. A vision document contradicted by the current plan discredits the practice, not just the document.

---

## Related documents

- [`product-requirements-document.md`](product-requirements-document.md). What to build, once this has settled why
- [`../waterfall/software-requirements-specification.md`](../waterfall/software-requirements-specification.md). The detailed requirements. Business assumptions stay here; technical ones go there
- [`../project-management/project-charter.md`](../project-management/project-charter.md). Authority and governance, as opposed to product direction
- [`../project-management/risk-register.md`](../project-management/risk-register.md). Delivery risk, as opposed to the business risk in section 1.6
