# Dataset catalog entry: {Dataset name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Dataset** | *Table, topic, or file path* |
| **Owner** | *A named, accountable person or team, not a mailing list* |
| **Domain** | *Which part of the business this data belongs to* |
| **Last reviewed** | YYYY-MM-DD |

*The question this document answers is not "what columns does this have," which a schema browser already answers. It is "does this dataset exist, what is it for, and can I trust it," asked by someone who was not in the room when it was built.*

---

## 1. What this dataset is

*Two or three sentences, written for someone outside the producing team. What real-world thing does a row represent, and what is it for.*

---

## 2. Ownership

*Under a domain-oriented ownership model, a dataset is a product with an accountable owner on the team that produces it, not an anonymous artifact of a shared pipeline. A dataset without a named owner is a dataset nobody can approve a change to, or ask a question about, once the person who built it moves on.*

| | |
|---|---|
| **Owner** | *A person, reachable* |
| **Producing team** | |
| **Data contract** | *Link to the [data contract](data-contract.md), if one exists* |

---

## 3. Where this comes from and where it goes

| | |
|---|---|
| **Upstream sources** | *What this is built from* |
| **Known downstream consumers** | *Who reads this, to the best of the owner's knowledge* |
| **Full lineage** | *Link the [lineage record](../governance/data-lineage-record.md) or lineage tool if the dependency graph is deeper than one hop* |

*Before changing or retiring this dataset, this is the section that answers "what depends on it." Keep it current even informally; a wrong answer here is worse than an admitted gap.*

---

## 4. Trust signals

| | |
|---|---|
| **Freshness** | *How current the data actually is, and how that compares to the [contract's](data-contract.md) stated target* |
| **Known issues** | *Anything a consumer should know before relying on this: a known gap, a deprecated field still present, a period with bad data* |
| **Status** | *Actively maintained, deprecated, or being replaced by {dataset}* |

---

## Notes on using this template

*Delete this section too.*

**A catalog entry without an owner is worse than no entry.** It creates the appearance of a supported dataset with none of the substance. If nobody can be named as owner, that is itself the finding worth recording, not a field to leave blank.

**Prefer a generated catalog over a hand-maintained one, at scale.** This template is for a team without a metadata or catalog tool, or as seed content for standing one up. A hand-maintained catalog entry drifts from reality within a quarter; a generated one drifts only as fast as the metadata source it reads from.

**Known issues is the section people skip and the one that matters most.** A dataset with an honestly documented gap is more useful than a dataset presented as clean that silently isn't. Write the known issue down even when it is embarrassing.

**Where this lives:** the organization's data catalog tool if one exists. This template is docs-as-code content for a team without one, kept next to the dataset's pipeline so it is at least as current as the code.

---

## Related documents

- [`data-contract.md`](data-contract.md). The full schema, quality, and SLA promises this entry summarizes
- [`../governance/data-lineage-record.md`](../governance/data-lineage-record.md). The full upstream/downstream dependency graph, when one hop is not enough
- [`../governance/data-classification-and-access-policy.md`](../governance/data-classification-and-access-policy.md). Who is allowed to access this dataset, separate from whether they can find it
