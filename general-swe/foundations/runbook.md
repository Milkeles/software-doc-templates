# Runbook: {Alert name or task}

*Also called: playbook.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | *The alert, symptom or scheduled task this handles. One runbook per alert.* |
| **Severity** | *What page level this arrives at.* |
| **Owner** | *Team.* |
| **Last reviewed** | YYYY-MM-DD |
| **Last executed** | *Date, filled in by whoever ran it. A runbook nobody has executed in a year is fiction.* |

*Write for the least experienced person who can be paged, at 3am, on a phone, under pressure. That reader scans; they do not read. Short lines, commands in full, no background.*

---

## Symptoms

*What the person is looking at right now. The alert text, the graph shape, what a user reports.*

*This is how someone lands on the right runbook. Include the exact alert name and the words a user would use, because both are what people search for.*

> **Example.** Alert `checkout_5xx_rate_high`. Users report "payment failed, please try again" on submit. Error rate panel on the checkout dashboard above 2%.

---

## Impact

*Who is affected and how badly, in one or two lines. What is still working.*

*Decides whether the next step is "fix it" or "wake three more people".*

---

## Before you start

*Access, tools and permissions needed, with links. Anything requiring a second approver.*

*This section prevents the most common delay in incident response: discovering at step 4 that you cannot log in.*

- *Access to: ...*
- *Escalate to ... if you do not have it*

---

## Diagnose

*Ordered checks, each with the command to run and how to read the result. Branch explicitly.*

*Order by likelihood, not by architecture. Put the check that resolves half of these alerts first.*

*Every step states what to do with the answer. A step that produces output but no decision wastes time.*

### 1. {Check}

```bash
```

- **If X:** *go to [Remediation A](#a-...)*
- **If Y:** *go to step 2*
- **If neither:** *escalate, see below*

### 2. {Check}

```bash
```

---

## Remediate

*One subsection per cause found above. Each is a numbered list of commands with the expected result after each.*

*Mark anything destructive or irreversible clearly, and say what confirms it is safe first.*

### A. {Cause}

1. *Step. Command. What you should see.*
2. *Step.*

**Verify.** *The specific signal that says it worked: a metric back under a threshold, a queue draining, a successful test request. Not "check it looks fine".*

**If this does not work.** *Next thing to try, or escalate.*

### B. {Cause}

---

## If none of this works

*The escalation path, in order, with names or rotas and how to reach them out of hours.*

*Also: what to do to limit damage while waiting. Failover, disable a feature flag, shed load, put up a status page notice. A responder who cannot fix it should still be able to reduce the impact.*

---

## Roll back

*The command, in full, and what it does not undo.*

*State the data question explicitly: if the new version wrote data in a format the old one cannot read, a code rollback is not enough, and the responder needs to know that before they run it, not after.*

---

## After

- *Update this runbook now, while you remember what was wrong with it.*
- *Record the incident and decide whether it triggers a [postmortem](incident-postmortem.md).*
- *Note anything that should be automated.*

---

## Notes on using this template

*Delete this section too.*

**One runbook per alert, linked from the alert itself.** An alert that fires without a link to its response is an alert that starts with five minutes of searching. If an alert has no runbook and needs no judgement, it should not be paging a human.

**If it is a deterministic list of commands, automate it and delete the runbook.** Anything a person executes without deciding is a script waiting to be written. The steps that survive are the ones needing judgement.

**Runbook, playbook, checklist.** AWS distinguishes a runbook (a known procedure for a known outcome) from a playbook (an investigation procedure for a situation you do not yet understand). Google's SRE materials do not keep that split at all: their "playbook" alone covers both diagnosis and remediation. Pick one meaning inside your organisation and write it down; do not assume a new joiner shares yours. This template covers both, with diagnosis before remediation.

**The known and the unknown.** Charity Majors argues that in distributed systems you rarely see the same failure twice, so investment belongs in observability rather than pre-written procedure. She is right about novel failures. Runbooks earn their place on the recurring and the procedural, and as the way on-call knowledge survives people leaving. Write them for those; do not pretend they cover the rest.

**Test it by handing it to someone else.** If a colleague cannot execute it without asking you a question, it is not finished. The steps you left out are the ones you no longer notice you know.

**Where this lives:** source in the repository, so it versions with the system and goes through review. Rendered somewhere reachable when the system it describes is down, and linked directly from the alert.

---

## Related documents

- [`incident-postmortem.md`](incident-postmortem.md). What the alert that fired here might turn into, if it meets the trigger
- [`service-readme.md`](service-readme.md). Where this runbook is linked from, under "operate it"
- [`deployment-plan.md`](deployment-plan.md). The single release this runbook's procedure should be written once for and referenced by
- [`branching-strategy.md`](branching-strategy.md). States that a rollback procedure belongs in this document, not there
