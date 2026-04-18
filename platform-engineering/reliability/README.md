# Reliability

The three documents Google's Site Reliability Engineering practice built around a single idea: a reliability promise only means something if it has a number and a stated consequence.

## The documents

| Document | Answers |
|---|---|
| [`slo-document.md`](slo-document.md) | What does "reliable" mean for this service, in numbers everyone agrees on? |
| [`error-budget-policy.md`](error-budget-policy.md) | What actually happens when we miss the target? |
| [`toil-log.md`](toil-log.md) | How much of the team's time is going to manual, repetitive work instead of engineering, and is that shrinking? |

## When to use each

**SLO document: any service with a consumer who cares whether it's up.** This does not require Google's scale to be worth doing; it requires only that "is this reliable enough" is currently answered by opinion instead of by a number.

**Error budget policy: as soon as the SLO document exists.** An SLO with no stated consequence for missing it is a number nobody is accountable to. The two are meant to be written together, or close to it.

**Toil log: any on-call rotation, once the team suspects manual work is crowding out actual engineering.** It does not need to start day one. It needs to start before "we're too busy keeping the lights on to fix the thing causing the pages" becomes the team's permanent state.

## Why we use them

Google's SRE book supplies the exact distinction that makes this group work: an SLI is "a carefully defined quantitative measure of some aspect of the level of service that is provided," an SLO is a target value for that measure, and an SLA is an SLO with a stated consequence attached if it's missed. Their own rule for telling an SLO from an SLA is simple and worth repeating here: if there is no explicit consequence, you are looking at an SLO, not an SLA, no matter what anyone calls it internally. Most of what makes an SLO document useful is refusing to let a target quietly become an unenforced suggestion.

The error budget policy is what keeps that refusal real. Its own stated purpose is not punitive: it exists to "protect customers from repeated SLO misses" and to "provide an incentive to balance reliability with other features," explicitly not "to serve as a punishment for missing SLOs." The mechanism that does the actual work is concrete and unambiguous by design: when a service exceeds its error budget, changes and releases halt until it's back within its SLO, other than P0 fixes. A policy without that kind of concrete, automatic trigger is a policy in name only.

The toil log exists because toil, defined by Google's own SRE practice as work that is "manual, repetitive, automatable, tactical, devoid of enduring value, and that scales linearly as a service grows," is invisible in the aggregate unless someone tracks it. A team drowning in toil rarely notices the drowning; they notice they're always behind, without a clear reason why. Naming and counting toil is what turns that vague feeling into a number a team can act on and watch shrink.

## Where these live

**Docs-as-code, next to the service it describes, for the SLO document.** It should be reviewed the way code is reviewed, since a change to an SLO is a change to what the team is accountable for.

**Docs-as-code or wiki for the error budget policy, but visible wherever releases are approved.** Its entire purpose is to be checked at the moment a release decision is made, not filed away.

**Wherever the team already tracks its own work, for the toil log**, reviewed on a set cadence rather than treated as a durable reference. It is an operational record, not a design document.
