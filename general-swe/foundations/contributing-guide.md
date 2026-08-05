# Contributing

> How someone who does not work here gets a change accepted.
>
> **Also called:** CONTRIBUTING.md, contribution guidelines.
>
> **It is a router, not a manual.** All five of kubernetes, rust, node, django and Homebrew keep this file between 1 and 4 KB and use it to point at the real documentation. The instinct to make it complete is the instinct that makes it unread.
>
> **The filename and location are load-bearing.** GitHub accepts three locations, in this precedence order: `.github/CONTRIBUTING.md`, then `CONTRIBUTING.md` at the repository root, then `docs/CONTRIBUTING.md`. Filenames are not case sensitive and `.md` is not required, but the "Contributing" tab and the link shown when someone opens an issue or pull request are conditioned on the name being `CONTRIBUTING` — an equivalent file called `HACKING.md` gets none of it. Root is the right default, because it is where contributors look without being told. Put one in an organisation-level `.github` repository to supply a default for every repo that lacks its own.
>
> **Order the sections by contributor intent, not by artefact.** Homebrew's headings are "Report a bug", "Propose a feature", "Discuss, ask questions about or disagree with changes" — which is how the reader actually arrives. The headings below follow that shape.
>
> **Be honest about what it buys.** No study measures whether adding this file converts more first-time contributors. "Evidence behind contributing guides" at the end states what is actually measured.
>
> **Where it lives.** The repository, in one of the three paths above. For an internal repository the same file still works; the audience is the next team, not the public.
>
> **Delete this block before publishing.**

*Italic text is guidance. Delete it as you fill each section in.*

---

## 1. Where to get help

*Name a place with humans in it, and put it first.*

*Rust puts this before any process: "the best way to get started is by asking for help in the #new members Zulip stream. We have a lot of documentation below on how to get started on your own, but the Zulip stream is the best place to* ask *for help." Someone who is stuck and cannot find a human leaves.*

> **Example.** Ask in `#project-help` on our Discord. Maintainers read it daily; issues are not the place for questions.

*If the channel list is long enough to need ranking, move it to a [support policy](support.md) and link it from here. GitHub shows that file on the new-issue page, which reaches people this one does not.*

---

## 2. What counts as a contribution

*One sentence. It changes who thinks this file is addressed to them.*

*Node states it explicitly: "contributions to Node.js include code, documentation, answering user questions, running the project's infrastructure, and advocating for all types of Node.js users."*

---

## 3. Reporting a bug

*The preconditions before opening one, as a checklist. Link the [bug report template](bug-report.md) rather than restating its fields.*

*Homebrew's version is four lines: update, run the diagnostic, read the troubleshooting page, then open one thing rather than both an issue and a pull request.*

*Say here that a security vulnerability does not go in the tracker, and link the [security policy](security.md). A reporter who is about to post an exploit publicly is reading this page, not that one.*

---

## 4. Proposing a change

*Whether an issue must exist first, and what a proposal has to contain.*

*State the rule, the consequence and the reason, in that order. Django does it in two sentences and it is the clearest example in the wild:*

> **Warning: non-trivial pull requests (anything more than fixing a typo) without Trac tickets will be closed!**
>
> Django uses Trac to keep track of bugs, feature requests, and associated patches because GitHub doesn't provide adequate tooling for its community.

*The rule is unambiguous, the consequence is stated, and the reason removes the reading that the project is being arbitrary. A rule with no stated consequence gets ignored; a consequence with no stated reason produces resentment.*

*State the size threshold too: small proposals use the [feature request](feature-request.md) form, and anything that changes behaviour users can observe and cannot easily undo goes to an [RFC](rfc.md). Say which, and link both.*

---

## 5. Submitting a pull request

*Branch naming, commit message format, what CI will run, and how long review takes.*

*Link the [branching strategy](branching-strategy.md) and the [code review guidelines](code-review-guidelines.md). Do not copy them — two copies of a review policy means one of them is wrong. The same applies to the [pull request template](pull-request-template.md): state the title format and the AI policy here in full, and let the template prompt for them.*

*Where you require evidence, say what evidence. Homebrew: "any pull request claiming performance improvements (e.g. 'this is faster') must include Hyperfine benchmark results demonstrating the improvement."*

---

## 6. Scope of issues and pull requests

*Channel misuse is the most common maintainer complaint, and the cheapest fix is one sentence.*

*Homebrew's: "our issues and pull requests are for maintainers and contributors to discuss work to be done, not users or contributors asking questions about Homebrew usage or disagreeing with changes already made."*

*If you say what a channel is not for, say where that traffic should go instead. Otherwise you have closed a door without opening one.*

---

## 7. Licensing and sign-off

