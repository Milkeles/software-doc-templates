# {What this change does, in one line}

*Also called: PR description, merge request description, change request.*

*Italic text is guidance. Delete it as you fill each section in.*

*Title in the imperative, as if completing "this change will…". "Cache the resolved config" beats "Caching fix". Many projects require a prefix — `feat:`, `fix:`, `docs:` for Conventional Commits, `gh-12345:` for CPython. Follow whatever your repository already enforces, because the title usually becomes the commit message.*

| | |
|---|---|
| **Related issue** | *`Fixes #123`. Use `Fixes`/`Closes` only if merging should close it.* |
| **Type of change** | *Bug fix, feature, documentation, refactor, build, or chore.* |
| **Breaking change** | *Yes or no. If yes, fill in the migration section below.* |

---

## Summary

*Why this change exists, then what it does. Motivation first.*

*This is the section reviewers actually need. Bacchelli and Bird studied code review at Microsoft for ICSE 2013 — observing 17 developers across 16 product teams, classifying 570 review comments, and surveying 165 managers and 873 programmers. Their finding: "context and change understanding is the key of any review", and most of those understanding needs are met by no tool. Your description is the tool.*

*React's template asks for exactly this and nothing softer: "Explain the motivation for making this change. What existing problem does the pull request solve?" Homebrew asks the two halves separately — "Have you explained what your changes do?" and "Have you explained why you'd like these changes included, not just what they do?"*

> The config loader re-read and re-parsed `config.toml` on every request, costing ~4 ms per call under load. This caches the parsed result and invalidates it on file mtime change.

*Do not describe the diff. The reviewer can read the diff. Describe what the diff cannot say: why now, what you ruled out, and what you are unsure about.*

## Testing

*How you verified this works. Commands you ran, cases you covered, what you could not test.*

*Be specific enough that a reviewer could repeat it. "Tested locally" tells them nothing.*

> `cargo test config::` — 14 passing, 2 new.
> Manually checked that editing `config.toml` while the server runs picks up the change within one request.
> Not tested: Windows file-mtime granularity. Flagging for a reviewer with a Windows machine.

*Say what you did not test. An honest gap gets checked by someone else; a hidden one ships.*

## Breaking changes and migration

*Delete this section if nothing breaks.*

*What stops working, who it affects, and the exact steps to move across. Angular asks contributors to "describe the impact and migration path for existing applications".*

> `load_config()` no longer accepts a `reload` argument. Callers passing `reload=True` should call `invalidate_config()` instead. No behaviour change for callers using defaults.

## Release note

*One sentence a user will read in the changelog, or "none".*

*Write it for someone who does not know your codebase. Kubernetes, Docker and Electron all fence this block so a bot can extract it — copy that pattern if you automate releases.*

*Docker's template gives the clearest worked contrast:*

> **Good:** Fix a panic when running `docker top` on a non-running Windows container.
> **Bad:** Refactor test TestFooWithBar

*The bad example is bad because it describes the work, not the user-visible effect.*

## AI assistance

*Whether you used an AI tool on this change, which one, and what you did to verify its output.*

*This is now standard practice, not a novelty. Five of fifteen major projects surveyed require it — Rust, Django, Deno, Homebrew and Electron. The shape is consistent everywhere: disclosure is mandatory, use is not banned, and verification stays with you. Rust states the trade plainly: "LLM contributions are not banned, but are held to a higher standard of review and correctness."*

> Used Claude to draft the cache-invalidation tests. I reviewed each assertion against the mtime semantics in the standard library docs and rewrote two that tested the mock rather than the behaviour.

*If your project has no AI policy yet, write one before adding this field — otherwise the question has no answer a contributor can act on.*

## Checklist

*Delete the items that do not apply to your project. Keep this short.*

- [ ] Tests cover the change
- [ ] Documentation updated
- [ ] Commit messages follow the project's format
- [ ] No unrelated changes included

---

## Notes on using this template

*Delete this section too.*

