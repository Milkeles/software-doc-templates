# Data Protection Impact Assessment

> The assessment you must finish before the processing starts, not after.
>
> **Why this name.** "DPIA" is the legal term in GDPR Article 35. "PIA" is the generic term used outside the EU and in most of the academic literature. Use the legal name in a document that has legal effect.
>
> **The timing is the obligation.** Article 35(1): where processing is "likely to result in a high risk to the rights and freedoms of natural persons", the controller shall, **"prior to the processing"**, carry out an assessment. A DPIA written after launch is not a late DPIA. It is a missed one.
>
> **The structure is not yours to choose.** Article 35(7) lists four mandatory contents. Sections 3 to 6 below are those four, in order. Add to them; do not drop them.
>
> **A caution about what this achieves.** Iwaya, Alaqra, Hansen and Fischer-Hübner reviewed 45 studies of privacy impact assessments in practice for *Array* (2024) and found only four quantitative studies, with practitioners reporting "limited evidence to indicate that PIAs are really attaining their stated goals". Treat the DPIA as a legal requirement and a structured way to think, not as a proven risk reducer.
>
> **Where it lives.** Wiki or a document store, alongside the [record of processing activities](record-of-processing-activities.md). It is reviewed by people who do not use git.
>
> **Delete this block before publishing.**

---

## 1. Do you need one?

Answer this in writing even when the answer is no, because the reasoning is the evidence of compliance.

**The three cases named in Article 35(3):**

- (a) systematic and extensive automated evaluation of personal aspects, including profiling, on which decisions with legal or similarly significant effects are based;
- (b) large-scale processing of special categories of data (Article 9) or criminal conviction data (Article 10);
- (c) systematic monitoring of a publicly accessible area on a large scale.

The chapeau to that list says **"in particular"**. The three are illustrative, not exhaustive. Your national supervisory authority also publishes a mandatory list under Article 35(4). Check it.

**The nine criteria from WP248 rev.01**, the Article 29 Working Party guidance the EDPB endorsed on 25 May 2018:

| # | Criterion |
|---|---|
| 1 | Evaluation or scoring, including profiling and predicting |
| 2 | Automated decision-making with legal or similar significant effect |
| 3 | Systematic monitoring |
| 4 | Sensitive data, or data of a highly personal nature |
| 5 | Data processed on a large scale |
| 6 | Matching or combining datasets |
| 7 | Data concerning vulnerable data subjects |
| 8 | Innovative use, or applying new technological or organisational solutions |
| 9 | Processing that prevents data subjects from exercising a right or using a service |

**The decision rule, verbatim:** "a processing meeting two criteria would require a DPIA… However, in some cases… only one of these criteria requires a DPIA."

Two things teams get wrong here:

**Criterion 7 explicitly includes employees.** The imbalance of power in an employment relationship makes staff vulnerable data subjects. Monitoring tooling aimed at your own workforce is a common unassessed high-risk processing.

**Criterion 8 catches anything new.** Adopting a technology whose privacy consequences are not yet understood is itself a trigger, which is why new machine learning features almost always need one.

---

## 2. What is being processed

The systematic description required by Article 35(7)(a): the processing operations and the purposes, including the legitimate interest pursued where that is your lawful basis.

Write this so someone outside the team can follow it. Cover:

- What the system does, in two or three sentences.
- The data flow from collection to deletion. A plain sequence of steps beats a diagram nobody can read.
- Categories of data subjects and categories of personal data.
- Recipients, including processors and any transfer outside the EEA with the transfer mechanism named.
- Retention periods, or a link to the [retention policy](data-retention-policy.md).
- The lawful basis for each purpose. One basis per purpose, not one for the whole system.

Pull the factual half from your [ROPA](record-of-processing-activities.md) rather than retyping it. The two documents describe the same processing and must not disagree.

---

## 3. Necessity and proportionality

Article 35(7)(b). The section most often reduced to a sentence, and the one a supervisory authority will read first.

Answer three questions, with reasons:

**Could you achieve the purpose with less data?** If yes, the current design fails minimisation and the answer is to change the design, not to justify it.

