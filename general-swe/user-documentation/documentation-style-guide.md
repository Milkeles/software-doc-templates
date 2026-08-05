# Documentation Style Guide

> The decisions that would otherwise be re-argued in every review.
>
> **Also called:** Style Guide, Writing Style Guide, or Content Style Guide.
>
> **Do not write this from scratch.** Every serious style guide layers on top of an existing one. Google's developer documentation style guide defers to Merriam-Webster for spelling, *The Chicago Manual of Style* for nontechnical style, and the Microsoft Writing Style Guide for technical style. Red Hat's supplementary guide states that the IBM Style Guide is "the primary source of style guidance" and supplements it. GitLab layers on Microsoft and Google. Your guide should be the thin layer of things your base guide does not settle.
>
> **What that thin layer is for.** Terminology specific to your product, the decisions where the major guides genuinely disagree, and structural rules for your document types. Twenty pages restating Chicago is twenty pages nobody reads.
>
> **Where it lives.** Docs-as-code, so it can be linked from review comments and, where possible, enforced by a linter.
>
> **Delete this block before publishing.**

---

## 1. Base guide

Name it in the first line, with the edition.

> Spelling: Merriam-Webster.
> General style: *The Chicago Manual of Style*, 18th edition.
> Technical style: Microsoft Writing Style Guide.
> Anything below overrides them.

**Check the edition you are citing.** Chicago's 18th edition was published on 19 September 2024 and reached CMOS Online on 15 August 2024. As of July 2026 Google's public guide still names the 17th, which is a live example of how quietly a base-guide reference goes stale.

**Choose a base that fits the work.** The Associated Press Stylebook is a journalism guide; Chicago is a book-publishing guide. Neither was written for software. Google builds on Chicago; none of the major technical guides build on AP. For software documentation, Chicago plus Microsoft is the realistic default.

Note that Google's guide is licensed CC BY 4.0, so you may quote and adapt it with attribution. Microsoft's, Apple's and IBM's are not openly licensed, and the IBM Style Guide is a paid book even though Red Hat's supplement to it is free.

---

## 2. Decisions your base guide leaves open
These are the points where the major public guides actually diverge. Pick one and record it, because in the absence of a decision every reviewer applies their own.

| Decision | The disagreement |
|---|---|
| **Contractions** | Microsoft requires them: "Use contractions like *it's*, *you'll*, *you're*, *we're*, and *let's.*" Google permits without mandating. The split reflects audience, consumer-facing versus developer-facing |
| **Register** | Microsoft: "Write like you speak… a friendly conversation." Google is neutral and professional. These produce visibly different documentation |
| **Second person** | Google: "In general, address the reader… using the second person instead of the first person: use *you* or *your* instead of *we*, *our*, or *us*." Near-universal, but say who *you* is. Google again: "It's important to identify who the *you* is that you're addressing (a developer? a sysadmin? someone else?)" |
| **Passive voice** | Google prefers active but permits passive "to emphasize an object over an action", "to de-emphasize a subject or actor", or "if your readers don't need to know who's responsible". Not the absolute ban most summaries report |
| **Future tense** | Google allows *will* for genuinely future actions. GitLab restricts it for a different reason entirely: "Do not promise to deliver features in a future release… We cannot guarantee future feature work, and promises like these can raise legal issues" |
| **Oxford comma** | Microsoft requires it. Chicago requires it. Little real disagreement, but write it down |

**Sentence-case headings are the one point of genuine convergence.** Microsoft, Google, Red Hat and GitLab all use them. Microsoft states it plainly: "Default to sentence-style capitalization… Don't use title-style capitalization (Like This)."

---

## 3. Terminology

The highest-value section, and the only one that cannot be borrowed.

A table of the terms your product uses, the one approved spelling of each, and the words not to use for it.

