# Game design document: {Game name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Status** | *Concept / pre-production / production / live* |
| **Owner** | *The person who resolves a disagreement about the design, not necessarily the person who wrote this* |
| **Last reviewed** | YYYY-MM-DD |
| **Platforms** | |

*This is not a requirements specification with extra steps. A 2018 review of requirements engineering in the games industry found that game studios invent requirements internally rather than eliciting them from a known customer, because market-driven development usually has no known customer at the start, and that verbal communication carries most of the load a written spec would carry elsewhere. This document exists to replace some of that verbal communication for a team too large or too dispersed to rely on it. Write it so a new artist, a new engineer, and a publisher's producer can all read the same page and understand the same game.*

---

## Why this document does not look like a spec

*A System Requirements Specification has no section for what the player should feel. A game design document does, because that omission is exactly what a 2012 IEEE paper proposing a game-design-document structure identified as the gap: aesthetics and experience are real requirements in a game, and they are absent from a conventional spec. The six sections below follow that structure.*

*Two more things a spec assumes and a game cannot: a stable customer, and a stable scope. Neither exists here. Update this document as the design changes; do not treat a stale version as a broken process.*

---

## 1. Overview

*The pitch, in the length of an elevator ride. What is the game, who is it for, and what is the one sentence that makes someone want to know more.*

> **Example.** A cooperative dungeon crawler where death is permanent but knowledge is not: your character dies for good, but the map, the monster weaknesses and the trap locations you discovered stay with your guild forever.

### Design pillars

*Two to four short phrases that every other design decision gets checked against. A pillar is not a feature; it is a filter. "Tense but fair" rules features in and out faster than a page of prose.*

| Pillar | Means | Rules out |
|---|---|---|
| | | |

---

## 2. Mechanics

*The game elements the player directly controls or interacts with: verbs, systems, controls. What can the player do, moment to moment?*

*Describe the rule, not the implementation. "The player can block, reducing incoming damage by 75% for the duration of the animation" is a mechanic. The code that enforces it belongs in a [technical design document](../../general-swe/foundations/technical-design-document.md), not here.*

---

## 3. Dynamics

*What emerges when the mechanics run over time and interact with each other, and with other players. Economies, difficulty curves, progression systems, the way individually reasonable mechanics combine into something nobody explicitly designed.*

*This is the section most often skipped, and the one most responsible for a game that plays differently from how it reads on paper. If two mechanics interact in a way that changes the intended experience, that interaction is a dynamic and belongs here, not as a surprise discovered in a [balance log](../live-operations/balance-log.md) entry six weeks after launch.*

---

## 4. Aesthetics

*What the player perceives with their senses, and the intended mood. This section states intent; the [art bible](art-bible.md) states the executable standard that delivers it.*

*Reference the art bible rather than duplicating it once one exists. Before it exists, this is where visual and audio intent lives.*

---

## 5. Experience

*What the game should make the player feel, and when. This is the section a conventional requirements document has no place for, and it is not decoration: published requirements-engineering research on games treats an emotional requirement as having two parts worth stating separately.*

| Moment | Intent (what the player should feel) | Artistic context (how you induce it) |
|---|---|---|
| *First boss encounter* | *Outmatched, then capable* | *Boss telegraphs are unreadable on attempt one, learnable by attempt three; music drops out entirely on the killing blow* |

*Security and progression-loss decisions belong in this conversation too. A published finding on games specifically is that a player's emotional reaction to losing progress can matter more than the strict security cost of preventing it, which is an argument for discussing the trade-off here rather than leaving it to whoever implements the save system.*

---

## 6. Assumptions and constraints

*Platform limits, team size, engine, timeline, budget ceiling, anything technical or organisational that bounds what sections 2 through 5 are allowed to promise.*

*Write these down even when they are uncomfortable. An assumption that turns out false is a much cheaper problem to find in a document than in production.*

---

## What this document does not cover

*Say what lives elsewhere, so nobody duplicates it here and lets the copy drift.*

- Visual production standards: the [art bible](art-bible.md)
- Funding, audience, and monetisation: the [business plan](business-plan.md)
- Engine architecture and technical approach: a [technical design document](../../general-swe/foundations/technical-design-document.md)
- Balance values and tuning history: the [balance log](../live-operations/balance-log.md)

---

## Notes on using this template

*Delete this section too.*

**This is a living document, not a baseline.** A design document frozen at the start of production describes a game you no longer have by the middle of it. Review it on a cadence, and date every review.

**Write pillars before you write mechanics.** A mechanic proposed without a pillar to check it against gets argued about on taste. A mechanic checked against "tense but fair" gets argued about whether it is actually tense and fair, which is a shorter, more finishable argument.

**The diversity of your team is the reason this document exists.** A published survey of game postmortems found that the range of job roles on a game team, story writers next to engineers next to composers, produces communication splits severe enough to break projects. If everyone on your team already shares a working vocabulary and sits in the same room, you need less of this document than a distributed or larger team does. Write to the team you have.

**Do not let this become the only source of truth for scope.** Feature creep driven by an ever-expanding design document was identified as a leading cause of trouble in the same postmortem survey. A pillar that a proposed feature fails is a reason to cut it, not a reason to rewrite the pillar.

**Where this lives:** the wiki, kept as one current page rather than a chain of dated copies. It is discussed constantly during pre-production, and Git's comment and notification model serves that badly.

---

## Related documents

- [`art-bible.md`](art-bible.md). The executable visual standard this document's aesthetics section only states intent for
- [`business-plan.md`](business-plan.md). The commercial case, kept separate so this document stays about the game
- [`../live-operations/balance-log.md`](../live-operations/balance-log.md). Where a dynamic described here gets measured after launch
- [`../../general-swe/foundations/technical-design-document.md`](../../general-swe/foundations/technical-design-document.md). Where a mechanic becomes an implementation plan
- [`../../general-swe/requirements/`](../../general-swe/requirements/). Conventional requirements documents, for the parts of a game that are ordinary software
