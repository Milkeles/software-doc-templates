# Security and Compliance

Five documents that exist because someone will ask a question under time pressure and the answer has to already be written down.

This group is different from the rest of `general-swe/`. Elsewhere, a missing document costs you clarity. Here, a missing document can cost you a legal deadline. Article 30 of the GDPR requires a record of processing activities. Article 35 requires a DPIA before certain processing starts. Article 33(5) requires you to document breaches you decided not to report. These are not conventions that experienced teams have converged on. They are obligations with named articles.

That changes how you should read the templates. In `foundations/`, skip what does not help you. Here, check whether the thing you want to skip is optional.

---

## The five documents

| Document | Answers | Required by law? |
|---|---|---|
| [`record-of-processing-activities.md`](record-of-processing-activities.md) | What personal data do we hold, for what purpose, and where does it go? | Yes. GDPR Art. 30 |
| [`data-protection-impact-assessment.md`](data-protection-impact-assessment.md) | Is this new processing too risky to people, and what will we do about it? | Yes, when Art. 35 is triggered |
| [`data-retention-policy.md`](data-retention-policy.md) | How long do we keep each thing, and why that number? | Effectively. Art. 5(1)(e) and 5(2) |
| [`incident-response-plan.md`](incident-response-plan.md) | Who does what in the first hour, and who decides whether to notify? | No, but the deadlines it serves are |
| [`security-review-checklist.md`](security-review-checklist.md) | What does a reviewer look at before this change ships? | No |

The [threat model](../foundations/threat-model.md) belongs to this conversation but lives in `foundations/`, because every team should have one whether or not it touches personal data.

---

## The clock is the reason all of this exists

Almost every decision in this group traces back to one constraint. When something goes wrong, you have hours, not weeks.

```
   HOUR 0        You become aware of a breach
     |
     |           NIS2 Art. 23(4)(a)
   HOUR 24  ---  early warning to the CSIRT or competent authority
     |           if the incident is "significant"
     |
     |           GDPR Art. 33(1)
   HOUR 72  ---  notification to the supervisory authority,
     |           unless the breach is unlikely to result in a risk
     |           NIS2 Art. 23(4)(b) full incident notification
     |
     |           GDPR Art. 34: notify affected individuals
     |           "without undue delay" if high risk. NO HOUR COUNT.
     |
   1 MONTH  ---  NIS2 Art. 23(4)(d) final report
```

Read that diagram as a staffing requirement rather than a paperwork one. **Someone must be able to make a regulatory-notification judgement within 24 hours, including at 2am on a Sunday.** That is the requirement the [incident response plan](incident-response-plan.md) exists to satisfy, and it is why the plan names roles and escalation paths rather than describing incident handling in the abstract.

Two errors are worth naming here because they are extremely common in published summaries:

**72 hours is a backstop, not an allowance.** The primary duty in Article 33(1) is "without undue delay". Late notification is permitted with reasons, so a missed deadline is not a cliff edge, but planning to use the full 72 hours is not compliance.

**There is no 72-hour rule for telling individuals.** Article 34 says "without undue delay" and gives no figure at all.

The other three documents are the ones that make the clock survivable. During a breach you will need to know whose data was in the affected system ([ROPA](record-of-processing-activities.md)), what was still there to lose ([retention](data-retention-policy.md)), and what risk you had already assessed and accepted ([DPIA](data-protection-impact-assessment.md)). Assembling those in hour three is how deadlines get missed.

---

## Why these documents help, beyond the legal duty

Compliance documents have a reputation, mostly earned, for being written to satisfy an auditor and read by nobody. The ones here earn their place for reasons that survive even if the regulation vanished.

**The ROPA is the only complete inventory anyone has.** Most organisations know their systems and do not know their data. The record forces one row per purpose, which surfaces the purposes nobody could name and the free-text fields quietly collecting health information. Teams that build it find systems nobody owns.

**The DPIA moves an argument earlier.** Its real function is forcing "should we build this?" to be answered before the build, with a written reason, by people who include someone other than the builder. Article 35(1) says "prior to the processing", and that timing is the whole value.

**A retention schedule converts a vague anxiety into a decision.** Without one, every team keeps everything, because deleting feels risky and keeping feels free. Naming a period, a trigger and an owner makes the cost visible and gives an engineer permission to delete.

**An incident plan removes decisions from the worst moment to make them.** Who declares. Who commands. Who may authorise a destructive action at 3am. None of these are hard questions in advance and all of them are hard at hour one. The plan's most valuable line is often the one saying **the incident commander must not also be the person fixing it**, because in a small team the person who understands the system will otherwise be debugging, updating stakeholders and deciding on notification simultaneously.

