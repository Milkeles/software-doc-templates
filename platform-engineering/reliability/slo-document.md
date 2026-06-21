# SLO document: {Service name}

*Also called: SLO spec, SLO definition document.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Status** | *Draft, approved, or under revision* |
| **Author** | |
| **Reviewers** | |
| **Approvers** | |
| **Approval date** | |
| **Revisit by** | *A date, not "periodically"* |

*This follows the structure Google's SRE practice uses for its own worked SLO documents. Three terms, kept distinct: an SLI is what you measure. An SLO is the target for that measurement. An SLA is an SLO with a stated consequence attached if it's missed. If this document has no consequence attached anywhere, it is describing SLOs, not SLAs, whatever a reader assumes from the word "target."*

---

## 1. Service overview

*Plain description of what the service does and who its consumers are. Someone unfamiliar with this service should understand what it's for from this section alone.*

---

## 2. SLIs and SLOs

*One row per indicator. State the SLI precisely enough that two different people, given the same underlying data, would compute the same number. A vague SLI produces an argument during the next incident, not before it.*

| Category | SLI | SLO | Measured where |
|---|---|---|---|
| *Availability* | *e.g. fraction of requests with a non-5xx response* | *e.g. 99.9% over a rolling 28 days* | *e.g. load balancer* |
| *Latency* | | | |
| *Freshness* | *If this service serves data rather than requests* | | |

**Start from what users care about, not from what you can already measure.** A latency number pulled from an existing dashboard because it's convenient is not the same thing as the number your users would actually notice degrading.

**Do not aim for 100%.** It is both unreachable in practice and, because it leaves no room for controlled risk or iteration, not actually the target you want.

---

## 3. Rationale

*Why these targets, not others. State the measurement period the targets were derived from, so a reader can tell whether this was calibrated against real data or asserted.*

---

## 4. Error budget

*100% minus the SLO, stated per objective, not as one number for the whole service. A 99.9% availability SLO leaves a 0.1% budget: for one million requests over the period, that is 1,000 permitted failures.*

| SLO | Error budget | Budget period |
|---|---|---|
| | | |

*See the [error budget policy](error-budget-policy.md) for what happens when this is exhausted.*

---

## 5. Clarifications and caveats

*Anything a reader would otherwise assume incorrectly. Where in the stack the SLI is measured, what's excluded from the count, known gaps in measurement.*

---

## Notes on using this template

*Delete this section too.*

**An SLO with no error budget policy behind it is not enforced by anything.** Write section 4 and the linked policy together; an SLO that nobody is required to act on when it's missed will drift into meaninglessness within a quarter.

**Keep the SLI count small.** A service with fifteen tracked SLIs has no real priorities, only a dashboard. Pick the few that would actually change a decision if they moved.

**Set internal targets tighter than any externally advertised ones.** The margin is what lets you catch a slide before a customer-facing promise is actually broken.

**Where this lives:** docs-as-code, next to the service it describes, reviewed the way a change to the service itself would be.

---

## Related documents

- [`error-budget-policy.md`](error-budget-policy.md). What happens when section 4's budget runs out
- [`../resilience/capacity-plan.md`](../resilience/capacity-plan.md). Whether the infrastructure behind this service can actually sustain the SLO under growth
- [`../foundations/service-catalog-entry.md`](../foundations/service-catalog-entry.md). Where this document's targets are summarized for a consuming team
