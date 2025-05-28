# ADR-NNNN: {Short title stating the decision}

*Italic text is guidance. Delete it as you fill each section in.*

*Title the decision, not the topic. "Use Postgres for the ledger" beats "Database choice". A reader scanning a list of forty ADRs should learn the outcome from the title alone. Number files sequentially and never renumber: `0007-use-postgres-for-the-ledger.md`.*

| | |
|---|---|
| **Status** | Proposed \| Accepted \| Rejected \| Deprecated \| Superseded by [ADR-0012](0012-....md) |
| **Date** | YYYY-MM-DD (the date the status last changed) |
| **Deciders** | Names or a role, whoever actually decided |

*Never edit an accepted ADR to change its decision. Write a new one and mark the old one `Superseded by`. The point of the log is that it shows how thinking changed. An ADR you can rewrite is a wiki page with extra steps.*

---

## Context and problem statement

*The forces in play, told neutrally. What is true today, what pressure made this a question now, what constraints are fixed. Written so someone who joins in two years understands the situation without asking anyone.*

*Include the constraints that turn out to be decisive: a compliance requirement, a team's existing skills, a contract, a latency budget, a deadline. Those are exactly what code cannot show and what people forget first.*

*State it as a problem, not a solution. If this section names your preferred option, you have written the conclusion in the wrong place.*

*Two or three paragraphs. If it runs longer, the decision is probably several decisions.*

> **Example.** Orders are written to the same MySQL instance that serves the catalogue. Catalogue reads spike at 40x during campaigns and have twice caused order writes to time out. The ledger must survive audit, so writes need durability guarantees we cannot relax. We have no DBA; whatever we pick, the four of us operate it.

---

## Decision drivers

*The criteria you judged options against, listed before the options so the ranking is visible. Optional, but it stops the classic failure where the "Considered options" section quietly rewards whatever was already chosen.*

*Order them. Unordered criteria decide nothing.*

- *Driver 1 (for example: no new operational surface the team cannot run)*
- *Driver 2*
- *Driver 3*

---

## Considered options

*A flat list of the options, one line each. Detail goes further down. Two options is the minimum that makes an ADR worth writing; "do nothing" is a legitimate option and often the strongest.*

1. *Option A*
2. *Option B*
3. *Option C*

---

## Decision

*One sentence, active voice, present tense: "We will ...". Then a short paragraph on why this option beat the others against the drivers above.*

*Do not hedge. An ADR that says the team "leans towards" something has not recorded a decision, and the next reader will not know whether they are allowed to build on it.*

> **Example.** We will move the order ledger to a dedicated Postgres instance, keeping the catalogue on MySQL. Postgres gives us the transactional guarantees the audit needs, and a separate instance removes the contention that caused both outages. We accept running two engines because splitting the load matters more than reducing the number of technologies.

---

## Consequences

*What becomes true once this is done. Both directions, honestly.*

*The negative list is the one that earns the document. An ADR with only benefits reads as advocacy and gets distrusted. Naming the costs up front is also what lets a later team recognise when a cost grew past what you accepted.*

**Positive**

- *What gets easier, faster, safer, cheaper.*

**Negative**

- *What gets harder, slower, more expensive, or more fragile. Include the ones you are choosing to accept.*

**Follow-on work**

- *Anything this decision forces someone to do, with an owner. Migration, a new alert, a deprecation, a document to update.*

> **Example (negative).** Two database engines to patch, back up and monitor. Cross-entity reporting queries can no longer be a single join and will need the reporting pipeline instead.

---

## Options in detail

*Optional. Include it when the rejected options were genuinely close, or when someone will propose them again. Skip it when the choice was obvious once the constraints were written down.*

*Pros and cons only. No narrative. The value here is that a future engineer can check whether your reasoning still holds after the constraints change.*

### Option A: {name}

- **Good.** *...*
- **Good.** *...*
- **Bad.** *...*
- **Neutral.** *...*

### Option B: {name}

- **Good.** *...*
- **Bad.** *...*

---

## Confirmation

*How anyone can verify the decision was actually carried out. A test, a lint rule, a CI check, an architecture fitness function, a review step. One line.*

*Decisions with no confirmation quietly stop being true. This section is what separates a record from an intention.*

> **Example.** CI fails if any module under `orders/` imports the MySQL client.

---

## More information

*Links: the design doc, the spike, the benchmark, the incident that triggered this, the ADRs this one relates to. Anything a reader would otherwise have to hunt for.*

*Also record the expiry condition if one exists: "revisit if write volume exceeds 5k/s" tells a future team when to reopen this rather than leaving them to guess.*

---

## Notes on using this template

*Delete this section too.*

**Keep it to one or two pages.** Nygard's original argument was that short records get written and long ones do not. If a decision needs twenty pages, that belongs in a design document, and the ADR records the outcome and links to it.

**Write it when the decision is made, not after the code ships.** An ADR written retroactively records what you did, which the code already shows. Written at decision time it records what you rejected, which nothing else does.

**Sections you may cut:** decision drivers, options in detail, confirmation. Sections you may not: context, decision, consequences. Those three are Nygard's minimum and every later format keeps them.

**Where this lives:** `docs/decisions/` in the repository that the decision constrains. Decisions spanning several repositories go in a central log, linked from each.
