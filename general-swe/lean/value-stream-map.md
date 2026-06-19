# Value stream map: {Product family}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Product family** | *One. Not everything the team does.* |
| **Mapped by** | *The person who walked it. Singular.* |
| **Walked on** | YYYY-MM-DD |
| **Trigger and endpoint** | *What starts the flow and what ends it.* |

**Draw the map on paper, by hand, while you walk the flow. This file is where the findings land afterwards.**

*That instruction is not stylistic. Rother and Shook give it a page under the heading "Always draw by hand in pencil" and argue it: "Drawing by hand means you will focus on understanding the flow, instead of on how to use the computer. The point of value stream mapping is not the map, but understanding the flow of information and material."*

*The same page says to map the whole stream yourself even when several people are involved, because "if different people map different segments, then no one will understand the whole." A tidy map assembled from other people's segments is better looking and worth less.*

---

## 1. Scope

*One product family, one trigger, one endpoint. Say what is outside.*

*The most common way this goes wrong is mapping "our work" rather than one flow. A map covering features, bugs and support requests together averages three different systems and describes none of them.*

> **Example.** A customer-reported defect, from the support ticket being raised to the fix running in production. Excludes feature work and planned maintenance.

---

## 2. Steps, in order

*Every step the work passes through, including the ones nobody calls steps. Approvals, handoffs and waiting for someone to notice are steps.*

| # | Step | Who does it | Process time | Elapsed time | %C&A |
|---|---|---|---|---|---|
| | | | | | |

**Process time** is time someone was working on this item. **Elapsed time** is wall clock, including the queue in front of the step. The gap between them is the finding.

**%C&A** is the share of work arriving at this step that is usable as it is, with no rework or clarification. Ask the people *downstream* of the step, never the people doing it. Nobody rates their own output accurately.

*One note on provenance: %C&A is not from the original method. Keyte and Locher added it in 2004 for office and administrative processes. It is the most useful column here for software, and it is an addition.*

---

## 3. Queues

*What sits between the steps, and how long. This is usually where the answer is.*

| Between | What is waiting | Typical wait | Why |
|---|---|---|---|
| | | | |

*The "why" column is what turns this into an action. "Waiting for review" is a fact. "Waiting for review because only two people can approve and both are on the on-call rota" is a cause.*

---

## 4. The comparison

*The one number the map exists to produce.*

| | |
|---|---|
| **Total elapsed time** | |
| **Total process time** | |
| **Ratio** | |

*Do not look for a benchmark to compare this against. Published "typical" figures for knowledge work contradict each other badly and none of them is sourced to anything. Your own number, measured again in three months, is the comparison that means something.*

*For scale, the original worked example: 188 seconds of processing time inside a lead time of 23.6 days.*

---

## 5. What we saw

*Findings, in the order of how much time they cost. Not opinions about the process.*

*Attach a number to each. A finding with no number cannot be prioritised against the others, and the whole point of walking the flow was to find out which problem is the big one.*

---

## 6. Future state

*How the flow should work, drawn. Then the changes that get you there.*

*Draw it, do not list it. The redraw is where you find out whether the changes actually connect.*

*Aim at the queues first. Steps are where the visible work is and queues are where the time is, and teams reliably attack the wrong one because the steps are the part they control.*

| Change | Expected effect | Owner | By |
|---|---|---|---|
| | | | |

*The plan is part of the method, not an optional follow-up. The original book gives it a section of its own and titles that part "Value Stream Improvement is Management's Job."*

---

## Notes on using this template

*Delete this section too.*

**Do not draw this from a meeting room.** Every claim in the method rests on having walked the flow and asked the people in it. "Bring your stopwatch and do not rely on standard times" is the instruction, and its software equivalent is to read the actual timestamps rather than asking people how long things usually take. People report the median case and remember the good one.

**In software this is a queue and handoff diagnostic, not a production one.** The original assumes a repeating flow with steps you can time consistently. Software work items are heterogeneous and mostly non-repeating, so per-step process time is a rough figure at best. What survives the translation is the part about waiting: where work queues, and who hands it to whom. That is real, it is usually the majority of elapsed time, and nothing else on your team's dashboard shows it.

**It is a qualitative tool and the authors say so.** "Numbers are good for creating a sense of urgency or as before/after measures." A value stream map converted into a recurring metrics dashboard has become the thing it was meant to expose.

**Map once, act, then map again.** A map maintained continuously is a document. A map drawn twice with a change in between is a measurement.

**Where this lives:** the drawing stays on paper and gets photographed into the wiki when the work is done. This file holds sections 1 to 6, which are the findings and the plan. Do not redraw the map in a diagramming tool. By the authors' own argument, a polished map has already lost the understanding it was a by-product of.

---

## Related documents

- [`a3.md`](a3.md). A dated, numbered finding from section 5 is the raw material for an A3's issue and background; one map often produces several A3s
- [`experiment-record.md`](experiment-record.md). The future-state changes in section 6 are predictions; once one is tested against a real split rather than a second walk of the flow, record it as an experiment
- [`improvement-kata.md`](improvement-kata.md). A single value stream map is a one-time deep look, but walking the flow is the same discipline as grasping the current condition in section 2 of the kata, and the future state can seed the kata's first target condition
