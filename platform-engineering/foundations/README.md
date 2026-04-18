# Foundations

The two documents that make a platform capability something other teams can actually find and adopt.

## The documents

| Document | Answers |
|---|---|
| [`service-catalog-entry.md`](service-catalog-entry.md) | What does this platform capability do, and how do I start using it? |
| [`platform-onboarding-guide.md`](platform-onboarding-guide.md) | I've decided to use it. What are the concrete steps to get a team onto it? |

## When to use each

**Service catalog entry: the moment a capability is meant to be used by a team other than the one that built it.** Internal tooling used by one team does not need a catalog entry; it needs a README. The moment a second team is a plausible user, discoverability stops being optional.

**Platform onboarding guide: any capability with more than a trivial setup step.** If using the platform is genuinely one command, the catalog entry's own instructions are enough. If it involves provisioning, configuration, or a migration from something a team already has, it earns its own guide.

## Why we use them

Team Topologies gave platform engineering its standard vocabulary: a platform team's job is to reduce the cognitive load of the teams it serves by providing self-service capabilities, and to do that as "platform as a product," with the same accountability to discoverability and usability a product team owes its own customers. A capability with no catalog entry is invisible to the very teams it was built to help, and an internal platform that isn't easier to adopt than building the thing yourself will not get adopted, no matter how good the engineering behind it is.

The onboarding guide is deliberately not the general [onboarding guide](../../general-swe/foundations/onboarding-guide.md) template, which orients a new hire to a team. This one orients an already-onboarded team onto a platform capability: the paved road, in Team Topologies' language, that lets a team move fast on its own problem instead of reinventing infrastructure the platform team has already solved.

## Where these live

**The platform's own catalog or developer portal, if one exists**, since that is where a team looking for a capability will already be searching. Docs-as-code as a fallback for a team without a dedicated portal tool.

**Docs-as-code, next to the platform tooling itself, for the onboarding guide.** It describes concrete setup steps against a real toolchain, and rots the moment the toolchain changes underneath it if kept anywhere else.
