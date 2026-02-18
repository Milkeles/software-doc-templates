# Performance

Two documents. One sets limits before the code is written, the other reports what actually happened to users.

| Document | Write it when |
|---|---|
| [`performance-budget.md`](performance-budget.md) | You have measured your current numbers and want to stop them getting worse. Not before you have measured |
| [`performance-review.md`](performance-review.md) | You have field data and someone asks quarterly whether the site is getting faster or slower |

Skip both if nobody has ever measured your site. A budget invented from a blog post sets a number your team will either sail under without effort or breach on day one and then disable. Measure first, then set limits you have a reason for.

---

## The distinction that everything else depends on

**Lab data is what a machine you control measured. Field data is what your users experienced.**

They answer different questions and cannot substitute for each other.

```
   LAB                                    FIELD
   synthetic run, your hardware           real users, their hardware

   Lighthouse, WebPageTest,               Chrome UX Report (CrUX),
   your CI performance job                your own RUM

   answers: did this change               answers: is the site fast
   make it slower?                        for the people using it?

   deterministic enough to                too noisy for a gate,
   gate a pull request                    the only thing that
   (for some metrics)                     tells you the truth

        |                                        |
        v                                        v
   performance-budget.md                  performance-review.md
```

The budget lives in the lab because it has to run before merge. The review lives in the field because a lab number tells you nothing about whether users are having a good time. Teams that confuse the two either gate on data too noisy to gate on, or ship a green CI badge to users on 4G.

---

## Core Web Vitals, and the parts of them worth knowing

Google's three field metrics, and the closest thing the web has to an agreed definition of "fast".

| Metric | Good | Poor | Measures |
|---|---|---|---|
| **LCP** Largest Contentful Paint | ≤ 2500 ms | > 4000 ms | When the main content appeared |
| **INP** Interaction to Next Paint | ≤ 200 ms | > 500 ms | How quickly the page responds to input, across the whole visit |
| **CLS** Cumulative Layout Shift | ≤ 0.1 | > 0.25 | How much content moved under the user |

Anything between good and poor is "needs improvement".

**All three are measured at the 75th percentile of page loads.** Google's stated reasoning: it ensures "the majority of visits to a site or page experienced the target level of performance", while the threshold "shouldn't be overly impacted by outliers". Your median tells you nothing about the quarter of visits that were worst, and the worst quarter is where users leave.

### How the thresholds were chosen, which is worth knowing before you treat them as physics

Google publishes its criteria: a threshold must reflect a quality of experience, be achievable by at least 10% of origins, and be groundable in research where research exists.

For LCP and INP, human-computer interaction research supports the numbers. Attention span research behind loading thresholds, and Michotte's work on perceived causality behind the roughly 100 ms boundary at which a response stops feeling caused by your action.

**For CLS there is no research basis and Google says so:** "we are not aware of research that can directly inform the thresholds we should set". The 0.1 and 0.25 values came from manual evaluation of a range of sites.

This does not make CLS a bad metric. It makes 0.1 a convention rather than a finding, and you should describe it that way when someone asks why the budget says 0.1.

### Stability, and what is coming

Google states that "stable Core Web Vitals metrics won't change more than once per year". INP replaced FID on 12 March 2024. As of July 2026 there has been no further metric change and no threshold change.

The Soft Navigations API, announced at Google I/O on 19 May 2026, will bring Core Web Vitals to single-page applications by attributing metrics to client-side route changes rather than only the initial load. It had not shipped as of July 2026. If you run an SPA, this is the change to watch; today your CWV data describes your first page load and almost nothing after it.

**Browser support is uneven and this constrains your field data.** LCP and INP became Baseline Newly available on 12 December 2025 with Safari 26.2. **CLS remains Chromium-only.** There is no cross-browser field source for CLS, which means your CLS number describes Chrome users. Say so in the review rather than presenting it as a site-wide figure.

---

## Where the numbers come from

### CrUX

The Chrome User Experience Report. Free, public, and the source Google itself uses for Search signals.

Its limits decide whether you can rely on it:

- **Eligibility.** A page must be publicly discoverable, and "sufficiently popular", defined as having "a minimum number of visitors". **Google does not publish that number.** Low-traffic pages and everything behind a login are absent, and you cannot predict which.
- **Which users.** Only Chrome users who have usage statistics reporting enabled, history synced, and no sync passphrase. Excludes Chrome on iOS, Android WebView, and non-Google Chromium builds.
- **Window.** A rolling 28-day aggregate. A fix landed today moves the number over a month, not overnight. Plan review cadence around this.

Google's own advice: "we strongly recommend supplementing it with your own RUM."

### Your own RUM

Covers logged-in pages, gives per-route and per-segment breakdowns, and reports in hours instead of weeks. Costs engineering time and a vendor bill. Worth it once CrUX stops covering the pages that matter to you, which for most products is the moment users log in.

### Lighthouse

Lab only. Useful for diagnosis, dangerous as a target.

The score weights, unchanged since Lighthouse 10 and still current in Lighthouse 13 (released 10 October 2025, "there are no changes to the performance scoring in this version"):

| Metric | Weight |
|---|---|
| Total Blocking Time | 30% |
| Largest Contentful Paint | 25% |
| Cumulative Layout Shift | 25% |
| First Contentful Paint | 10% |
| Speed Index | 10% |

