# Data quality specification: {Dataset or domain}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

*A 1996 study of what data quality means to actual data consumers, not to the IS professionals maintaining the data, surveyed consumers directly and found 15 distinct quality dimensions across four categories: intrinsic, contextual, representational, and accessibility (Wang and Strong, "Beyond Accuracy: What Data Quality Means to Data Consumers", Journal of Management Information Systems 12(4), 1996). Their central finding: firms had narrowed "data quality" to accuracy alone, the easiest dimension to automate a check for, while consumers held a broader conception that included completeness, timeliness, and consistency. This document exists to specify all the dimensions that matter here, not just the one easiest to check.*

---

## 1. Which dimensions matter here, and why only those

*Not every dimension applies to every dataset. Name the two or three that actually decide whether this data is trustworthy, the same discipline the game-development [balance log](../../game-development/live-operations/balance-log.md) applies to metrics: more dimensions checked is not automatically better, and each one costs more to maintain than it returns.*

| Dimension | Why this one matters for this dataset |
|---|---|
| *Accuracy* | *Values match reality* |
| *Completeness* | *Nothing expected is missing* |
| *Timeliness* | *Data is current enough to act on. Cross-reference the [data contract's](../foundations/data-contract.md) freshness SLA* |
| *Consistency* | *Agrees with related data elsewhere* |
| *Uniqueness* | *No unintended duplicates* |
| *Validity* | *Conforms to a defined format or domain of values* |

---

## 2. Checks

*One row per dimension named above, specific enough that two people implementing the same check would write the same test.*

| Check | Dimension | Rule | Severity | On failure |
|---|---|---|---|---|
| | | | *Blocking / warning* | *Halt the pipeline, alert, or log and continue* |

**A blocking check and a warning check are different commitments.** A blocking check stops bad data from publishing; a warning check flags it after the fact. Decide which each check is, rather than defaulting every check to a warning because that is the path of least resistance when it is first written.

---

## 3. What happens on failure

| | |
|---|---|
| **Blocking failures** | *Pipeline halts, consumers are not served stale-but-passing data. Cross-reference the [pipeline design document's](../foundations/data-pipeline-design-document.md) failure modes* |
| **Warning failures** | *Logged, alerted, but the pipeline continues. State who reviews these and how often* |
| **Escalation** | *Who is paged for a blocking failure* |

---

## Notes on using this template

*Delete this section too.*

**Accuracy is not the only dimension, and it is not even the one consumers complain about most often.** Completeness and timeliness problems are usually what a consumer actually notices first: a report that's missing rows, or a dashboard that's a day stale. Do not let the specification default to only the checks that are easiest to write.

**A check with no stated severity is a check nobody has decided what to do with.** Write the on-failure behavior for every row, not just the ones that seem obviously blocking.

**This is the ongoing version of what the pipeline design document does once.** A [pipeline design document](../foundations/data-pipeline-design-document.md) designs for failure modes at build time; this specification is what keeps checking for them on every run afterward.

**Where this lives:** docs-as-code, next to the checks it describes, ideally as the literal configuration a validation tool reads, so the specification and the enforcement cannot drift apart.

---

## Related documents

- [`../foundations/data-contract.md`](../foundations/data-contract.md). The specific promises this dataset makes to consumers, which this specification's checks verify
- [`../foundations/data-pipeline-design-document.md`](../foundations/data-pipeline-design-document.md). Where a pipeline is designed to fail loudly rather than publish bad data
- [`../operations/freshness-and-sla-log.md`](../operations/freshness-and-sla-log.md). The measured record of whether timeliness checks actually passed over time
