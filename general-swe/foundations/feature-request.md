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

*This is the only required field. Svelte and Tauri both prompt for it with `I'm always frustrated when...`; Bevy asks "What problem does this solve or what need does it fill?". Either phrasing works.*

> I run one test file at a time while fixing a failure. The runner only accepts a directory, so a two-second check takes ninety seconds.

*Write this even if the solution feels obvious. A maintainer who understands your problem can offer a fix you did not know existed — and often does.*

## Proposed solution

*What you think should happen. One paragraph.*

*Say it plainly and hold it loosely. You are describing an outcome you want, not specifying an implementation. If you have a concrete API in mind, show one line of it.*

> `test --file path/to/one_test.ts`, running only that file.

## Current workaround

*What you do today instead, and what it costs you.*

*Ask for the workaround, not for "alternatives considered". TypeScript's phrasing gets better answers: "What workarounds are you using in the meantime?" Ordinary users can answer that; most cannot list design alternatives.*

*An expensive workaround is the strongest argument you have. "I copy the file to a temp directory first" tells a maintainer more about the cost than any severity rating.*

## Scope and prior discussion

*Why this belongs in the project rather than in a plugin, a wrapper, or your own code. Link anything that shows others want it too.*

*This is where a request is usually decided. Homebrew asks whether at least 90% of users would use the feature; Nuxt asks whether it could be a module instead. Both tests need the project's scope written down somewhere — link it, or say plainly that no scope document exists.*

*For demand, link the discussion, the duplicate report, or the thread. Do not paste "+1" comments. Most large projects count thumbs-up reactions instead, because GitHub can sort by them (`sort=reactions-+1`) and cannot sort by comments.*

## Additional context

*Screenshots, links, prior art in other tools, constraints a maintainer would not guess.*

*Optional, and never required. Leave it empty rather than padding it.*

---

## Notes on using this template

*Delete this section too.*

**Ask for the problem; everything else is optional.** Node's own feature-request guidance says the quiet part: "Feature requests are not a valuable source of input for the project. It is usually more productive to first send the Pull Request implementing the feature, even imperfectly, and let the discussion happen during code review." Set expectations accordingly, and close requests nobody will build rather than leaving them open — an open request "may be detrimental as it may result in an expectation that will never be fulfilled".

**Do not ask for acceptance criteria, user stories, or a priority rating.** Priority is the maintainer's field; a requester who sets it is guessing at a schedule they cannot see. The same rule holds in [`bug-report.md`](bug-report.md).

**Do not ask whether the requester will implement it.** As a filter it does nothing. If you want the field, invert it into an offer, as Babel does: "Check this if you would like to implement a PR, we are more than happy to help you go through the process."

**Route the request before you collect it.** Use `.github/ISSUE_TEMPLATE/config.yml` to put forum or Discussions links in front of the form with `contact_links`, and consider `blank_issues_enabled: false`. A request filed in the wrong place costs a maintainer more than one never filed.

**Send big ideas to a design process instead.** Rust's RFCs, Python's PEPs, Go's proposals, Kubernetes' KEPs and Vue's RFCs draw the line in the same place: an idea needs a design process when it changes something users can observe and cannot easily undo. Say in the form which it is and link the process.

**Where this lives:** in the issue tracker, as a form the tracker enforces — `.github/ISSUE_TEMPLATE/feature_request.yml` for GitHub, or a description template under `.gitlab/issue_templates/` for GitLab. Use the YAML issue-form schema rather than a Markdown file so the problem field can be genuinely required; `required: true` is enforced on public repositories. Keep the file in the repository so the form versions with the code.

---

## Related documents

- [`bug-report.md`](bug-report.md). The sibling form. A bug is behaviour that is wrong; a feature request is behaviour that is missing
- [`contributing-guide.md`](contributing-guide.md). Where the routing rules and the design-process threshold are stated in full
- [`rfc.md`](rfc.md). Where a request goes when it is too large to be an issue
- [`technical-design-document.md`](technical-design-document.md). What an accepted request becomes once someone commits to building it
- [`architecture-decision-record.md`](architecture-decision-record.md). Where the design conversation lands if the request needs one
