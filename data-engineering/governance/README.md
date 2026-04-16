# Governance

The three documents that answer "can this data be trusted, understood, and safely accessed" once more than one team depends on data they did not build.

## The documents

| Document | Answers |
|---|---|
| [`data-quality-specification.md`](data-quality-specification.md) | What does "good data" mean here, beyond just accuracy? |
| [`data-classification-and-access-policy.md`](data-classification-and-access-policy.md) | How sensitive is this data, and who is allowed to query it? |
| [`data-lineage-record.md`](data-lineage-record.md) | Where did this number come from, and what breaks if I change it? |

## When to use each

**Data quality specification: any dataset with more than one downstream consumer, or any dataset feeding a decision.** A dataset only its producer reads can rely on the producer noticing when something looks wrong. A dataset feeding a dashboard, a model, or a report needs its expectations written down, because the person who notices a quality problem is rarely the person who can fix it.

**Data classification and access policy: as soon as any dataset contains anything sensitive, whether personal data, financial detail, or plain business-confidential information.** This does not replace the [record of processing activities](../../general-swe/security-and-compliance/record-of-processing-activities.md) or the [data protection impact assessment](../../general-swe/security-and-compliance/data-protection-impact-assessment.md); those cover a specific processing activity under a specific legal basis. This document answers a broader, standing question: for any dataset in the warehouse, what tier is it, and who may query it, independent of any one activity's legal justification.

**Data lineage record: once the dependency graph between datasets is more than one hop deep, or once "what does this break" cannot be answered from memory.** Below that size, the sources and consumers fields in the [dataset catalog entry](../foundations/dataset-catalog-entry.md) are enough.

## Why we use them

Wang and Strong's 1996 study of what data quality actually means to data consumers, still one of the most-cited works in the field, found that consumers hold a broader conception of quality than the accuracy-only view engineering teams default to: completeness, timeliness, consistency, and relevance all matter as much as whether a value is technically correct. A data quality specification exists because the easiest checks to automate, type and range checks, answer a narrower question than the one consumers actually have.

A classification and access policy exists for the same reason a building has locked doors on some rooms and not others: not every dataset carries the same risk if it leaks or is queried by someone who shouldn't. Treating all data as equally sensitive either over-restricts data nobody needs to protect, or under-restricts data that genuinely needs it. Naming the tiers is what lets both mistakes be avoided at once.

A lineage record exists because impact analysis, in either direction, is a question that comes up under time pressure: before a schema change, what depends on this; when a number looks wrong, what does it depend on. A team without a written or generated answer to that question re-derives it by hand, under pressure, every single time.

## Where these live

**Docs-as-code for the data quality specification**, next to the checks it describes, so an unenforced expectation is visibly a wish rather than a promise.

**Wiki for the classification and access policy**, owned jointly by data governance and security, changing by policy decision rather than by code change, the same reasoning the general [data retention policy](../../general-swe/security-and-compliance/data-retention-policy.md) template gives.

**Generated from a lineage or catalog tool where one exists.** The lineage record template here is for a team without one, or as a way to think through what a tool should surface once you get one. A hand-maintained lineage document is close to useless past a handful of datasets, because it goes stale exactly as fast as the pipelines it describes change.
