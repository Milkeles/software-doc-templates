# Contributing Guide

> How someone who does not work here gets a change accepted.
>
> **Also called:** CONTRIBUTING.md, contribution guidelines.
>
> **It is a router, not a manual.** All five of kubernetes, rust, node, django and Homebrew keep this file between 1 and 4 KB and use it to point at the real documentation. The instinct to make it complete is the instinct that makes it unread.
>
> **The filename and location are load-bearing.** GitHub only renders the "Contributing" link on the new-issue and pull-request pages when the file is named `CONTRIBUTING.md` and sits in one of three specific places. Section 1 has them.
>
> **Be honest about what it buys.** No study measures whether adding this file converts more first-time contributors. What is measured is narrower and still useful, and section 7 states it.
>
> **Where it lives.** The repository, in one of the three paths GitHub recognises. For an internal repository the same file still works; the audience is the next team, not the public.
>
> **Delete this block before publishing.**

---

## 1. Put it where the host will find it

GitHub accepts three locations, and uses this precedence when more than one exists:

```
   .github/CONTRIBUTING.md      <- checked first
   CONTRIBUTING.md              <- repository root
   docs/CONTRIBUTING.md         <- checked last
```

Filenames are not case sensitive, and `.md` is not required. But the "Contributing" tab and the link that appears when someone opens an issue or a pull request are conditioned on the name being `CONTRIBUTING`, so an equivalent file called `HACKING.md` gets none of that.

Root is the right default: it is where contributors look without being told. Use `.github/` only if you are already collecting community health files there. Put one in an organisation-level `.github` repository to supply a default for every repo that lacks its own.

---

## 2. Route, do not explain

The structure that works, in the order it should appear.

**Where to ask for help, first.** Rust puts this before any process: "the best way to get started is by asking for help in the #new members Zulip stream. We have a lot of documentation below on how to get started on your own, but the Zulip stream is the best place to *ask* for help." Someone who is stuck and cannot find a human leaves.

**What counts as a contribution.** Node states it explicitly: "contributions to Node.js include code, documentation, answering user questions, running the project's infrastructure, and advocating for all types of Node.js users." One sentence, and it changes who thinks the file is addressed to them.

**Reporting a bug.** The preconditions before opening one, as a checklist. Homebrew's version is four lines: update, run the diagnostic, read the troubleshooting page, then open one thing rather than both an issue and a pull request. Link the bug report template rather than restating its fields.

**Proposing a change.** Whether an issue must exist first, and what a proposal needs to contain.

**Submitting a pull request.** Branch naming, commit message format, what CI will run, how long review takes. Link the branching strategy and the code review guidelines; do not copy them.

**The legal step.** DCO or CLA. Section 5.

**Code of conduct.** A link and the enforcement contact. Not the text.

Organising by contributor intent rather than by artefact reads better. Homebrew's headings are "Report a bug", "Propose a feature", "Discuss, ask questions about or disagree with changes", which is how the reader arrives.

---

## 3. State the rule, the consequence, and the reason

Where you have a hard requirement, give all three in that order. Django does this in two sentences and it is the clearest example in the wild:

> **Warning: non-trivial pull requests (anything more than fixing a typo) without Trac tickets will be closed!**
>
> Django uses Trac to keep track of bugs, feature requests, and associated patches because GitHub doesn't provide adequate tooling for its community.

The rule is unambiguous, the consequence is stated, and the reason removes the reading that the project is being arbitrary. A rule with no stated consequence gets ignored; a consequence with no stated reason produces resentment.

Homebrew applies the same shape to an evidence requirement: "any pull request claiming performance improvements (e.g. 'this is faster') must include Hyperfine benchmark results demonstrating the improvement."

---

## 4. Say what the file is not for

Channel misuse is the most common complaint from maintainers, and the cheapest fix is one sentence. Homebrew's: "our issues and pull requests are for maintainers and contributors to discuss work to be done, not users or contributors asking questions about Homebrew usage or disagreeing with changes already made."