| Use | Not | Note |
|---|---|---|
| workspace | project, org, tenant | The UI says workspace |
| sign in (verb), sign-in (noun) | login, log in, logon | Matches the button text |
| deprecated | obsolete, legacy | Has a defined meaning. See the deprecation plan |

**Two names for one thing costs more than any other style error.** It makes search fail, it makes readers wonder whether they are the same thing, and it compounds every release.

The [glossary](../foundations/glossary.md) defines terms for readers. This table decides which word you use. Keep them consistent and do not duplicate the definitions here.

---

## 4. Structure rules per document type

Where your guide earns its length. Fix the field order for each type once, and reference pages become scannable.

- **Reference:** field order, fixed. See [`reference-page.md`](reference-page.md).
- **How-to:** titles begin "How to". One goal per document.
- **Tutorial:** numbered steps, expected output after each.
- **Troubleshooting:** symptom, confirm, cause, fix, next.

---

## 5. Formatting

The small decisions, settled once.

- **Code:** inline `code` for identifiers, values, and literal input. Blocks for anything multi-line. Name the language on every block.
- **UI elements:** the convention for buttons, menus and fields. Pick one, use it everywhere.
- **Placeholders:** one form only, `<key-id>` or `KEY_ID`, never both.
- **Links:** descriptive text. Never "click here", never a bare URL in prose.
- **Lists:** when to use bullets, when to number, whether items end in full stops.
- **Admonitions:** which types exist (note, warning, caution) and what each means. Three at most, or readers stop distinguishing them.
- **Images:** when they earn their place, what alternative text is required, and where the source files live.

---

## 6. Accessible and inclusive language

Not a separate concern from style; it is style.

- Alternative text on every meaningful image. Decorative images marked as such.
- No direction-only or colour-only instructions. "Select **Save**", not "click the green button on the right".
- Descriptive link text, because screen reader users navigate by link list.
- Real heading levels in order, never bold text standing in for a heading.
- Tables for data, not for layout.

For the conformance target and how it is tested, see [`../../web-development/accessibility/`](../../web-development/accessibility/).

Prefer terms that describe rather than assume: *primary/replica*, *allowlist/blocklist*, and specific words over *simply*, *just*, *obviously*, and *easy*. The last group is worth a rule of its own: telling a stuck reader the step is easy tells them the problem is them.

---

## 7. Enforcement
A style guide nobody can check is a style guide nobody follows.

- Run a prose linter in CI. Vale is the common choice and reads rule sets in the repository.
- Encode the terminology table as a linter rule. It is the highest-value automation available and the easiest to write.
- Link the specific rule in review comments rather than restating it. Arguments end faster when the rule is written down.
- Keep unenforceable rules short. A judgement call is fine; a page of judgement calls is decoration.

---

## 8. Changes

Keep a dated record of amendments at the end. Apple's style guide carries a "Changes to the guide" section, and it is a good precedent.

Writers need to know what changed since they last read it. Without a change log, the only way to find out is to reread the whole document, which nobody does.

---

## Common failures in this document

- **Rewrites the base guide.** Long, redundant, and out of date the moment Chicago revises.
- **No terminology table.** Leaves the single most expensive inconsistency unaddressed.
- **Unenforceable.** Rules that no linter and no reviewer can apply consistently.
- **Silent on the real disagreements.** Contractions and register get re-argued in every review.
- **No change record.** Writers cannot tell what moved.
- **Cites a superseded edition.** Check the base guide's current edition when you review this.

---

## Related documents

- [`README.md`](README.md). Which document type to write, and why the split exists
- [`reference-page.md`](reference-page.md). Where the fixed field order is applied
- [`../foundations/glossary.md`](../foundations/glossary.md). Definitions for readers, as opposed to word choice for writers
- [`../foundations/code-review-guidelines.md`](../foundations/code-review-guidelines.md). The same instinct applied to code
- [`../../web-development/accessibility/`](../../web-development/accessibility/). The conformance target behind section 6
