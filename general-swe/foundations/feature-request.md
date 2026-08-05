# Feature request: {the problem, in one line}

*Also called: enhancement request, feature proposal.*

*Italic text is guidance. Delete it as you fill each section in.*

*Title by the problem, not the solution. "No way to run a single test file" beats "Add a `--file` flag". You may be wrong about the fix. You are not wrong about the friction.*

| | |
|---|---|
| **Requested by** | |
| **Date** | YYYY-MM-DD |
| **Version in use** | *Where you hit the limitation.* |
| **Status** | *Open, accepted, declined, or needs a design process. A maintainer sets this, not the requester.* |

---

## Problem

*What you were trying to do, and what stopped you. Concrete situation, not an abstract capability.*

*This is the section that matters. Across 15 feature-request forms from major projects, 13 ask for the problem and 12 make it required — the highest agreement on any field in the genre. Svelte and Tauri independently use the same placeholder text, `I'm always frustrated when...`. Bevy asks "What problem does this solve or what need does it fill?".*

> I run one test file at a time while fixing a failure. The runner only accepts a directory, so a two-second check takes ninety seconds.

*Write this even if the solution feels obvious. A maintainer who understands your problem can offer a fix you did not know existed — and often does.*

## Proposed solution

*What you think should happen. One paragraph.*

*Say it plainly and hold it loosely. You are describing an outcome you want, not specifying an implementation. If you have a concrete API in mind, show one line of it.*

> `test --file path/to/one_test.ts`, running only that file.

## Current workaround

*What you do today instead, and what it costs you.*

*Ten of the 15 forms surveyed ask for "alternatives considered", but only four require it — it is the most over-recommended field in the genre. TypeScript's rewrite is better and gets better answers: "What workarounds are you using in the meantime?" Ordinary users can answer that. Most cannot list design alternatives.*

*An expensive workaround is the strongest argument you have. "I copy the file to a temp directory first" tells a maintainer more about the cost than any severity rating.*

## Scope and prior discussion

*Why this belongs in the project rather than in a plugin, a wrapper, or your own code. Link anything that shows others want it too.*

*Two of the three gates that decide a request are answered here. Homebrew asks whether the feature would be used by at least 90% of users. TypeScript runs a viability checklist. Nuxt asks whether it could be a module instead. Every one of those tests depends on the project having written its scope down somewhere — if yours has not, link the design goals or say plainly that no scope document exists.*

*For demand, link the discussion, the duplicate report, or the thread. Do not paste "+1" comments. Most large projects count thumbs-up reactions instead, because GitHub can sort by them (`sort=reactions-+1`) and cannot sort by comments.*

## Additional context

*Screenshots, links, prior art in other tools, constraints a maintainer would not guess.*

*Optional. Eight of 15 forms have this field and none require it. Leave it empty rather than padding it.*

---

## Notes on using this template

*Delete this section too.*

**The honest answer to "what gets a feature built" is uncomfortable, and Node.js publishes it.** Node's own feature-request management document, linked from its issue form, opens: "Feature requests are not a valuable source of input for the project. It is usually more productive to first send the Pull Request implementing the feature, even imperfectly, and let the discussion happen during code review." It goes further: "The project is volunteer run and does not have the ability to direct resources toward specific work… The best way to ensure a feature gets implemented is to create a PR to add it." And it names the harm in leaving requests open: an open request "may be detrimental as it may result in an expectation that will never be fulfilled". Everything a form collects is secondary to whether someone with commit access wants to build the thing.

**Do not ask whether the requester will implement it.** This field is recommended constantly and used almost never. Zero of the eleven largest projects surveyed have it — not Node, Kubernetes, VS Code, React, Rust, Electron, Homebrew, TypeScript, Angular, CPython or Go. Three smaller projects include it, all optional, and in none of them does it gate anything. Babel is the one worth copying because it inverts the tone: "Check this if you would like to implement a PR, we are more than happy to help you go through the process." That is an offer of mentorship. As a filter it does nothing.

**Do not ask for acceptance criteria, user stories, or a priority rating.** None of the 19 templates examined ask for acceptance criteria or user stories. None ask the requester to set priority or severity. Priority is the maintainer's field; a requester who sets it is guessing at a schedule they cannot see. The same rule holds in `bug-report.md` and for the same reason.

**Route the request before you collect it.** Several major projects deliberately do not accept feature requests as issues. React offers no route at all. Rust, Vue and Next.js send them to forums or Discussions. Use `.github/ISSUE_TEMPLATE/config.yml` to put those links in front of the form with `contact_links`, and consider `blank_issues_enabled: false`. A request filed in the wrong place costs a maintainer more than one never filed.

**Send big ideas to a design process instead.** Five projects with formal processes — Rust's RFCs, Python's PEPs, Go's proposals, Kubernetes' KEPs, Vue's RFCs — draw the line in the same place using different words: "substantial", "PEP-able", "notable", "non-trivial". The common core is that **an idea needs a design process when it changes something users can observe and cannot easily undo.** Everything else is an issue. Say in your form which it is and link the process, as Svelte does: maintainers "may close the issue and ask you to open an RFC".

**A duplicate search is worth less than it looks.** Only 5 of 15 forms gate on it. TypeScript reframes its search-terms field as a contribution to discoverability rather than a gate, and the FSE 2008 bug study found duplicates are not a significant maintainer pain point — a second report often carries information the first missed. Ask for links to related discussion; do not refuse the report.

**What this evidence is and is not.** The field frequencies above are a survey of what large projects converged on independently, which is a stronger signal than most template advice can offer. It is still convention, not measurement. No project publishes data showing that problem-first requests get accepted more often. Treat the structure as well-attested practice and the causal claims as unproven.

**Where this lives:** in the issue tracker, as a form the tracker enforces — `.github/ISSUE_TEMPLATE/feature_request.yml` for GitHub, or a description template under `.gitlab/issue_templates/` for GitLab. Use the YAML issue-form schema rather than a Markdown file so the problem field can be genuinely required; `required: true` is enforced on public repositories. Keep the file in the repository so the form versions with the code.

---

## Related documents

- [`bug-report.md`](bug-report.md). The sibling form. A bug is behaviour that is wrong; a feature request is behaviour that is missing
- [`contributing-guide.md`](contributing-guide.md). Where the routing rules and the design-process threshold are stated in full
- [`rfc.md`](rfc.md). Where a request goes when it is too large to be an issue
- [`technical-design-document.md`](technical-design-document.md). What an accepted request becomes once someone commits to building it
- [`architecture-decision-record.md`](architecture-decision-record.md). Where the design conversation lands if the request needs one
