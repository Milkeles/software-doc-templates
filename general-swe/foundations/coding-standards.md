# Coding Standards

> The rules about how code in this repository is written, and which tool enforces each one.
>
> **Also called:** style guide, coding conventions.
>
> **Most of this document should not exist.** Anything a formatter can fix belongs in the formatter's config, and anything a linter can detect belongs in the linter's config. What is left is the small set of decisions a tool cannot check, and that set is what you write down.
>
> **Justify rules as coordination decisions, not as findings.** Google says its own conventions are "sometimes arbitrary", and that is the honest framing. "Evidence behind style rules" at the end lists the very few style claims with measured support, and the larger number that are folklore.
>
> **There is no standard section set for this document.** PEP 8, the Google C++ Style Guide and the Linux kernel guide share no common outline. The headings below are a proposal that covers what teams usually need. Rename or drop them freely.
>
> **Where it lives.** The repository, beside the config files it describes. A style guide that is not in the same commit as the lint rules will drift from them.
>
> **Delete this block before publishing.**

*Italic text is guidance. Delete it as you fill each section in.*

---

## 1. Scope

*Which languages and which repositories this document governs, and which layer of rules it covers.*

*Separate the mandatory layers from the advisory one, and say which layer each rule sits in. Rust's ecosystem does this cleanly and is the model worth copying: a Style Guide for formatting, clippy for correctness, and API Guidelines for design — of which it says they "should not in any way be considered a mandate". Keeping the mandatory and advisory layers apart stops the advisory ones being argued as rules.*

| Layer | Question | Enforced by | Negotiable |
|---|---|---|---|
| **Formatting** | Where does the whitespace go | A formatter, on save and in CI | No. Nobody edits it |
| **Correctness and safety** | Is this construct a bug waiting to happen | A linter, failing the build | Per rule, with a reason |
| **Design and naming** | Is this the right shape | Review, guided by this document | Yes. That is what review is for |

*Do not restate a rule the formatter or linter already enforces. The config file is the authoritative copy, and a second copy here will drift from it silently.*

*Do write down the conventions that decide how the code reads, even where a tool can partly check them. A linter can flag an abbreviation; it cannot tell you whether the name that replaces it communicates intent. The test is whether the rule teaches a reader something the CI failure would not have.*

---

## 2. Base guide and deviations

*Name the guide you adopt, then record only where you differ. Writing a style guide from scratch is weeks of argument for a result nobody reads.*

| Field | Example |
|---|---|
| Language | Python 3.12 |
| Base guide | PEP 8, plus Google Python Style Guide for docstrings |
| Formatter and version | Black 25.1, line length 100 |
| Linter and config | Ruff, config in `pyproject.toml` |
| Deviations | Line length 100, not 88. Reason: two of our services have long ORM expressions and the wrapping hurt more than the width |

*The deviations row is the document. Every entry needs a reason — a deviation with no reason is indistinguishable from an accident, and the next person who reads the base guide will revert it.*

*Do not overstate what the base guide claims for itself. PEP 8 opens by saying it "gives coding conventions for the Python code comprising the standard library in the main Python distribution", and states that "project-specific guides take precedence for that project".*

---

## 3. Formatting

*Name the formatter, its version and its config file. Then stop writing.*

*Everything in this section is a solved problem. Adopt gofmt, rustfmt, Black, Prettier, clang-format or the equivalent, take its defaults, and move on. Black's README states the deal plainly: "by using it, you agree to cede control over minutiae of hand-formatting... Style configuration options are deliberately limited and rarely added." Prettier's stated goal is the same: "we want to free mental threads and end discussions around style."*

*Be precise about what a formatter buys, because two of the four usual claims are unsupported. It ends style arguments, which is true by construction. It shrinks diffs, which is mechanically verifiable. It makes reviewers focus on logic, which is plausible and unmeasured. It makes code faster to comprehend or less buggy, for which no study exists. Claim the first two.*

> **Example.** rustfmt 1.8, default profile, `rustfmt.toml` in the repository root. Runs on save and fails CI.

---

## 4. Naming

*What a good name looks like here. Give one compliant and one non-compliant example per rule — it beats a paragraph of description every time.*

*Spend the rules on descriptiveness, not on casing. Full descriptive words beating abbreviations is the best-supported rule in this whole area; camelCase versus under_score is a small effect that is close to nil for experienced readers.*

> **Example.** `calculate_invoice_total`, not `calc_inv_tot`. `elapsed_since_last_retry`, not `t2`. Domain nouns match the [glossary](glossary.md): a "charge" is never called a "payment" in code.

---

## 5. Comments

*What must be commented, and what must not.*

*"Comment why, not what" survives the evidence. "Comment everything" does not — see the evidence notes at the end of this document before you mandate comment volume.*

---

## 6. Error handling

*Which errors are raised, which are returned, which are logged and swallowed, and what goes in a message.*

