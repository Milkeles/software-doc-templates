# {Organisation or platform} architecture principles

*Also called: guiding principles, design principles.*

*Italic text is guidance. Delete it as you fill each section in.*

*Each principle carries a statement, a rationale, its implications and a way to verify it. The sections around them are a proposal, so rename or drop them freely.*

| | |
|---|---|
| **Owner** | *The person accountable for this set, and their role, so the row still makes sense after they move on. The Owner approves changes and settles conflicts the Conflicts section does not cover. They also grant waivers, unless the Waivers section names another authority.* |
| **Applies to** | *The teams and systems that must follow this set. "Every service in the retail platform" or "all Payments systems".* |
| **Builds on** | *The wider set this one narrows, if any. Link it. Delete the row if there is none.* |
| **Last reviewed** | YYYY-MM-DD |
| **Review cadence** | *Yearly, and whenever one of the goals or constraints changes. State one.* |

*This document answers "which way do we lean when we design". It holds a short list of principles, each with its reason and its cost. Design docs and RFCs check their options against it. [Architecture decision records (ADRs)](architecture-decision-record.md) cite it by ID. Each repository's [architecture overview](architecture-overview.md) links to it.*

*Optional. Write it when several teams or repositories keep facing the same design choices. If they do not, skip it and let each ADR give its own reasons.*

*Audience: the engineers who make design choices when no architect is in the room, and the people who approve a waiver when a team needs to break a principle. Write so both can follow it.*

---

## 1. Purpose and scope

*What these principles are for, in two or three sentences. Then where they stop applying.*

*Say which level this set works at. A company-wide set stays general and changes rarely. A set for one domain or product line can be sharper, because it only has to hold there. If this set builds on a wider one, say which wins when they disagree, and do not copy the wider principles in.*

> **Example.** These principles guide design choices for every service in the retail platform, including Checkout and Catalogue, so that six teams working separately still build systems that fit together. They do not cover the data warehouse, which follows the Analytics principles. Where this set and the company-wide principles disagree, the company-wide set wins unless a waiver says otherwise.

---

## 2. Goals and constraints

*What these principles serve: the organisation's goals, its quality targets, and the constraints it works under. Link the source document instead of restating it: the strategy, the [non-functional requirements](../requirements/non-functional-requirements.md), the policy or regulation. Reuse existing requirement IDs where they exist.*

| ID | Goal or constraint | Source |
|---|---|---|
| *G1* | *Teams release without waiting on each other* | *Engineering strategy 2026, goal 2* |
| *G2* | *Auditors can trace every ledger entry to the team and the change that produced it* | *Finance audit policy, section 4* |
| *NFR-04* | *Checkout stays available when one downstream service is slow* | *[Non-functional requirements](../requirements/non-functional-requirements.md), reused under its own ID* |

---

## 3. Role in decisions

*When people read these principles. One or two lines.*

*Read them before a design takes shape, because a design is cheap to change until someone has drafted it. Cite principles by ID, such as `AP-01`. Breaking a Rule follows the Waivers section.*

---

## 4. Principles

*A summary table first, holding the full statement of every Proposed and Accepted principle, so a reader can take in the whole set in a minute. Superseded and Retired entries stay below but leave the table. Then one entry per principle. If the summary and the entry disagree, the entry is right: update both in the same edit.*

*Keep the set short: about ten at the top level is typical. Keep a principle only if you can name a decision it changed or will change.*

*Some things look like principles but belong elsewhere. A house rule for one system, such as its retry policy, goes in that system's overview, under cross-cutting concerns. A single firm decision, with the options it rejected, goes in an ADR, even when it spans repositories. A principle is a reason you expect to cite in many future ADRs. If a central ADR sets up such a reason, add it here as a principle and have the ADR cite it.*

| ID | Name | Statement | Strength | Status |
|---|---|---|---|---|
| *AP-01* | *Each service owns its data* | *Each service is the only writer to its own datastore. Other services read its data through its API or the events it publishes.* | *Rule* | *Accepted* |
| *AP-02* | *Prefer events between services* | *Services tell each other about changes through events. A service calls another directly only when it needs the answer before it can reply to its own caller.* | *Guideline* | *Accepted* |

### AP-NN: {Short name}

*One entry per principle. People will use the name in conversation ("that breaks data ownership"), so keep it to a few words. Write the statement first and pick the name last.*

