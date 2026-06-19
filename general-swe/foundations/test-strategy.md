# Test strategy: {Team or system}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | *Which systems or teams this governs.* |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

*This document settles recurring arguments: what to test, where to test it, and what "enough" means. It is durable and system-wide. A test **plan**, which is project-scoped and carries a schedule, is a different document; see [`../waterfall/master-test-plan.md`](../waterfall/master-test-plan.md). What a cycle actually found goes in a [test summary report](test-summary-report.md).*

---

## What we are protecting

*What failure would actually cost you. Money, data, safety, reputation, a certification.*

*Everything below is a spending decision, and this section sets the budget. A team protecting card transactions and a team protecting an internal dashboard should reach different answers, and this is where that divergence is justified.*

> **Example.** Incorrect ledger entries are unrecoverable and auditable. A broken admin page costs an afternoon. Testing effort is weighted accordingly.

---

## Cost and confidence at each level

*The core of the strategy. For each level of test you use, state what it costs to write and run, and what it lets you believe.*

*Fill this in with your own measurements, not with received wisdom. The famous testing shapes are conclusions drawn from someone else's numbers; the numbers are what transfer, not the shape.*

| Level | What it covers | Runs in | Flake rate | What passing lets us believe |
|---|---|---|---|---|
| *Unit* | *One module, no I/O* | *< 2 min full suite* | | *The logic is right* |
| *Integration* | *Service with its real database* | *< 8 min* | | *The wiring and queries are right* |
| *Contract* | *Our API against consumer expectations* | | | *We have not broken a caller* |
| *End to end* | *Full stack through the UI* | *22 min* | | *The main journeys work* |
| *Manual / exploratory* | | | | |

**Our shape, and why.** *One paragraph. Where the weight sits and what made you put it there.*

*Fowler states the pyramid's premise as broad-stack tests being expensive, slow and brittle compared with focused ones, and immediately adds that while this is usually true, there are exceptions. Kent C. Dodds' trophy moves weight to integration tests and scopes that claim to front-end JavaScript, where the tooling makes those tests fast and stable. Both are arguments from cost. Make yours the same way, from the table above, and it will survive contact with your team.*

---

## What we test where

*The rule that tells someone writing a test today where it belongs. Ambiguity here is what produces duplicated coverage and slow suites.*

| Concern | Tested at | Not tested at | Why |
|---|---|---|---|
| *Business rules* | *Unit* | *End to end* | *Cheap to enumerate, expensive to drive through the UI* |
| *Database queries* | *Integration, real engine* | *Unit with a mock* | *Mocks pass while the query is wrong* |
| *Critical user journeys* | *End to end, a handful* | | *Only place the pieces meet* |

**Test doubles.** *Where you mock and where you refuse to. State it explicitly: this is the single most common source of disagreement in a codebase, and it decides whether your integration tests mean anything.*

---

## What we do not test

*Named exclusions, each with a reason. Third-party libraries, generated code, spikes, the framework itself.*

*Writing these down stops the coverage argument from restarting every quarter, and stops a reviewer blocking a change for missing a test nobody wants.*

---

## Entry and exit conditions

*What must be true for a change to merge, and for a release to ship. State them as automated gates wherever possible.*

**To merge**

- *All tests at levels X and Y pass*
- *New code covered by ... , measured as ...*
- *Static analysis and lint clean*

**To release**

- *...*

*If a condition is not enforced by CI, say who enforces it and how you know it happened. A gate that depends on remembering is not a gate.*

---

## Coverage

*What you measure, what target you hold, and what the number does not mean.*

*Be explicit that coverage measures execution, not verification: a test that runs code without asserting anything raises the number and catches nothing. Use it to find untested areas, not to certify tested ones.*

*If you set a threshold, set it on new code rather than on the whole repository. A global target on a legacy codebase produces tests written to satisfy the tool.*

---

## Flaky tests

*The rule, in advance, because in the moment nobody wants to make it.*

*Define the threshold at which a test is flaky, what happens then (quarantine, deadline, deletion), and who owns fixing it. Google's practice is to treat around 1% flakiness as the point where a suite starts losing its authority, because past that engineers begin re-running failures by reflex, and a suite that gets re-run is a suite that catches nothing.*

| | |
|---|---|
| **Flaky means** | *Fails on retry of the same commit more than once in N runs* |
| **Then** | *Quarantined within a day, owner assigned, fixed or deleted within two weeks* |
| **Who decides** | |

---

## Non-functional testing

*Only the kinds you actually do. Delete the rest; a strategy listing eight kinds of testing you never run is not believed.*

- **Performance.** *What you test, against what target, how often, in which environment.*
- **Security.** *Scanning, dependency checks, penetration testing cadence.*
- **Accessibility.** *Automated checks and manual audit cadence.*
- **Resilience.** *Failure injection, if any.*
- **Data migration.** *How you verify one before it runs on production data.*

---

## Environments and data

*Where each level of test runs, and where its data comes from. How production-like each environment is, and where it is not.*

*Say plainly how you handle personal data in test environments. This is where teams accidentally acquire a compliance problem.*

---

## Who does what

*Whether testing is owned by the engineer writing the code, a separate function, or both, and what each is accountable for.*

*State it even if the answer is "engineers test their own work". Unstated, it becomes "the last person to touch it".*

---

## Notes on using this template

*Delete this section too.*

**Write the arguments you are actually having.** A strategy that answers questions nobody asked is ignored. If your team's live disputes are about mocking and flakiness, those sections carry the document and the rest can be three lines each.

**Do not adopt a shape.** Pyramid, trophy, honeycomb and diamond are all conclusions from particular cost structures. Copying the picture without the costs gives you a ratio you cannot defend when someone asks why.

**Two rules worth stealing.** Google's "size" taxonomy (small tests take no network or filesystem, medium stay on one machine, large may not) is enforceable by tooling in a way that "unit versus integration" is not. And the Beyoncé Rule: if you liked it, you should have put a test on it. Anything not covered by a test may be broken by anyone, and neither side gets to be surprised.

**Where this lives:** in the repository it governs, beside the CI configuration it describes. When the pipeline changes, this document is wrong, and only co-location makes that visible in review.

---

## Related documents

- [`../waterfall/master-test-plan.md`](../waterfall/master-test-plan.md). The project-scoped plan with a schedule; this document is the standing policy it should reference instead of restating
- [`test-summary-report.md`](test-summary-report.md). What one cycle run against these rules actually found
- [`test-case-specification.md`](test-case-specification.md). What gets written down as a check, decided by which level this document says a concern belongs at
- [`../../ai-assisted-development/evaluation/evaluation-plan.md`](../../ai-assisted-development/evaluation/evaluation-plan.md). The counterpart for behaviour that depends on a model's judgment rather than deterministic logic