*No linter can judge error semantics, so this section carries its full weight.*

> **Example.** Errors crossing a service boundary are wrapped with the call that produced them before they are returned. A caller reading `timeout calling billing.charge: context deadline exceeded` can act; a bare `context deadline exceeded` sends them to the logs.

---

## 7. Structure and file layout

*Module boundaries, where a new file goes, what belongs in a shared package.*

---

## 8. Testing conventions

*Naming, fixture placement, and what a test's name has to communicate.*

*Conventions only. What to test, and at which level, belongs in the [test strategy](test-strategy.md) — do not duplicate it here.*

---

## 9. Consistency: local or global

*State which consistency wins when they conflict, because the two most-cited guides disagree and you have to resolve it for your own repository.*

*PEP 8 says local consistency wins. From "A Foolish Consistency is the Hobgoblin of Little Minds": "Consistency with this style guide is important. Consistency within a project is more important. Consistency within one module or function is the most important." It then lists reasons to ignore a guideline, including when applying it "would make the code less readable, even for someone who is used to reading code that follows this PEP".*

*Google says global consistency wins, and gives a mechanism rather than a preference. Its C++ guide asks you to "be mindful of our scale", with more than 100 million lines in one repository, and to "be consistent with existing code... just pick one and stop worrying about it". At that scale uniformity is what makes automated refactoring across the whole codebase possible, which is a concrete return a small repository does not get.*

*Neither cites evidence. Both are reasoned. The deciding question is whether you run automated changes across many repositories. If you do, buy the global consistency. If you do not, PEP 8's position costs you less.*

---

## 10. Waivers

*Who grants a waiver, whether it is per-line or per-file, and whether a suppression comment must carry a reason.*

*A guide with no exception process gets ignored wholesale the first time it is wrong. Google's model sets the bar by what the rule protects: rules whose violation risks correctness get a high bar, stylistic ones are cheaper to waive. Suppressions without reasons accumulate until the linter is decorative.*

*Say also that "the absence of a prohibition is not the same as a license to proceed", in Google's phrasing, so the document is not read as an exhaustive list of the only forbidden things.*

> **Example.** `# noqa: E501 — generated SQL, reformatting breaks the parser`. Any suppression without a reason after the dash fails review.

---

## 11. Enforcement

*Which check runs where: on save, on commit, in CI. Which ones block a merge and which only warn.*

*Link the [branching strategy](branching-strategy.md) rather than restating the required-checks list, so there is one place to change it.*

---

## Notes on using this template

*Delete this section too.*

**Say that the reason is coordination, not defect prevention.** A codebase where everyone formats differently costs attention every day, and that is worth fixing. It is also the whole of the benefit. A standard that claims it prevents bugs will lose the argument with the first person who asks for the proof, and the rest of the document loses credibility with it.

**Spend your naming rules on descriptiveness, not on casing.** Whether a reader gains anything from `camelCase` over `under_score` is marginal, and it disappears entirely for people who have worked in the codebase for a while. Whether they can tell what `elapsed_since_last_retry` holds without opening another file is not marginal. Argue about the first and you have spent a meeting on nothing.

**Do not restyle a working file to match a new convention.** You gain no readability anyone can detect, and every edit carries a chance of introducing a defect. Apply new rules to new code and to files you are already changing.

**Do not trust a preference, including your own.** People are consistently wrong about which style is easier for them to read. This is the argument for settling style with a formatter and moving on, rather than with a discussion in which the loudest preference wins.

**A rule that makes bad structure painful is the most defensible kind.** The Linux kernel's 8-character indent is not a readability claim: it exists because "if you need more than 3 levels of indentation, you're screwed anyway". If a formatting rule pushes people towards better structure, say that out loud — it is a stronger justification than consistency.

---

## Common failures in this document

- **Formatting rules written in prose.** Put them in the formatter and delete the prose.
- **Rules presented as findings.** Almost all of them are conventions. Say so.
- **A guide written from scratch.** Adopt one and record deviations.
- **Deviations with no reason.** Indistinguishable from mistakes.
- **A restyle-the-whole-repo project.** No readability gain, nonzero defect risk.
- **Naming rules that are only about casing.** The measured effect is in descriptiveness.
- **No waiver process.** The first wrong rule discredits the whole document.
- **Not in the same repository as the lint config.** They will drift apart within a quarter.

---

## Related documents

- [`code-review-guidelines.md`](code-review-guidelines.md). Where the design and naming layer is actually applied
- [`contributing-guide.md`](contributing-guide.md). How an outside contributor finds out these rules exist
- [`branching-strategy.md`](branching-strategy.md). Where the required checks are listed
- [`test-strategy.md`](test-strategy.md). Testing conventions belong there, not here
- [`glossary.md`](glossary.md). Naming rules are worth little if the domain words are ambiguous
