# Incident Response Plan

> What happens in the first hour, decided before the first hour.
>
> **Also called:** IRP, Incident Response Playbook, or Cyber Incident Response Plan (CIRP).
>
> **The reference model changed in 2025.** NIST SP 800-61 Revision 3, *Incident Response Recommendations and Considerations for Cybersecurity Risk Management: A CSF 2.0 Community Profile* (April 2025), supersedes Revision 2 and replaces the familiar four-phase lifecycle with the six CSF 2.0 Functions. Almost every article online still describes the four-phase model. It is no longer NIST's.
>
> **Rev 3 is not a playbook.** It deliberately removed Rev 2's operational detail to become a risk-management profile. For concrete handling steps, use Rev 2 as the historical source or ISO/IEC 27035-3, and write your own procedures here.
>
> **The deadline that shapes everything.** GDPR gives 72 hours to notify a supervisory authority. NIS2 gives 24 hours for an early warning. So **someone must be able to make a regulatory-notification judgement within 24 hours, including at 2am on a Sunday.** That is a staffing and escalation requirement, not a paperwork one, and it is the main reason this document exists.
>
> **Where it lives.** Wiki, plus an offline copy. A plan reachable only through the systems that are down is not a plan. See the group [README](README.md).
>
> **Delete this block before publishing.**

---

## 1. Scope and definitions

What counts as an incident, and what does not. Be precise enough that two people classify the same event the same way.

Define at least: **event**, **incident**, **personal data breach**, and **major incident**. The last one is the trigger for this document; the others are not.

**Define severity levels and tie each to a response.** A level with no consequence attached is a label.

| Level | Means | Response |
|---|---|---|
| SEV1 | Confirmed data exposure, or total loss of service | Page immediately. Incident commander appointed. Legal and DPO notified within 1 hour |
| SEV2 | Degraded service, or suspected compromise unconfirmed | Page during hours. Assess within 4 hours |
| SEV3 | Contained, no user impact, no data at risk | Ticket. Review at the next weekly |

---

## 2. The lifecycle you are using

State which model you follow. NIST is explicit that the choice is yours: "Organizations should use the incident response life cycle framework or model that suits them best."

The current NIST model organises response around the six CSF 2.0 Functions, and its shape carries an argument worth understanding:

```
   PREPARATION, which is not incident response
   ----------------------------------------------------
   GOVERN     strategy, expectations and policy
   IDENTIFY   understand your current risks
   PROTECT    safeguards that reduce what can happen

   CONTINUOUS IMPROVEMENT, during and after
   ----------------------------------------------------
   IDENTIFY (Improvement)  feeds back at every stage,
                           not only at the end

   INCIDENT RESPONSE ITSELF
   ----------------------------------------------------
   DETECT     find and analyse the compromise
   RESPOND    act on it
   RECOVER    restore assets and operations
```

**Why NIST moved.** Verbatim from Rev 3: "incidents were relatively rare, the scope of most incidents was narrow and well-defined, and incident response and recovery was usually completed within a day or two… However, the current state of incident response has greatly changed since then. Today, incidents occur frequently and cause far more damage. Recovering from them often takes weeks or months… The lessons learned during incident response should often be shared as soon as they are identified, not delayed until after recovery concludes."

That last clause is the practical change. Improvement is continuous, not a phase you reach after recovery. If your process only captures lessons at a postmortem, you lose the ones discovered on day two of a three-week incident.

If you are migrating from the old model, NIST publishes the mapping:

| Rev 2 phase | CSF 2.0 Functions |
|---|---|
| Preparation | Govern; Identify (all); Protect |
| Detection and Analysis | Detect; Identify (Improvement) |
| Containment, Eradication and Recovery | Respond; Recover; Identify (Improvement) |
| Post-Incident Activity | Identify (Improvement) |

---

## 3. Roles

Name the roles, not the people. People leave; a document naming individuals is stale within a year. Maintain the mapping in the on-call rota instead.

| Role | Owns |
|---|---|
| Incident commander | Decisions and coordination. Does not fix things |
| Technical lead | Diagnosis and remediation |
| Communications lead | Internal updates, status page, customers |
| Legal and privacy | Notification obligations. Reachable within 1 hour for SEV1 |
| Scribe | Timeline as it happens, not reconstructed afterward |

**The incident commander must not also be the person fixing it.** The commonest failure in small teams, and the reason incidents run long: the one person who understands the system is simultaneously debugging, updating stakeholders, and deciding whether to notify a regulator.

For a small team, one person may hold several roles. Say which combinations are allowed and which are not.

---

## 4. Declaring an incident

How anyone raises one, and what happens next. Include the channel, the command, and the escalation path if nobody responds.

**Make declaring cheap.** A process where declaring an incident feels like an accusation produces late declarations. Say explicitly that over-declaring is fine and costs nothing.

---

## 5. Detect and analyse

What to do first, in order. Log sources, dashboards, and how to tell a real signal from noise.

**Preserve evidence before you fix.** Snapshot the instance, export the logs, capture memory if it matters. The instinct to restore service destroys the evidence that tells you what happened and whether data left.

