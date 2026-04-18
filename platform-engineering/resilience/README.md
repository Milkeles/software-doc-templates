# Resilience

The two documents that plan for what happens when normal operating assumptions stop holding: a major outage, or growth outrunning capacity.

## The documents

| Document | Answers |
|---|---|
| [`disaster-recovery-plan.md`](disaster-recovery-plan.md) | If we lose a system, a site, or a region, how do we recover, and how much do we lose? |
| [`capacity-plan.md`](capacity-plan.md) | Do we have enough headroom for expected growth, and when do we run out? |

## When to use each

**Disaster recovery plan: any system whose extended loss would be a business event, not just an incident.** A service with a same-day fix and no lasting consequence does not need one. A system whose loss threatens data, revenue, or the business's ability to operate does, regardless of how rarely that loss is expected to happen.

**Capacity plan: any system with a growth trend, once "we'll notice when we're close" stops being a safe assumption.** Below that scale, watching a dashboard is capacity planning. Above it, a written, revisited forecast is the difference between scaling on a schedule and scaling in an incident.

## Why we use them

NIST's federal contingency planning guide, SP 800-34, supplies the vocabulary and the discipline this group runs on, and it is worth taking directly rather than reinventing: a Recovery Time Objective (RTO) is the maximum time a resource can be unavailable before the impact becomes unacceptable; a Recovery Point Objective (RPO) is how much data loss, measured as a point in time, the business can tolerate; and a Maximum Tolerable Downtime (MTD) is the outer bound the RTO has to fit inside. These three are easy to blend into one vague "how bad can it get" conversation, and the guide's own point is that they answer different questions and need separate, explicit values. The guide also names testing and exercising the plan as a distinct required step, not an afterthought: an untested plan and a tested one are not the same document, whatever they claim on paper.

A capacity plan exists because industry guidance on the right amount of headroom to carry genuinely disagrees, from roughly 10% to 50% depending on the source, which is itself the finding worth keeping: there is no single correct number to borrow, only a risk-based decision a team has to make and revisit against its own actual burstiness and its own actual ability to react. The plan's real job is not picking the "right" percentage; it's making the choice explicit and checking it against reality on a schedule, rather than discovering the limit during a traffic spike.

## Where these live

**Docs-as-code for the disaster recovery plan, with a rendered copy reachable somewhere that does not depend on the systems it describes.** The same logic a runbook follows: a plan only reachable through the thing that's currently down is not a usable plan.

**Wiki or the tracker already holding the forecast, for the capacity plan**, revisited on a set cadence rather than written once and left. A forecast is a living document by nature; docs-as-code review overhead works against the frequent, lightweight updates it needs.