*Give the entry an anchor built from its ID alone, such as `<a id="ap-01"></a>` above the heading or an anchor macro in a wiki, so links survive a rename.*

| | |
|---|---|
| **Status** | Proposed \| Accepted \| Superseded by AP-NN \| Retired |
| **Strength** | Rule (breaking it needs a waiver) \| Guideline (not following it needs a written reason, in the ADR if there is one) |
| **Applies to** | *Only if narrower than the whole set. Otherwise delete the row.* |
| **Effective from** | YYYY-MM-DD |

*A Proposed principle sets a direction, but nobody has to follow it yet. List what has to be true before teams can, such as a platform service that must ship first, and link that work. Mark it Accepted, with an effective date, once they can.*

**Statement.** *One or two sentences in the present tense that describe what people do. "Services publish an event for every change to an order" can be checked. "Services should consider publishing events" commits nobody. Leave product names out: choosing Kafka is a decision, and it belongs in an ADR.*

*Try arguing the opposite before you keep a statement. If no sensible team would ever choose the reverse, as with "systems are secure", the statement settles nothing. Sharpen it or cut it.*

**Rationale.** *Why the principle exists, in words the person approving a waiver can follow. Cite the goals and constraints it serves by ID. Claim only what the principle contributes, since other measures usually share the work.*

**Implications.** *What changes for the people who follow it: what they now do, what they stop doing, and what it costs them. A short bulleted list of the main effects. Name the costs plainly. Teams will meet them anyway.*

**Verification.** *How a reviewer or a pipeline tells whether a design follows the principle, who checks, and at what point. Use an automated check where one fits and a review question where it does not. Link the check. When a check fails, fix the design or do what the principle's strength asks for.*

**Related.** *Optional. Principles this one narrows or conflicts with, and a few ADRs that applied it, so a newcomer can see it in use. Link ADRs by full URL.*

