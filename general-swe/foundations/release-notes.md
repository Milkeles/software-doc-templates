# {Product} {version or date}

*Italic text is guidance. Delete it as you fill each section in.*

*Audience: people who use the product and do not read your repository. Customers, support staff, sales, internal users of a platform.*

*This is not a [changelog](changelog.md). A changelog says what changed, for someone deciding whether to upgrade. Release notes say what you can now do and why you would care. Same release, different question, different document. Support staff cannot answer a customer question from a changelog, and customers cannot tell which changelog entries apply to them.*

---

## In this release

*Two or three sentences on the theme. What is different about using the product now.*

*If you cannot name a theme, list the single most useful thing and stop. A summary that lists everything is not a summary.*

> **Example.** Exports now run in the background, so large accounts no longer time out. Two-factor authentication is available for all plans.

---

## New

*Each item: what it is, who it helps, and what to do to use it. One short paragraph, in the reader's vocabulary rather than yours.*

*Lead with the benefit. "Export up to 500,000 rows without the request timing out" lands; "asynchronous export job queue" does not, and it is the same feature.*

### {Feature name, as the user would say it}

*What it does and why it helps. Then how to reach it: the menu, the setting, the endpoint. Screenshot or short clip where it is visual.*

*Link to the documentation for depth. Release notes announce; they do not teach.*

---

## Improved

*Changes to things that already existed. Include the measurement where you have one, because "faster" is not believed and "3x faster on accounts over 10,000 rows" is.*

- *...*

---

## Fixed

*Only the bugs users noticed or reported. Describe the symptom they saw.*

*Skip internal fixes. A user who never saw a bug does not need to learn it existed, and a long fix list reads as instability rather than diligence.*

- *Exported timestamps showed server time instead of your account timezone.*

---

## Action needed

*The section a reader will be annoyed to have missed. Put it high if it is not empty, and remove the heading entirely if it is.*

*Anything requiring the reader to do something: a breaking change, a setting that must be reviewed, a migration, a deprecation with a date, a minimum version.*

| What changed | Who it affects | What you must do | By when |
|---|---|---|---|
| | | | |

---

## Known issues

*Problems shipping with this release, each with a workaround and a fix timeline where you have one.*

*Publishing these costs less than the support load of not publishing them, and it is the difference between a user thinking the product is broken and thinking it is being handled.*

---

## Availability

*Who has this and when. Rollout schedule, regions, plans, whether an update is required.*

*A reader who does not see the feature after reading this will open a support ticket. Answer it here.*

---

## Notes on using this template

*Delete this section too.*

**One curation step per audience.** Commits become a changelog for engineers; the changelog becomes release notes for users. Each step drops what that audience cannot act on. Skipping a step means someone receives a document written for a different reader.

**No internal vocabulary.** Service names, ticket numbers, component names and internal codenames mean nothing outside the company and make the notes feel like a leak. Name things the way the user interface names them.

**Write "action needed" first.** It is the only section with a cost attached to being missed, and it is the one most often buried at the bottom.

**Do not ship an empty release note.** A release with nothing user-visible does not need announcing. Publishing one anyway teaches readers that these notes can be skipped.

**Where this lives:** the product site, documentation portal, in-app, or a release email. Not the repository. The audience is not there, the content needs images, and the people who should review it, support and product, do not open pull requests.

---

## Related documents

- [`changelog.md`](changelog.md). What changed, for the audience that reads the repository; this document answers a different question for people who do not
- [`deprecation-plan.md`](deprecation-plan.md). Where the deprecation named under "action needed" was decided, with its own date and replacement
- [`deployment-plan.md`](deployment-plan.md). The same release, written for the people executing it rather than customers reading about it
- [`test-summary-report.md`](test-summary-report.md). What the person deciding to ship was told; this document is for people the decision already reached
