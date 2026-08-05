# Explanation: {Topic}

> Why it works this way. The document nobody is required to read and everybody needs.
>
> **What it is for.** Understanding. Procida's summary: it exists "to illuminate a topic", it answers "Why…?", and its form is "discursive explanation". His analogy for the type is an article on culinary social history, which is exactly right about the register: the reader is not mid-task.
>
> **The evidence that it is missing.** Prana and colleagues annotated 4,226 README sections from 393 randomly sampled GitHub repositories for *Empirical Software Engineering* (2019) and found that "information discussing the 'What' and 'How' of a repository is very common, while many README files lack information regarding the purpose and status of a repository". The systematic gap is *why*, not *what*.
>
> **A note on the name.** The Good Docs Project calls this template `concept`, and Red Hat's modular documentation model uses concept as one of its three types. If your team already says "concept", use that word. The need is the same.
>
> **There is no settled section set for this document, because explanation is a register rather than a form.** The headings below are a proposal. Sections 1 to 3 and 7 follow The Good Docs Project's explanation template, which uses Overview, a glossary, the explanation topic itself, and a see-also. The middle sections are a suggested way to break up the body. Rename or drop them freely; a single well-argued run of prose under one heading is a legitimate explanation.
>
> **Where it lives.** Docs-as-code. It changes when the design changes, and the design changes in pull requests.
>
> **Delete this block before publishing.**

*Italic text is guidance. Delete it as you fill each section in.*

---

## 1. Title

*Frame it as the question, or as the topic plus its angle.*

> Good: "Why keys rotate on a schedule" · "How the scheduler decides priority" · "Consistency guarantees"
> Bad: "Key rotation" · "Scheduler" · "Advanced topics"

*"Advanced topics" is where explanation goes to be unfindable.*

---

## 2. Overview

*Two or three sentences: what this explains, and who will be glad they read it. A reader should be able to decide from this alone whether to keep going.*

*Name the question the page answers, in the words a reader would use to ask it.*

> This page explains why the platform rotates signing keys on a fixed schedule rather than on demand, and what that means for anyone integrating with it.

---

## 3. Terms

*Only the words this page uses in a way the reader would not guess. Three or four at most.*

*Anything more belongs in the [glossary](../foundations/glossary.md). A definition list that runs past half a screen has become a reference page wearing an explanation's clothes.*

---

## 4. The model

*The picture the reader should carry away. Diagrams belong here more than anywhere else in the documentation set.*

*Comparisons to something the reader already knows teach fast and mislead fast, so name where the analogy breaks.*

> A key is not revoked when it is rotated. Both the old and the new key verify signatures during the overlap window, which is why nothing breaks at the moment of rotation.

---

## 5. Design rationale

*The decision, the alternatives, and what the rejected options would have cost.*

*This is the single most useful thing an explanation can carry, because it is the information most expensive to reconstruct and the least likely to be written anywhere else.*

**Date the reasoning.** *A design rationale is true as of a moment. Say when the decision was made and link the [ADR](../foundations/architecture-decision-record.md) if one exists.*

**Admit uncertainty and disagreement.** *"We chose eventual consistency here and it is a real trade-off; strongly consistent reads would have cost us cross-region writes" is worth more than a confident claim. Readers detect the confident version and discount everything around it.*

---

## 6. Limits and non-goals

*The limits, and whether each one is fundamental or merely current.*

*Boundaries teach faster than definitions. "The scheduler is not a queue: work can be preempted after it starts" tells a reader more than three paragraphs about what the scheduler is. A reader who knows a limit is deliberate stops filing bugs about it.*

*Naming a real weakness is also what makes the rest credible. An explanation that only says why the design is good reads as promotion and gets discounted wholesale.*

---

## 7. Further reading

*Where the reader goes next: the procedure that uses this, the reference that lists the details, the ADRs behind the reasoning.*

*Explanation sprawls, because everything connects to everything. Link outward instead of absorbing.*

---

## Notes on using this template

*Delete this section too.*

**Write one when a question keeps arriving and no other document can hold the answer.** The reliable signals:

- The same question is asked in support or in review every few weeks.
- A reader asks "but why does it do that", and the honest answer is longer than a sentence.
- Two features look inconsistent and the inconsistency has a reason.
- People keep using a feature for something it will not do well.
- A [how-to guide](how-to-guide.md) or [reference page](reference-page.md) is growing a paragraph of background that does not belong there.

That last one is the commonest origin. Explanation is often extracted rather than written from scratch, and extracting it is what makes the other document usable again.

**Prose, not bullets.** This is the one documentation type where connected argument beats a list. Bullets strip out the causal links, and the causal links are the content. The italic guidance above uses bullets; your filled-in version should not.

**Three things do not belong here.** Steps — the moment the reader can act on it, it is a [how-to guide](how-to-guide.md). Complete parameter lists — that is [reference](reference-page.md), so link it. And anything the reader needs mid-task: if they must read this to finish a procedure, the procedure is under-documented and the fix is in the procedure.

**Explanation and architecture decision records overlap, and are not the same.**

| | ADR | Explanation |
|---|---|---|
| Audience | The team, now and later | Users of the system |
| Time | Frozen at the decision. Superseded, never edited | Living. Rewritten as understanding improves |
| Scope | One decision | One topic, often several decisions |
| Includes | Options considered, consequences | The resulting model, and what it means for the reader |

The practical relationship: **ADRs are the record, explanation is the synthesis.** An explanation of the consistency model may draw on six ADRs written over three years and mention none of them by number. Link them for the reader who wants the archaeology. See [`../foundations/architecture-decision-record.md`](../foundations/architecture-decision-record.md).

---

## Common failures in this document

- **Never written.** The commonest failure. The reasoning lives in the heads of three people and leaves with them.
- **Hidden under "Advanced".** Nobody browsing knows they need it, and nobody searching finds it.
- **Instructions leak in.** The reader tries to follow it and fails, because it was never a procedure.
- **Only the upside.** Reads as promotion and gets discounted wholesale.
- **Undated.** Reasoning that describes a system two rewrites ago, asserted in the present tense.
- **Unlinked.** Written, correct, and never reached, because no how-to guide points at it.

---

## Related documents

- [`how-to-guide.md`](how-to-guide.md). Link out to this from procedures rather than explaining inside them
- [`reference-page.md`](reference-page.md). Facts, not reasoning
- [`../foundations/architecture-decision-record.md`](../foundations/architecture-decision-record.md). The frozen record behind the synthesis
- [`../foundations/architecture-overview.md`](../foundations/architecture-overview.md). The same instinct, aimed at engineers rather than users
