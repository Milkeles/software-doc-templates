# Bug: {What a user would say went wrong}

*Also called: defect report, issue.*

*Italic text is guidance. Delete it as you fill each section in.*

*Title by observable effect, not by suspected cause. "Refund button does nothing on orders over 1000 EUR" beats "Race condition in the refund handler". You do not know the cause yet, and the title is what people search.*

| | |
|---|---|
| **Reported by** | |
| **Date** | YYYY-MM-DD |
| **Severity** | *Effect on the user. See the scale below.* |
| **Priority** | *When we will fix it. Set by the owner, not the reporter.* |
| **Affected version** | *Build, commit, or release.* |
| **Environment** | *OS, browser, device, region, account type.* |

---

## Reproduction details
*Ask for what developers actually use, weighed against what reporters can actually produce. Both have been measured, and the ranking is stable.*

*Steps to reproduce are the most useful thing on a bug report by a wide margin, and about half of reporters find them hard to write. That is a good trade: make the field required and help people fill it in. A stack trace is the next most useful and one of the easiest to supply, so ask for it every time — reports carrying one get fixed sooner.*

*A failing test case is genuinely valuable and the single hardest thing to ask for; most reporters cannot produce one. Invite it, never require it. Screenshots and a statement of expected behaviour are cheap to give and used less than you would think, so keep those fields optional and small.*

### Steps to reproduce

*Numbered, starting from a state the reader can reach. Include the data you used.*

*The most common defect in a bug report is a defect in this section. Wrong steps are the single biggest complaint developers have about reports, ahead of missing information and well ahead of everything else. It is worth spending the form's one required field here.*

> 1. Log in as an operator on staging.
> 2. Open order `ORD-88213` (settled, 1,200 EUR).
> 3. Click Refund, enter 1,200.00, submit.
> 4. Nothing happens. No error, no network request in the console.

**Reproduces:** *every time / 3 times in 10 / once, not since.* **Say so even when the answer is "once".** An intermittent bug reported as intermittent is useful. An intermittent bug reported as certain wastes an afternoon and gets closed as unreproducible.

### Stack trace or logs

*Paste the whole trace, not the line you think matters. Include a correlation or request ID if you have one.*

*If you have nothing, say "no trace produced" rather than leaving the section out. Absence is itself information: it tells the developer the failure is silent.*

### What you expected, and what happened

*Two sentences. They are separate on purpose, because a report that says only "it's broken" leaves the developer guessing which behaviour was intended.*

> **Expected:** the refund is submitted and the order shows Refunded.
> **Actual:** the button click is ignored. The order is unchanged after reload.

---

## Everything else

**Impact.** *Who is affected and how many. A workaround, if one exists. This is what sets priority, and it is the field a reporter is uniquely able to fill.*

**When it started.** *Last known good version, first known bad. This alone can replace hours of bisecting.*

**Screenshot or recording.** *For anything visual or interaction-dependent. Only 26% of developers ranked screenshots highly, so do not send one instead of steps to reproduce.*

**Related.** *Duplicates, linked reports, the test case that caught it.*

---

## Severity and priority are different fields

*Conflating them is the most common structural fault in a bug tracker. Severity describes the product. Priority describes the schedule. A reporter can judge the first and should not set the second.*

| Severity | Means |
|---|---|
| *S1* | *Data loss, corruption, security exposure, or a core flow unusable with no workaround* |
| *S2* | *Core flow broken with an awkward workaround, or a non-core flow unusable* |
| *S3* | *Wrong behaviour with a straightforward workaround* |
| *S4* | *Cosmetic, or wrong only in an unlikely path* |

*Define these once for your team and put them here. Left undefined, every reporter uses their own scale and the field becomes noise.*

---

## Notes on using this template

*Delete this section too.*

**Reporters already know what you need. They cannot produce it.** This is the finding that should change how you write the form: what reporters *think* developers want lines up almost exactly with what developers say they want, and what reporters actually attach lines up with neither. The mismatch is not ignorance and no amount of asking politely will fix it.

**So fix the form before you write the etiquette guide.** If steps to reproduce are the most valuable field, make the form refuse to submit without them. If stack traces get bugs fixed sooner, attach them from the crash handler so nobody has to find one. A prose plea to write better reports is the weakest intervention available to you.

**Absent beats wrong, and both lose to present.** Delay comes from missing information far more often than from incorrect information. A short report that is complete on the fields that matter beats a long one with half the fields guessed at.

**Stop policing duplicates.** Maintainers rank duplicates well below bad reproduction steps and missing information as a source of pain, and a second report often carries the step the first one missed. Link them and move on. Do not gate reporting behind a search that nobody can perform well, because the cost of that gate is the reports you never receive.

**Do not measure report quality by time to fix.** The two are unrelated. A good report on a hard bug stays open for months, and a useless report on a trivial one closes in an hour. Use time-to-close as a quality metric and you will teach your team to file easy bugs.

**On the standard's name.** ISO/IEC/IEEE 29119-3:2021 calls this a **test incident report**, and notes that "anomaly reports, bug reports, defect reports, error reports, issues, problem reports and trouble reports" are the same thing. Use whichever word your team already uses. The standard states its own nomenclature "is not mandatory".

**Where this lives:** in the issue tracker, as a template the tracker enforces. GitHub, GitLab and Jira all support required issue forms; use them, because a checklist in a wiki page is a checklist nobody opens. Keep this file in the repository under `.github/ISSUE_TEMPLATE/` so the form and the code version together.

---

## Related documents

- [`incident-postmortem.md`](incident-postmortem.md). What a bug becomes when it took production down. Different document, different audience
- [`test-case-specification.md`](test-case-specification.md). Where a reproducible bug should end up as a permanent check
- [`test-summary-report.md`](test-summary-report.md). Where open bugs are weighed against shipping
- [`contributing-guide.md`](contributing-guide.md). How an outside reporter finds this form
- [`test-strategy.md`](test-strategy.md). Why the bug was not caught, and whether that is worth changing
