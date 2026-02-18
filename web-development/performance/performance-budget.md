# Performance Budget

> Limits the team agrees not to exceed, enforced automatically, so that no single change can quietly make the site slower.
>
> **Prerequisite: you have measured.** A budget copied from an article sets a number nobody has a reason for. Measure your current values first, then set limits with a stated relationship to them.
>
> **Where it lives.** Docs-as-code, next to the CI configuration that enforces it. If the document and the enforced thresholds are separate files, they will disagree within a quarter, and the document will be the one that is wrong.
>
> **Delete this block before publishing.**

---

## 1. What this budget covers

State the pages and the conditions. A budget without stated conditions is unenforceable, because the same page measured on different hardware gives different answers.

| Field | Example |
|---|---|
| Pages in scope | Home, search results, product detail, checkout steps 1 to 3 |
| Device profile | Moto G Power class, 4x CPU throttling |
| Network profile | Simulated 4G, 1.6 Mbps down, 150 ms RTT |
| Measurement tool and version | Lighthouse 13, five runs, median reported |
| Runner | Dedicated CI machine, not shared, not a function-as-a-service instance |

**Budget by page type, not by page.** One number for a whole site either lets the heavy pages through or blocks the light ones for no reason. Home pages and checkout pages have genuinely different budgets, and the review will show your home page is the worst offender.

---

## 2. The limits

Split the table by what you can actually enforce, because this is the decision that determines whether the budget survives its first quarter.

### Hard limits: fail the build

Only deterministic metrics belong here. These produce the same value on the same input, so a breach is always a real breach.

| Metric | Budget | Current | Why this number |
|---|---|---|---|
| JavaScript, compressed, initial route | 170 KB | 148 KB | Current plus 15% headroom |
| CSS, compressed | 40 KB | 31 KB | |
| Images, initial viewport | 250 KB | 210 KB | |
| Total requests, initial load | 45 | 38 | |
| Third-party scripts | 6 | 6 | At the limit. New tags require removing one |

**The "why this number" column is not optional.** In six months someone will want to breach the budget, and the argument will be won by whoever can say what the limit was for. "Current plus 15%" is a reason. A number with no reason gets raised.

### Soft limits: warn, do not block

Timing metrics belong here, because they are not stable enough to gate on.

| Metric | Target | Alert if | Source |
|---|---|---|---|
| LCP, lab, median of 5 | ≤ 2.0 s | > 2.5 s or 10% worse than 7-day median | Lighthouse CI |
| Total Blocking Time | ≤ 200 ms | > 300 ms | Lighthouse CI |
| LCP, field, 75th percentile | ≤ 2.5 s | Above threshold for 2 consecutive weeks | CrUX / RUM |
| INP, field, 75th percentile | ≤ 200 ms | Above threshold for 2 consecutive weeks | CrUX / RUM |
| CLS, field, 75th percentile | ≤ 0.1 | Above threshold for 2 consecutive weeks | CrUX / RUM |

Field metrics are lagging indicators on a rolling 28-day window. They cannot block a pull request and should not be wired to try.

### Why timing metrics do not get hard gates

The Lighthouse project documents this against itself:

> Lighthouse performance scores will change due to inherent variability in web and network technologies, even if there hasn't been a code change. Run Lighthouse multiple times and beware of variability before drawing conclusions.

And on how to configure thresholds:

> When creating your thresholds for failure, either mental or programmatic, use aggregate values like the median, 90th percentile, or even min/max instead of single test results.

A single-run timing gate will fail builds that changed nothing. Each false failure teaches the team that the gate is noise, and the gate is disabled shortly afterwards. A soft alert on a median that someone reads is worth more than a hard gate everyone routes around.

If you want timing gates anyway, the project's own conditions are:

- **Median of at least five runs.** "The median Lighthouse score of 5 runs is twice as stable as 1 run."
- **Dedicated hardware.** "Avoid function-as-a-service infrastructure (Lambda, GCF, etc)" and "avoid 'burstable' or 'shared-core' instance types".
- **One at a time.** "DO NOT collect multiple Lighthouse reports at the same time on the same machine."

Meet all three or keep timing metrics as alerts.

---

## 3. Enforcement

Say exactly where each limit is checked and what happens on breach. A budget nothing checks is a wish.

| Limit type | Checked by | On breach |
|---|---|---|
| Bundle and asset sizes | Bundler plugin or size check in CI, every pull request | Build fails |
| Request count | Lighthouse CI assertion | Build fails |
| Lab timings | Lighthouse CI, median of 5, on main after merge | Warning comment, no block |
| Field metrics | Weekly job against CrUX and RUM | Alert to the owning channel |

Name the config file and keep the path current:

> Enforced by `lighthouserc.json` and `bundlesize.config.json`. Both are reviewed in the same pull request as this document.

---

## 4. Breaking the budget

The section that decides whether the budget is real. Without it, the first urgent feature raises the number silently and the budget is decorative from then on.

State:

**Who can approve a breach.** A named role, not "the team".

**What an approval requires.** At minimum: what is being added, the measured cost, what it buys, and either a date to bring it back under or an explicit permanent raise with a reason.

**Where the decision is recorded.** In the pull request, and in this document's history. If a limit changes, the commit message says why.

> A breach requires approval from the frontend lead. The pull request states the measured cost, the reason, and either a remediation date or a request to raise the limit permanently. Raising a limit is a change to this file and is reviewed as one.

**Do not allow silent raises.** The failure mode is not one deliberate breach; it is twenty undiscussed ones, each defensible alone.

---

## 5. Review

The budget stops matching reality as the product changes. Say when it gets revisited.

Review triggers:
- Quarterly, alongside the [performance review](performance-review.md).
- After any major framework or platform change.
- When a limit has been breached twice in a quarter, which usually means the limit is wrong rather than the team is careless.

Record the review date in this file. A budget last reviewed two years ago is being ignored, whatever the numbers say.

---

## Setting the initial numbers

Three ways, in descending order of how well they hold up under challenge.

**From your current values.** Measure, then set the limit slightly above. This freezes the status quo and stops decay, which is what most teams actually need. It does not make you faster, and you should say so rather than letting anyone think otherwise.

**From a target.** Pick the experience you want, work backwards to the asset sizes and request counts that permit it, and set those. Honest, harder, and usually reveals the target is unreachable without removing something. That revelation is the useful output.

**From a competitor.** Measure two or three competitors on the same profile and set limits below theirs. Defensible as a business argument. Note that the widely repeated advice to be "20% faster than your fastest competitor" has no source behind it, so use the comparison, not the multiplier.

Google's categories are useful for structuring the table: quantity-based limits (bytes, requests), milestone timings, and rule-based scores. Its published starter figures are not; they derive from a 2017 analysis of median mobile hardware and networks, and both have moved.

---

## Common failures in this document

- **Written before measuring.** Produces limits with no relationship to the product, breached on day one, then disabled.
- **Hard gates on timing metrics from single runs.** Fails builds that changed nothing, and the gate is removed within a month.
- **One budget for the whole site.** Either too loose for the light pages or impossible for the heavy ones.
- **No "why this number" column.** Every limit is negotiable when nobody remembers what it was for.
- **No breach process.** The budget is raised quietly the first time it is inconvenient.
- **Document and CI config out of sync.** The document says 170 KB, CI checks 250 KB, and nobody notices until an audit.

---

## Related documents

- [`performance-review.md`](performance-review.md). Reports what users experienced. The budget prevents decay; the review tells you whether prevention worked
- [`../foundations/browser-support-policy.md`](../foundations/browser-support-policy.md). The device and browser profile the budget measures against should match the policy, not a machine someone had spare
