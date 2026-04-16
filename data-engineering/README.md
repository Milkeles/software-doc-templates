# Data engineering

Documents for teams that move, store, and transform data other teams depend on.

These sit on top of [`general-swe/`](../general-swe/), not instead of it. A data team still writes architecture decision records, runbooks, and incident postmortems. This area covers what a pipeline adds that a typical service does not: a producer and a consumer who may never talk to each other, a rerun that has to produce the same answer as the first run, and a failure that can silently corrupt a number before anyone notices it is wrong.

---

## Groups

| Group | Use it when |
|---|---|
| [`foundations/`](foundations/) | Always. What a pipeline does, what a dataset means, and the agreement between whoever produces data and whoever consumes it. |
| [`governance/`](governance/) | More than one team depends on data you did not personally produce, or a dataset needs to answer "can I trust this" and "where did this come from" for someone who was not in the room when it was built. |
| [`operations/`](operations/) | The pipeline is live: it runs on a schedule, it can fail, and someone has to fix a wrong number without doubling it. |

There is no methodology split here, for the same reason web development has none: Scrum and Kanban do not change what a data contract has to say.

---

## What makes data documentation different

Three things are true of a data pipeline that are not true of a typical service, and most of this area exists because of them.

**The producer and the consumer are often strangers.** A data contract exists because the person generating an event in application code and the analyst building a dashboard from it may never meet, and by the time the analyst discovers a field changed meaning, the damage is already in a report. This is the same boundary problem [`interface-control-document.md`](../general-swe/foundations/interface-control-document.md) solves for an API, applied to a dataset instead of a call.

**A pipeline has to be safe to run twice.** Code that isn't idempotent fails loudly. A pipeline that isn't idempotent fails quietly: rerun it after a partial failure and it doubles yesterday's revenue instead of crashing. Idempotency and a stated backfill strategy are not optional hardening for a data pipeline the way they might be for a web service; they are close to the definition of a pipeline that can be operated at all.

**A wrong number rarely pages anyone.** A service that returns errors gets noticed. A dashboard that quietly reports the wrong number gets used, sometimes for months, because nothing about a wrong number looks like a failure. Data quality checks, lineage records, and a stated freshness target exist because the alternative to writing them down is discovering the number was wrong from someone who acted on it.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| Data pipeline design document | Docs-as-code | Describes the pipeline, rots fastest separated from its code |
| Data contract | Docs-as-code, ideally as the schema file the pipeline enforces | Only trustworthy if a change to it breaks a build |
| Dataset catalog entry | The data catalog tool, if one exists; docs-as-code otherwise | Its readers are searching for a dataset, not reading a repository |
| Data quality specification | Docs-as-code, next to the checks it describes | An unenforced expectation is a wish |
| Data classification and access policy | Wiki, owned jointly by data governance and security | Changes by policy decision, not by code change |
| Data lineage record | Generated from the catalog or lineage tool where possible; this template is for teams without one | Lineage that is hand-maintained goes stale within a quarter |
| Backfill and reprocessing plan | Wherever the change is tracked, one per backfill | Short-lived, like a rollout plan |
| Pipeline runbook | Docs-as-code, linked from the alert | Same reasoning as any runbook |
| Freshness and SLA log | Docs-as-code, next to the data contract it measures against | A record of whether a promise was kept |

---

## What to write first

1. **Data contract**, for any dataset a team other than its producer depends on. Before the second consumer arrives, not after the second incident.
2. **Data pipeline design document**, once a pipeline has more than one stage or a backfill has ever been needed.
3. **Dataset catalog entry**, once discovering what data exists takes longer than asking someone who remembers.
4. The rest as the need appears, governance and operations both scaling with how many teams and how much history depend on the data.