> **Example (Rule).**
>
> **AP-01: Each service owns its data.** Accepted. Rule. Effective from 2026-03-01.
>
> **Statement.** Each service is the only writer to its own datastore. Other services read its data through its API or the events it publishes.
>
> **Rationale.** A team that owns its schema has fewer changes to coordinate with other teams. Only its published API and events need care to stay compatible (G1). Every record also has one accountable owner, which makes audit questions quicker to answer (G2).
>
> **Implications.**
> - A service holds write access to its own database and to no other.
> - Reports that combine several services' data read from the reporting pipeline.
> - The owning team publishes the events other services need. That is extra work, and it falls on them.
> - Copies of another service's data are read-only and may lag by a few seconds.
>
> **Verification.** The platform team runs a nightly job that lists effective database permissions and fails if any service account can write to a database its service does not own. Design reviews ask how each new feature reads data that belongs to another service.
>
> **Related.** Applied in [orders ADR-0009](https://git.example.com/orders/docs/decisions/0009-publish-order-events-for-reporting.md).

> **Example (Guideline).**
>
> **AP-02: Prefer events between services.** Accepted. Guideline. Effective from 2026-03-01.
>
> **Statement.** Services tell each other about changes through events. A service calls another directly only when it needs the answer before it can reply to its own caller.
>
> **Rationale.** A slow service then holds up its own work and not every service that calls it, which protects checkout availability (NFR-04).
>
> **Implications.**
> - Most cross-service flows complete a few seconds after the user's request, not during it.
> - Teams run and monitor message consumers, including retries and dead-letter handling.
> - A service that needs the answer before it can reply still calls directly, such as a price check during checkout.
>
> **Verification.** At design review, the reviewing engineer checks each new direct call against the statement. A call that needs the answer before it can reply follows it. Any other direct call, such as a notification sent synchronously to reuse an existing client, gets its trade-off written in the ADR, or in the design doc if no ADR is written. No waiver is needed.

---

## 5. Conflicts

*Pairs of principles that pull in different directions, and which one wins where. Omit the section if none remain.*

*Resolve each tension by narrowing a principle's scope or by stating which takes precedence. If two principles clash everywhere, the set has not made a choice yet: drop one. Conflicts between quality targets belong in the [non-functional requirements](../requirements/non-functional-requirements.md#4-conflicts).*

> **Example.** AP-03 (prefer managed cloud services) and AP-06 (keep the ledger portable between providers) meet over the ledger database. AP-06 wins for the ledger, which is why it runs on plain Postgres. AP-03 wins everywhere else.

---

## 6. Waivers

*How a team gets approval to break a Rule, and who grants it. Some organisations call this a dispensation or a variance. Name a body other than the Owner only if one already decides architecture questions, such as an architecture board, and link the [governance](governance.md) document or page where its authority is written down.*

*Record each waiver in an ADR, however small the change, so later engineers can find every decision to break a Rule. The ADR holds the reasoning, the deciders, the role responsible for follow-up, and an end date or a review trigger. Keep only an index here.*

*Without an end date or a review trigger, a waiver never ends, and the principle has changed without approval. Before the end date, the team complies or gets a new waiver in a new ADR. Proposing a change to the principle does not extend a waiver. When the team complies, mark the waiver ADR `Superseded by` the ADR that brings it into line, and delete its row here.*

*The team that writes a waiver ADR adds its row. Link each record by its full URL, because ADR numbers repeat across repositories.*

| Principle | Repository | Record |
|---|---|---|
| *AP-01* | *invoicing (legacy service)* | *[invoicing ADR-0011](https://git.example.com/invoicing/docs/decisions/0011-keep-shared-invoice-tables-until-migration.md)* |

---

## 7. Changes and history

*How someone proposes a new principle or a change to one, who approves it, and what happens to systems built under the old wording.*

*Edit a Proposed entry freely. Once it is Accepted, fix wording in place only when the meaning stays the same. When the meaning changes, add a new entry with a new ID and mark the old one `Superseded by AP-NN`. A change to a principle's strength or to its own "Applies to" row counts as a change of meaning. A change to the whole set's "Applies to" row does not: record it in the table below. Never reuse an ID, so ADRs that cited the old entry still point at what it said when they were written.*

*Waivers against a superseded principle run to their end date. A renewal cites the new ID.*

*Mark a principle Retired when it no longer applies and nothing replaces it. Keep the entry, so old links still resolve.*

*Review the principles that keep collecting waivers first. They are the likeliest to need changing.*

*Say whether existing systems must move to a changed principle, and by when. "New designs from the effective date, existing systems at their next major change" is a usable answer.*

| Date | Change | Approved by |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**Collect before you invent.** Read your existing ADRs and design docs. A reason that keeps coming back across them is a principle you already follow, and writing it down makes it citable. Collecting alone misses the principles you need but do not follow yet, so go through the goals and constraints and ask which principle serves each one.

**Keep beliefs as names.** "Applications are decoupled" is a belief, and it changes no design. It can survive as a principle's name, as long as the statement is the checkable form: "Services talk to each other only through published APIs and events."

**Give every principle a strength.** Teams, and the books they learn from, disagree on whether a principle can be a firm rule or only advice. Marking each one Rule or Guideline lets one set hold both, and readers know which kind they are looking at.

**The waiver and versioning rules are this template's own convention.** No standard sets them. Recording waivers as ADRs, the four statuses and the new-ID rule borrow from how ADRs are kept. If your organisation already runs a dispensation process, link it and drop these.

**Where this lives:** the wiki, as one copy. Principles are agreed before the design and change only through "Changes and history", so they do not need to version with the code, and approvers can read and comment without cloning anything. Each repository's architecture overview links here, and so does every ADR that cites a principle, so a frontend and a backend repository point at the same AP-01. The one exception is a waterfall project whose principles apply only to one design. Its [software design description](../waterfall/software-design-description.md) is approved at a gate as one baseline, and principles that apply to nothing else have no other reader, so the SDD can hold them in its "Design rationale" section. If this document moves, keep the old URL working or redirect it.

---

## Related documents

*Delete this section too.*

- [`architecture-decision-record.md`](architecture-decision-record.md). Applies these principles to one decision and cites them by ID
- [`architecture-overview.md`](architecture-overview.md). The system that results, described as it is now
- [`technical-design-document.md`](technical-design-document.md) and [`rfc.md`](rfc.md). Where options are checked against these principles before anything is decided
- [`../requirements/non-functional-requirements.md`](../requirements/non-functional-requirements.md). The quality targets most principles serve, with the numbers this document leaves out
- [`governance.md`](governance.md). Who holds the authority to approve changes and waivers, if your project already defines it
- [`coding-standards.md`](coding-standards.md). Rules for how code is written, mostly enforced by tools. Principles sit above them and change less often