If you say what a channel is not for, say where that traffic should go instead. Otherwise you have closed a door without opening one.

---

## 5. Pick DCO or CLA, and know what you bought

| | Developer Certificate of Origin | Contributor License Agreement |
|---|---|---|
| Mechanism | `Signed-off-by:` trailer on each commit | A signed agreement, usually once per person or company |
| What it does | The contributor **asserts** they have the right to submit the code | The contributor **grants** the project rights, typically including relicensing |
| Friction | One flag on `git commit` | An out-of-band signing step before the first merge |
| Use it when | The licence will never change | You may relicense, dual-licence, or need to enforce copyright centrally |
| Examples | Linux, Node | Kubernetes, Apache projects |

The distinction that matters: **the DCO grants no rights.** Its text (version 1.1, Linux Foundation, 2004) is a per-commit assertion by the contributor about the origin of their work, including that "I understand and agree that this project and the contribution are public and that a record of the contribution... is maintained indefinitely". A CLA is a grant, which is why it costs contributors real friction and why you need one if you might ever change the licence.

You may use both and split by directory. GitLab requires the DCO for its MIT-licensed code and a CLA for the proprietary `ee` directory. Django, Homebrew and Rust require neither.

Whichever you pick, automate the check. A legal requirement enforced by a human reading commits is a legal requirement that will be missed.

---

## 6. Say something about AI-assisted contributions

Most projects have not yet, and maintainers are the ones absorbing the cost. Homebrew's policy is the clearest published one and is worth adapting rather than inventing:

- Disclose the tool used.
- Review the output yourself before asking a human to review it.
- Do not credit the tool as an author: contributors "must not attribute a commit to AI/LLM as an author, co-author, committer or signatory, including through an `Assisted-by`, `Co-developed-by` or similar commit trailer".
- Answer review comments yourself.
- Keep at most one AI-assisted pull request open at a time.

The last rule is the interesting one. It caps the rate at which one contributor can consume maintainer attention, which is the actual scarce resource.

---

## 7. What the evidence supports, and what it does not

**Nobody has measured whether this file converts contributors.** No study found tests the causal effect of adding a `CONTRIBUTING.md` on first-time contribution. Do not claim one.

**What has been measured** is that newcomer barriers are mostly not documentation barriers. Steinmacher and colleagues catalogued 58 barriers facing open-source newcomers for CSCW 2015, drawn from 69 practitioners across 19 projects and 21 prior studies. Documentation problems are one contributor to one of six categories, not the headline.

The follow-up is the useful part. Their FLOSScoach portal, tested with 65 students for ICSE 2016, "played an important role in guiding newcomers and in lowering barriers related to the orientation and contribution process, whereas it was not effective in lowering technical barriers". Self-efficacy dropped significantly in the control group and held steady in the portal group.

**So the honest claim is narrow and worth making:** a contributing guide helps with orientation and process, and does nothing for the technical difficulty of the codebase. Write it to answer "what happens next and who do I ask", not "how does this system work".

Two more findings worth carrying. The 2017 GitHub Open Source Survey, 5,500 respondents sampled from more than 3,800 repositories, found "incomplete or outdated documentation is a pervasive problem, observed by 93% of respondents", and that "60% of contributors say they rarely or never contribute to documentation". That 93 percent is the share who encountered the problem, not the share of documentation that is bad; it is quoted wrongly often. The same survey found that "documentation that clearly explains a project's processes, such as contributing guides and codes of conduct, is valued more by groups that are underrepresented in open source".

And Turzo, Sultana and Bosu tested 15 commonly recommended onboarding practices across 5 Gerrit projects and 1,155 GitHub projects for IEEE TSE in 2025. Four had a positive association, four were context-dependent, and **four were significantly negative**. Popular onboarding advice is not uniformly good advice, which is an argument for keeping this file short and for measuring what happens to your own first-time contributors.

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
- [`onboarding-guide.md`](onboarding-guide.md). The same problem for someone who does work here
- [`service-readme.md`](service-readme.md). What the project is, which this file assumes the reader already knows
