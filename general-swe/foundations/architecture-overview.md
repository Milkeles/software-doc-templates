# {System} architecture overview

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | *The team accountable for this document, not an individual who may leave.* |
| **Last reviewed** | YYYY-MM-DD |
| **Review cadence** | *Quarterly, or on every change that moves a boundary. State one.* |

*This document answers "what is this system and how is it shaped". It does not answer "why is it shaped that way": that belongs in [ADRs](architecture-decision-record.md), linked from here. Mixing the two produces a document that is neither consultable nor readable.*

*Audience: a competent engineer who does not work on this system. A new hire in week one, an incident responder at 3am, a team that wants to integrate, an auditor. Write for them, not for yourself.*

---

## 1. Purpose and scope

*What the system does, in business terms, in three sentences. Then what is inside the boundary and what is outside it.*

*The boundary is the useful part. Most confusion about a system is confusion about where it ends.*

> **Example.** Handles order capture, payment authorisation and fulfilment handoff for the retail site. Inventory and pricing are outside the boundary and owned by Catalogue.

---

## 2. Quality attributes

*The handful of non-functional properties this architecture is actually built to deliver, each with a number and a source.*

*Every system claims to value availability, performance and security. That claim decides nothing. The value here is the ranking and the numbers, because they are what justify the structure below and what a reviewer can hold you to.*

| Attribute | Target | Why it matters | Where it is measured |
|---|---|---|---|
| *Availability* | *99.9% monthly for checkout* | *Contractual* | *Link to SLO* |
| *Latency* | *p99 under 400ms for authorisation* | *Cart abandonment above this* | *Link to dashboard* |

*Then, in one or two lines: which of these you trade away when they conflict. A system that ranks nothing has not made an architectural choice.*

---

## 3. Constraints

*What was not open to choice, and by whom it was imposed. Technical, organisational, regulatory, contractual.*

*A reader who does not know the constraints will read the architecture as a series of odd decisions. Name them once here and half the questions disappear.*

- *Constraint, and its source: "Card data may not touch our infrastructure (PCI DSS scope reduction, mandated by Security)"*

---

## 4. Context

*The system as one box, and everything it talks to.*

*Include: users and roles, external systems, and for each connection what flows, in which direction, over what protocol. Nothing about internals.*

*Draw this as a diagram in a text format that can be diffed and reviewed. Include the source in the repo, not an exported image.*

| Neighbour | Direction | What flows | Protocol | Owner |
|---|---|---|---|---|
| | | | | |

---

## 5. Containers

*The separately deployable or runnable things inside the boundary: services, jobs, databases, queues, front ends. What each is responsible for, what it is built with, and how the others reach it.*

*Keep the responsibility to one sentence. If you cannot, that container does more than one thing, and saying so here is more useful than hiding it.*

| Container | Responsibility | Technology | Called by | Calls |
|---|---|---|---|---|
| | | | | |

*Then a diagram showing the containers and the connections between them.*

*Stop here for most systems. Component-level detail below the container is worth documenting only where it is genuinely non-obvious, and it goes stale fastest.*

---

## 6. Runtime behaviour

*Two to four scenarios traced end to end through the containers above. Pick the ones that matter: the main flow, the money flow, the flow that breaks most often.*

*Numbered steps or a sequence diagram. Include what happens when a step fails, because that is what an incident responder came here to find.*

### {Scenario name}

1. *...*
2. *...*

**When it fails.** *Where the retry is, what is idempotent, what a user sees.*

---

## 7. Data

*What data lives where, which store is authoritative for each entity, and how data moves between them.*

*The authoritative-source column is the point of this section. Systems rot when two stores both look authoritative for the same thing.*

| Entity | System of record | Copies live in | How copies update | Retention |
|---|---|---|---|---|
| | | | | |

*Also note anything with legal or privacy weight: personal data, payment data, anything with a mandated retention or deletion period.*

---

## 8. Deployment

*How the containers above map onto real infrastructure. Environments, regions, what is redundant and what is not.*

*Say plainly where the single points of failure are. Every system has some. A document that implies there are none is not trusted by anyone who has been on-call.*

---

## 9. Cross-cutting concerns

*The conventions that apply everywhere, stated once so no one has to infer them from code.*

*Only the ones that are real for you. Delete the rest.*

- **Authentication and authorisation.** *How a caller is identified and what decides access.*
- **Error handling and retries.** *The house rules: what is retried, with what backoff, what is never retried.*
- **Observability.** *Where logs, metrics and traces go, and what correlates them.*
- **Configuration and secrets.** *Where they come from and how they rotate.*
- **Versioning and compatibility.** *What guarantees you make to callers.*

---

## 10. Architecture decisions

*Links to the ADRs that produced this structure, newest first. Not summaries: links.*

*This section is what keeps the rest of the document short. Anywhere a reader is likely to ask "why like that", link the ADR instead of answering inline.*

- [ADR-0007: Use Postgres for the ledger](decisions/0007-....md)

---

## 11. Known problems and direction

*What is wrong with this architecture today, and what you intend to do about it. Debt with consequences, not a wish list.*

*Every experienced reader already suspects the weak points. Naming them buys credibility for everything above, and it stops a new engineer proposing a fix you rejected two years ago.*

| Problem | Impact today | Intended direction | Owner |
|---|---|---|---|
| | | | |

---

## 12. Glossary

*Domain terms used above, or a link to the [glossary](glossary.md). Define anything a competent outsider would guess wrong.*

---

## Notes on using this template

*Delete this section too.*

**Cut sections without hesitation.** This skeleton follows arc42's structure and C4's abstraction levels, and both are explicit that the sections are a checklist, not a mandatory contents page. A single service with one datastore needs sections 1, 4, 5 and 10 and nothing else.

**Keep diagrams as text.** Structurizr DSL, PlantUML, Mermaid, D2: anything that lives in the repo, diffs in review, and regenerates in CI. An exported PNG on a wiki cannot be reviewed alongside the change that invalidated it, and so it will not be.

**Give it an owner and a review date, or it will rot.** This is the document in the group most likely to be quietly wrong, because nothing fails when it drifts. The review cadence in the header is the only thing standing between it and fiction. If a review passes with no change, update the date anyway: "reviewed and still correct" is information.

**Where this lives:** in the repository, rendered to HTML in CI so non-engineers can read it without cloning.
