# Platform engineering

Documents for a team whose customers are other engineering teams.

These sit on top of [`general-swe/`](../general-swe/), not instead of it. A platform team still writes architecture decision records, runbooks, and incident postmortems for its own systems. This area covers what changes when a team's job is building the ground other teams stand on: a promise about reliability has to be a number, not a feeling, and a platform that isn't easier to use than doing it yourself will simply not get used.

---

## Groups

| Group | Use it when |
|---|---|
| [`foundations/`](foundations/) | Always. What the platform offers, and how a team actually gets onto it. |
| [`reliability/`](reliability/) | The platform, or a service on it, has users who need to know how reliable it is, in numbers rather than in reassurance. |
| [`resilience/`](resilience/) | You need to plan for how the platform survives a major failure, and how much capacity it has before it doesn't. |

There is no methodology split here, for the same reason web development and data engineering have none.

---

## What makes platform documentation different

Two things distinguish a platform team's documentation from a typical service team's, and this area exists because of them.

**Your product is used by other engineers, and adoption is optional.** A platform team cannot mandate its way to being used; Team Topologies' framing of "platform as a product" exists precisely because a platform team that treats its own users as a captive audience, rather than as customers who can build around it, ends up ignored. A service catalog entry and an onboarding guide exist because discoverability and ease of adoption are not nice-to-haves for internal tooling, they are the entire mechanism by which a platform earns use.

**A reliability promise that has no number and no consequence is not a promise.** Google's Site Reliability Engineering practice supplies the vocabulary this area runs on: an SLI is what you measure, an SLO is the target, and an SLA is the target with a stated consequence attached if it's missed. Most of what makes SRE practice different from good intentions is refusing to call something a guarantee unless it has both a number and a consequence.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| Service catalog entry | The platform's own catalog or portal, if one exists; docs-as-code otherwise | Its readers are searching for a capability, the same as any catalog |
| Platform onboarding guide | Docs-as-code, next to the platform's own tooling | Describes the tooling, rots fastest separated from it |
| SLO document | Docs-as-code, next to the service it describes | Reviewed alongside the service; an SLO nobody enforces in code review drifts from reality |
| Error budget policy | Docs-as-code or wiki, but must be visible to whoever approves releases | Its entire function is to be checked before a risky release ships |
| Toil log | Wherever the team already tracks its own work, reviewed on a set cadence | A rolling operational record, not a durable reference |
| Disaster recovery plan | Docs-as-code, with a rendered copy reachable when primary systems are down | Same reasoning as a runbook: useless if it's only reachable through the thing that's down |
| Capacity plan | Wiki or the tracker holding the forecast, revisited on a set cadence | A living forecast, not a one-time document |

---

## What to write first

1. **Service catalog entry**, the moment a second team starts depending on something you built for internal use only. A platform capability nobody can find is not being used as a platform.
2. **SLO document**, once any team outside your own depends on a service you run. Before someone asks what "reliable" means, not after an incident forces the question.
3. **Error budget policy**, the moment the SLO document exists, since an SLO with no stated consequence for missing it is an aspiration, not an operating rule.
4. The rest as scale and risk justify: a disaster recovery plan once an outage would be catastrophic rather than merely bad, a capacity plan once growth is fast enough that "we'll notice when we're close" stops being true.
