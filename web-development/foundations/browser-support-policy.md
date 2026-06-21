# Browser Support Policy

> Which browsers you support, what "support" means, and how a browser leaves the list.
>
> **Also called:** browser support matrix, or browser compatibility matrix.
>
> **The cheapest document in this repository.** One page, and it ends an argument that otherwise recurs every few months in design review, in QA triage, and in every bug report that begins "on Safari 14".
>
> **Where it lives.** Docs-as-code, next to the `browserslist` configuration. The prose and the machine-readable version must not disagree, and the only reliable way to keep them together is to keep them together.
>
> **Delete this block before publishing.**

---

## 1. Supported browsers

The list, with what support means for each tier. Tiers matter because "support" is not one thing: full parity for everything is expensive and nobody actually does it.

| Tier | Browsers | What we guarantee |
|---|---|---|
| **Full** | Chrome, Edge, Firefox, Safari: current and previous major. Chrome and Firefox on Android, Safari on iOS: current and previous | Every feature works. Tested every release. Visual parity within reason |
| **Functional** | Firefox ESR, Samsung Internet current | All tasks completable. Visual differences accepted. Tested per release, not per change |
| **Unsupported** | Everything else | No testing, no bug fixes. The site is not deliberately blocked |

**Define the tiers by what you promise, not by a percentage.** "We support browsers above 0.5% usage" tells a developer nothing about whether to fix a bug. "All tasks completable, visual differences accepted" tells them exactly.

**Say what "unsupported" means in practice.** Blocked with a message, or left to work if it works? Leaving it unblocked is usually right: users on old browsers are often unable to upgrade, and a hard block converts a degraded experience into no experience.

---

## 2. The machine-readable version

The prose above and this configuration must match. If they can differ, they will.

```
# .browserslistrc
last 2 versions
Firefox ESR
> 0.5%
not dead
```

`browserslist` is the de facto standard here. Babel, autoprefixer, PostCSS and most bundlers read it, which is why it, and not this document, decides what actually ships.

Two things to know before copying a query:

**`defaults` is not neutral.** It expands to `> 0.5%, last 2 versions, Firefox ESR, not dead`. That is a real policy, chosen by someone else, and it may not be yours.

**Percentage-based queries use global usage data**, not your usage data. If your product is enterprise software in one country, global share is the wrong denominator. Export your own analytics and set the list from that, or use `browserslist`'s regional queries.

Run `npx browserslist` and paste the resolved list into a comment. It is the only way anyone can see what the query actually means today, and it changes as usage data moves underneath you.

---

## 3. How a browser gets added or removed

The section that stops the policy from freezing.

State the rule, the review cadence, and who decides.

> Reviewed quarterly against our own analytics. A browser drops to Functional when it falls below 1% of sessions for two consecutive quarters, and to Unsupported one quarter later. Removal is announced in the release notes one release ahead. The frontend lead decides.

Three parts make this work:

- **Your data, not global data.** Global share tells you what the web uses. Your analytics tell you what your users use, and the two often differ by more than an order of magnitude.
- **Two consecutive periods.** Stops a seasonal dip removing a browser.
- **Notice before removal.** Some of your users cannot upgrade. A corporate fleet on a locked build needs lead time, and the person who can act on the notice is not the person using the browser.

---

## 4. Feature adoption

The question this policy actually gets asked: can I use this new API?

**Baseline** is the current best answer. It is maintained by the W3C WebDX Community Group and gives every web feature a support status:

| Status | Means |
|---|---|
| **Limited availability** | Not in all core browsers. Needs a fallback |
| **Newly available** | Works in all core browsers as of a given date |
| **Widely available** | Newly available plus 30 months |

The core browser set is Chrome (desktop and Android), Edge, Firefox (desktop and Android), and Safari (macOS and iOS): four browsers, six targets.

State your own rule against it:

> Widely available features: use freely. Newly available: use with a tested fallback, and note it in the pull request. Limited availability: requires approval and a documented fallback.

**Baseline is not a substitute for your policy**, because it says nothing about the browser versions you actually support. A feature can be Widely available and still absent from the Firefox ESR you promised to support. Check both.

State your position on polyfills too, since a permissive polyfill policy quietly moves cost into the [performance budget](../performance/performance-budget.md). "Polyfills for Full tier browsers only, and each one is counted against the JavaScript budget" is a clear position.

---

## 5. Testing

Which browsers are actually tested, how, and where. This is where policies usually turn out to be fiction.

| Browser | How | When |
|---|---|---|
| Chrome latest | Automated end-to-end | Every pull request |
| Firefox, Safari latest | Automated end-to-end | Every release |
| Safari iOS, Chrome Android | Real devices, manual smoke test | Every release |
| Firefox ESR, Samsung Internet | Manual smoke test | Every release |

**If a browser is in the Full tier and nothing tests it, either test it or move it down a tier.** An untested support claim is discovered by a user, and by then it is a bug report about a browser you said worked.

Note where the tests run: a real device lab, a cloud provider, or emulation. Emulated Safari is not Safari, and the difference shows up in exactly the places that are hardest to debug remotely.

---

## 6. What users on unsupported browsers see

A short, deliberate answer. Not an accident.

Options, in descending order of how well they usually work:

- **Nothing special.** The site works as well as it works. Best default.
- **A dismissible notice** suggesting an upgrade, with the site fully usable behind it.
- **A hard block.** Only defensible where a security or correctness requirement makes degraded operation genuinely unsafe, such as a browser with no support for a cryptographic primitive you depend on.

If you show a notice, base it on feature detection rather than user-agent parsing. User-agent strings are deliberately unreliable and increasingly frozen; a policy built on parsing them will misfire on browsers that did not exist when it was written.

---

## Common failures in this document

- **Prose and `browserslist` disagree.** The config wins silently, so the document describes a policy that is not in effect.
- **Copied `defaults` without reading it.** Adopts someone else's policy by accident.
- **Global usage data for a regional product.** Supports browsers nobody uses, drops browsers your customers depend on.
- **Full tier with no tests.** Support in name only.
- **Never reviewed.** Two years later you are supporting a browser with 0.01% of your traffic and paying for it in every design review.
- **User-agent sniffing.** Breaks as browsers change their strings, which they do deliberately.

---

## Related documents

- [`frontend-architecture.md`](frontend-architecture.md). Build targets must match this policy. When they diverge, this document is usually the one that is wrong
- [`../performance/performance-budget.md`](../performance/performance-budget.md). The device and network profile you measure against should come from the same data as this list
- [`../accessibility/accessibility-test-plan.md`](../accessibility/accessibility-test-plan.md). The accessibility support baseline is the same kind of statement, made about assistive technology
