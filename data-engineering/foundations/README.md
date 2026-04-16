# Foundations

The three documents almost every data team needs, regardless of scale.

## The documents

| Document | Answers |
|---|---|
| [`data-pipeline-design-document.md`](data-pipeline-design-document.md) | How does this pipeline move data, and what happens when a run fails partway through? |
| [`data-contract.md`](data-contract.md) | What does this data mean, what quality can a consumer expect, and who answers when it changes? |
| [`dataset-catalog-entry.md`](dataset-catalog-entry.md) | Does this dataset exist, what is it, and can I trust it? |

## When to use each

**Data pipeline design document: any pipeline with more than one stage, or one that has ever needed a backfill.** A single script that reads a file and loads a table does not need a design document. A pipeline with retries, dependencies on other pipelines, or a schedule that matters to someone downstream does.

**Data contract: the moment a second team depends on data it did not produce.** One team using its own data internally can get away with tribal knowledge. Two teams cannot, because the producer will eventually change something the consumer was silently relying on, and neither side will know until a report is wrong.

**Dataset catalog entry: once "does this dataset exist" is a question someone has to ask a person to answer.** Below that size, a catalog is overhead. Above it, it is the difference between reusing a dataset and rebuilding it.

## Why we use them

A data pipeline moves the boundary problem that `interface-control-document.md` solves for an API into a place with less social pressure to get it right. An API's consumer calls you when it breaks. A dataset's consumer usually does not know it broke; they build on top of a wrong number and only notice when the wrongness compounds into something visible. The data contract exists to make the boundary explicit before that happens, not after.

The pipeline design document exists for the same reason the general [technical design document](../../general-swe/foundations/technical-design-document.md) exists for a service: so failure modes get thought through before they happen live, not during an incident. A pipeline's specific failure mode, a rerun that is not safe to run twice, does not have a service-side equivalent worth borrowing from; it has to be designed for directly.

The catalog entry solves a search problem that only appears at scale: once an organization has more datasets than any one person can hold in memory, "what does this table mean and can I trust it" needs an answer that does not require finding the one person who remembers building it.

## Where these live

**Docs-as-code for the pipeline design document and the data contract.** Both describe something that changes with the code, and a design document or a contract that can drift from what the pipeline actually does is worse than no document, because it is actively misleading.

**A data catalog tool for the catalog entry, if one exists.** Purpose-built catalog tools (a metadata platform, a lineage tool with a catalog feature) generate much of this from the pipeline and warehouse metadata directly, which stays current in a way a hand-maintained document cannot. This template is for a team without one, or as the starting content to seed one.
