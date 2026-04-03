# Bug: {What a user would say went wrong}

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

## The three fields that decide whether this gets fixed

*Not an opinion. Bettenburg and colleagues surveyed 466 people across the Apache, Eclipse and Mozilla projects for FSE 2008: 156 developers and 310 reporters, then filtered to 130 and 215 consistent responses. They asked developers which contents helped most, and reporters which were hardest to supply.*

| Content | Developers who said it helps | Reporters who said it is hard to give |
|---|---|---|
| Steps to reproduce | **83%** | 51% |
| Stack traces | **57%** | 24% |
| Test cases | **51%** | **75%** |
| Observed behaviour | 33% | |
| Screenshots | 26% | |
| Expected behaviour | 22% | |

*The same study mined 150,000 reports and found that reports containing stack traces get fixed sooner, that reports which are easier to read have lower lifetimes, and that including code samples increases the chance of a fix.*

### Steps to reproduce

*Numbered, starting from a state the reader can reach. Include the data you used.*

*The most common defect in a bug report is a defect in this section: 79% of developers named errors in the steps to reproduce as a problem they hit, ahead of everything else. Second was incomplete information, at 74%.*

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

**The gap is tooling, not ignorance.** The FSE 2008 study measured three correlations. What developers use against what reporters actually provide: 0.321. What developers consider important against what reporters provide: **-0.035**, which the authors call "a huge gap". What developers consider important against what reporters *expect* to be important: **0.839**. Their conclusion is worth quoting: "most reporters know which information developers need. In other words, ignorance of reporters is *not* a reason for the aforementioned information mismatch", and "to a large extent, lacking tool support causes this mismatch."

**So fix the form before you write the etiquette guide.** If steps to reproduce are the single most valuable field, make the form refuse to submit without them. If stack traces get bugs fixed sooner, attach them automatically from the crash handler. A prose plea to write better reports is the weakest available intervention.

**Absent beats wrong, and both lose to present.** A developer in the same study: "the biggest causes of delay are not wrong information, but absent information." Half-filled fields are worse than a short report that is complete on the fields that matter.

**Stop policing duplicates.** Only 10% of developers named duplicates as a problem, far below errors in steps to reproduce and incomplete information. The authors were blunt: "developers do not suffer too much from bug duplicates, although earlier research considered this to be a serious problem", and "duplicates are not really problems. They often add useful information." A second report often carries the reproduction step the first one missed. Link them; do not gate reporting on a search nobody can do well.

**Do not measure report quality by time to fix.** The same study found report quality and report lifetime are effectively independent, with correlations between 0.002 and 0.068. A good report on a hard bug stays open for months. Using time-to-close as a quality metric will teach your team to file trivial bugs.

**Scope of the evidence.** Three large open-source projects, experienced participants, voluntary response. The authors state they "do not contend that they are transferable to closed-software projects". The direction of the findings is sound; treat the percentages as indicative.

**On the standard's name.** ISO/IEC/IEEE 29119-3:2021 calls this a **test incident report**, and notes that "anomaly reports, bug reports, defect reports, error reports, issues, problem reports and trouble reports" are the same thing. Use whichever word your team already uses. The standard states its own nomenclature "is not mandatory".

**Where this lives:** in the issue tracker, as a template the tracker enforces. GitHub, GitLab and Jira all support required issue forms; use them, because a checklist in a wiki page is a checklist nobody opens. Keep this file in the repository under `.github/ISSUE_TEMPLATE/` so the form and the code version together.

---

## Related documents

- [`incident-postmortem.md`](incident-postmortem.md). What a bug becomes when it took production down. Different document, different audience
- [`test-case-specification.md`](test-case-specification.md). Where a reproducible bug should end up as a permanent check
- [`test-summary-report.md`](test-summary-report.md). Where open bugs are weighed against shipping
- [`contributing-guide.md`](contributing-guide.md). How an outside reporter finds this form
- [`test-strategy.md`](test-strategy.md). Why the bug was not caught, and whether that is worth changing
