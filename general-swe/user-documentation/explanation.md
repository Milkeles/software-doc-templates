# Explanation

> Why it works this way. The document nobody is required to read and everybody needs.
>
> **What it is for.** Understanding. Procida's summary: it exists "to illuminate a topic", it answers "Why…?", and its form is "discursive explanation". His analogy for the type is an article on culinary social history, which is exactly right about the register: the reader is not mid-task.
>
> **The evidence that it is missing.** Prana and colleagues annotated 4,226 README sections from 393 randomly sampled GitHub repositories for *Empirical Software Engineering* (2019) and found that "information discussing the 'What' and 'How' of a repository is very common, while many README files lack information regarding the purpose and status of a repository". The systematic gap is *why*, not *what*.
>
> **A note on the name.** The Good Docs Project calls this template `concept`, and Red Hat's modular documentation model uses concept as one of its three types. If your team already says "concept", use that word. The need is the same.
>
> **Where it lives.** Docs-as-code. It changes when the design changes, and the design changes in pull requests.
>
> **Delete this block before publishing.**

---

## 1. When to write one

Write an explanation when a question keeps arriving and no other document can hold the answer.

The reliable signals:

- The same question is asked in support or in review every few weeks.
- A reader asks "but why does it do that", and the honest answer is longer than a sentence.
- Two features look inconsistent and the inconsistency has a reason.
- People keep using a feature for something it will not do well.
- A [how-to guide](how-to-guide.md) or [reference page](reference-page.md) is growing a paragraph of background that does not belong there.

That last one is the commonest origin. Explanation is often extracted rather than written from scratch, and extracting it is what makes the other document usable again.

---

## 2. Title

Frame it as the question, or as the topic plus its angle.

> Good: "Why keys rotate on a schedule" · "How the scheduler decides priority" · "Consistency guarantees"
> Bad: "Key rotation" · "Scheduler" · "Advanced topics"

"Advanced topics" is where explanation goes to be unfindable.

---

## 3. What belongs here

Anything a reader needs to hold in their head that is not a step and not a fact.

**Design decisions and their alternatives.** What you chose, what you rejected, and what the rejected option would have cost. This is the single most useful thing an explanation can carry, because it is the information most expensive to reconstruct and the least likely to be written anywhere else.

**Constraints.** What the system cannot do, and whether that is fundamental or current. A reader who knows a limit is deliberate stops filing bugs about it.

**Mental models.** The picture the reader should carry. Diagrams belong here more than anywhere else in the documentation set.

**History.** How it came to be this way. Legitimate and often the only explanation available for something otherwise inexplicable.

**Comparisons.** How this relates to a thing the reader already knows. Handle with care: comparison teaches fast and misleads fast, so name where the analogy breaks.

---

## 4. What does not belong here

**Steps.** The moment the reader can act on it, it is a [how-to guide](how-to-guide.md).

**Complete parameter lists.** That is [reference](reference-page.md). Link it.

**Marketing.** An explanation that only says why the design is good is not an explanation. Naming a real weakness is what makes the rest credible.

**Anything the reader needs mid-task.** If they must read this to finish a procedure, the procedure is under-documented and the fix is in the procedure.

---

## 5. How to write it

**Prose, not bullets.** This is the one documentation type where connected argument beats a list. Bullets strip out the causal links, and the causal links are the content.

**Say what it is not.** Boundaries teach faster than definitions. "The scheduler is not a queue: work can be preempted after it starts" tells a reader more than three paragraphs about what the scheduler is.

**Admit uncertainty and disagreement.** "We chose eventual consistency here and it is a real trade-off; strongly consistent reads would have cost us cross-region writes" is worth more than a confident claim. Readers detect the confident version and discount everything around it.

**Date the reasoning.** A design rationale is true as of a moment. Say when the decision was made and link the [ADR](../foundations/architecture-decision-record.md) if one exists.

**Keep it to one topic.** Explanation sprawls, because everything connects to everything. Link outward instead of absorbing.

---

## 6. Explanation and architecture decision records

They overlap and they are not the same.

| | ADR | Explanation |
|---|---|---|
| Audience | The team, now and later | Users of the system |
| Time | Frozen at the decision. Superseded, never edited | Living. Rewritten as understanding improves |
| Scope | One decision | One topic, often several decisions |
| Includes | Options considered, consequences | The resulting model, and what it means for the reader |

The practical relationship: **ADRs are the record, explanation is the synthesis.** An explanation of the consistency model may draw on six ADRs written over three years and mention none of them by number. Link them for the reader who wants the archaeology.

See [`../foundations/architecture-decision-record.md`](../foundations/architecture-decision-record.md).

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
