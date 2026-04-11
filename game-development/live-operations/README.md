# Live operations

Six documents for a game that has shipped and keeps changing: patches, tuning, live content, and the legal and platform obligations that only start to bite once real players are sending you real data and real money.

## The documents

| Document | Answers |
|---|---|
| [`deployment-plan.md`](deployment-plan.md) | How does a specific release reach certified platforms and live servers? |
| [`release-notes.md`](release-notes.md) | What changed, written for the player who has to decide whether they care? |
| [`balance-log.md`](balance-log.md) | Why is this value what it is, and did changing it work? |
| [`live-ops-plan.md`](live-ops-plan.md) | What content and events are scheduled, and can the team actually deliver them? |
| [`privacy-ledger.md`](privacy-ledger.md) | What player data do we hold, why, and under what legal basis? |
| [`age-rating-compliance-record.md`](age-rating-compliance-record.md) | What have we told rating bodies and platforms, and is it still true? |

## When to use each

**Deployment plan and release notes: every release to a live game.** These extend the general-purpose [deployment plan](../../general-swe/foundations/deployment-plan.md) and [release notes](../../general-swe/foundations/release-notes.md) with what is specific to a certified platform and a player audience: submission lead times you do not control, a client patch that cannot be un-downloaded once a player has it, and a patch note that has to explain a balance change to someone who has never seen a tuning spreadsheet.

**Balance log: any live game with tunable values.** Damage numbers, drop rates, matchmaking parameters, economy sinks and faucets. If a number in your game can make a player feel cheated when it changes, write down why it changed.

**Live-ops plan: any game running events, seasons, or scheduled content after launch.** A single-release game with no post-launch content plan can skip this.

**Privacy ledger and age rating and compliance record: before your first live release, not after.** These are not optional once real players are sending real data through a product that a broad, plausibly-including-minors audience can download. Writing them under regulatory pressure after a problem is found is a materially worse position than writing them on your own schedule.

## Why these are separate from the general-purpose versions

Three of these six have close relatives in `general-swe/foundations/`: a deployment plan, release notes, and (loosely) a changelog. They earn separate game-specific versions because a live game adds real, verifiable constraints that the general templates do not carry: certification lead times measured in weeks that you do not control, a client patch a player has already installed that cannot be rolled back the way server code can, and patch notes that have to translate a balance change for a non-technical, often emotionally invested reader.

The other three, balance log, live-ops plan, privacy ledger, and age rating record, have no general-purpose equivalent because the problem they solve does not exist outside games and similarly data-hungry, broadly-distributed, regulator-attention-drawing consumer products: a tuning decision that is opinion until measured, a content calendar that competes with your team's actual capacity, and a set of disclosure obligations, some legal and some self-regulatory, that a published 2023 study found game companies comply with roughly 29% of the time on mobile storefronts when nobody is forcing them to.

## Where these live

| Document | Home |
|---|---|
| Deployment plan | With the release ticket |
| Release notes | The store page or in-client patch notes |
| Balance log | Docs-as-code, next to the tuning data |
| Live-ops plan | Wiki or the tracker holding the calendar |
| Privacy ledger | A controlled record your legal or compliance function owns |
| Age rating and compliance record | The same controlled location as the privacy ledger |

See the area [README](../README.md) for the reasoning behind each.