Two questions decide everything downstream, so answer them explicitly and record the reasoning:

- **Was personal data accessed or exfiltrated?** This starts the GDPR clock.
- **Is the attacker still present?** This decides whether you contain or observe.

---

## 6. Respond

Containment options and their trade-offs. Isolating a host, revoking credentials, disabling a feature, blocking a range.

Record each action with a timestamp and who took it. Record actions considered and rejected too, with the reason.

**Say who can authorise a destructive or customer-visible action** and what happens when they cannot be reached. This is the decision that stalls at 3am.

---

## 7. Notification

The section that must be correct, because errors here are legal errors.

| Obligation | Deadline | Threshold |
|---|---|---|
| GDPR Art. 33, supervisory authority | "without undue delay and, where feasible, not later than 72 hours after having become aware of it" | Unless "unlikely to result in a risk to the rights and freedoms of natural persons" |
| GDPR Art. 34, data subjects | "without undue delay". **No hour count** | "likely to result in a **high risk**" |
| GDPR Art. 33(2), processor to controller | "without undue delay". **No 72-hour figure applies** | Any personal data breach |
| NIS2 Art. 23(4)(a), early warning | **24 hours** | "significant incident" |
| NIS2 Art. 23(4)(b), incident notification | **72 hours** | As above |
| NIS2 Art. 23(4)(d), final report | **One month** after the notification | As above |

Four things this table exists to prevent, all of them common errors:

**72 hours is a backstop, not an allowance.** The primary duty is "without undue delay". Late notification is permitted with reasons, so a missed deadline is not a cliff edge, but planning to use the full 72 hours is not compliance.

**The threshold is negative.** You notify *unless* risk is unlikely. The default is to notify.

**There is no 72-hour rule for telling individuals.** Article 34 says "without undue delay" and nothing else.

**Processors notify the controller, not the regulator.** If you are a processor for customer data, your obligation runs to your customer.

Article 34(3)(a) exempts you from notifying individuals where you "implemented appropriate technical and organisational protection measures… in particular those that render the personal data unintelligible to any person who is not authorised to access it, **such as encryption**". That is the concrete payoff of encryption at rest, and worth stating to anyone who asks why it matters.

**Article 33(5) requires you to document every breach, including the ones you decide not to report**, so that the authority "can verify compliance". Keep an internal breach register. It is a legal requirement, not good practice.

NIS2 is a Directive, so the binding deadlines in your country come from national transposition and may differ. Check.

For US teams: there is no general federal breach law. A multi-state breach can trigger dozens of statutes with different clocks and different definitions of personal information. **Build your plan around the shortest applicable clock** and check the statutes rather than a summary table.

---

## 8. Recover

Restoring service, confirming the attacker is gone, and what must be true before you declare the incident closed.

State the criteria for closure explicitly. Incidents that end because everyone got tired recur.

---

## 9. After

Link the [postmortem](../foundations/incident-postmortem.md). Do not duplicate its structure here.

**A caution about the confidence of this section.** Patterson, Nurse and Franqueira systematically reviewed 30 studies on organisational learning from cyber security incidents for *Computers and Security* (2023) and found: "None of the studies reported that the organisations were exploring how to learn better or had any measures in place to assess their ability to learn and the effectiveness of the improvements made following incidents." The authors add, and it is fair to repeat, "However, it is unclear whether the researchers had sought data on evaluation practices directly."

There is also **no peer-reviewed evidence that blameless postmortems reduce incidents.** The practice rests on experience reports and on psychological-safety research that is about something adjacent. Run them anyway; the argument is that people report accurately when they are not being blamed, which is a claim about candour rather than about outcomes. Do not present it as evidence-backed.

---

## 10. Exercises

The plan is untested until you run it.

- Tabletop the top two scenarios twice a year. An hour each.
- Test the one thing most likely to fail: **reaching a legal or privacy decision-maker out of hours.** The 24-hour clock makes this the highest-value drill available.
- Record what the exercise found and fix it. An exercise with no output is theatre.

---

## Common failures in this document

- **Describes the four-phase NIST model as current.** Superseded in April 2025.
- **Individuals named instead of roles.** Stale within a year.
- **Commander also debugging.** Coordination stops and the incident runs long.
- **Notification thresholds wrong.** Especially "72 hours to tell users" and processors notifying regulators.
- **No offline copy.** Unreachable during the incidents that matter most.
- **Never exercised.** First run is the real one.
- **No breach register.** Article 33(5) requires documenting the ones you did not report.

---

## Related documents

- [`../foundations/incident-postmortem.md`](../foundations/incident-postmortem.md). What happens after
- [`../foundations/runbook.md`](../foundations/runbook.md). Per-system procedures this plan invokes
- [`../foundations/threat-model.md`](../foundations/threat-model.md). What you expected to happen
- [`record-of-processing-activities.md`](record-of-processing-activities.md). Tells you whose data is in the affected system, which is the first question during a breach
- [`data-retention-policy.md`](data-retention-policy.md). Determines what was still there to lose