**The review checklist works for a reason that is not the checklist.** See the evidence section below. This is the one document in the group whose usual justification is wrong.

---

## What the evidence actually supports

This group attracts confident numbers, most of which do not survive being checked. What follows is what we could verify, including where the answer is uncomfortable.

**Naming security as a review step works. The checklist does not add to it.** Braz, Aeberhard, Çalikli and Bacchelli ran a randomised online experiment with 150 participants, 62% professionals, across four conditions, for ICSE 2022. Reviewers instructed to focus on security were **eight times more likely** to detect the planted vulnerability. But "a security checklist does not significantly improve the outcome", including a checklist tailored to that specific vulnerability. Keep the list for knowledge transfer; attribute the effect to the instruction.

**Code review has a low ceiling for finding vulnerabilities.** Edmundson and colleagues gave 30 developers code with seven known vulnerabilities (ESSoS 2013). "None of the subjects found all confirmed vulnerabilities", none found more than five, and more experience did not predict more accuracy. Review is one control, not the control.

**Nobody has shown that organisations learn from incidents.** Patterson, Nurse and Franqueira systematically reviewed 30 studies for *Computers and Security* (2023): "None of the studies reported that the organisations were exploring how to learn better or had any measures in place to assess their ability to learn and the effectiveness of the improvements made following incidents." They add, fairly, that it is unclear whether researchers sought that data directly. Related: **there is no peer-reviewed evidence that blameless postmortems reduce incidents.** Run them anyway, but on the argument that people report accurately when they are not blamed, which is a claim about candour rather than outcomes.

**Privacy impact assessments have thin evidence too.** Iwaya, Alaqra, Hansen and Fischer-Hübner's scoping review in *Array* (2024) covered 45 studies and found only four quantitative ones, with practitioners reporting "limited evidence to indicate that PIAs are really attaining their stated goals".

**Numbers not to repeat.** "95% of breaches are caused by human error" traces to a 2014 IBM report that is no longer public. "82% involve the human element" is from the 2022 Verizon DBIR; the 2026 edition says 62%, and the DBIR is a convenience sample of contributed incidents, so phrase any figure as "in Verizon's dataset". Cost-per-record breach figures are disputed on method, with published R² values around 0.13 and 0.02; Verizon abandoned the approach and Ponemon defends it, which is a disagreement to report rather than resolve. Dwell-time medians move with caseload composition, not detection capability.

If you want free, methodologically careful cost work, CISA's "Cost of a Cyber Incident: Systematic Review and Cross-Validation" (October 2024) and the World Bank's 2024 study are the better starting points.

---

## The standards, and which version is current

Published guidance in this area goes stale fast and most articles online are describing superseded documents.

| Standard | Current | Note |
|---|---|---|
| NIST SP 800-61 | **Revision 3, April 2025** | Replaced the four-phase lifecycle with the six CSF 2.0 Functions. Free |
| NIST CSF | **2.0, CSWP 29, 26 Feb 2024** | GOVERN is the new Function |
| OWASP Top 10 | **2025, released January 2026** | A03 and A10 are new categories |
| OWASP ASVS | **5.0.0, 30 May 2025** | Levels are now priority-based, not risk tiers |
| NIST SSDF | SP 800-218 **v1.1, Feb 2022** | SP 800-218A covers generative AI |
| SLSA | **v1.2** | Adds a Source Track. Levels are per artifact |
| CIS Controls | **v8.1, June 2024** | 18 controls, 153 safeguards |
| OWASP SAMM | **v2.0, Jan 2020** | Still current. Programme maturity, not verification |
| ISO/IEC 27035 | Parts 1-2 (2023), 3 (2020), 4 (2024) | Paywalled |

Two of these deserve a flag.

**NIST SP 800-61r3 is not a playbook.** It deliberately dropped Revision 2's operational detail to become a CSF 2.0 Community Profile. For concrete handling steps, use Rev 2 as a historical source or ISO/IEC 27035-3, and write your own procedures. Note also that a NIST page labelled "Rev. 3 (Withdrawn)" refers to the initial public draft, not the final publication.

**ASVS 5.0 introduced documentation requirements.** Certain security decisions must now be written down so implementation can be verified against them, and the standard states that "verifying that the documentation is in place and that the actual implementation are two separate activities". A security standard formally making "write the decision down" a verifiable requirement is the strongest external argument for this group of documents.

---

## Where each document lives

The deciding question is who maintains it, not what it is about.