*State whether you require a Developer Certificate of Origin, a Contributor License Agreement, or neither — and automate the check. A legal requirement enforced by a human reading commits is one that will be missed.*

| | Developer Certificate of Origin | Contributor License Agreement |
|---|---|---|
| Mechanism | `Signed-off-by:` trailer on each commit | A signed agreement, usually once per person or company |
| What it does | The contributor **asserts** they have the right to submit the code | The contributor **grants** the project rights, typically including relicensing |
| Friction | One flag on `git commit` | An out-of-band signing step before the first merge |
| Use it when | The licence will never change | You may relicense, dual-licence, or need to enforce copyright centrally |
| Examples | Linux, Node | Kubernetes, Apache projects |

*The distinction that matters: the DCO grants no rights. Its text (version 1.1, Linux Foundation, 2004) is a per-commit assertion by the contributor about the origin of their work, including that "I understand and agree that this project and the contribution are public and that a record of the contribution... is maintained indefinitely". A CLA is a grant, which is why it costs contributors real friction and why you need one if you might ever change the licence.*

*You may use both and split by directory. GitLab requires the DCO for its MIT-licensed code and a CLA for the proprietary `ee` directory. Django, Homebrew and Rust require neither.*

---

## 8. AI-assisted contributions

*Most projects have no policy yet, and maintainers absorb the cost. Homebrew's is the clearest published one and is worth adapting rather than inventing.*

- *Disclose the tool used.*
- *Review the output yourself before asking a human to review it.*
- *Do not credit the tool as an author: contributors "must not attribute a commit to AI/LLM as an author, co-author, committer or signatory, including through an `Assisted-by`, `Co-developed-by` or similar commit trailer".*
- *Answer review comments yourself.*
- *Keep at most one AI-assisted pull request open at a time.*

*The last rule is the interesting one. It caps the rate at which one contributor can consume maintainer attention, which is the actual scarce resource.*

---

## 9. Code of conduct

*A link and the enforcement contact. Not the text.*

*Do not write your own. Adopt the [Contributor Covenant](https://www.contributor-covenant.org/), which is the de facto standard, translated widely, and already familiar to most contributors. Pasting it in full here pushes everything a contributor actually needs below the fold.*

> **Example.** This project follows the Contributor Covenant, in `CODE_OF_CONDUCT.md`. Report concerns to conduct@example.org.

---

## Notes on using this template

*Delete this section too.*

**Write it to answer "what happens next and who do I ask", not "how does this system work".** That is the narrow thing this file is good at. It lowers the barriers around orientation and process — where do I start, what will happen to my pull request, who will read it. It does nothing at all for the technical difficulty of your codebase, and a contributing guide that tries to explain the architecture fails at both jobs.

**Do not claim it increases contribution.** Nobody has shown that adding this file converts a single first-time contributor. Write it because a newcomer who cannot find the process leaves, which you can watch happen, and because clear process documentation matters most to the people least sure they belong.

**Be sceptical of onboarding advice, including this page.** Of the practices commonly recommended for welcoming newcomers, roughly as many turn out to be neutral or actively unhelpful as helpful, and which is which depends on the project. That is an argument for keeping this file short and for watching what actually happens to your own first-time contributors rather than adopting a checklist wholesale.

---

## Common failures in this document

- **It tries to be the developer guide.** Route to that; do not become it.
- **Written for people who already contribute.** The reader has never opened the repository before.
- **No named place to ask a human.** The most common silent exit.
- **Rules with no reason given.** Reads as arbitrary and gets argued with instead of followed.
- **A legal requirement with no automated check.** It will be missed.
- **The code of conduct pasted in full.** Link it and name the contact.
- **Named something other than `CONTRIBUTING`.** The host stops linking it.
- **Claims it increases contribution.** Nothing measures that.

---

## Related documents

- [`code-review-guidelines.md`](code-review-guidelines.md). What happens to the pull request once it exists
- [`branching-strategy.md`](branching-strategy.md). Where to branch from and what to name it
- [`coding-standards.md`](coding-standards.md). The rules the automated checks will apply
- [`bug-report.md`](bug-report.md). The form this file routes bug reporters to
- [`feature-request.md`](feature-request.md). The form for people asking for something that does not exist yet
- [`pull-request-template.md`](pull-request-template.md). What the contributor fills in once they have the change
- [`security.md`](security.md). The private route, for the one report that must not become an issue
- [`support.md`](support.md). Where questions go instead of the tracker
- [`governance.md`](governance.md). Who decides, when this file's rules are disputed
- [`onboarding-guide.md`](onboarding-guide.md). The same problem for someone who does work here
- [`service-readme.md`](service-readme.md). What the project is, which this file assumes the reader already knows
