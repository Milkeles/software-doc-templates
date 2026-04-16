# Backfill and reprocessing plan: {What and when}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Pipeline** | *Link the [pipeline design document](../foundations/data-pipeline-design-document.md)* |
| **Reprocessing period** | *Exact date range or partition list* |
| **Owner** | |
| **Planned start** | |

*Read the pipeline's [design document](../foundations/data-pipeline-design-document.md) section 3 first. This plan only works if the pipeline is actually idempotent and actually backfillable; if it is not, this document is the wrong place to discover that.*

---

## 1. Why this reprocessing is needed

*The bug, the late-arriving source data, or the corrected logic that makes reprocessing necessary. Write it before starting, so the reason is on record independent of the outcome.*

---

## 2. Scope

| | |
|---|---|
| **Exact partitions or dates affected** | *As narrow as correctness allows. Reprocessing more than necessary widens both cost and risk* |
| **What changes as a result** | *Which fields, which rows. If the answer is "everything," say so plainly* |
| **What does not change** | *Explicitly out of scope, to prevent scope creep mid-run* |

---

## 3. Downstream impact

*Every consumer named in the [dataset catalog entry](../foundations/dataset-catalog-entry.md) or [lineage record](../governance/data-lineage-record.md) whose numbers will change as a result of this reprocessing.*

| Downstream consumer | Impact | Notified? |
|---|---|---|
| | | |

**A silent backfill is a trap for whoever built something on the old numbers.** A dashboard, a report, or a model retrained on this data will show a discontinuity the day this runs. Tell consumers before it happens, not after they ask why a historical number moved.

---

## 4. Execution

| Step | Action | Verification |
|---|---|---|
| 1 | *Reprocess in a staging or shadow location first, if feasible* | |
| 2 | *Compare old and new output for a sample before promoting* | |
| 3 | *Promote to production* | |
| 4 | *Confirm downstream pipelines picked up the change* | |

---

## 5. Rollback

*What undoes this if the reprocessing itself turns out to be wrong. If the pipeline overwrites partitions, keeping the prior version until this is verified is usually the cheapest insurance available.*

---

## Notes on using this template

*Delete this section too.*

**Scope this as narrowly as correctness allows.** The reliable pattern is reprocessing only the affected partitions, not the whole dataset: it costs less, and it limits the damage if the reprocessing logic itself has a bug.

**Tell consumers before the numbers move, not after.** The single most common way a backfill causes a support incident is a downstream user noticing a historical number changed with no explanation available.

**Keep the old version until the new one is verified.** A backfill that turns out to be wrong is much cheaper to undo if the previous output was never actually deleted, only superseded.

**Where this lives:** wherever the change is tracked, one per backfill event. Short-lived; archive once reprocessing completes and downstream impact is confirmed resolved.

---

## Related documents

- [`../foundations/data-pipeline-design-document.md`](../foundations/data-pipeline-design-document.md). Where the idempotency and backfill strategy this plan executes was designed
- [`../governance/data-lineage-record.md`](../governance/data-lineage-record.md). How downstream consumers in section 3 were identified
- [`pipeline-runbook.md`](pipeline-runbook.md). What to do if execution in section 4 fails partway through
