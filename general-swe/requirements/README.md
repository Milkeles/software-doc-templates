# Requirements

Four documents for working out what to build, before building it.

| Document | Write it when |
|---|---|
| [`vision-and-scope.md`](vision-and-scope.md) | The project is large enough that people disagree about why it exists. Always, for anything over a few weeks |
| [`product-requirements-document.md`](product-requirements-document.md) | The people who must agree cannot all be in the room. See the objection below before writing one |
| [`use-case-specification.md`](use-case-specification.md) | A flow has real branching. Payment, authentication, onboarding, anything regulated |
| [`non-functional-requirements.md`](non-functional-requirements.md) | How well matters as much as what. Platform, embedded, regulated, or anything with a load |

These are methodology-neutral. A Scrum team, a Kanban team and a plan-driven team all need to know why the project exists and what "fast enough" means. What changes is the ceremony around the document, not whether the thinking happens.

---

## Where the boundaries are, and why they are drawn there

The most common failure in requirements work is not writing badly. It is writing the same thing in three documents, which then disagree.

```
   WHY                    WHAT                          HOW

   vision-and-scope       product-requirements-doc      technical design doc
   business objectives    features, acceptance criteria architecture
   success metrics        priorities                    interfaces
   what is excluded       open questions                data model
                          |
                          +-- use-case-specification
                          |     one goal, every path
                          |
                          +-- non-functional-requirements
                                how well, measurably

           each fact lives in exactly one of these.
           the others link to it.
```

Two boundary rules are worth stating explicitly, because they are the ones that break down first.

**Business assumptions belong in vision and scope. Technical assumptions belong in the SRS.** "We assume finance keeps owning reconciliation" is a business assumption; if it is wrong, the scope changes. "We assume the identity provider supports SAML 2.0" is technical; if it is wrong, the design changes. Different readers, different consequences, different documents.

**Strategic, market and financial risk belongs in the business plan, not in vision and scope.** Vision and scope carries the risks to *this project's* business case. Whether the market exists at all is a prior question and a different document.

If you keep only one rule from this section: **every fact lives in exactly one document, and the others link to it.** Duplication is not redundancy, it is a guarantee that two versions will diverge and nobody will know which is current.

---

## How this relates to what is already here

Nothing in this group replaces anything. It fills gaps.

| If you already have | This group adds |
|---|---|
| [`waterfall/software-requirements-specification.md`](../waterfall/) | The document that comes before it. An SRS answers what the software must do; vision and scope answers why anyone is paying for it |
| [`agile-scrum/product-backlog-item.md`](../agile-scrum/) | The forms a backlog item cannot carry. A story is a placeholder for a conversation and is deliberately thin. Use cases hold the branches; NFRs hold the measures |
| [`foundations/technical-design-document.md`](../foundations/) | The requirements it is designed against |

**ISO/IEC/IEEE 29148:2018** is the standard behind the split, and it is more granular than most teams realise. It defines four separate information items, each with its own mandated content: a Business Requirements Specification, a Stakeholder Requirements Specification, a System Requirements Specification, and a Software Requirements Specification. The 2018 edition "cancels and replaces" the 2011 first edition.

Mapping this repository onto it, approximately:

| 29148 item | Closest document here |
|---|---|
| BRS, business purpose and objectives | [`vision-and-scope.md`](vision-and-scope.md) |
| StRS, user requirements and operational scenarios | [`use-case-specification.md`](use-case-specification.md) |
| SyRS, whole-system including hardware | Not covered. Most software teams do not need it |
| SRS, software view | [`../waterfall/software-requirements-specification.md`](../waterfall/software-requirements-specification.md) |

Most teams should not produce four documents. The value of knowing the standard's split is that it tells you which conversation you are having, which is the thing that actually gets confused.

---

## Why these documents work, and how good the evidence is

This section is longer than usual because requirements engineering is unusually well studied and the results are not what most practitioners assume.

### The short version

**The evidence base is thin, and the field's own researchers say so in print.**

