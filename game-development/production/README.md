# Production

Two documents for a team that has moved past a two-person prototype: one tracking the assets flowing in from a growing and often outsourced contributor base, one reviewing how a whole production phase actually went.

## The documents

| Document | Answers |
|---|---|
| [`asset-and-contribution-log.md`](asset-and-contribution-log.md) | What is this asset, who made it, and do we actually have the right to ship it? |
| [`cycle-retrospective.md`](cycle-retrospective.md) | What did this milestone teach us, and what changes before the next one? |

## When to use each

**Asset and contribution log: the moment a non-employee touches an asset.** A contractor, an outsourcing vendor, a licensed music track, a stock asset, a community contribution. In-house, full-time teams working entirely in owned tools can often get away without this; the moment rights are not automatically and uniformly yours, you need a record of who made what and under what terms, because that question will eventually get asked by a publisher, a platform reviewer, or a lawyer, and "we think we're fine" is not an answer.

**Cycle retrospective: at the end of each production milestone.** Vertical slice, alpha, beta, gold, or a live-ops season. This is not the same event as a Scrum [sprint retrospective](../../general-swe/agile-scrum/sprint-retrospective.md); it runs on a longer, milestone-shaped cadence and looks specifically at the failure patterns published research has found recurring in game production: scope creep, schedule slippage, crunch, and the communication cost of a diverse team. Run both if your team also works in sprints. They answer different questions at different scales.

## Why these two, not folded into general-swe

`general-swe/foundations/configuration-management-plan.md` already defines what a configuration item is and who controls it, and `general-swe/foundations/changelog.md` already tracks what changed in code. Neither handles the specific failure mode games hit constantly: a visual or audio asset whose rights were never actually cleared, because it moved through a contractor, a stock library, or an outsourcing vendor rather than through a single employer's default ownership. The asset and contribution log is a configuration item record, purpose-built for that gap.

The cycle retrospective exists because a game production milestone is not a sprint. It spans months, involves roles a sprint retrospective format was never written for, and needs a lens tuned to the problems that recur in game postmortems specifically, not general software delivery.

## Where these live

Both are dated, discussed records more than they are engineering references. See the area [README](../README.md) for the full placement table and reasoning.
