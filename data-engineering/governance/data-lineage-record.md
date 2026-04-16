# Data lineage record: {Dataset name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Dataset** | |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

*Prefer a generated lineage graph from a catalog or lineage tool over this document wherever one exists. This template is for a team without one, or as a way to think through what such a tool should show. A hand-maintained lineage record goes stale as fast as the pipelines it describes change, which in practice means quickly.*

*Lineage is asked in two directions, and both matter. Before changing or retiring a dataset: what depends on it. When a number looks wrong: what does it depend on. Table-level lineage answers "which datasets" for both questions; column-level lineage answers "which specific fields," and is the difference between a map that names the right neighborhood and one that names the right door.*

---

## 1. Upstream

*What this dataset is built from, one hop at a time. Follow the chain into the source system's own lineage record if one exists, rather than re-deriving it here.*

| Source dataset | Fields used | Transformation | Owner |
|---|---|---|---|
| | | | |

---

## 2. Downstream

*What reads this dataset, to the best of the owner's knowledge. This list decays; treat gaps here as expected and worth closing, not as a failure of the document.*

| Consumer | Fields used | Criticality if this breaks |
|---|---|---|
| | | |

---

## 3. Column-level notes

*Only for fields where table-level lineage is not precise enough: a derived or aggregated field whose upstream source is not obvious from its name.*

| Field | Derived from | Logic |
|---|---|---|
| | | |

---

## Notes on using this template

*Delete this section too.*

**Lineage exists to answer a question under time pressure.** Before a schema change ships, or when a dashboard number looks wrong, someone needs this answer fast. A record that requires archaeology to reconstruct has already failed at its one job.

**An honest, incomplete downstream list beats a confident, wrong one.** If a dataset's consumers are not fully known, say so, and treat closing that gap as a real task rather than leaving the impression that the list is complete when it isn't.

**Automate this the moment it is feasible.** Lineage extracted from query logs or pipeline metadata stays accurate because it is regenerated from the thing it describes. Lineage typed into a document by a person is accurate on the day it is written and nowhere else.

**Where this lives:** generated from a catalog or lineage tool where one exists. Docs-as-code, next to the dataset's pipeline, if maintained by hand.

---

## Related documents

- [`../foundations/dataset-catalog-entry.md`](../foundations/dataset-catalog-entry.md). Where this record is linked from for someone discovering the dataset
- [`../foundations/data-pipeline-design-document.md`](../foundations/data-pipeline-design-document.md). The pipeline that produces the transformation this record describes
- [`../../general-swe/foundations/interface-control-document.md`](../../general-swe/foundations/interface-control-document.md). The same dependency-mapping problem, for an API boundary rather than a dataset