Note what this means: **Total Blocking Time carries the largest single weight, and TBT is not a Core Web Vital.** Optimising the Lighthouse score and optimising the user experience are related but not the same activity. Google positions TBT as "a reasonable proxy metric for INP for the lab", while stating it is "not a substitute for INP in and of itself", and advises against measuring TBT in the field at all because "user interaction can affect your page's TBT in ways that lead to lots of variance".

---

## Why these documents work, and how good the evidence is

### The budget works because a limit converts a diffuse worry into a specific event. Evidence: none, and the origin is honest about it

There is no authoritative definition of a performance budget and no study showing budgets improve performance. The idea comes from Tim Kadlec's 2013 post "Setting a Performance Budget", responding to Brad Frost's "Performance As Design" of 28 January 2013. Kadlec's definition: "a clearly defined limit on one or more performance metrics that the team agrees not to exceed, and that is used to guide design and development".

The mechanism it relies on is not measured but is easy to state. Without a budget, "the site feels slow" is an opinion any individual change can deny responsibility for, because no single change made it slow. With a budget, a specific pull request either breaches a specific number or does not. That converts an argument about taste into a check, and moves the cost of slowness from everyone later to the author now.

Treat it as a coordination device with a plausible mechanism, not as an evidence-backed practice. Say that when someone asks.

### Reviews work because the 28-day window makes short-term reactions meaningless

Field data moves slowly. A team watching a CrUX dashboard weekly is watching a lagging 28-day average and will attribute noise to whatever shipped most recently.

A periodic review with a fixed cadence, a fixed set of numbers, and last period's figures printed next to this period's removes the temptation. It also forces the comparison that matters: not "is 2.4 seconds good", but "is it better or worse than last quarter, and what did we do in between".

### Arguments you should not use

**"Users notice a change of 20%."** This number is real but it is not a web performance finding. It traces to a 2015 Smashing Magazine article applying the Weber-Fechner law, which reports the just-noticeable difference for intervals under 30 seconds as somewhere between 7% and 18%, with 20% used as conservative rounding. It is a psychophysics result about interval perception, generalised. Cite it as that or not at all.

**"Be 20% faster than your fastest competitor."** The same number, repurposed. No source tests it. It is folklore.

**Conversion-rate case studies.** The figures circulating for Core Web Vitals business impact come largely from `web.dev/case-studies`, which is Google-hosted but partner-submitted; the page invites companies to "submit a content proposal". Of the studies collected there, only Vodafone describes a controlled experiment. Figures quoted to two decimal places from uncontrolled before-and-after comparisons imply a precision the method cannot support. If you need a business case, run your own experiment. If you cannot, argue the point on user experience and stop.

**Google's published starter budget numbers.** The commonly cited "under 5 seconds to interactive, under 170 KB of compressed critical-path resources" comes from Alex Russell's 2017 analysis of median mobile hardware and networks. Both have moved substantially. The reasoning still holds; the numbers do not.

---

## What everyone else is achieving, for calibration

From the Web Almanac 2025, which analyses CrUX across millions of origins:

- **48% of mobile origins and 56% of desktop origins pass all three Core Web Vitals.**
- Measured individually in June 2025: LCP good for 74%, CLS good for 72%, INP good for 97%.
- In 2024 the pass rates were 43% mobile and 54% desktop.
- **Secondary pages outperform home pages**, 61% versus 47% on desktop. Home pages carry hero images, carousels and marketing tags. If you sample only your home page you will see your worst number and misdiagnose the site.

Do not compute year-on-year deltas from these figures. The measured population changes between editions, so the bases are not consistent.

The useful reading: passing all three CWV puts you in roughly the better half of the web, not in an elite. And your INP is probably fine while your LCP probably is not, which is where to look first.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| Performance budget | Docs-as-code, next to the CI config that enforces it | An unenforced budget is a wish. Keeping the document and the threshold file apart guarantees they diverge |
| Performance review | Wiki, one per period | A dated record whose value is comparison against previous editions. It never changes after publication, and nothing in the code depends on it |

The budget is the stronger case in this repository for docs-as-code, because the document and the enforcement can be made literally the same file. If your CI reads thresholds from a config, the budget document should either be that config with comments, or sit beside it and be reviewed in the same pull request.

---

## What to write first

1. **Measure.** CrUX for your origin takes ten minutes and costs nothing. You cannot write either document without it.
2. **Performance budget**, on quantity metrics only. Bundle size and request count are deterministic, so you can gate on them from day one.
3. **Performance review**, once you have two periods to compare. One period is a number, not a review.
4. **Extend the budget to timing metrics** only after you have a dedicated runner and a median-of-five setup. See the budget template for why.

---

## Sources

- web.dev, "Web Vitals", "Defining the Core Web Vitals metrics thresholds", "Largest Contentful Paint", "Interaction to Next Paint", "Cumulative Layout Shift", "Total Blocking Time", "Time to First Byte"
- Chrome UX Report documentation, methodology and eligibility
- Lighthouse scoring documentation; `GoogleChrome/lighthouse` release notes for v13
- Tim Kadlec, "Setting a Performance Budget" (2013); Brad Frost, "Performance As Design" (28 January 2013)
- HTTP Archive, Web Almanac 2025, Performance chapter
- Denys Mishunov, "Why Perceived Performance Matters", Smashing Magazine (2015), for the Weber-Fechner derivation

**On sourcing.** Threshold values, metric definitions and browser support here come from primary Google and W3C documentation. Where a widely repeated claim has no primary source, this README says so rather than repeating it. That applies to automated business-impact figures, competitor-relative speed targets, and any percentage attributed to Google that Google has not published.
