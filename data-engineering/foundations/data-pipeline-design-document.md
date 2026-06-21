# Data pipeline design document: {Pipeline name}

*Also called: ETL design document, pipeline design doc.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |
| **Schedule** | *Cron expression, trigger, or "continuous"* |
| **Criticality** | *What breaks downstream if this pipeline stops or produces wrong data* |

*Read the general [technical design document](../../general-swe/foundations/technical-design-document.md) first, if this pipeline is complex enough to need one. This template adds what is specific to moving data rather than serving requests: a rerun has to produce the same answer as the first run, and a failure can produce a wrong number instead of an obvious error.*

---

## 1. What this pipeline does

*Two or three sentences. What goes in, what comes out, why it exists.*

---

## 2. Sources and sinks

| | Location | Format | Owned by | Contract |
|---|---|---|---|---|
| **Source(s)** | | | | *Link the [data contract](data-contract.md) if the source is another team's dataset* |
| **Sink(s)** | | | | *Link the data contract this pipeline promises to its own consumers* |

*If a source has no data contract, this pipeline is depending on an implicit agreement nobody wrote down. Say so, rather than letting the gap stay invisible.*

---

## 3. Idempotency and backfill

*The question a service rarely has to answer and a pipeline always does: what happens if this run executes twice, or reprocesses a period it already processed?*

| | |
|---|---|
| **Idempotent?** | *Yes or no, stated plainly. If no, say what breaks on a rerun and why that risk is accepted* |
| **Idempotency mechanism** | *Partition overwrite, upsert on a natural key, deduplication window, or another named approach. The most common reliable pattern is a full overwrite of the output partition for the period being processed, rather than an append* |
| **Backfillable?** | *Can this pipeline accept an explicit date or partition parameter and reprocess exactly that period, rather than only ever processing "now"?* |
| **Backfill blast radius** | *Reprocessing one day should not require reprocessing the whole dataset. State the smallest unit that can be safely reprocessed alone* |

**An idempotent pipeline produces the same end state no matter how many times it runs.** A non-idempotent pipeline that appends rows on every run will silently double-count on a retry, and the failure looks exactly like correct output until someone reconciles a total. Design for reruns before the first incident forces the question, not after.

---

## 4. Schedule and dependencies

| | |
|---|---|
| **Trigger** | *Cron, event, or upstream pipeline completion* |
| **Upstream dependencies** | *Pipelines or datasets this one waits on, and what happens if they are late* |
| **Downstream dependents** | *Who consumes this pipeline's output, and by when they expect it. Cross-reference the [data contract's](data-contract.md) SLA fields* |
| **Expected runtime** | *So a stuck run is recognizable as stuck, not just slow* |

---

## 5. Failure modes

*What can go wrong, and whether it fails loudly or quietly. A pipeline that silently produces a partial or wrong result is more dangerous than one that crashes.*

| Failure | Loud or quiet? | Detection | Response |
|---|---|---|---|
| *Source data late or missing* | | | |
| *Source schema changed unexpectedly* | | | |
| *Partial write, job killed mid-run* | | | |
| *Duplicate or double-processed input* | | | |

**Prefer designs that fail loudly.** A pipeline that validates its own output against expectations before publishing, and refuses to publish on failure, converts a silent wrong number into a loud, fixable outage. This is the same logic a [data quality specification](../governance/data-quality-specification.md) applies as an ongoing check; build the cheapest version of it into the pipeline itself.

---

## 6. Monitoring

| Signal | Alerts when | Where |
|---|---|---|
| *Freshness* | *Data older than the [contract's](data-contract.md) stated SLA* | |
| *Volume* | *Row count outside an expected range* | |
| *Schema* | *An unexpected column added, removed, or retyped* | |

---

## Notes on using this template

*Delete this section too.*

**Idempotency is not an optimization, it is close to a definition.** A pipeline that cannot be safely rerun cannot be safely operated: every on-call response to a partial failure becomes a judgment call about whether rerunning will make things worse.

**Design the backfill path before you need it.** A pipeline built only to process "today" turns every historical correction into a special one-off script, written under pressure, that has never been tested. A pipeline built to accept a date parameter from day one turns the same correction into the same code path used every day.

**A loud failure is a feature.** Resist the instinct to make a pipeline resilient to bad input by silently dropping or defaulting it. A dropped row that nobody notices is a worse outcome than a run that stops and pages someone.

**Where this lives:** docs-as-code, next to the pipeline's own code, for the same reason the general [data model](../../general-swe/foundations/data-model.md) template gives: it is only true relative to a specific version of the code, and separating them guarantees they drift.

---

## Related documents

- [`data-contract.md`](data-contract.md). What this pipeline promises its consumers, and what its own sources promise it
- [`../governance/data-quality-specification.md`](../governance/data-quality-specification.md). The ongoing checks that watch what this document only designs for once
- [`../operations/backfill-and-reprocessing-plan.md`](../operations/backfill-and-reprocessing-plan.md). The record of an actual reprocessing event, using the strategy this document defines
- [`../operations/pipeline-runbook.md`](../operations/pipeline-runbook.md). What an on-call responder does when section 5's failure modes actually happen
- [`../../general-swe/foundations/technical-design-document.md`](../../general-swe/foundations/technical-design-document.md). The base template this one extends
