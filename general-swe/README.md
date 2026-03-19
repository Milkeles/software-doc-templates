# General Software Engineering

Documents any software team needs, whatever it builds.

Start here. The templates in this area apply to a payments backend, a mobile app, a game engine, and a data pipeline alike. The other areas add domain-specific documents on top; they do not replace these.

---

## Groups that apply whatever your methodology

| Group | Use it when |
|---|---|
| [`foundations/`](foundations/) | Always. Architecture decisions, design docs, runbooks, postmortems, review standards, onboarding. |
| [`requirements/`](requirements/) | Before you build. Why the project exists, what to build, and what "fast enough" means. |
| [`user-documentation/`](user-documentation/) | Someone outside the team uses what you built. Tutorials, how-to guides, reference, installation, troubleshooting. |
| [`security-and-compliance/`](security-and-compliance/) | You hold anyone's personal data. Several of these are legal obligations, not conventions. |

The first three answer different questions and overlap almost nowhere. Requirements comes before the work, foundations runs alongside it, and user documentation ships with it.

Security and compliance is the exception to the rule at the bottom of this page. Elsewhere you skip what does not earn its place; there, check first whether the thing you want to skip is required by an article of the GDPR.

---

## Groups that depend on how you plan work

| Group | Use it when |
|---|---|
| [`agile-scrum/`](agile-scrum/) | You work in sprints with a Product Owner and a Scrum Master. |
| [`kanban/`](kanban/) | You pull work continuously against WIP limits instead of committing to iterations. |
| [`waterfall/`](waterfall/) | Requirements are fixed by contract or regulation, or a certifying body needs an audit trail. |
| [`lean/`](lean/) | You are attacking a process problem or validating a product bet rather than delivering known scope. |
| [`shape-up/`](shape-up/) | You fix time and vary scope in fixed cycles, and shape work before betting on it. |

Nothing stops you using more than one. A Scrum team still writes architecture decision records from `foundations/`, and still runs an A3 from `lean/` when a recurring problem needs root-cause work.

Pick at most one from this second table. Pick freely from the first.

---

## Pick a group by how work arrives, not by what you call yourselves

Most teams pick a methodology label first and inherit its documents second. Do it the other way round.

- **Work arrives in batches you commit to, and stakeholders expect a regular review.** Scrum documents fit.
- **Work arrives continuously and unpredictably, and cannot be batched into iterations.** Support, platform, and operations teams live here. Kanban documents fit.
- **Scope is fixed before you start and someone will audit that you built what was specified.** Plan-driven documents fit, and they are not optional.
- **You do not know whether the thing is worth building.** Lean experiment documents fit.
- **You know roughly what to build, but scope will have to give way to hit a date.** Shape Up documents fit.

If none of these describes you, stay in `foundations/` and add nothing else. Documents you adopt to look like a methodology are pure cost.

---

## The one rule that survives every methodology

A document earns its place by changing a decision someone makes.

An architecture decision record changes what the next engineer builds on. A runbook changes what an on-call engineer does at 3am. A postmortem changes what the team fixes next week. A status report that nobody acts on changes nothing, and no methodology makes it worth writing.

Before you write, name the decision. If you cannot, skip the document.