Frattini and colleagues, in *Requirements Engineering* (2023), surveyed the state of requirements quality research and concluded that it "focuses on normative rules and mostly fails to connect requirements quality to its impact on subsequent software development activities, impeding the relevance of the research." In their sample, claimed impacts were "dominantly hypothesized" at 47.5%, and the selection of which downstream activities are affected "is usually justified by anecdotal or folkloric circumstances". Economic impact appeared in 15.8% of papers and was "only hypothesized or referenced, never determined empirically".

Montgomery and colleagues, in the same journal (2022), screened 6,905 articles down to 105 primary studies and found that "empirical research on requirements quality focuses on improvement techniques, with very few primary studies addressing evidence-based definitions and evaluations of quality attributes".

So: writing requirements well is a widely held professional conviction with a weak measured basis. That is not a reason to skip it, but it is a reason not to claim more than you can support.

### What does hold up

**Practitioners consistently report incomplete requirements as their biggest problem.** The NaPiRE survey (Méndez Fernández et al., *Empirical Software Engineering*, 2017) covered 228 companies across ten countries. Incomplete or hidden requirements was the most frequently cited problem, named by roughly half of respondents, and ranked among the top perceived causes of project failure. **This is self-reported perception at scale, not measured outcomes.** It tells you what experienced people believe hurts them, which is worth knowing and is not the same as causation.

**One study measured it and got a surprising result.** Chari and Agrawal (*Empirical Software Engineering*, 2018) examined 49 plan-driven projects in one organisation. Change requests arising from *new* requirements increased both defects and effort. Change requests from *incorrect* requirements increased defects and further requirements churn. But change requests from *incomplete* requirements had **no measurable impact on outcomes**.

That last finding cuts directly against the practitioner consensus above, and it is worth sitting with. The population is 49 projects in a single organisation at one maturity level, so do not generalise from it. But it is a reason to spend your effort on getting requirements *right* rather than on getting them *complete*, and completeness is where most requirements ceremony goes.

### Two arguments you should not use

**"Fixing it later costs more."** The exponential cost-of-change curve attributed to Boehm's work is the standard justification for requirements effort. A 2017 study in *Empirical Software Engineering* examined 171 projects from 2006 to 2014 and found no evidence for the delayed issue effect. Notably, the curve is still cited uncritically in current peer-reviewed requirements literature, which tells you how durable a well-shaped claim can be. See [`../waterfall/`](../waterfall/) for the detail.

**"X% of defects originate in requirements."** Every version of this statistic traces back through blog citations to Boehm-era data or to nothing at all. The same applies to "requirements errors cost 100 times more to fix in production." No primary source exists for any specific figure. Do not repeat them.

### The argument that actually works

These documents are coordination devices, and the mechanism does not need a study.

A stated exclusion is an argument that does not recur. A numbered acceptance criterion is a dispute settled before it costs anything. A written non-goal is an idea that stops returning every fortnight. A measured availability target is a decision made calmly rather than at 2am.

None of that requires the cost-of-change curve to be true. It requires only that people forget, disagree, and leave, which they demonstrably do.

---

## The objection to the PRD, stated fairly

Marty Cagan has argued against requirements documents for twenty years, and the argument is good enough that the template addresses it directly rather than ignoring it.

From "Revisiting the Product Spec" (2006): "most specs take too long to write, they are seldom read, they don't provide the necessary detail". And, on the deeper failure: "it is all too easy for the mere existence of the spec to serve as a false indicator to management and the product team". His alternative is a high-fidelity prototype. From "The End of Requirements" (2013): "Most requirements are not actually requirements, and the rest are better thought of as constraints."

**He is right about the situations he describes.** A co-located team that can prototype and talk daily gets more from a prototype and a one-page brief than from a PRD.

He is describing a situation, not a universal law. When the people who must agree cannot all be in the room, when a supplier is building it, when a regulator needs a record, or when the decision must outlive the person who made it, the document does work the prototype cannot. Write it then. Do not write it as ritual.