**Do not claim a PR template speeds up review.** It is the most common justification and the evidence points the other way. Li and colleagues studied issue and PR templates at scale for *IEEE Transactions on Software Engineering* in 2023 — the only large study of this artifact. After a project adopts templates, incoming volume drops, discussion comments drop, and **issue resolution takes longer, not shorter**. A plausible reading is that templates filter out the easy and duplicate items, so what remains is harder and naturally slower — but the study cannot separate that from the alternative, and neither can anyone else. Projects that adopt templates are usually already drowning, which confounds the comparison badly. The honest position: templates measurably change how a project behaves, and the direction is not uniformly good.

**The description is the part with evidence behind it.** Bacchelli and Bird's finding that reviewers need context and change understanding is well-sourced and directly supports one thing: a field that explains why the change exists. It does not support checklists, type selectors, or breaking-change flags. Those are conventions — useful ones, often mechanical, but not evidence-backed.

**Checklists are weaker than they look.** The one controlled experiment on review checklists — Gonçalves and colleagues, *Empirical Software Engineering* 2022, pre-registered, with professional developers across three review tasks — concluded that they "did not identify a strong relationship between the guidance provided and code review performance". Two caveats cut both ways: most participants were novice reviewers, and the study measured checklists for *reviewers*, not the author-facing checklist this template carries. Nobody has measured the author-facing kind at all. Keep yours short, and drop any item a contributor cannot honestly self-assess.

**Keep the whole thing small.** A 2026 survey of 2,689 PR template files from 2,614 repositories found that 68% organise their content into two or fewer categories, and 71% never restructure after the first version. Real templates are short and static. VS Code ships 344 bytes; Kubernetes ships 3,195. If you are choosing, the distribution says choose small.

**Most real templates are invisible.** The dominant style is instructions inside `<!-- HTML comments -->` that never render in the submitted PR. VS Code's and Vite's entire templates are a single comment. That trades a clean PR body for guidance nobody is forced to read. Headings the author fills in, as above, trade the reverse. Pick deliberately.

**Skip GitHub's own advice about @mentions.** GitHub's documentation suggests the template include "@mentions of the person or team responsible for reviewing". None of the fifteen major projects surveyed does this. Use `CODEOWNERS` and automatic assignment instead — Rust uses an `r? <reviewer name>` command — because a hardcoded name in a template goes stale and pings the wrong person for years.

**Decide whether the template is a gate or a hint.** Electron enforces it — "PRs submitted that do not follow this template will be automatically closed" — as does Homebrew: "Don't delete these checkboxes or this pull request is closed automatically." React warns that an empty testing section means "your PR will very likely be closed". VS Code and Vite enforce nothing. Both approaches run at scale. What fails is enforcing informally, where contributors cannot tell which fields are real.

**Where this lives:** in the repository, as `.github/pull_request_template.md`. GitHub also accepts `pull_request_template.md` in the root or in `docs/`, and either casing works — projects genuinely use both, so a 404 on one spelling does not mean a project has no template. One rule catches people out: templates only take effect once merged to the default branch.

**For multiple templates,** put them in `.github/PULL_REQUEST_TEMPLATE/` and select one with the `template` query parameter. Ansible does this in production: its default `PULL_REQUEST_TEMPLATE.md` is a symlink to a file named *"Unclear purpose or motivation.md"*, alongside `Bug fix.md`, `New feature.md`, `Documentation change.md` and `Tests.md`. Contributors who do not pick get the catch-all. Note that the query parameter must be built into your links — GitHub shows no template picker for pull requests the way it does for issues.

---

## Related documents

- [`code-review-guidelines.md`](code-review-guidelines.md). What the reviewer is looking for once this description is written
- [`contributing-guide.md`](contributing-guide.md). Where the title format, sign-off, and AI policy are stated in full
- [`bug-report.md`](bug-report.md). Often the issue this pull request closes
- [`changelog.md`](changelog.md). Where the release note ends up
- [`branching-strategy.md`](branching-strategy.md). Which branch this targets and why
