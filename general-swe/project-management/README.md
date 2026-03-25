# Project Management

Four documents for work that has a sponsor, a budget and an end.

Most software teams do not need this group. A standing product team pulling from a roadmap already has authority, already knows who its stakeholders are, and tracks risk in the same place it tracks everything else. Adopting a charter and a risk register because a methodology mentions them is pure cost.

You need these when **someone outside the team is committing money or people to a bounded piece of work**, and it will later matter who agreed to what.

| Document | Answers | Write it when |
|---|---|---|
| [`project-brief.md`](project-brief.md) | Is this worth planning properly? | Before anyone is funded to think |
| [`project-charter.md`](project-charter.md) | Does this project exist, and who may spend on it? | When a sponsor commits resources |
| [`risk-register.md`](risk-register.md) | What could go wrong, who owns it, what are we watching for? | Always, if the work has a deadline that matters |
| [`stakeholder-register.md`](stakeholder-register.md) | Who can affect this, what do they want, who talks to them? | When more than one team or function is affected |

The risk register is the one worth having even if you skip the rest.

---

## The two gates

The single most useful structural idea in this group, and the reason the brief and the charter are separate documents.

```
   THE COMMON SHAPE                      THE TWO-GATE SHAPE

   idea                                  idea
     |                                     |
     |                                   BRIEF
     |                                     |
   CHARTER  <- approve the whole         GATE 1: approve spending
     |          project, using               |     on PLANNING only
     |          estimates nobody              |
     |          was paid to produce      planning, estimating,
     |                                   de-risking
   planning                                  |
     |                                   CHARTER or PID
     |                                     |
   delivery                              GATE 2: approve the PROJECT,
                                           |     on real numbers
                                         delivery
```

PMI puts one signature up front: the charter authorises the project before planning. PRINCE2 splits it. Its **Project Brief** supports one decision, *Authorise Initiation*, which funds the initiation stage and nothing else. Its **Project Initiation Documentation** supports *Authorise the Project*, and that is the signature equivalent to a PMI charter.

If your organisation's real complaint is that charters contain invented estimates, this is the cause and the two-gate shape is the fix. You are not asked to approve a project before anyone has been paid to think about it.

---

## Why these documents help

**A charter ends an argument that would otherwise recur monthly.** Its function is authorisation: it makes the project exist and gives one person the authority to apply resources. The failure it prevents is the slow one, where a project has no agreed owner and every decision escalates. The most valuable line in a charter is the one stating what the project manager may decide without going back to the sponsor, and PRINCE2's version of that idea, expressing authority as numeric **tolerances** rather than a paragraph, is worth borrowing whatever framework you use.

**A brief creates a cheap moment to say no.** Ideas that never get written down never get rejected either; they persist as background pressure. A one-page brief with a named decision and a date converts a standing conversation into a resolved one, in either direction.

**A risk register works through the trigger, not the score.** Its psychological value is that it moves a diffuse worry into a named observable with a named owner. That is why the trigger column matters more than the rating: a team that has agreed in advance what "this is happening now" looks like will notice it, and one carrying a general sense of unease will not.

**A stakeholder register makes engagement someone's job.** Its real output is the relationship owner column. Without it, engagement is everyone's responsibility and therefore nobody's, and the stakeholder who was never contacted appears at the worst possible moment.

---

## Baseline, record, report

PRINCE2 classifies every management document into one of three types, and this is the most portable idea in the framework because it answers a question every documentation repository has to answer: **does this get version-controlled?**

| Type | Behaviour | Where it belongs | Examples here |
|---|---|---|---|
| **Baseline** | Approved, then under change control | Wiki with page history, or docs-as-code | Charter, brief, business case, plan |
| **Record** | Updated continuously, never baselined | A live tool people already use | Risk register, stakeholder register, issue log |
| **Report** | A snapshot at a point in time | An archive, dated, never edited | Status reports, end-stage reports |

The common mistake is treating a record like a baseline. A risk register that needs an approval to change will not be changed, and a register nobody changes is worse than none, because it produces confident stale answers.

---

## Where each document lives

| Document | Home | Why |
|---|---|---|
| Project brief | **Wiki** | Short-lived, read widely outside engineering, and often discarded once the charter exists |
| Project charter | **Wiki**, with page history | Signed by a sponsor who does not use git. Needs a visible version trail because re-approval matters |
| Risk register | **The tracker, or a wiki table** | A record. It must be editable in under a minute or it will not be reviewed weekly |
| Stakeholder register | **Wiki, access-restricted** | Contains candid written judgements about named colleagues. Treat accordingly |

The rule is the same one that governs the rest of this repository: put the document where its maintainers already work. A charter in the code repository will be accurate and unread. A risk register behind a pull request will be neither.

---

## What the standards actually say, and what they no longer say

Two edition changes matter, because most published templates are quoting superseded text.

**PMBOK 7 (2021) removed the contents lists.** The seventh edition moved from process groups to principles and performance domains. The project charter survived the rewrite as a **one-sentence entry** in a list of strategy artifacts, and the stakeholder register as a one-sentence entry in a list of registers. There is no Develop Project Charter process, no Initiating Process Group, no inputs and outputs table, no field list for either document. The definition is unchanged from earlier editions, but the how-to is gone from the standard: PMI relocated procedural content to PMIstandards+, a subscription platform.

**So any template claiming "PMBOK says a charter contains these twelve items" is quoting PMBOK 6 (2017) §4.1.3.1.** That list is still the best one available and our charter template uses it, attributed correctly. The point is to know which document you are citing.