**Note on attribution.** Melissa Perri is often cited alongside Cagan on this point. *Escaping the Build Trap* argues against measuring success by outputs rather than outcomes; it does not take a specific published position against PRDs. Do not attribute one to her.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| Vision and scope | Wiki | Co-authored with business stakeholders, changed by discussion, read by people who will never clone the repository |
| Product requirements document | Wiki | Same. It is superseded rather than versioned, and comments on it are part of its value |
| Use case specification | Wiki if analysts own it, docs-as-code if developers do | Decide by who edits it. Extensions convert to test cases, which argues for proximity to the tests |
| Non-functional requirements | With the requirements they accompany, and the measurable ones also in CI | An availability target nothing checks is a hope. Where a number can be asserted automatically, assert it |

The pattern differs from most of this repository, where docs-as-code usually wins. **Requirements documents are the exception, because their authors are frequently not engineers.** A document whose co-authors cannot open a pull request belongs where they already work.

The exception to the exception is the last row. A performance or availability requirement should exist both as prose for humans and as an assertion in a pipeline, and the two must not disagree.

---

## The document control block

For wiki-hosted documents, open with:

```
   Document ID      ACME-VNS-2026-03-14
   Version          2.1
   Date             2026-03-14
   Organisation     Acme
   Team             Product
   Author(s)        [name]
   Reviewer(s)      [name]
   Confidentiality  Public | Internal | Confidential
```

Then a revision history table, then a table of contents.

**Add it only where the platform does not already supply the information.** Git records authorship, version and history more accurately than any hand-maintained table, so a repository-hosted document should not carry one. A wiki with weak history should. The reviewer line is worth keeping in both cases, because approval is a fact neither system records.

---

## What to write first

1. **Vision and scope**, and specifically its limitations and exclusions section. That one section prevents more wasted work than everything else in this group combined.
2. **Non-functional requirements**, if any quality attribute is load-bearing. These are the requirements that get discovered during an incident when they were not written down.
3. **Use cases**, for the two or three flows with real branching. Not for everything.
4. **A PRD**, only if you have established that a prototype and a conversation will not do.

---

## Sources

- Karl Wiegers and Joy Beatty, *Software Requirements*, 3rd edition, Microsoft Press, 2013, and the published Vision and Scope template. Wiegers and Candase Hokanson, *Software Requirements Essentials*, Addison-Wesley, 2022, supplements it rather than replacing it
- Karl Wiegers, *Creating a Software Engineering Culture*, Dorset House, 1996, for driver, constraint and degree of freedom
- ISO/IEC/IEEE 29148:2018, *Systems and software engineering: Life cycle processes: Requirements engineering*, second edition, November 2018
- ISO/IEC 25010:2023, *SQuaRE: Product quality model*. Quality in use moved to ISO/IEC 25019:2023
- Len Bass, Paul Clements and Rick Kazman, *Software Architecture in Practice*, 4th edition, Addison-Wesley, 2021, for the six-part quality attribute scenario
- Alistair Cockburn, *Writing Effective Use Cases*, Addison-Wesley, 2000
- Mike Cohn, *User Stories Applied*, Addison-Wesley, 2004, for the use case and story distinction
- OMG UML 2.5.1, December 2017
- Frattini et al., "Requirements quality research: a harmonized theory, evaluation, and roadmap", *Requirements Engineering*, 2023
- Montgomery et al., "Empirical research on requirements quality: a systematic mapping study", *Requirements Engineering* 27(2), 2022
- Méndez Fernández et al., "Naming the pain in requirements engineering", *Empirical Software Engineering* 22(5), 2017
- Chari and Agrawal, "Impact of incorrect and new requirements on waterfall software project outcomes", *Empirical Software Engineering* 23(1), 2018
- Marty Cagan, "Revisiting the Product Spec" (2006) and "The End of Requirements" (2013), Silicon Valley Product Group

**On sourcing.** Structures here come from the named books and standards. ISO standards are paywalled, so clause-level content is drawn from official previews and from sources that agree with each other; where a detail could not be confirmed, the templates omit it rather than assert it. Claims widely repeated without a traceable source, including defect-origin percentages and cost-multiplier figures, are named and left out.