| Document | Home | Why |
|---|---|---|
| Record of processing activities | **Wiki or structured store** | Legal, Support and People own most rows. Engineers do not know the answers for HR or marketing processing. Article 30(3) accepts any written electronic form |
| DPIA | **Wiki** | Reviewed and signed by the DPO, Legal and sometimes the supervisory authority. None of them use git |
| Data retention policy | **Wiki**, enforcement in code | The decision is legal and is owned jointly. The TTLs, lifecycle rules and deletion jobs live with the code and must be traceable back to a row |
| Incident response plan | **Wiki, plus an offline copy** | A plan reachable only through the systems that are down is not a plan. Print it, or keep a copy somewhere with independent authentication |
| Security review checklist | **Docs-as-code** | It runs inside pull requests, changes with the code, and should be short enough to sit in the PR template |

The offline copy is the one people skip. Incidents that take out identity providers, wikis or VPNs are exactly the incidents where the plan matters most.

---

## What to write first

In this order, for a team that has none of these.

**1. The ROPA.** Everything else depends on knowing what data you hold. It is also the only one that is unconditionally required for essentially every operating business: the Article 30(5) exemption for organisations under 250 people falls away where processing "is not occasional", and running a product is not occasional.

**2. The incident response plan.** It is short, it is the highest-value document per hour spent, and the 24-hour clock does not wait for you to be ready.

**3. The retention policy.** Feeds directly off the ROPA and closes the "keep everything forever" default.

**4. The security review checklist.** Cheap, and it changes what happens on every pull request rather than once a year.

**5. The DPIA.** Written per processing activity as it arises, not up front. Write the first one when Article 35 is first triggered, and use it as the pattern.

Then exercise the incident plan. Tabletop the two most likely scenarios twice a year, and test the thing most likely to fail: reaching a legal or privacy decision-maker out of hours. An untested plan is a first draft that will be debugged during a real incident.

---

## Jurisdiction

The templates are written against EU law because the GDPR and NIS2 are the most demanding widely applicable regimes, and a team that satisfies them has a workable base elsewhere. Two adjustments matter.

**NIS2 is a Directive.** The binding deadlines in your country come from national transposition and may differ from the numbers in Article 23. Check the transposing statute, not the Directive.

**The US has no general federal breach law.** A multi-state breach can trigger dozens of statutes with different clocks and different definitions of personal information. Build the plan around the shortest applicable clock and read the statutes rather than a summary table.

If you operate in the UK, note also that the Cyber Security and Resilience Bill is **not law**. As of July 2026 it is at Lords Committee stage. Do not plan against it as though it were in force.

---

## Sources

Legal texts read directly: Regulation (EU) 2016/679 (GDPR), Articles 5, 6, 9, 17, 21, 30, 32-36 and 49; Directive (EU) 2022/2555 (NIS2), Article 23, OJ L 333, 27.12.2022.

Regulator guidance: Article 29 Working Party WP248 rev.01 on DPIAs (4 October 2017) and WP250 rev.01 on breach notification, both endorsed by the EDPB on 25 May 2018; EDPB Coordinated Enforcement Framework 2025 on the right to erasure, report published February 2026.

Standards: NIST SP 800-61r3 (April 2025); NIST CSF 2.0 / CSWP 29 (February 2024); NIST SP 800-218 v1.1; OWASP Top 10:2025; OWASP ASVS 5.0.0; OWASP SAMM 2.0; SLSA v1.2; CIS Controls v8.1; PCI DSS v4.0.1 requirement 10.5.1.

Peer-reviewed: Braz, Aeberhard, Çalikli and Bacchelli, "Less is More: Supporting Developers in Vulnerability Detection during Code Review", ICSE 2022, 1317-1329; Edmundson et al., ESSoS 2013, LNCS 7781, 197-212; Patterson, Nurse and Franqueira, "Learning from cyber security incidents", *Computers and Security* 132 (2023), 103309; Iwaya, Alaqra, Hansen and Fischer-Hübner, "Privacy Impact Assessments in the Wild: A Scoping Review", *Array* (2024); Paul et al., *Empirical Software Engineering* (2024) on security review comments in OpenSSL and PHP.

**On sourcing.** Paywalled standards, principally the ISO/IEC 27035 series and the IBM Style Guide, are named but their contents are not quoted, because we could not read them. Where a widely repeated statistic could not be traced to a live primary source, it is listed above as a number not to repeat rather than reproduced with a hedge.

---

## Related groups

- [`../foundations/`](../foundations/). Threat model, postmortem, runbook and review guidelines that this group depends on
- [`../requirements/`](../requirements/). Where security and privacy requirements are stated before the build
- [`../../web-development/`](../../web-development/). Application-layer security specifics for web systems
