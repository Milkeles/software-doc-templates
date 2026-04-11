# Balance log: {System, e.g. weapons, economy, matchmaking}

*Italic text is guidance. Delete it as you fill each section in.*

*A published academic definition of a game metric: "a quantitative measure of one or more attributes of one or more objects that operate in the context of games" (Drachen, Seif El-Nasr and Canossa, in* Game Analytics: Maximizing the Value of Player Data*, Springer, 2013). The same source stresses that a metric is meaningless without stating what it is a function of, usually time or build version. This log exists so "why is this value 0.85" has a written answer that names the metric, the build it was measured against, and the reasoning, instead of living only in one designer's memory.*

---

## The log

| ID | Date | Value | Was | Now | Metric(s) watched | Measured effect | Shipped alone? | Reverted? |
|---|---|---|---|---|---|---|---|---|
| *BL-0091* | *2026-03-14* | *Longbow damage vs. armored* | *18* | *22* | *Pick rate, win rate in armored-heavy matchups* | *Pick rate rose from 4% to 9% over two weeks* | *Yes* | |

**Shipped alone, always answer honestly.** *The source above splits game analytics into strategic, tactical, and operational categories, and names an A/B test as the standard example of tactical analytics: one change, isolated, so an effect can be attributed to it. A patch that bundles this change with three others is not an A/B test, and "measured effect" for a bundled change is a guess dressed as a measurement. Say so plainly rather than implying a confidence the data does not support.*

---

## Reasoning

*For each change, one short paragraph: what problem the data or design review showed, why this specific new value, and what you expected to happen. Write this before you look at the result, not after, or you will unconsciously fit the reasoning to whatever the result turned out to be.*

> **Example, BL-0091.** Longbow pick rate sat under 5% for three weeks post-launch despite no execution-difficulty complaints in feedback, suggesting a power problem rather than a usability one. Damage against armored targets specifically, rather than a flat buff, targeted the matchup data showed it losing hardest.

---

## Which metrics, and why only those

*Per the source above's own worked example: evaluating weapon balance needs only a small number of metrics, "range, damage done and the frequency of use," and adding more variables "may not add any new relevant insights, or may even add noise or confusion to the analysis." Name the two or three metrics that actually decide whether a change to this system worked, once, here, and reuse them for every entry in this log rather than picking a new dashboard each time.*

| System | Metric | Why this one |
|---|---|---|
| | | |

*The same source frames this as a cost-benefit relationship with diminishing returns: the first well-chosen metrics carry most of the insight, and each additional one costs more to collect and analyze than it returns. Resist the temptation to add a metric because it is available rather than because it answers the question this log exists to answer.*

---

## Open questions

*A change that has not resolved yet: shipped, being watched, no verdict.*

| ID | Watching | Since | Decision due |
|---|---|---|---|
| | | | |

---

## Notes on using this template

*Delete this section too.*

**A reverted change is data, not a failure to hide.** Record it in the log exactly like any other entry, with what the measurement actually showed. A balance log with no reverts in it either had a perfect record or is not being kept honestly, and the second is far more likely.

**Ship one change at a time when you want a real answer.** If the release schedule forces you to bundle changes, the log should say so and should not claim a measured effect it cannot support. A qualitative note, "shipped alongside two other changes, effect not separable," is more honest and more useful than a number nobody can trust.

**This is not a public document, but the [patch notes](release-notes.md) are.** Write patch notes for what a player feels; write this log for what a designer needs to defend the decision six months from now.

**Where this lives:** docs-as-code, next to the tuning data or config it explains. It is only trustworthy if it changes in the same commit as the values it describes, the same reasoning the general [data model](../../general-swe/foundations/data-model.md) template gives for keeping a schema's explanation next to its migrations.

---

## Related documents

- [`release-notes.md`](release-notes.md). The player-facing summary of a subset of what this log records in full
- [`../foundations/game-design-document.md`](../foundations/game-design-document.md). Where an intended dynamic gets stated before it gets measured here
- [`../../general-swe/foundations/data-model.md`](../../general-swe/foundations/data-model.md). The same principle of keeping an explanation next to the values it explains
