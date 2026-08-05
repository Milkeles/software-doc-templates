# Project Charter

> The document that authorises the project and names who may spend on it.
>
> **Also called:** Project Initiation Document (PID) in PRINCE2 environments.
>
> **One job, and it is not description.** PMI's definition, unchanged across five editions of the PMBOK Guide: "A document issued by the project initiator or sponsor that formally authorizes the existence of a project and provides the project manager with the authority to apply organizational resources to project activities." Two things in one sentence. It makes the project exist, and it gives someone authority. Everything else in the charter is supporting material.
>
> **If it does not authorise anything, it is a [project brief](project-brief.md).** That is the cleanest distinction available from a primary source: PMBOK's charter definition contains "formally authorizes" and "authority"; its brief definition contains neither.
>
> **Where the contents list actually comes from.** PMBOK 7 (2021) gives the charter one sentence in a list of strategy artifacts and **no contents list at all**. No Develop Project Charter process, no Initiating Process Group, no inputs and outputs table. Any template claiming "PMBOK says a charter contains X" is quoting **PMBOK 6** (2017) §4.1.3.1. Section 2 below says so where it borrows.
>
> **Where it lives.** Wiki. It is signed by a sponsor, read by people outside the engineering org, and referenced rather than edited.
>
> **Delete this block before publishing.**

---

## 1. Authority

Put these at the top, above everything else. A reader who stops here should still know what was authorised and who is now in charge.

> **Authorised by:** [name, role, date]
> **Project manager:** [name], with authority to [what they may decide and spend without returning to the sponsor]

The second line is the one teams leave vague, and it is the one the charter exists to settle. "Authority to run the project" authorises nothing. "May commit up to £50k and reassign anyone in the platform team without further approval" does.

PRINCE2 handles this differently and the contrast is instructive: it expresses authority as **tolerances** rather than as a paragraph, so the project manager may proceed freely until a threshold on time, cost, scope, quality, risk or benefit is breached. Borrow that if a prose sentence keeps coming out mushy.

---

## 2. Contents

The twelve-item list from PMBOK 6 §4.1.3.1, which is the one everyone means. Cite it as PMBOK 6, not PMBOK 7.

| Item | Note |
|---|---|
| Purpose | Why this project, now |
| Measurable objectives and success criteria | Numbers, or it is not measurable |
| High-level requirements | Not a specification. Link the [PRD](../requirements/product-requirements-document.md) |
| High-level description, boundaries and key deliverables | What is out of scope matters more than what is in |
| Overall project risk | The whole-project risk statement, not the [register](risk-register.md) |
| Summary milestone schedule | Dates that mean something to the sponsor |
| Preapproved financial resources | The number that was actually approved |
| Key stakeholder list | Link the [stakeholder register](stakeholder-register.md) |
| Project approval requirements | What counts as success, who decides, who signs off |
| Project exit criteria | The conditions under which you stop or cancel |
| Assigned project manager, responsibility and authority level | Section 1 |
| Name and authority of the sponsor | Who authorised it, and on what standing |

The last four carry the authorising function and are the four most often dropped from published templates. A charter without exit criteria and named approvers is a summary, not an authorisation.

---

## 3. Out of scope
**Not a plan.** The charter says a project exists and is worth doing. How it will be done comes later, in whatever your methodology produces.

**Not a requirements document.** High-level means a paragraph, not a list of features. Link to [`../requirements/`](../requirements/).

**Not a living document.** A charter that gets edited quietly has stopped being an authorisation. If the scope or the money changes materially, the sponsor re-approves and you keep both versions.

---

## 4. When you do not need one

PMBOK 7 does not insist every project has a charter, and this is worth knowing before you write one out of habit. Its §2.2.1.1 frames the charter as what you use **where management is centralised**: "In an environment where management activities are centralized… a project charter or other authorizing document can provide approval for the project manager to form a project team." The next subsection describes distributed, self-organising teams with no designated project manager.

Note also that PMBOK hedges with "**or other authorizing document**" both times it discusses this. The standard cares about the authorising function, not the artefact.

So: write a charter when someone outside the team is committing money or people, and when it matters later who agreed to what. A standing product team working from a roadmap does not need one per initiative.

---

## 5. The PRINCE2 alternative
PRINCE2 has no project charter. It splits the authorisation into **two gates**, and for anything genuinely uncertain the split is an improvement.

| | PMI | PRINCE2 |
|---|---|---|
| First gate | none | **Project Brief** authorises the *initiation stage* only. You are funded to plan |
| Second gate | **Project charter** authorises the whole project up front | **Project Initiation Documentation** authorises the *project*. This is the charter-equivalent signature |
| Afterwards | The charter stays live | The brief is discarded once the PID exists. The PID is a baseline under change control |

The value is that you are not asked to approve a project before anyone has been paid to think about it. If your organisation's real complaint is that charters contain invented estimates, this is why, and the two-gate shape is the fix.

PRINCE2's wider classification is worth borrowing whatever framework you use, because it answers "does this document get version-controlled":

- **Baselines** are approved and then change-controlled. Charter, business case, plan.
- **Records** are updated continuously and never baselined. [Risk register](risk-register.md), issue register, lessons log.
- **Reports** are a snapshot at a point in time. Status reports, end-stage reports.

PRINCE2 7 (2023) also added Change, Commercial, Data and **Sustainability** management approaches to the set carried through initiation. Sustainability being promoted to a first-class planning concern in a mainstream standard is worth knowing.

---

## Common failures in this document

- **Authority stated in words, not limits.** "Full authority to deliver" settles nothing at the first disagreement.
- **No exit criteria.** Projects then end by exhaustion rather than decision.
- **Contents attributed to PMBOK 7.** That list is PMBOK 6 §4.1.3.1.
- **Turned into a plan.** Duplicates work that has not been done yet.
- **Edited silently.** An authorisation nobody re-approved is not one.
- **Written for a project that needed none.** A standing team with a roadmap already has authority.
- **Approved before anyone was funded to think.** The PRINCE2 two-gate shape exists for this.

---

## Related documents

- [`project-brief.md`](project-brief.md). The lighter, earlier document that authorises nothing
- [`../requirements/vision-and-scope.md`](../requirements/vision-and-scope.md). Where the purpose and boundaries are developed properly
- [`risk-register.md`](risk-register.md). Where the "overall project risk" line is decomposed
- [`stakeholder-register.md`](stakeholder-register.md). Where the key stakeholder list is maintained
- [`../foundations/architecture-decision-record.md`](../foundations/architecture-decision-record.md). The same instinct at technical scale: record who decided, and why
