# Platform onboarding guide: {Capability name}

*Also called: golden path guide, paved road guide.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *The capability this onboards a team onto* |
| **Owner** | |
| **Last used** | *Date and by which team. If nobody has followed this in a while, assume it is stale* |

*This is not the general [onboarding guide](../../general-swe/foundations/onboarding-guide.md), which orients a new hire to a team. This document orients an already-working team onto a platform capability: the paved road that lets them stop solving a problem the platform team has already solved. Write it for an engineer who knows their own system well and knows nothing about this platform.*

---

## Before you start

*Access, accounts, and quotas needed, requested ahead of time. The same principle the general onboarding guide applies to a new hire's first week: access delays are the single largest source of a stalled adoption, and they are avoidable.*

| Access or resource | Requested by | Granted by | Needed by |
|---|---|---|---|
| | | | |

---

## First integration

*A real, small, working integration, reaching the platform in the first session. As with a new hire's first change, this both teaches by doing and tests every step of the onboarding path while someone is watching.*

1. *Step, with the exact command or console action.*
2. *Step.*
3. *Confirm it worked: what to check, and what success looks like.*

**When a step in this list doesn't work, fix the document.** The team going through onboarding is the one best placed to see the gap, while they can still see it.

---

## Moving your real workload over

*Once the first integration works, what a full adoption actually involves: configuration, migration of existing state, cutover.*

| Step | What it involves | Rollback if it goes wrong |
|---|---|---|
| | | |

---

## What you now own versus what the platform owns

*The boundary a team needs to understand before an incident forces them to. State it as plainly as the [service catalog entry's](service-catalog-entry.md) section 3 does, in more operational detail.*

| | Platform's responsibility | Your team's responsibility |
|---|---|---|
| | | |

---

## Getting help

*Support channel, escalation path, and where the platform team's own [runbooks](../../general-swe/foundations/runbook.md) or status page live.*

---

## Notes on using this template

*Delete this section too.*

**A working first integration beats a document full of explanation.** A team that has actually gotten something onto the platform in the first session has tested your onboarding path for real; a team that has only read about it hasn't.

**State the ownership boundary before the first incident, not during it.** The most common cause of a bad on-call experience with a platform dependency is a team discovering, live, that something they assumed the platform handled was actually theirs.

**Update this the moment it breaks for a real team.** The same rule the general onboarding guide gives: ask the onboarding team to fix what tripped them up, while the friction is still fresh.

**Where this lives:** docs-as-code, next to the platform's own tooling, so a tooling change and a guide update are more likely to land in the same review.

---

## Related documents

- [`service-catalog-entry.md`](service-catalog-entry.md). Where a team decides to start this guide in the first place
- [`../../general-swe/foundations/onboarding-guide.md`](../../general-swe/foundations/onboarding-guide.md). The different problem of onboarding a person to a team, not a team to a platform
- [`../../general-swe/foundations/runbook.md`](../../general-swe/foundations/runbook.md). What a team follows once something goes wrong after onboarding is done
