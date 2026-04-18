# Disaster recovery plan: {System or service}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |
| **Last tested** | *Date and outcome. A plan never tested is fiction, not a plan* |

*This follows NIST SP 800-34's contingency planning guidance. Three terms, kept separate rather than blended into one "how bad can it get": Maximum Tolerable Downtime (MTD), Recovery Time Objective (RTO), and Recovery Point Objective (RPO). Determine each from a business impact analysis, not by asserting a number that sounds reasonable.*

---

## 1. Business impact analysis

*What this system supports, and what breaks if it's unavailable. This is what should determine the targets below, not the other way around.*

| | |
|---|---|
| **Mission or business process supported** | |
| **Impact if unavailable** | *Revenue, safety, legal, or reputational, stated concretely* |
| **Maximum Tolerable Downtime (MTD)** | *The total outage time the business can accept, all impacts considered* |

---

## 2. Recovery targets

| | |
|---|---|
| **Recovery Time Objective (RTO)** | *Must be shorter than the MTD above. Include any reprocessing time needed after systems are back, since that eats into the same budget* |
| **Recovery Point Objective (RPO)** | *How much data loss, as a point in time before the disruption, is tolerable. Distinct from RTO: this is about data loss, not downtime* |

**RTO and RPO answer different questions, and conflating them is the most common mistake in this document.** RTO is how long you can be down. RPO is how much data you can afford to have lost when you come back up. A system can have a short RTO and a long RPO, or the reverse, and the plan needs both numbers stated separately.

---

## 3. Recovery strategy

| | |
|---|---|
| **Alternate site or region** | |
| **Alternate processing method** | *Failover, manual process, or degraded mode, if full recovery takes longer than the RTO allows* |
| **Backup approach** | *Frequency, and whether it can actually meet the stated RPO* |

*Verify explicitly that your backup frequency can meet the stated RPO. A daily backup cannot deliver a four-hour RPO, no matter what the plan says elsewhere.*

---

## 4. Recovery procedure

*The actual steps, in order, with named owners. Link the [runbook](../../general-swe/foundations/runbook.md) if the recovery is procedural enough to have one.*

| Step | Action | Owner | Expected duration |
|---|---|---|---|
| | | | |

---

## 5. Testing, training, and exercises

*NIST names this as a distinct, required step, not an optional add-on. Testing validates that the plan's recovery capability actually works; training validates that the people executing it know how. Neither substitutes for the other.*

| | |
|---|---|
| **Test type** | *Tabletop, functional, or full failover* |
| **Frequency** | |
| **Last conducted** | |
| **Findings from last test** | |

---

## Notes on using this template

*Delete this section too.*

**The business impact analysis comes first, not the recovery targets.** A plan that asserts an RTO without a stated business reason behind it is a number nobody can defend when it's expensive to meet.

**Keep RTO, RPO, and MTD as three separate fields.** They get conflated constantly in casual conversation; this document is where the conflation has to stop.

**An untested plan is not a plan.** Treat "last tested" as seriously as "last reviewed." A recovery procedure nobody has actually exercised is a hypothesis, not a capability.

**Where this lives:** docs-as-code, with a rendered copy kept somewhere reachable independent of the system it describes. A disaster recovery plan only accessible through the system that's currently down has failed at its one job.

---

## Related documents

- [`../../general-swe/foundations/runbook.md`](../../general-swe/foundations/runbook.md). The procedural steps behind section 4, for the parts that are routine enough to script
- [`../../general-swe/foundations/incident-postmortem.md`](../../general-swe/foundations/incident-postmortem.md). Where an actual invocation of this plan gets reviewed afterward
- [`capacity-plan.md`](capacity-plan.md). Whether the alternate site or region in section 3 actually has the capacity to absorb full production load
