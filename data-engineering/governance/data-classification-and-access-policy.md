# Data classification and access policy: {Dataset, domain, or warehouse}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | |
| **Owner** | *Data governance jointly with security* |
| **Last reviewed** | YYYY-MM-DD |

*This document is not a replacement for the [record of processing activities](../../general-swe/security-and-compliance/record-of-processing-activities.md) or the [data protection impact assessment](../../general-swe/security-and-compliance/data-protection-impact-assessment.md). Those cover a specific processing activity under a specific legal basis. This one answers a standing, broader question that applies whether or not the data is personal data at all: for any dataset in the warehouse, what tier is it, and who may query it.*

---

## 1. Classification tiers

*Define the tiers once, here, and apply them consistently. Most organizations need no more than four; more than that and nobody remembers which tier is which.*

| Tier | Meaning | Example |
|---|---|---|
| *Public* | *No harm if disclosed* | *Published pricing* |
| *Internal* | *Not for external release, low individual harm if leaked* | *Internal usage metrics* |
| *Confidential* | *Real business or competitive harm if leaked* | *Unreleased financials, contract terms* |
| *Restricted* | *Personal data, credentials, or anything with legal or safety consequences if leaked* | *Customer PII, payment details* |

---

## 2. Dataset classification

| Dataset | Tier | Contains personal data? | Classified by | Date |
|---|---|---|---|---|
| | | | | |

*Cross-reference the [dataset catalog entry](../foundations/dataset-catalog-entry.md) for each row; this table can be a single "tier" field there once it is populated.*

---

## 3. Access rules by tier

| Tier | Default access | Approval required for wider access | Access logged? |
|---|---|---|---|
| *Public* | *All employees* | *No* | *No* |
| *Internal* | *All employees* | *No* | *No* |
| *Confidential* | *Named roles only* | *Manager or data owner* | *Yes* |
| *Restricted* | *Named individuals only* | *Data owner plus security* | *Yes, reviewed periodically* |

---

## 4. Review

| | |
|---|---|
| **Access review cadence** | *How often granted access is re-checked, not just granted* |
| **Reclassification trigger** | *What causes a dataset to move tiers: new field added, new regulation, business change* |

---

## Notes on using this template

*Delete this section too.*

**Four tiers is a starting point, not a rule.** What matters more than the exact count is that every dataset actually gets classified, rather than defaulting to "internal" because nobody assigned the question to anyone.

**Access granted is not access reviewed.** A restricted-tier dataset with logging but no periodic review means access accumulates and never shrinks. Section 4 exists because grants without review are the common failure mode, not the rare one.

**This document does not decide legal basis.** Whether a piece of personal data may be processed at all is a [record of processing activities](../../general-swe/security-and-compliance/record-of-processing-activities.md) question. This document assumes the data may exist and asks who inside the organization may see it.

**Where this lives:** wiki, owned jointly by data governance and security, changing by policy decision rather than by code change.

---

## Related documents

- [`../foundations/dataset-catalog-entry.md`](../foundations/dataset-catalog-entry.md). Where a dataset's classification tier is surfaced to someone searching for it
- [`../../general-swe/security-and-compliance/record-of-processing-activities.md`](../../general-swe/security-and-compliance/record-of-processing-activities.md). The legal-basis record this policy does not replace
- [`../../general-swe/security-and-compliance/data-protection-impact-assessment.md`](../../general-swe/security-and-compliance/data-protection-impact-assessment.md). Assessed per processing activity, not per dataset tier
