# Contributing

Contributions are welcome. The bar is high on purpose: a resource about writing well has to be written well.

---

## Before you write anything

**Raise an issue first.** Explain the problem or the addition and the reasoning behind it — what teams do today, why it falls short, and what the new or changed document would fix. This saves you writing a template that turns out to duplicate one already here, or one that belongs in a different area.

**Check whether the document already exists elsewhere.** [`INDEX.md`](INDEX.md) lists every template in the repository. Several documents appear in more than one area on purpose, because a game studio's deployment plan and a backend team's are different documents with the same name. Say in the issue which one you mean.

---

## The research discipline

Templates here are researched, not remembered. This is the rule that matters most.

1. **Research.** Find what experienced teams actually use. Which sections are conventional? What is widely accepted, and what is one person's opinion? What does the document exist to accomplish?
2. **Verify.** Cross-check sources against each other. Drop anything a source can't support. Where credible sources disagree, say so in the template or README instead of picking a side quietly.
3. **Write** only once you're certain. "Probably correct" is not the bar.

Cite your sources in the pull request description. A single unsourced claim is a reason to keep researching, not to ship.

---

## What a template must contain

Every section and subsection carries a short description of two things: **what content belongs in it**, and **how to write it** — concrete instructions on what to do and what to avoid.

Keep the descriptions short. A reader should understand a section's purpose in seconds. Do not write an essay inside a template.

Show, don't just tell. A one-line example beats a paragraph of description wherever it fits.

---

## Headings

This is the rule these templates most often got wrong, so it is spelled out.

A template is not an article about how to write the document. It is the document, empty. The headings therefore belong to the finished document, not to the advice for filling it in.

**Apply the survival test.** Imagine a team copies the template, fills every section in, deletes the guidance, and ships the result to their colleagues. Does the heading still make sense as a section of that finished document?

| Fails | Passes |
|---|---|
| `## Deploy it` | `## Deployment and rollback` |
| `## First, decide whether you need this document` | `## Scope` |
| `## Why the brief is worth getting right` | *(cut — it is about the template, not the project)* |
| `## How to write each requirement` | *(cut — move it under the requirements heading as guidance)* |

Three common ways to fail it:

- **The heading instructs the author.** "Put it where the host will find it" is advice. Nobody ships a document with that section in it.
- **The heading argues a point.** "The PRINCE2 alternative, and why it is often better" is a paragraph wearing a heading's clothes.
- **The heading refers to the document itself.** "Deploy *it*", "Keeping *it* short". The pronoun gives it away: the heading is talking about the template rather than naming a section.

**Put the guidance under the heading, in italics.** Everything the failing headings were trying to say still belongs in the template — one line below the heading, where the reader deletes it after filling the section in.

**Keep headings parallel within a level.** Microsoft's style guide asks for parallel sentence structure across headings at the same level, and it is the rule these templates broke most often — noun phrases and imperatives alternating down one page. Pick one shape per level and hold it. Across levels you may mix: Google's developer documentation style guide recommends a bare infinitive for task sections ("Create an instance") and a noun phrase for conceptual ones, and explicitly permits both in one document.

**Grammatical form is not the test; survival is.** Some correct headings look wrong to a linter and must not be changed:

- `threat-model.md` uses "What are we working on", "What can go wrong", "What are we going to do about it" and "Did we do a good enough job" — Shostack's Four Question Frame, verbatim, as published in the Threat Modeling Manifesto.
- `incident-postmortem.md` uses "What went well", "What went wrong" and "Where we got lucky" — verbatim from the Google SRE Book's example postmortem.
- `how-to-guide.md` and `runbook.md` use "Before you start" — verbatim from The Good Docs Project's how-to template.

These pass because a real threat model, postmortem and how-to genuinely carry those headings. When a discipline has settled on a heading, use its wording and say in the pull request where it comes from.

**Meta sections stay outside the document's own sequence.** "Notes on using this template" and "Related documents" are addressed to the person filling the template in, not to the document's readers. Never number them into the document's section sequence — a numbered "7. Why the brief is worth getting right" gets shipped by accident. Keep them unnumbered, at the end, and tell the reader to delete them.

**Where no standard heading set exists, propose one and say so.** Many document types have no agreed structure. That is fine. Give the template a sensible set of headings anyway and state plainly, near the top, that these are a proposal rather than a convention, so a team knows it can rename them without losing anything.

---

## What a group README must contain

If you add a new methodology folder, its README answers three questions:

- **When to use each document.** Which templates in the group matter, and which are optional or situational. Naming the ones a team can skip is as useful as naming the ones it needs.
- **Why they help.** The reasoning behind each document — how it helps people think, coordinate, or remember. Not "convention expects it."
- **Where each document should live.** Wiki, docs-as-code in the repository, the issue tracker, or somewhere else. Explain the reasoning. Documents that go wrong when the code changes belong next to the code; documents whose value is in the discussion belong where discussion happens.

The throughline: documentation supports development. It is not busywork. If a document doesn't help a team build better software, say so and say when to skip it.

---

## Writing principles

Every committed word follows these.

- Write for understanding, not to impress.
- Put the important information first.
- Use plain language. No jargon unless the audience already knows it.
- Short sentences. Short paragraphs.
- Active voice.
- Be specific. Concrete details, examples, numbers.
- Say what the reader gains, not just what a thing is.
- Address objections directly instead of hoping nobody raises them.
- Cut every word that doesn't change the meaning.

Then re-read what you wrote against this list and cut again. Editing is where most of the quality comes from.

---

## Pull requests

**One focused change per pull request.** A new template is one pull request; rewriting a README is another. Small changes get reviewed; large ones sit.

**Explain your commits.** Say *why* the change is being made, not just what changed. "Add threat model template" tells a reader nothing they can't see in the diff. "Add threat model template so teams have a security document short enough to actually finish" tells them the reasoning.

**Update [`INDEX.md`](INDEX.md)** when you add or rename a template, and the group README when you add one to an existing group.

**File naming.** Lowercase, hyphenated, matching the document's name: `architecture-decision-record.md`, not `ADR.md`.

---

## Licence

Contributions are accepted under the [MIT Licence](LICENSE), the same terms the rest of the repository uses.
