# Data contract: {Dataset name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Dataset** | *Table, topic, or file path this contract governs* |
| **Producer** | *Team and a named owner, not just a team name* |
| **Consumers** | *Every known team or system reading this dataset* |
| **Last reviewed** | YYYY-MM-DD |

*A data contract does for a dataset what an API contract does for a service: it lets a consumer build against this data without asking the producer every question first, and it gives the producer a way to know what will break before they change something. The producer and the consumer of a dataset are often strangers to each other in a way an API's caller and callee usually are not, which is exactly why this needs to be written rather than assumed.*

---

## 1. Schema

*Field name, type, and nullability. Link the actual schema definition if one exists in code; do not hand-maintain a second copy that can drift from it.*

| Field | Type | Nullable? | Means |
|---|---|---|---|
| | | | |

**Means is the column that makes this a contract and not a schema dump.** A type says a field is an integer; it does not say whether `status` includes cancelled orders or whether `amount` is in cents or in the major currency unit. A consumer who has to guess will guess wrong for some fraction of rows, and the wrongness will not look like an error.

---

## 2. Quality expectations

*Constraints beyond type: uniqueness, ranges, referential rules. State what a consumer can assume is always true, so they know what actually needs validating on their own side.*

| Constraint | Applies to | Statement |
|---|---|---|
| *Uniqueness* | | |
| *Range* | | |
| *Referential* | *e.g. every `customer_id` exists in the customers table* | |
| *Completeness* | *e.g. no more than 0.1% null in `email`* | |

*For the full set of dimensions worth considering beyond accuracy, see the [data quality specification](../governance/data-quality-specification.md). This section states the promises specific to this one dataset; that document names the dimensions worth checking across all of them.*

---

## 3. Service levels

| | |
|---|---|
| **Freshness** | *How stale can this data be before it violates the contract, e.g. "updated within 2 hours of the source event"* |
| **Completeness** | *What fraction of expected records must be present* |
| **Availability** | *Uptime of the serving layer, if this is queried live rather than batch-delivered* |
| **Consequence of a miss** | *What happens if this SLA is not met. If there is no stated consequence, this is a target, not a guarantee, and should not be called an SLA* |

*This distinction matters and is easy to blur: a promise with no consequence attached is an objective, not an agreement. Say plainly which one this is, rather than calling an aspiration a guarantee.*

---

## 4. Change management

| | |
|---|---|
| **Breaking change definition** | *What counts as breaking for this dataset: removing a field, changing a type, changing what a field means without changing its name* |
| **Notice period** | *How long consumers get before a breaking change ships* |
| **Notification channel** | *Where consumers are actually told, not just where it is theoretically discoverable* |

*A field silently changing meaning without a type or name change is the failure mode that does the most damage, because nothing about it looks like a breaking change to any automated check. Treat a meaning change as breaking even when the schema is untouched.*

---

## Notes on using this template

*Delete this section too.*

**Implement this as code where you can.** A contract enforced by a schema validator or a CI check that fails a build is a guarantee. A contract that exists only as a document a producer might remember to reread before shipping a change is a hope.

**The producer rarely uses their own data the way the consumer does.** The person generating an event as a side effect of building a feature is usually not the person building a dashboard on top of it. That asymmetry is the entire reason this document needs to exist; do not skip it because "we all work at the same company and can just ask."

**A meaning change is a breaking change.** Renaming or retyping a field breaks a schema check automatically. Changing what `status = 'complete'` includes breaks nothing automatically and can go undetected for months. Section 4 exists specifically to make this class of change visible.

**Where this lives:** docs-as-code, ideally as the literal schema file a validator enforces against, so a change to the contract and a change to the data are the same commit.

---

## Related documents

- [`data-pipeline-design-document.md`](data-pipeline-design-document.md). What produces and moves the data this contract describes
- [`dataset-catalog-entry.md`](dataset-catalog-entry.md). Where this dataset is discoverable, with this contract linked from it
- [`../governance/data-quality-specification.md`](../governance/data-quality-specification.md). The fuller set of quality dimensions this contract's section 2 draws from
- [`../operations/freshness-and-sla-log.md`](../operations/freshness-and-sla-log.md). Whether section 3's promises were actually kept, measured over time
- [`../../general-swe/foundations/interface-control-document.md`](../../general-swe/foundations/interface-control-document.md). The same boundary problem, solved for an API instead of a dataset
