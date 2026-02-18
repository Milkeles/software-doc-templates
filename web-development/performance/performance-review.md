# Performance Review

> A dated record of what users actually experienced this period, next to what they experienced last period, with what you did in between.
>
> **Why it is periodic and not a dashboard.** Field data is a rolling 28-day aggregate. A team watching it daily is watching an average that cannot move fast, and will attribute noise to whatever shipped most recently. A fixed cadence with the previous period printed alongside removes that.
>
> **Where it lives.** Wiki, one page per period, never edited after publication. Its value is the comparison, so the archive is the document.
>
> **Cadence.** Quarterly for most teams. Monthly if you ship performance work continuously. Anything faster than monthly fights the 28-day window.
>
> **Delete this block before publishing.**

---

## 1. Header

| Field | Content |
|---|---|
| Period | The window covered, with dates. "Q2 2026, 1 April to 30 June" |
| Data sources | CrUX, your RUM, and the date the data was pulled |
| Author | Who to ask about the numbers |

Pin the pull date. CrUX moves under you, so a review re-read in six months should say what it was looking at.

---

## 2. Headline numbers

Three metrics, this period against last, at the 75th percentile.

| Metric | This period | Last period | Change | Threshold |
|---|---|---|---|---|
| LCP (mobile) | 2.9 s | 3.3 s | −0.4 s | ≤ 2.5 s good |
| INP (mobile) | 180 ms | 210 ms | −30 ms | ≤ 200 ms good |
| CLS (mobile) | 0.14 | 0.11 | +0.03 | ≤ 0.1 good |
| Origins passing all three | No | No | | |

**Report mobile and desktop separately.** Combining them hides the segment that is worse, which is almost always mobile, and which is almost always the majority of traffic.

**Report per page type, not just per origin.** The Web Almanac 2025 finding is consistent: secondary pages outperform home pages, 61% versus 47% passing on desktop. An origin-level number is dominated by whichever pages get the most traffic and will tell you the site is fine while checkout is not.

State clearly what each number is measured from. CrUX describes Chrome users who opted into usage reporting, on eligible public pages. It excludes everything behind a login, Chrome on iOS, and Android WebView. **CLS has no cross-browser field source at all**, so a CLS figure describes Chromium users only. Write that once in the review rather than letting a reader assume site-wide coverage.

---

## 3. What changed and why

The part that makes the review worth writing. Numbers without attribution are a dashboard screenshot.

For each meaningful movement:

**What moved.** The metric, the page type, the size of the change.

**What you believe caused it.** Deploys, infrastructure changes, a third-party tag added or removed, a traffic-mix shift.

**How confident you are.** Say it plainly. Most attributions are informed guesses, because you did not run a controlled experiment. A review that presents guesses as findings trains the team to distrust the whole document.

> LCP on product pages improved from 3.4 s to 2.7 s. We moved hero images to the CDN in week 3 and added `fetchpriority="high"`. Confidence: high. The change landed mid-period and the weekly RUM series steps at the same point.

> CLS on the home page rose from 0.09 to 0.16. The most likely cause is the promotional banner added in week 5, which loads after first paint with no reserved space. Confidence: medium. We have not reproduced it in the lab.

**Watch for traffic-mix effects.** A number can move because your users changed, not because your site did. A marketing campaign bringing older devices, or a new market with slower networks, moves the 75th percentile without a single line of code changing. Check the device and country mix before crediting an engineering change.

---

## 4. Budget status

How the [performance budget](performance-budget.md) held up.

| Limit | Budget | End of period | Breaches this period |
|---|---|---|---|
| JS, compressed, initial | 170 KB | 163 KB | 1, approved for the checkout rewrite |
| Third-party scripts | 6 | 7 | 1, raised permanently |

For each breach: what caused it, whether it was approved, and whether it was resolved or the limit was raised.

**A limit raised twice in a year is not a limit.** Say so here. This is the only place anyone reviews the budget's credibility rather than its contents.

---

## 5. What we will do next period

Two to four items. Fewer than that and the review had no consequence; more and none of them will happen.

Each item names an owner and the metric it targets.

> - Reserve space for the promotional banner. Target: home page CLS back under 0.1. Owner: [name].
> - Audit third-party tags and remove two. Target: INP on product pages. Owner: [name].

**Carry forward unfinished items from last period explicitly**, with the reason they did not happen. Silently dropping them is how a quarterly review becomes a ritual that changes nothing.

---

## 6. Limitations of this period's data

A short standing section. It stops each review re-arguing what the numbers mean.

State any that apply:

- CrUX omits pages that are not publicly discoverable or not "sufficiently popular". Google does not publish the popularity threshold, so you cannot tell which of your pages are missing.
- CrUX is a rolling 28-day window. Changes landing near the period boundary are partly attributed to the wrong period.
- CLS is Chromium-only.
- Single-page navigations are not captured as separate loads. The Soft Navigations API, announced in May 2026, will address this; it had not shipped as of July 2026. Until then, these figures describe initial loads.
- Any RUM sampling rate you apply.

---

## Common failures in this document

- **A dashboard screenshot with no attribution.** Records that something changed without establishing what changed it, so nothing is learned.
- **Origin-level numbers only.** Hides the page type that is failing.
- **Mobile and desktop combined.** Hides the segment that matters.
- **Guesses presented as findings.** Discredits the document the first time one is disproved.
- **Actions with no owner.** Nothing happens, and the next review lists the same items.
- **Edited after publication.** Destroys the comparison, which was the only reason to write it.

---

## Related documents

- [`performance-budget.md`](performance-budget.md). The limits this review reports against
- [`README.md`](README.md). Where the metrics, thresholds and their evidential status are explained, so this document does not have to repeat them
