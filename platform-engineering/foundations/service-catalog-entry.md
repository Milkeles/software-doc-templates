# Service catalog entry: {Capability name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | *A named, reachable team* |
| **Status** | *GA, beta, deprecated, or being replaced by {capability}* |
| **Last reviewed** | YYYY-MM-DD |

*A platform team that treats its own capabilities as a product, not just as infrastructure, gives them a roadmap, a feedback loop, and a discoverable entry a customer team can find without asking around. This is that entry. Write it the way you would write a product's landing page: what it does, what it costs the reader to adopt, and how to get started, in that order.*

---

## 1. What this is and who it's for

*Two or three sentences. What problem does this solve, and for which kind of team? Lead with the benefit to the reader, not with the implementation.*

---

## 2. Getting started

| | |
|---|---|
| **Self-service?** | *Can a team provision or adopt this without filing a ticket? If not, say so plainly rather than implying a paved road that isn't one* |
| **Setup time** | *Realistic, not aspirational* |
| **Prerequisites** | |
| **Full onboarding guide** | *Link the [platform onboarding guide](platform-onboarding-guide.md) if setup is more than trivial* |

---

## 3. What you're agreeing to

*The reliability and support promise this capability makes, and what it does not. State both, since an unstated boundary gets discovered during an incident.*

| | |
|---|---|
| **SLO** | *Link the [SLO document](../reliability/slo-document.md) if one exists* |
| **Support channel** | |
| **Escalation** | *For when the support channel doesn't respond fast enough* |
| **What this capability does not cover** | *The boundary of the paved road: what a team is on their own for if they adopt this* |

---

## 4. Alternatives and exit

| | |
|---|---|
| **What teams did before this existed** | |
| **How to leave** | *If a team outgrows or needs to move off this capability, what does that migration look like* |

*Naming the exit path is not a sign the capability is expected to fail. It's the same honesty a [deprecation plan](../../general-swe/foundations/deprecation-plan.md) requires: a capability with no stated way off is one every future migration has to invent from scratch.*

---

## Notes on using this template

*Delete this section too.*

**Write this for someone who has never talked to your team.** The test is whether a team can decide to adopt this and take the first step without a Slack message. If they can't, the catalog entry isn't finished.

**Say what this capability does not cover, not just what it does.** The gap between what a team assumes a platform handles and what it actually handles is where the worst incidents happen, discovered at the worst time.

**Keep the status field honest.** A capability marked GA that is actually still stabilizing sets an expectation the platform team cannot meet. Beta is a legitimate status; a false GA is not.

**Where this lives:** the platform's own catalog or developer portal if one exists, since that's where a searching team will already be looking. Docs-as-code otherwise.

---

## Related documents

- [`platform-onboarding-guide.md`](platform-onboarding-guide.md). The concrete steps behind section 2's "getting started"
- [`../reliability/slo-document.md`](../reliability/slo-document.md). The specific numbers behind section 3's reliability promise
- [`../../general-swe/foundations/deprecation-plan.md`](../../general-swe/foundations/deprecation-plan.md). How this capability itself gets retired, when that day comes
