# Software Documentation Templates

Documentation templates for software teams, organised by what you build and how you work.

> **Example.** A backend team adopting Kanban starts in [`general-swe/kanban/`](general-swe/kanban/), reads the group README to see which documents earn their place, and copies the ones that do into their own repository.

| | |
|---|---|
| **What it is** | Templates and READMEs, not a framework or a tool. Copy what you need. |
| **Start here** | [`general-swe/foundations/`](general-swe/foundations/) — the documents most teams need before anything else |
| **Who it's for** | Engineers writing a design doc or runbook, tech leads setting up documentation practice, anyone new to a methodology's paperwork |
| **Status** | Growing. See Coverage below for what is finished. |

Every template tells you what goes in each section and how to write it. Every group of templates comes with a README that answers three questions: **when** to use each document, **why** it helps, and **where** it should live.

---

## Find your templates

1. **Pick your area.** Backend service, web app, game, data pipeline, platform. Areas differ in what they must document: a game studio needs an art bible, a payments team needs a threat model.
2. **Pick your methodology.** Scrum, Kanban, plan-driven, Lean, Shape Up, or none of them. If none, start in the area's `foundations/` group, which is methodology-agnostic.
3. **Read the group README first.** It says which documents in that group earn their place and which to skip. Skipping is a valid answer and the READMEs say so.
4. **Copy the template into your own repository or wiki.** Delete the guidance text as you fill each section.

You do not need to adopt a methodology wholesale to use its templates. Take the retrospective format without taking sprints.

---

## How this is organised

```
<area>/                      what you build
  <methodology>/             how you work
    README.md                when, why, and where each document lives
    <document>.md             the template itself
```

| Area | What it covers |
|---|---|
| [`general-swe/`](general-swe/) | Documents any software team needs, whatever the domain: architecture decisions, design docs, runbooks, postmortems, review standards. |
| [`web-development/`](web-development/) | Browser and API-facing work: frontend architecture, API contracts, accessibility, performance budgets, rollout plans. |
| [`game-development/`](game-development/) | Games and interactive media: design documents, art and audio direction, level design, playtesting, milestone delivery, certification. |
| [`data-engineering/`](data-engineering/) | Pipelines, warehouses, and models: data contracts, metric definitions, dataset and model documentation, quality specifications. |
| [`platform-engineering/`](platform-engineering/) | Infrastructure and operations: service level objectives, on-call practice, disaster recovery, capacity planning, change management. |
| [`ai-assisted-development/`](ai-assisted-development/) | Working with coding agents and language models: agent instruction files, task plans, task specifications, evaluation plans. |

Within each area, `foundations/` holds documents that do not depend on a methodology. The other folders are named for the methodology they serve.

---

## Where documentation should live

Every group README answers this per document, because getting it wrong is the most common reason documentation rots. Two questions decide it:

**Does the document become wrong when the code changes?** If yes, it belongs in the repository next to the code, so one commit changes both and code review catches the drift. Architecture decision records and API contracts fail this way.

**Is the value in the discussion or the final text?** If it's in the discussion, the document needs threaded comments and access for people who don't use pull requests. Design docs under review belong in a wiki. Extract the durable outcome into the repository afterward.

Some documents belong in neither. Sprint backlogs belong in the tracker that already holds them. Kanban policies belong on the board, read at the moment a decision is made. Regulated records requiring signatures belong in a controlled document system.

---

## What this is not

- **Not a methodology guide.** The READMEs explain enough of Scrum or Kanban to make the documents make sense, then point at the primary sources.
- **Not a standard.** Nothing here is normative. Where credible sources disagree, the READMEs say so instead of picking a side quietly.
- **Not a checklist to complete.** Documents you don't need cost time to write and time to distrust. Every group README names the documents you can safely skip.

Documentation supports development. When a document stops helping the team build software, delete it.

---

## Contributing

Contributions are welcome. The bar is high on purpose: a resource about writing well has to be written well.

**Raise an issue first.** Explain the problem or the addition and the reasoning behind it — what teams do today, why it falls short, and what the new or changed document would fix.

**Follow the research discipline.** Templates here are researched, not remembered. Find what experienced teams actually use, pull from multiple independent sources, cross-check them against each other, and drop anything a source can't support. A single unsourced claim is a reason to keep researching, not to ship. Cite sources in the pull request description.

**Follow the writing principles.** Write for understanding, not to impress. Put the important information first. Use plain language. Short sentences, short paragraphs, active voice. Be specific. Say what the reader gains, not just what a thing is. Cut every word that doesn't change the meaning.

**Keep pull requests focused.** One change per pull request. A new template is one pull request; rewriting a README is another.

**Explain your commits.** Say *why* the change is being made, not just what changed. "Add threat model template" tells a reader nothing they can't see in the diff. "Add threat model template so teams have a security document short enough to actually finish" tells them the reasoning.

---

## Coverage

This repository grows a group at a time. A folder appears once its README and templates are researched and written, not before. Check the folder listing above for current coverage.

---

## Related documents

- [`general-swe/README.md`](general-swe/README.md) — documents any team needs regardless of domain; start here if you're unsure where else to look
- [`web-development/README.md`](web-development/README.md) — browser and API-facing work
- [`game-development/README.md`](game-development/README.md) — games and interactive media
- [`data-engineering/README.md`](data-engineering/README.md) — pipelines, warehouses, and models
- [`platform-engineering/README.md`](platform-engineering/README.md) — infrastructure and operations
- [`ai-assisted-development/README.md`](ai-assisted-development/README.md) — working with coding agents and language models
