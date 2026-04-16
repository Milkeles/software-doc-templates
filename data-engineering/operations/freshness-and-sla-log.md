# Freshness and SLA log: {Dataset name}

*Italic text is guidance. Delete it as you fill each section in.*

*A [data contract](../foundations/data-contract.md) states a target. This log states whether reality matched it. Keep both, the same way the game-development [balance log](../../game-development/live-operations/balance-log.md) keeps a designer's intended value next to what a change actually measured: a promise nobody checks against reality quietly becomes fiction.*

---

## The log

| Period | Promised freshness | Actual | Met? | Cause of miss |
|---|---|---|---|---|
| | | | | |

*Record misses as plainly as hits. A log with no misses in it either had a perfect record or is not being kept honestly, and the second is far more likely, the same caution the balance log applies to reverted changes.*

---

## Recurring misses

*A single miss is an incident. The same cause appearing twice is a pattern worth a design change, not another apology.*

| Cause | Times seen | Action taken |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**A target that is never measured is not a guarantee, whatever the contract calls it.** This log is what makes the [data contract's](../foundations/data-contract.md) service level section an actual claim rather than an aspiration nobody checks.

**Log the miss, not just the average.** A dataset that is on time 29 days out of 30 and three hours late on the 30th has a real problem the average hides. Keep the period-by-period record, not just a rolled-up percentage.

**A recurring cause is a design problem, not an operations problem.** If the same upstream dependency causes the miss every month, the fix belongs in the [pipeline design document](../foundations/data-pipeline-design-document.md), not in another round of manual intervention.

**Where this lives:** docs-as-code, next to the data contract it measures against.

---

## Related documents

- [`../foundations/data-contract.md`](../foundations/data-contract.md). The promise this log measures against
- [`../foundations/data-pipeline-design-document.md`](../foundations/data-pipeline-design-document.md). Where a recurring miss's root cause gets fixed
- [`pipeline-runbook.md`](pipeline-runbook.md). What happens the moment a miss is detected, before it reaches this log
