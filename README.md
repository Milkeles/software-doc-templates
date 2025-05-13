# Software Documentation Templates

Documentation templates for software teams, organised by what you build and how you work.

Every template tells you what goes in each section and how to write it. Every group of templates comes with a README that answers three questions: **when** to use each document, **why** it helps, and **where** it should live.

---

## The problem this solves

Most teams write documentation badly for one of two reasons.

They copy a template they found online, fill in every heading because the heading is there, and produce a document nobody reads. Or they write nothing, and six months later nobody remembers why the payment service retries three times instead of five.

Both failures come from the same gap: no one said what the document is *for*. A template with empty headings does not tell you that. A blank page does not either.

So each template here carries instructions inside it. Each section says what belongs in it, what to avoid, and often shows a one-line example. Delete the instructions when you fill it in.

---

## Who this is for

- **Engineers** who need to write a design doc, a runbook, or a postmortem and want a starting point that is not a guess.
- **Tech leads and engineering managers** setting up documentation practice for a team.
- **Product and delivery people** who need to know which documents a methodology actually requires and which are optional.
- **Anyone joining a team** that uses Scrum, Kanban, or a stage-gated process and wants to understand why the paperwork exists.

You do not need to adopt a methodology wholesale to use its templates. Take the retrospective format without taking sprints.

---

## How to use this repository

1. **Pick your area.** Backend service, web app, game, data pipeline, platform. Areas differ in what they must document. A game studio needs an art bible; a payments team needs a threat model.
2. **Pick your methodology.** Scrum, Kanban, plan-driven, Lean, Shape Up, or none of them. If none, start in the area's `foundations/` group, which is methodology-agnostic.
3. **Read the group README first.** It tells you which documents in that group earn their place and which to skip. Skipping is a valid answer and the READMEs say so.
4. **Copy the template into your own repository or wiki.** Delete the guidance text as you fill each section.

Start with `general-swe/foundations/`. Those documents apply regardless of area or methodology, and most teams need them before they need anything else.

---

## How this is organised

```
<area>/                      what you build
  <methodology>/             how you work
    README.md                when, why, and where each document lives
    <document>.md            the template
```

| Area | What it covers |
|---|---|
| `general-swe/` | Documents any software team needs, whatever the domain. Architecture decisions, design docs, runbooks, postmortems, review standards. |
| `web-development/` | Browser and API-facing work. Frontend architecture, API contracts, accessibility, performance budgets, rollout plans. |
| `game-development/` | Games and interactive media. Design documents, art and audio direction, level design, playtesting, milestone delivery, certification. |
| `data-engineering/` | Pipelines, warehouses, and models. Data contracts, metric definitions, dataset and model documentation, quality specifications. |
| `platform-engineering/` | Infrastructure and operations. Service level objectives, on-call practice, disaster recovery, capacity planning, change management. |
| `ai-assisted-development/` | Working with coding agents and language models. Agent instruction files, task plans, prompt specifications, evaluation plans. |

Within each area, `foundations/` holds documents that do not depend on a methodology. The other folders are named for the methodology they serve.

---

## Where documentation should live

Every group README answers this per document, because getting it wrong is the most common reason documentation rots.

The decision comes down to two questions:

**Does this document become wrong when the code changes?** If yes, it belongs in the repository next to the code, so one commit changes both and code review catches the drift. Architecture decision records, definitions of done that encode CI gates, and API contracts all fail this way.

**Is the value in the discussion or in the final text?** If the value is in the discussion, the document needs threaded comments, notifications, and access for people who do not use pull requests. Design docs under review and product goals belong in a wiki. Extract the durable outcome into the repository afterwards.

Some documents belong in neither. Sprint backlogs belong in the tracker that already holds them. Kanban policies belong on the board, where they are read at the moment a decision is made. Regulated records requiring signatures and audit trails belong in a controlled document system.

---

## What this is not

- **Not a methodology guide.** The READMEs explain enough of Scrum or Kanban to make the documents make sense, then point at the primary sources.
- **Not a standard.** Nothing here is normative. Where credible sources disagree, the READMEs say so and explain the trade-off instead of picking a side quietly.
- **Not a checklist to complete.** Documents you do not need are worse than no documents, because they cost time to write and time to distrust. Every group README names the documents you can safely skip.

Documentation supports development. When a document stops helping the team build software, delete it.

---

## Contributing

Contributions are welcome. The bar is high on purpose, because a resource about writing well has to be written well.

### Raise an issue before opening a pull request

Open an issue that explains the problem or the addition and the reasoning behind it. Say what teams do today, why it falls short, and what the new or changed document would fix. This saves you writing a template that gets rejected on scope.

### Follow the research discipline

Templates here are researched, not remembered.

1. **Research.** Find what experienced teams actually use. Pull from multiple independent sources.
2. **Verify.** Cross-check the sources against each other. Drop anything a source cannot support. Where sources disagree, say so in the README rather than picking one silently.
3. **Write.** Only once you are certain of the content.

A single unsourced claim is a reason to keep researching. Cite the sources in the pull request description.

### Follow the writing principles

Every committed word follows these:

- Write for understanding, not to impress.
- Put the important information first.
- Use plain language. No jargon unless the reader already has it.
- Short sentences. Short paragraphs.
- Active voice.
- Be specific. Concrete examples, numbers, evidence.
- Say what the reader gains, not just what a thing is.
- Answer the obvious objection instead of hoping nobody raises it.
- Cut every word that does not change the meaning.

If a sentence survives deletion without the paragraph losing anything, delete it.

### Keep pull requests focused

One change per pull request. A new template is one pull request. Rewriting a README is another. Reviewers cannot give useful feedback on a diff that does four things.

### Explain your commits

Every commit message says *why* the change is being made, not just what changed. "Add threat model template" tells a reader nothing they cannot see in the diff. "Add threat model template so teams have a security document short enough to actually finish" tells them the reasoning.

---

## Coverage

This repository grows a group at a time. A folder appears once its README and templates are researched and written, not before.

Check the folder listing for current coverage. Empty areas listed in the table above are planned, not finished.
