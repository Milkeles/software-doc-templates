# Pipeline runbook: {Alert or pipeline name}

*Also called: playbook, on-call runbook.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | *The pipeline and the specific alert this handles* |
| **Severity** | *What page level this arrives at* |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |
| **Last executed** | *Date, filled in by whoever ran it* |

*Read the general [runbook](../../general-swe/foundations/runbook.md) template first; the discipline of writing for the person paged at 3am, scanning rather than reading, holds entirely. This adds the questions specific to a data pipeline: is the wrong data already downstream, and is it safe to just rerun this.*

---

## Symptoms

*The alert text, the graph shape, or what a consumer reported. Include both, because a consumer's report ("this dashboard looks wrong") often arrives before the alert does.*

---

## Impact

*What is downstream of this pipeline and how stale or wrong it now is. Cross-reference the [dataset catalog entry's](../foundations/dataset-catalog-entry.md) known consumers.*

---

## Diagnose

### 1. Is this a source problem or a pipeline problem?

```bash
```

- **Source late or malformed:** *go to Remediation A*
- **Pipeline itself failed:** *go to step 2*

### 2. Did this fail before or after publishing output?

*The single most important branch in a data runbook. A failure before publishing is safe: consumers still see the last good data. A failure after partial publishing means wrong data may already be live.*

- **Before publishing:** *go to Remediation B, rerun is safe*
- **After partial publishing:** *go to Remediation C, wrong data may be live*

---

## Remediate

### A. Source late or malformed

1. *Check whether the source has a stated SLA in its own [data contract](../foundations/data-contract.md). If it is within SLA, wait; if not, escalate to the source owner.*
2. *Decide whether to wait or run with partial data, per the pipeline's stated failure-mode response.*

### B. Failed before publishing, safe to rerun

*Confirm the [pipeline design document's](../foundations/data-pipeline-design-document.md) idempotency section before assuming this. If the pipeline is genuinely idempotent, rerunning is the fix.*

1. *Rerun command, in full.*

**Verify.** *Output row count and freshness back within the [contract's](../foundations/data-contract.md) stated range, not "looks fine."*

### C. Wrong data may already be published

1. *Do not simply rerun if the pipeline is not idempotent; a naive rerun may double-count rather than correct.*
2. *Check the [pipeline design document's](../foundations/data-pipeline-design-document.md) backfill strategy for the correct reprocessing approach.*
3. *If the affected range is non-trivial, open a [backfill and reprocessing plan](backfill-and-reprocessing-plan.md) rather than fixing ad hoc.*
4. *Notify known downstream consumers that the data was wrong for the affected window, even before the fix ships.*

---

## If none of this works

*Escalation path, in order, with names or rotas.*

---

## After

- *Update this runbook now.*
- *Record the incident and decide whether it needs a full [incident postmortem](../../general-swe/foundations/incident-postmortem.md), the same threshold the general runbook applies.*
- *If a downstream consumer relied on wrong data before this was caught, note it, even if fixing the pipeline is the only concrete action taken.*

---

## Notes on using this template

*Delete this section too.*

**The published/unpublished branch is the one that matters most.** Every other diagnostic step is secondary to knowing whether wrong data is already downstream, because that changes the response from "fix and rerun" to "fix, notify, and reprocess."

**Do not rerun a non-idempotent pipeline reflexively.** The instinct to "just run it again" is correct for most software incidents and can make a data incident worse. Check the pipeline's own design document before assuming a rerun is safe.

**Where this lives:** docs-as-code, linked from the alert, same as any runbook.

---

## Related documents

- [`../../general-swe/foundations/runbook.md`](../../general-swe/foundations/runbook.md). The base template this one extends
- [`../foundations/data-pipeline-design-document.md`](../foundations/data-pipeline-design-document.md). Idempotency and failure modes this runbook assumes
- [`backfill-and-reprocessing-plan.md`](backfill-and-reprocessing-plan.md). What to open when the fix is bigger than a rerun
- [`../../general-swe/foundations/incident-postmortem.md`](../../general-swe/foundations/incident-postmortem.md). Where a significant miss gets analyzed after the fact
