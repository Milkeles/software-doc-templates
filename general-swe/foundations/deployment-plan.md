# Deployment plan: {Release}

*Also called: release plan, rollout plan.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Release** | *Version or build identifier.* |
| **Planned window** | YYYY-MM-DD, HH:MM to HH:MM, timezone |
| **Deployment owner** | *One person, running it.* |
| **Go/no-go decision** | *One person or named group. Not the same as the owner.* |
| **Can call rollback** | *Anyone on this list, without seeking approval.* |

---

## First, decide whether you need this document

*Most deployments should not have one. If you ship several times a day through a pipeline that canaries and rolls back automatically, the pipeline is the plan, and a per-release document is theatre that slows you down without making anything safer.*

**Write a plan for a specific deployment when at least one is true.**

- Something in it cannot be rolled back. A destructive migration, a third-party cutover, an outbound notification.
- It has to be coordinated with another team, a customer, or a vendor.
- It requires a maintenance window or planned downtime.
- It is the first deployment of a new component, or the first after a serious incident.
- Someone outside engineering must approve it, for contractual or regulatory reasons.

**Otherwise, write the deployment procedure once as a [runbook](runbook.md)** and let each release reference it. A plan rewritten from a template every Tuesday stops being read by the third Tuesday.

---

## What ships

*The release contents, precisely enough that someone could verify them afterwards.*

| | |
|---|---|
| **Build** | *Artefact identifier and the commit it was built from.* |
| **Supersedes** | *The version currently running.* |
| **Includes** | *Link the changelog entry. Do not restate it.* |
| **Also shipping** | *Migrations, config changes, feature flag states, infrastructure changes, documentation.* |

*That last row is where deployments go wrong. Code is the part people track; the schema change, the new environment variable and the flag default are the parts that get forgotten and then break something.*

---

## Go / no-go

*The conditions checked immediately before starting, and who confirms each.*

| Condition | Confirmed by | Status |
|---|---|---|
| *All required checks green on the release commit* | *CI, automatically* | |
| *No open S1 defects against this release* | *QA lead* | |
| *On-call is staffed and has been told* | *Deployment owner* | |
| *Rollback tested against the staging database* | *Deployment owner* | |

*Every condition needs a person, not a team. IEEE 828's release management clause asks for exactly two things before any release: the "delivery qualification criteria for delivering a release" and "the person(s) or group(s) who will make the decision to deliver a release". Those two are this table.*

**No-go is a normal outcome.** *Say so here, and name the next available window. A plan that treats no-go as a failure produces deployments that proceed on bad conditions.*

---

## Sequence

*Ordered steps, each with an owner and an expected duration. Include the checks between steps, because the gaps are where a bad deployment is caught.*

| # | Step | Owner | Expected | Check before continuing |
|---|---|---|---|---|
| 1 | *Enable maintenance banner* | | *1 min* | *Banner visible on production* |
| 2 | *Run migration `0043_add_refund_reason`* | | *4 min* | *Migration reports success. Row count unchanged* |
| 3 | *Deploy to canary (5% of traffic)* | | *3 min* | *See evaluation below* |
| 4 | *Deploy to remaining fleet* | | *8 min* | *Error rate and latency within limits* |
| 5 | *Remove banner, close the window* | | *1 min* | |

*Give a real expected duration for each step. Without it, nobody in the room knows whether step 3 taking twenty minutes is a problem or normal, and that is the moment when a rollback decision is either made or missed.*

---

## Canary evaluation

*Delete this section if you deploy to everything at once. Keep it and be specific if you do not.*

*Google's SRE workbook defines canarying as "a partial and time-limited deployment of a change in a service and its evaluation", and names three things a canary process needs: a way to deploy to a subset, an evaluation process that decides good or bad, and "integration of the canary evaluations into the release process". The third is the one teams skip, and a canary whose verdict is a person glancing at a dashboard is not integrated into anything.*