**Is the lawful basis sound?** Consent must be freely given, which it usually is not in an employment context. Legitimate interests requires a documented balancing test; write it here or link it.

**How are data subject rights actually served?** Access, rectification, erasure, portability and objection are not policy statements. Name the mechanism for each: who runs it, what it costs, how long it takes.

---

## 4. Risks to individuals

Article 35(7)(c). The pivot that most teams get backwards.

**The risk is to the data subject, not to you.** Reputational damage to the company is not a GDPR risk. Identity theft, discrimination, financial loss, loss of confidentiality, exclusion from a service, and distress are.

| Risk to the individual | Source | Likelihood | Severity | Rating |
|---|---|---|---|---|
| Identity theft after credential exposure | Breach of the account store | Possible | Severe | High |
| Wrongful denial of service | Scoring model error, no human review | Likely | Significant | High |

Rate likelihood and severity separately and say what your words mean. A scale where every risk is "medium" is not a scale.

This section overlaps with the [threat model](../foundations/threat-model.md), which asks a different question: the threat model asks what an attacker can do to the system, the DPIA asks what the system can do to a person. Link them; do not merge them.

---

## 5. Measures

Article 35(7)(d). The measures envisaged to address the risks, including safeguards, security measures and mechanisms to ensure the protection of personal data.

For each risk in section 4, name a measure, an owner, and a date. Then restate the risk after the measure is in place. That residual figure is what matters next.

| Risk | Measure | Owner | Date | Residual |
|---|---|---|---|---|
| Identity theft after credential exposure | Encryption at rest, key rotation, breach alerting | Platform | 2026-04-30 | Low |
| Wrongful denial of service | Human review before any adverse decision | Product | 2026-05-15 | Medium |

A measure with no owner and no date is a wish.

---

## 6. Consultation

**Article 36(1) triggers on the residual risk**, not the initial one. The text is "in the absence of measures taken by the controller to mitigate the risk". If your measures bring high risk down to acceptable, you do not consult. If high risk remains, you must consult the supervisory authority **before processing begins**.

Budget for it. Article 36(2) gives the authority **eight weeks**, extendable by **six**, so up to **fourteen weeks** before you may start. That is a schedule item, not a formality.

Article 35(2) requires you to seek the DPO's advice where one is designated. Article 35(9) says that "where appropriate" you shall seek the views of data subjects or their representatives. If you decide that is not appropriate, record why.

---

## 7. Outcome and review

State the decision plainly: proceed, proceed with conditions, or do not proceed. Sign and date it.

Article 35(11) requires review "where necessary and… at least when there is a change of the risk". Name the trigger conditions, not just a calendar date. A new data source, a new purpose, a new recipient, a new country, or a model change all reopen the assessment.

---

## Tooling

**CNIL's PIA software** is free, open source under GPL-3.0, and available at [github.com/LINCnil/pia](https://github.com/LINCnil/pia). Version 4.1.0 was released on 2 April 2026 and the project is actively maintained. Note that CNIL's own English-language page has lagged behind the releases, so take the version from the repository.

The ICO also publishes a DPIA template. Both are starting points; neither removes the thinking.

---

## Common failures in this document

- **Written after launch.** Article 35(1) says "prior to the processing".
- **Risk to the company, not to the person.** Inverts the whole exercise.
- **Necessity treated as a formality.** The section an authority reads first.
- **Consultation triggered by initial rather than residual risk.** Sends you to the regulator unnecessarily, or fails to when you should go.
- **Fourteen weeks not in the plan.** Article 36(2) can stop a launch.
- **Employees not recognised as vulnerable data subjects.** WP248 says they are.
- **Never reviewed.** Article 35(11) makes review an obligation, not hygiene.

---

## Related documents

- [`record-of-processing-activities.md`](record-of-processing-activities.md). The factual description this assessment builds on
- [`data-retention-policy.md`](data-retention-policy.md). The retention periods this assessment relies on
- [`../foundations/threat-model.md`](../foundations/threat-model.md). Risk to the system, as opposed to risk to the person
- [`incident-response-plan.md`](incident-response-plan.md). What happens when a risk in section 4 materialises
- [`security-review-checklist.md`](security-review-checklist.md). Where the section 5 measures get verified
