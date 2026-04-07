# Game Development

Documents for teams building games, on top of everything in [`general-swe/`](../general-swe/). A game team still writes architecture decision records, runbooks, and postmortems. This area covers what a game adds: a creative and technical spec written for a team with no shared engineering vocabulary, a visual language that has to survive contact with outsourced art vendors, tuning decisions that are opinions until someone measures them, and a set of legal and platform obligations that most software never meets.

---

## Groups

| Group | Use it when |
|---|---|
| [`foundations/`](foundations/) | Always, from the first pitch. What the game is, what it looks like, and how it gets funded. |
| [`production/`](production/) | You have more than a couple of contributors and more than one milestone between you and ship. |
| [`live-operations/`](live-operations/) | The game ships to players and keeps changing after launch: patches, live content, tuning, ratings, and player data. |

There is no methodology split here, for the same reason there is none in `web-development/`: a design pillar or a loot box disclosure obligation does not change shape because the team runs Scrum instead of Kanban. Pull sprint or Kanban documents from `general-swe/` as your team needs them.

---

## What makes game documentation different

Four things recur across the research behind this area, and each explains a document you will not find written this way anywhere else in the repository.

**Games are market-driven, not customer-driven.** A 2018 review of requirements engineering in the games industry (Hussain, Asadi and Richardson, UC Irvine) found that game studios invent requirements internally rather than eliciting them from a known customer, because there usually is no known customer at the start: the market is broad and anonymous. Requirements documentation is consequently thin by tradition, and verbal communication carries most of it. That is precisely the gap the [game design document](foundations/game-design-document.md) exists to close, and it is why the document reads unlike a requirements specification.

**Fun is a requirement, and it is subjective.** The same review, and the older requirements-engineering literature it surveys (Callele, Neufeld and Schneider's work on emotional requirements), treats a player's intended feeling as a real requirement that has to be written down, not an unmeasurable extra. A conventional software requirements document has no section for this. A game design document does.

**A studio is a market-driven team with the most job-role diversity in software.** Programmers, artists, writers, composers, and designers rarely share a working vocabulary. A survey of twenty published game postmortems (Petrillo, Pimenta, Trindade and Dietrich, 2009) found that this diversity produces communication splits severe enough to break projects, alongside scope creep, underestimated schedules, and crunch. Several documents in this area exist specifically to give a non-uniform team one shared, written reference instead of relying on everyone being in the same room.

**A live game accumulates legal and platform obligations that most software never triggers.** Processing player data continuously, at scale, for a game aimed at a broad audience that plausibly includes children, is close to the textbook case the GDPR's record-keeping requirement was written for. Age rating bodies require disclosure of paid randomised purchases under a self-regulatory scheme that published research has found is followed roughly 29% of the time on mobile storefronts. Regulators in different countries have reached opposite conclusions about whether the same mechanic is gambling. None of this is optional once a game is live and earning money, and none of it is covered anywhere else in this repository.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| Game design document | Wiki, one page kept current | Discussed constantly during pre-production, read by non-technical roles, changes by consensus rather than by pull request |
| Art bible | Shared drive or DAM, linked from the wiki | It is mostly images. This repository, and Git generally, is a poor home for a document whose content is visual reference |
| Business plan | Wherever the pitch lives: wiki, shared drive, or a deck tool | Written for people outside engineering, often outside the company |
| Asset and contribution log | Docs-as-code or the asset pipeline tool, whichever already tracks version and rights | It is a status and rights record for configuration items; treat it the way a [configuration management plan](../general-swe/foundations/configuration-management-plan.md) treats any other item under control |
| Cycle retrospective | Wiki | A dated, discussed record, kept in a series so patterns across milestones are visible |
| Deployment plan | With the release ticket, one per submission | Dated and single-use, same reasoning as the general [deployment plan](../general-swe/foundations/deployment-plan.md) |
| Release notes | The store page, patch notes site, or in-client | Written for players, not for the team |
| Balance log | Docs-as-code, next to the tuning data it explains | Only trustworthy if it changes in the same commit as the values it describes |
| Live-operations plan | Wiki or the tracker that already holds the calendar | A living schedule, edited constantly, read by non-engineering roles |
| Privacy ledger | Wherever your legal or compliance function keeps controlled records, referenced from engineering docs | It is closer to a regulatory filing than to engineering documentation, and it needs an owner outside engineering |
| Age rating and compliance record | Same controlled location as the privacy ledger | Same reasoning: an auditable compliance record, not a design document |

The pattern underneath: **documents written for engineering and read against the code go in the repository. Documents written for players, publishers, regulators, or a whole studio go where those readers already are.** Most of this area's documents fall in the second group, which is the opposite balance from `general-swe/` and worth noticing.

---

## What to write first

1. **Game design document**, even a short one, before the pitch. It is what makes the pitch coherent.
2. **Business plan**, once the pitch needs funding or a greenlight decision.
3. **Art bible**, once direction is locked and more than one person or vendor is producing art against it.
4. **Everything in `live-operations/`**, before the first live release, not after. A privacy ledger and an age rating record written after launch are written under regulatory pressure instead of on your own schedule.
