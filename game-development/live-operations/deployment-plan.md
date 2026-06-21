# Deployment plan: {Release}, live game

*Also called: release plan, rollout plan.*

*Italic text is guidance. Delete it as you fill each section in.*

*Read the general [deployment plan](../../general-swe/foundations/deployment-plan.md) first. Everything there, go/no-go, sequence, canary evaluation, rollback, applies here. This document adds what a certified platform and a live player base change about it. Use both, or fold this section into the general template rather than maintaining two full copies if your release only touches server-side systems.*

| | |
|---|---|
| **Release** | |
| **Platforms** | *Every platform this release ships to* |
| **Deployment owner** | |
| **Go/no-go decision** | |

---

## What certification changes

*A server-side deployment is yours to schedule. A console or storefront release is not: it passes through a submission and review process you do not control the timing of.*

| Platform | Submission required | Typical review time | Submitted | Approved | Notes |
|---|---|---|---|---|---|
| *Steam* | *No formal cert, but store page and build review apply* | | | | |
| *PlayStation* | *Yes* | | | | |
| *Xbox* | *Yes* | | | | |
| *Nintendo Switch* | *Yes* | | | | |
| *Mobile (iOS)* | *Yes, App Store review* | | | | |
| *Mobile (Android)* | *Yes, Play Store review, faster in practice* | | | | |

**Plan the earliest platform's submission date backward from your target release date, not forward from when the build is ready.** The slowest platform's review time sets your real deadline. A build that is code-complete on Tuesday does not mean a Thursday release if console certification takes two weeks.

**Cross-platform parity is not guaranteed to be simultaneous.** If one platform's review takes materially longer, decide now whether you release when the fastest platform clears, accepting a content or balance gap between platforms, or hold every platform for the slowest. Either is defensible; an undecided default is not, because it becomes a support and community problem the moment players compare notes across platforms.

---

## Go / no-go

*Extend the general template's table with what is specific to a live service.*

| Condition | Confirmed by | Status |
|---|---|---|
| *All required checks green on the release commit* | *CI* | |
| *Every targeted platform's certification approved* | *Deployment owner* | |
| *Live server capacity headroom confirmed for expected patch-day traffic* | *Ops* | |
| *No conflicting item on the [live-ops plan](live-ops-plan.md) calendar* | *Live-ops owner* | |
| *Patch notes drafted and reviewed against the [balance log](balance-log.md)* | *Community or design* | |

---

## Sequence

*As the general template, with platform submission and store publishing as explicit steps, since they have real duration and can fail independently of your own pipeline.*

| # | Step | Owner | Expected | Check before continuing |
|---|---|---|---|---|
| 1 | *Submit build to platform certification* | | | *Submission accepted, not just uploaded* |
| 2 | *Certification result received* | | | *Approved, or a rejection with a named reason to fix* |
| 3 | *Deploy server-side changes* | | | |
| 4 | *Publish client build to storefront* | | | |
| 5 | *Publish patch notes* | | | |

---

## Rollback

*The general template's rule holds and matters more here: code rolls back, data and outbound messages do not. A live game adds a case that rule does not cover.*

**A client patch a player has already downloaded cannot be un-downloaded.** Server-side rollback restores the previous server behaviour immediately. A broken client patch already installed on a player's device stays broken until you ship a follow-up patch, which is itself subject to the same certification lead time that got you into this release. Plan for this explicitly: a client-side rollback is not a rollback, it is a second release, on the same submission timeline as the first.

| Irreversible or slow-to-reverse action | Why | Mitigation |
|---|---|---|
| *Client build already downloaded by players* | *Cannot be recalled; a fix is a new submission* | *Feature-flag risky client changes so they can be disabled server-side without a new client build* |
| *Certification-gated re-release* | *Subject to the same review time as the original submission* | *Reserve an expedited-review path with the platform if one exists, and know its criteria in advance* |

---

## After

*As the general template. Add platform-specific monitoring: crash rates and store reviews per platform, since a problem specific to one platform's hardware or OS version will not show up in aggregate metrics.*

---

## Notes on using this template

*Delete this section too.*

**Certification lead time is a scheduling input, not a risk to manage around.** Treat the slowest platform's review time as fixed, and build your release calendar backward from it, the same way the general deployment plan treats an irreversible action as a fact to plan around rather than a risk to accept.

**Server-first releases where a client rebuild is optional deserve real design effort.** A change that can ship entirely server-side, a tuning value, a drop rate, a server-authoritative rule, avoids certification lead time and rollback risk entirely. Not every change can be structured this way, but the ones that can are worth the extra design cost.

**Where this lives:** with the release ticket, same as the general deployment plan.

---

## Related documents

- [`../../general-swe/foundations/deployment-plan.md`](../../general-swe/foundations/deployment-plan.md). The base template this one extends
- [`release-notes.md`](release-notes.md). Published once this deployment completes
- [`balance-log.md`](balance-log.md). What a tuning change in this release actually changed, and why
- [`live-ops-plan.md`](live-ops-plan.md). What this release must not collide with on the calendar
