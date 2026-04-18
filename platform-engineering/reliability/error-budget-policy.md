# Error budget policy: {Service name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *Link the [SLO document](slo-document.md) this policy enforces* |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

*This policy has two stated purposes, not one, and both matter: protect consumers from repeated SLO misses, and give product and reliability work a shared, objective basis for deciding when to prioritize which. It is explicitly not a punishment for missing an SLO. Say that plainly to the team; a policy read as punitive gets worked around rather than followed.*

---

## 1. Goals and non-goals

| | |
|---|---|
| **Goals** | *Protect consumers from repeated misses; give a shared, objective signal for balancing reliability against feature work* |
| **Non-goals** | *This is not a performance review input. Not a substitute for good incident response* |

---

## 2. SLO-miss policy

*What happens when the error budget for the current window is exhausted. Be concrete. The value of this section is entirely in how unambiguous it is.*

| Condition | Action |
|---|---|
| *Budget exhausted for the preceding window* | *e.g. halt all changes and releases other than P0 issues or security fixes, until back within SLO* |
| *Budget at {threshold}% and trending toward exhaustion* | *e.g. warn, require reliability work alongside feature work* |

**A policy without a concrete halt condition is not a policy.** "We'll be more careful" is not enforceable. "Releases stop except for P0 and security fixes until the service is back within SLO" is.

---

## 3. Outage and postmortem policy

| | |
|---|---|
| **Single-incident threshold requiring a postmortem** | *e.g. any incident consuming more than 20% of the budget* |
| **Postmortem template** | *Link the [incident postmortem](../../general-swe/foundations/incident-postmortem.md) template* |

---

## 4. Escalation

*Who resolves a disagreement about whether the halt condition applies, or whether an exception is warranted. Name a person or a forum, not "leadership."*

---

## Notes on using this template

*Delete this section too.*

**State the policy as not punitive, and mean it.** Its actual function is to give product and reliability work a shared incentive to balance against each other, not to assign blame. A team that experiences this policy as punishment will find ways around the halt condition instead of respecting it.

**The halt condition is the whole document.** Everything else is context for that one enforceable rule. If a reader can walk away unsure what actually happens when the budget runs out, rewrite section 2 until they can't.

**Review this alongside the SLO, not on a separate cycle.** A stale error budget policy attached to a current SLO document is worse than having neither, since it creates false confidence that a consequence exists when it no longer matches reality.

**Where this lives:** docs-as-code or wiki, but wherever it lives, it must be visible to whoever approves a release. A policy nobody checks before shipping is not being enforced.

---

## Related documents

- [`slo-document.md`](slo-document.md). The targets and budget this policy enforces
- [`../../general-swe/foundations/incident-postmortem.md`](../../general-swe/foundations/incident-postmortem.md). Where a budget-consuming incident is analyzed in full
- [`toil-log.md`](toil-log.md). Where the reliability work this policy triggers often shows up as reduced toil once it's actually done
