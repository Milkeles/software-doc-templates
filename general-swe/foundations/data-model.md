# Data model: {System or domain}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *Which datastore or bounded context.* |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |
| **Authoritative schema** | *Link to the migrations directory. That is the truth; this explains it.* |

*The database already knows the columns and types. This document holds what it cannot: what each thing means, why the boundaries fall where they do, and which parts are mid-change.*

---

## Work at the right level, and say which one you are on

*Chen's 1976 paper, which introduced the entity-relationship model, opens by separating four levels of logical views of data:*

> *"(1) Information concerning entities and relationships which exist in our minds. (2) Information structure, organization of information in which entities and relationships are represented by data. (3) Access-path-independent data structure, the data structures which are not involved with search schemes, indexing schemes, etc. (4) Access-path-dependent data structure."*

| Level | Holds | Belongs |
|---|---|---|
| **Conceptual** | *What the business means by "order". No tables* | *Here, section 1. Also the [glossary](glossary.md)* |
| **Logical** | *Entities, relationships, keys, cardinality* | *Here, section 2* |
| **Physical** | *Indexes, partitions, storage* | *The migrations, not this document* |

**Most arguments about a data model are arguments across levels.** *One person is asking what a customer is, the other is asking whether it needs a compound index. Say at the top of a meeting which level you are on.*

*Physical detail dates fastest and is the least useful thing to write in prose. Record an index in a migration and the reason for it in an [ADR](architecture-decision-record.md).*

---

## 1. The entities

*What each one means in the business, not what columns it has.*

| Entity | Means | Identified by | Created when | Ends when | Owner |
|---|---|---|---|---|---|
| *Customer* | *A legal party we can bill. Not a user account* | *`customer_id`, internal* | *First successful signup* | *Never deleted. Anonymised on request* | *Billing* |
| *Order* | *A commitment to supply, at agreed prices* | *`order_id`* | *Checkout completes* | *Terminal state, then archived after 7 years* | *Commerce* |

*The **Means** column is the document. "A customer is a row in the customers table" is not a definition and will not settle the dispute that made you write this.*

*The lifecycle columns catch the questions nobody asks until an incident: can this be deleted, does it ever come back, what is the retention obligation.*

**Scope it deliberately.** *Chen's own caveat applies: "A complete description of an entity or relationship may not be recorded in the database of an enterprise. It is impossible (and, perhaps, unnecessary) to record every potentially available piece of information about entities and relationships." Model what the system needs, and say what you left out.*

---

## 2. Relationships

```
   CUSTOMER  1 ----------- * ORDER  1 ----------- * ORDER_LINE
                                                        |
                                                        * 
                                                        |
                                                        1
                                                     PRODUCT

   PROJECT  * ---- ASSIGNMENT ---- * EMPLOYEE
                  percentage_of_time
                  (belongs to the relationship,
                   not to either side)
```

| Relationship | Cardinality | Optional | Means |
|---|---|---|---|
| *Customer to Order* | *1 to many* | *A customer may have none* | *Who is liable for payment* |
| *Order to Product* | *many to many, via Order line* | *No* | *What was bought* |

**Relationships carry attributes of their own.** *Chen's example is exactly the one teams get wrong: `percentage-of-time` on a project-worker relationship "is neither an attribute of EMPLOYEE nor an attribute of PROJECT". If an attribute only makes sense when two entities are connected, it belongs to the connection.*

**Whether something is an entity or a relationship is a decision, not a fact.** *Chen said so in a footnote: some people view a marriage as an entity, others as a relationship, and "this is a decision which has to be made by the enterprise administrator [...] so that the distinction is suitable for his environment." Record which way you decided and why, and the argument does not recur.*

---

## 3. Identity and keys

| | |
|---|---|
| **Primary key style** | *Surrogate, natural, or composite, and the reason* |
| **Externally visible identifiers** | *What appears in URLs and API responses* |
| **Natural keys enforced** | *Uniqueness constraints that carry business meaning* |
| **Cross-system identity** | *How this entity is matched with the same thing elsewhere* |

*Say plainly whether internal keys ever leak outside. Sequential integers in URLs tell a competitor your order volume and let anyone enumerate your data; that is a modelling decision with a security consequence, so make it here rather than by accident.*

---

## 4. Ownership and boundaries

*Which system may write each entity, and which only read.*

| Entity | Written by | Read by | Shared how |
|---|---|---|---|
| *Customer* | *Billing only* | *Commerce, Support* | *API. No cross-service database access* |
| *Order* | *Commerce only* | *Billing, Analytics* | *Event stream* |

*Two services writing the same table is the most expensive mistake available in this document, and it is invisible in a schema diagram. Write the row.*

---

## 5. What is currently changing

*The section that makes this document worth keeping open.*

*Evolutionary database design handles a breaking change with a transition phase in which "the database supports both the old access pattern and the new ones simultaneously", letting consumers migrate at their own pace behind views or triggers. During that window the model has two shapes, and a document showing only one of them is wrong.*

| Change | Old shape | New shape | Transition ends | Owner |
|---|---|---|---|---|
| *Split `address` into structured fields* | *`customers.address` text* | *`addresses` table* | *2026-06-30* | | 
| *Drop `orders.legacy_ref`* | *Still written* | *Not written since 4.2* | *2026-09-01* | |

*An empty table here means either nothing is changing or nobody is tracking it. Every row with a past end date is a cleanup someone owes. Feed anything with external consumers into the [deprecation plan](deprecation-plan.md).*

---

## Notes on using this template

*Delete this section too.*

**The migrations are the schema of record.** Keep every change as a numbered, version-controlled migration applied by tooling, never as an ad-hoc statement against a shared database. This document explains that schema and must never contradict it; when they disagree, the migration is right and this file is stale.

**Separate the schema change from the data change.** A migration carries both the structural statement and the transformation, and keeping them distinct is what makes a failure diagnosable.

**Model the domain, then the storage.** Section 1 should be readable by someone who does not know what a foreign key is. If it is not, you have written the physical model twice and the conceptual model never.

**Reuse the glossary's words.** If this document calls it a customer and the [glossary](glossary.md) calls it an account, one of them is wrong and both are now unreliable. The glossary wins; it has a wider audience.

**Diagram what changed, not everything.** A generated diagram of ninety tables is a poster, not an explanation. Draw the eight entities in the area under discussion and let the tooling render the rest on demand.

**Where this lives:** in the repository, beside the migrations. It is only true relative to a schema version, and separating them guarantees they diverge. Publish a rendered copy where analysts and support staff can read it without cloning anything.

---

## Related documents

- [`glossary.md`](glossary.md). The words this model uses, defined once for everyone
- [`architecture-overview.md`](architecture-overview.md). Which service owns which entity
- [`architecture-decision-record.md`](architecture-decision-record.md). Where the reason for a storage choice belongs
- [`deprecation-plan.md`](deprecation-plan.md). Retiring a shape that external consumers depend on
- [`interface-control-document.md`](interface-control-document.md). What crosses a boundary, as opposed to what is stored
- [`../waterfall/software-design-description.md`](../waterfall/software-design-description.md). Where fixed-scope work carries the full data design