| | |
|---|---|
| **Population** | *5% of production traffic, all regions* |
| **Duration** | *20 minutes* |
| **Compared against** | *The remaining 95%, over the same period* |
| **Fails if** | *Error rate exceeds control by 0.5 points, or p99 latency exceeds control by 200 ms* |
| **On failure** | *Automatic rollback. No human decision* |

**Compare against a concurrent control, not against yesterday.** *The same source: "because time is one of the biggest sources of change in observed metrics, it is difficult to assess degradation of performance with before/after evaluation."*

**Pick few metrics.** *"Too many metrics can bring diminishing returns, and at some point, the returns are outweighed by the cost of maintaining them."*

*Two limits worth stating if they apply to you. Isolation is never perfect, so "bad behavior of the canary deployment can also negatively impact the control". And asynchronous pipelines need a canary duration longer than the time it takes to process one work unit, or you will measure nothing.*

---

## Rollback

*Decided now, in writing, while nobody is under pressure.*

| | |
|---|---|
| **Trigger** | *The specific conditions. Not "if it looks bad".* |
| **Method** | *The exact command or pipeline job.* |
| **Expected duration** | |
| **Last tested** | YYYY-MM-DD, *against which environment* |
| **Who may call it** | *Named people, who do not need to ask anyone* |

**Name what cannot be rolled back.** *This is the section that earns the document.*

| Irreversible action | Why | Mitigation |
|---|---|---|
| *Dropping `orders.legacy_ref`* | *Data is gone* | *Deferred to next release. This one only stops writing to it* |
| *Customer emails on refund completion* | *Already sent* | *Feature flag off by default, enabled after the deploy is confirmed* |

*Code rolls back. Data, outbound messages and third-party state do not. If a step in the sequence above is irreversible, either move it to a separate release or accept that "rollback" means forward-fix only, and say which.*

---

## After

*Record the release. IEEE 828 asks for five fields as a minimum, and they are the ones an auditor or an incident responder will want six months from now.*

| | |
|---|---|
| **Date released** | |
| **Delivered to** | *Which environments, which customers* |
| **State** | *Released / superseded / archived* |
| **Environment** | *OS, runtime, platform versions* |
| **Supersedes** | |

*Note that "release tracking is often required for compliance with external laws and regulations. It may also be a contractual requirement." If that applies to you, this table is not optional and should be generated by the pipeline rather than typed.*

**What to do afterwards.** *Who watches what, for how long. Name the point at which the release is considered stable and the extra attention stops.*

---

## Notes on using this template

*Delete this section too.*

**Deploy smaller, more often, for a reason that is not speed.** Google's release engineering chapter puts it plainly: "frequent releases result in fewer changes between versions. This approach makes testing and troubleshooting easier." The benefit is a shorter suspect list when something breaks. That argument survives in places where "move faster" does not.

**Builds must be reproducible or none of this holds.** The same source: "if two people attempt to build the same product at the same revision number in the source code repository on different machines, we expect identical results." A rollback to version 4.2 is only meaningful if version 4.2 is one specific thing.

**Separate the deploy from the release.** Shipping code and turning a feature on are different events, and treating them as one is what forces risky rollbacks. A feature behind a flag can be deployed on Tuesday and released on Thursday, and turned off in seconds without a redeployment.

**Automate every check you wrote down.** Anything on the go/no-go table that a human confirms by looking is a check that will eventually be confirmed by someone who did not look.

**Where this lives:** with the release ticket, not in the repository. It is dated, single-use, and its readers include people who do not clone the code. The *procedure* it references does belong in the repository, as a runbook beside the pipeline configuration.

---

## Related documents

- [`runbook.md`](runbook.md). The repeatable procedure this plan should be referencing
- [`changelog.md`](changelog.md). What is in the release, stated once
- [`release-notes.md`](release-notes.md). The same release, written for customers
- [`configuration-management-plan.md`](configuration-management-plan.md). What counts as a release and how it is baselined
- [`incident-postmortem.md`](incident-postmortem.md). Where a deployment that went wrong is examined
- [`branching-strategy.md`](branching-strategy.md). Where the release branch and hotfix path are defined
