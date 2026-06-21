# Test summary: {Release or test cycle}

*Also called: test completion report.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *Release, build, or date range.* |
| **Period** | YYYY-MM-DD to YYYY-MM-DD |
| **Written by** | |
| **Decision needed from** | *The person who acts on this.* |

*This report exists to support one decision: ship or do not ship. Everything that does not help someone make that decision belongs in the tracker, not here.*

---

## Recommendation

*First, in two sentences. The reader who stops after this section should still get the answer.*

> **Ship.** The two open S2 defects affect the bulk export path, which under 40 accounts use, and both have documented workarounds. Nothing outstanding touches payments or authentication.

*If the recommendation is conditional, name the condition and who confirms it is met. "Ship once the migration dry run passes on the production replica, confirmed by Priya."*

---

## What we now believe, and what we do not

*The section that makes this report worth writing. Testing buys confidence in specific claims. Say which claims, and say where you bought none.*

| Area | Confidence | Basis |
|---|---|---|
| *Payments* | *High* | *42 automated cases, 3 exploratory sessions, provider sandbox and one live 1 EUR transaction* |
| *Bulk export* | *Low* | *Not covered. Test data generator broke on day two and was not fixed* |
| *Concurrent editing* | *None* | *No environment supports it. Untested since 4.1* |

**The "None" rows are the ones people need.** *An area with no coverage and no row reads as an area that passed. Listing gaps is the only thing that prevents that.*

---

## What was tested

*Scope, in the terms the reader already uses: features, requirement IDs, platforms, environments. Link the [test cases](test-case-specification.md) rather than restating them.*

| | Planned | Executed | Passed | Failed | Blocked |
|---|---|---|---|---|---|
| *Regression suite* | *312* | *312* | *306* | *6* | *0* |
| *New feature cases* | *48* | *41* | *38* | *3* | *7* |
| *Exploratory sessions* | *12* | *9* | | | |

*Explain every gap between planned and executed. Seven blocked cases with no explanation is the single most common way a report loses its reader's trust.*

---

## Exploratory sessions

*Delete this section if you did not run any. If you did, this is where the work is recorded, and a session is the unit, not a test case.*

*The format comes from Jonathan Bach's session-based test management (STQE, November 2000), which defines a session as "an uninterrupted block of reviewable, chartered test effort". Sessions in his team ran "ninety minutes, give or take", and testers completed "about three sessions on a typical day".*

| Charter | Tester | Date | Duration | Design & exec | Bug investigation | Setup |
|---|---|---|---|---|---|---|
| *Explore refund limits looking for amounts that bypass validation* | *Sam* | *2026-03-14* | *90 min* | *60%* | *30%* | *10%* |

*Those last three columns are the **TBS metrics**: test design and execution, bug investigation and reporting, and session setup. Setup is "anything else testers do that makes the first two tasks possible, including tasks such as configuring equipment, locating materials, reading manuals, or writing a session sheet". They are estimated by the tester, in a debrief, not measured by a tool.*

**A session sheet carries eight things.** *Charter with the areas to be tested, tester names, start date and time, the task breakdown above, data files used, test notes, issues, and bugs.*

**Bugs and issues are separate on purpose.** *"Bugs are concerns about the quality of the product. Issues are questions or problems that relate to the test process or the project at large."* *An issue is "the staging database resets nightly and we lose our fixtures". It never reaches the bug tracker, and if you have nowhere to put it, it is simply lost.*

---

## Defects

*Open defects only, ordered by severity. Fixed ones belong in the [changelog](changelog.md) or the release notes, not here.*

| ID | Severity | Summary | Status | Workaround |
|---|---|---|---|---|
| *BUG-1042* | *S2* | *Bulk export truncates at 10,000 rows without warning* | *Open, fix in 4.3* | *Export by date range* |

*Include a line on defects found late. A cluster of S1s discovered in the final two days says something about the release that the counts above do not.*

---

## Residual risk

*What could still go wrong after shipping, what it would cost, and how you would know. Write this even when the recommendation is to ship, especially then.*

| Risk | If it happens | How we would detect it | Owner |
|---|---|---|---|
| *Concurrent editing corrupts a document* | *Unrecoverable customer data loss* | *Support ticket. No alerting exists* | | 

*A risk with no detection method is the one to name loudest. Feed anything durable into the [risk register](../project-management/risk-register.md); this table covers this release only.*

---

## Notes on using this template

*Delete this section too.*

**Do not lead with a pass rate.** "97% passed" invites the reader to skip the report. It also hides the shape of the failures, and six failures concentrated in checkout mean something different from six spread across the product.

**Coverage is not a quality target.** Inozemtseva and Holmes generated 31,000 test suites across five systems of up to 724,000 lines and measured fault detection with mutation testing. Their conclusion: coverage is "useful for identifying under-tested parts of a program" but "should not be used as a quality target because it is not a good indicator of test suite effectiveness". Report it as a map of gaps. Never report it as a grade.

**Session metrics are gameable, and the man who invented them said so first.** Jonathan Bach's warning is worth carrying: the process and metrics "could *easily* be distorted by a confused or biased test manager. A silver-tongued tester could bias the sheets and manipulate the debriefing in such a way as to fool the test manager about the work being done." Report TBS numbers alongside the debrief, not instead of it, and never use them to rank testers.

**Expect most of the time to be outside sessions.** Bach's own measured breakdown over a real project: 61% non-session work, 28% testing, 6% setup, 4% bug investigation, 1% opportunity testing. If your report implies testers spent their week in sessions, it is wrong, and the plan built on it will be wrong too.

**Write it as the cycle runs.** A report assembled the day before the go/no-go meeting is a reconstruction. The gaps section in particular gets written honestly only while the reasons are still fresh.

**On the standard's name.** ISO/IEC/IEEE 29119-3:2021 calls this a **test completion report** and lists "test summary report" as a synonym. The standard also states that its headings "may be modified (e.g. added to, combined or re-titled)" and that "the use of the nomenclature used in Clauses 5, 6, 7 and 8 is not mandatory". If you need to claim conformance, note that the standard distinguishes full conformance from tailored conformance, and that "where tailoring occurs, justification shall be provided".

**Where this lives:** the wiki, or the release ticket. It is written once, read around a decision, and then consulted as a record. It does not version with the code, and putting it in the repository buries it from the people who need it, who are often not developers.

---

## Related documents

- [`test-strategy.md`](test-strategy.md). The standing rules this cycle was run against
- [`test-case-specification.md`](test-case-specification.md). What "executed" refers to
- [`bug-report.md`](bug-report.md). Where the defects in this report came from
- [`release-notes.md`](release-notes.md). What the customer is told, as opposed to what the decision-maker is told
- [`../waterfall/master-test-plan.md`](../waterfall/master-test-plan.md). Where fixed-scope work states in advance what this report must answer
- [`../project-management/risk-register.md`](../project-management/risk-register.md). Where residual risk goes when it outlives the release
