# Definition of Done

*Also called: DoD.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | *The product. One Definition of Done per product, shared by every team working on it.* |
| **Owner** | *The Scrum Team. If your organisation has a standard, that standard is your minimum and you may add to it.* |
| **Last changed** | YYYY-MM-DD |

*This is what "done" means. An item that does not meet every criterion below is not part of the Increment: it cannot be released, cannot be shown at the Sprint Review, and returns to the Product Backlog.*

*Say that out loud once. It is the entire mechanism, and a Definition of Done that is not enforced that way is a wish list.*

---

## The criteria

*Each row is a binary check on a completed Product Backlog item. State how it is verified and by what.*

*The verification column is the most important thing on this page. The largest survey of Definition of Done practice found that over 70 percent of projects had criteria that were hard or slow to verify, and over 60 percent had criteria that were impossible to verify at all. An item you cannot check is not a criterion, it is a sentiment, and it will quietly become optional.*

| Criterion | Verified by | Automated |
|---|---|---|
| *Code reviewed and approved by someone who did not write it* | *Branch protection* | *Yes* |
| *Unit and integration tests written and passing* | *CI pipeline* | *Yes* |
| *No new critical or high static analysis findings* | *CI pipeline* | *Yes* |
| *Deployed to staging and exercised against real data volumes* | *Pipeline stage* | *Yes* |
| *User-facing text reviewed by ...* | *Named reviewer on the pull request* | *No* |
| *Changelog entry added* | *CI check for a changed CHANGELOG.md* | *Yes* |
| *Monitoring and alerting in place for the new path* | *Reviewer checks the dashboard link in the pull request* | *No* |

**Rewrite anything that fails this test:** could two people disagree about whether it is met, and would you have to argue rather than look? If so, either make it checkable or remove it.

*Examples of criteria that fail: "code is clean", "properly tested", "documentation updated", "performance is acceptable", "the Product Owner is happy". Each can be rescued by naming the check. "Documentation updated" becomes "any change to a public endpoint updates the OpenAPI file, verified by a CI diff".*

---

## Not yet in our Definition of Done

*Criteria you want but cannot yet meet, with what has to happen first and who owns it.*

*Keep this section. It converts an unrealistic Definition of Done into a roadmap, and it stops the two failures the research identifies: writing criteria the team cannot actually satisfy, and quietly dropping ones that became inconvenient.*

| Criterion we want | Blocked by | Owner | Revisit |
|---|---|---|---|
| *Deployed to production behind a flag* | *No feature flag system* | | *Q3* |
| *Load tested at 2x peak* | *No load environment* | | |

---

## What this is not

*Keep this section too. Both confusions below are common and both cause real damage.*

**Not acceptance criteria.** Acceptance criteria are per item and answer "does this do the right thing". The Definition of Done applies to every item and answers "is this releasable". An item can meet all its acceptance criteria and still not be done.

**Not a stage gate.** These criteria are met continuously during the Sprint, not checked at the end by someone else. If the Definition of Done is being verified in a meeting after the work stops, you have a handoff, not a commitment.

---

## Amendment process
*When and how this changes, decided in advance so it does not change under pressure.*

*The Sprint Retrospective is the natural place. Strengthening it is normal and expected as capability grows. Weakening it to make a Sprint succeed is the point at which the whole mechanism stops working, so require it to be a deliberate, recorded decision rather than something that happens on a Thursday afternoon.*

- *Reviewed in the retrospective every N Sprints*
- *Any change agreed by the whole Scrum Team*
- *Where multiple teams share this product, changes agreed across all of them*
- *Changes recorded here with a date and a reason*

---

## Notes on using this template

*Delete this section too.*

**Start with what you already do, then add one criterion at a time.** A Definition of Done written aspirationally is unmet from the first Sprint, and a standard that is routinely unmet trains everyone to treat it as decorative.

**Automate as much as you can, and mark what you did not.** Every manual check depends on someone remembering under time pressure, which is exactly when checks get skipped. The automated column tells you honestly how much of this is real.

**Where this lives:** in the repository. Most of the criteria are enforced by CI, and when the pipeline changes, this document is wrong. Co-location is what makes that visible in review.

---

## Related documents

- [`product-backlog-item.md`](product-backlog-item.md). Acceptance criteria answer whether one item is right; this document answers whether any item is releasable
- [`sprint-review-notes.md`](sprint-review-notes.md). An item that fails this cannot be shown at the review, which shapes what those notes can contain
- [`../foundations/test-strategy.md`](../foundations/test-strategy.md). Where the checks behind each verifiable criterion, especially the automated ones, get designed
- [`../foundations/changelog.md`](../foundations/changelog.md). One of the example criteria requires a changelog entry, so the two are enforced together