**PRINCE2 7 (2023) added sustainability.** Alongside Change, Commercial and Data Management, Sustainability Management is now one of the management approaches carried through initiation. A mainstream project standard treating sustainability as a first-class planning concern is worth knowing about.

---

## What the evidence supports, and what it does not

This group attracts more confidently repeated falsehoods than any other in the repository. Four are worth naming.

**Risk matrices have no evidential support for improving decisions.** Cox's 2008 analysis in *Risk Analysis* proved that ordinal matrices "can correctly and unambiguously compare only a small fraction (e.g., less than 10%) of randomly selected pairs of hazards", can "mistakenly assign higher qualitative ratings to quantitatively smaller risks", and under negative correlation between frequency and severity can be "worse than useless". Ball and Watt then showed empirically that "different risk assessors may assign vastly different ratings to the same hazard" and that "even following lengthy reflection and learning scatter remains high". The only randomised experimental work, Sutherland and colleagues with **n=2,699**, found matrices "are not always superior to text" but that geometric axis labelling and axis-integrated detail both improve comprehension.

No paper refutes Cox. What exists is a "repair, do not abandon" literature. The honest position is that the burden of proof is on the matrix.

**The power/interest grid is miscredited and untested.** Mendelow's 1981 ICIS paper plots power against **environmental dynamism**, to allocate scanning effort. The word "interest" does not appear in it. The power/interest form traces to Johnson and Scholes. No study tests whether it improves outcomes. The commonly seen citation "Mendelow, A. (1991), Stakeholder Mapping, Proceedings of the 2nd International Conference on Information Systems" is doubly wrong: the second ICIS was 1981, and that is not the title.

**The salience model has been tested, within limits.** Mitchell, Agle and Wood's power, legitimacy and urgency triad was validated by Agle, Mitchell and Sonnenfeld against CEOs of 80 large US firms, with urgency the strongest predictor, and by later studies across several countries and sectors. But it measures *perceived* salience rather than actual, it treats stakeholder groups as homogeneous, and the same study found **no link to financial performance**. PMBOK 7 names it as its only stakeholder model.

**Standish CHAOS failure rates are not measurements.** Eveleens and Verhoef examined 5,457 forecasts across 1,211 real projects for *IEEE Software* (2010) and found the Standish definitions "misleading, one-sided, pervert the estimation practice, and result in meaningless figures". Flipping the sign of every deviation in one real organisation turned a 6% success rate into 94% with identical forecasting quality. In their sample the worst forecaster had the highest Standish success rate. Standish's reply to them was that its reports "should be considered Standish opinion", a disclaimer never printed in the reports. Robert Glass, Magne Jørgensen and Nicholas Zvegintzov raised related objections. These figures reached a 1999 US Presidential advisory report, so the cost of an unchecked statistic is not hypothetical.

**The one place a survey figure is usable.** The BetterBriefs Project surveyed over 1,700 marketers and agency staff in more than 70 countries. 80% of brief authors said they wrote good briefs; 10% of recipients agreed. That perception gap is what the survey measured and it is the strongest available argument for a brief template with explicit acceptance criteria: the author cannot self-assess. The same study's "33% of budget wasted" figure is a self-reported respondent estimate, not a measurement, and the dollar headlines derived from it are a further extrapolation. Do not repeat those.

---

## Sources

Read directly: PMBOK Guide, Seventh Edition (PMI, 2021, ANSI/PMI 99-001-2021); RIBA Plan of Work 2020 Overview; Mendelow, "Environmental Scanning: The Impact of the Stakeholder Concept", *Proceedings of the Second International Conference on Information Systems* (1981), 407-417; Eveleens and Verhoef, "The rise and fall of the Chaos report figures", *IEEE Software* 27(1) (2010), 30-36; Krisper, "Problems with Risk Matrices Using Ordinal Scales", arXiv:2103.05440 (2021); Wood, Mitchell, Agle and Bryan, "Stakeholder Identification and Salience After 20 Years", *Business & Society* 60(1) (2021), 196-245.

Abstracts verified from publisher metadata, full texts not read: Cox, "What's Wrong with Risk Matrices?", *Risk Analysis* 28(2) (2008), 497-512; Ball and Watt, "Further Thoughts on the Utility of Risk Matrices", *Risk Analysis* 33(11) (2013), 2068-2078; Sutherland, Recchia, Dryhurst and Freeman, "How People Understand Risk Matrices, and How Matrix Design Can Improve their Use", *Risk Analysis* 42(5) (2022), 1023-1041.

Named but not read, and therefore not quoted: PMBOK Guide Sixth Edition (2017); *PRINCE2 7: Managing Successful Projects* (PeopleCert, 2023); Mitchell, Agle and Wood (1997); Agle, Mitchell and Sonnenfeld (1999); IEC 31010:2019 body text; Levine (2012); Duijm (2015).

**On sourcing.** Where a contents list comes from a source we could not read, this group says so in the template rather than presenting it as verified. The PMBOK 6 charter list and the PRINCE2 composition lists are both in that category.

---

## Related groups

- [`../requirements/`](../requirements/). Where a charter's "high-level requirements" line becomes real
- [`../foundations/`](../foundations/). Architecture decision records apply the same "record who decided and why" instinct at technical scale
- [`../waterfall/`](../waterfall/). If scope is fixed by contract, these documents are not optional and the plan-driven set extends them
- [`../shape-up/`](../shape-up/). The shaped pitch is the closest relative of the project brief
- [`../lean/`](../lean/). If the honest answer is that nobody knows whether the thing is worth building
