# Operations

The three documents that matter once a pipeline is live: something ran wrong, something needs fixing without making it worse, and someone needs to know whether a promise is actually being kept.

## The documents

| Document | Answers |
|---|---|
| [`backfill-and-reprocessing-plan.md`](backfill-and-reprocessing-plan.md) | We need to reprocess a period of data. What's the safe way to do it, and who needs to know? |
| [`pipeline-runbook.md`](pipeline-runbook.md) | The pipeline failed. What does an on-call responder do about it, right now? |
| [`freshness-and-sla-log.md`](freshness-and-sla-log.md) | Are we actually meeting the SLA we promised, measured over time? |

## When to use each

**Backfill and reprocessing plan: any time historical data is being reprocessed on purpose.** A routine daily run does not need one. A one-off correction touching weeks or months of history does, for the same reason a [deployment plan](../../general-swe/foundations/deployment-plan.md) exists for a routine release: the stakes and the blast radius are large enough that "run the script" is not a plan.

**Pipeline runbook: any pipeline that pages someone when it fails.** If a failure requires no judgment, automate the fix and delete the runbook, the same rule the general [runbook](../../general-swe/foundations/runbook.md) template gives. What earns a runbook here is the failure a person has to reason about: a schema drift, a source that's late for a reason that changes the response.

**Freshness and SLA log: any dataset with a stated SLA in its [data contract](../foundations/data-contract.md).** A contract with a promised freshness target and no record of whether it was met is a promise nobody is checking.

## Why we use them

A backfill is the moment a data pipeline's central risk, a rerun that is not safe to run twice, actually gets exercised on purpose rather than by accident. The plan exists to make that a deliberate, scoped, communicated event instead of a script someone runs at their desk and hopes about.

The pipeline runbook exists for the reason any runbook does: a wrong number rarely announces itself as an emergency the way a service outage does, and the person paged for it needs a written path to diagnosis that does not depend on already knowing the pipeline's history.

The freshness and SLA log exists because a target that is never measured against reality quietly becomes fiction. It plays the same role for a data contract's promises that the game-development [balance log](../../game-development/live-operations/balance-log.md) plays for a tuning change: a record of what was promised, and what was actually true, kept honest by writing down misses as plainly as hits.

## Where these live

**Wherever the change is tracked, one per backfill, for the backfill plan.** Short-lived, like a rollout plan; done when the reprocessing completes.

**Docs-as-code, linked from the alert, for the pipeline runbook.** Same reasoning as any runbook: versioned with the system, reachable when the system it describes is down.

**Docs-as-code, next to the data contract it measures against, for the freshness and SLA log.** A record of promise-versus-reality belongs next to the promise.
