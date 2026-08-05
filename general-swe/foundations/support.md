# Getting help with {project}

*Also called: SUPPORT.md, support policy, getting help.*

*Italic text is guidance. Delete it as you fill each section in.*

*This file has one reader: someone about to open an issue that is really a question. It should answer "where do I go instead?" before they finish typing.*

*Keep it short — the median real example is about 500 bytes. ESLint's entire file is one sentence: "If you have a question about how to use ESLint, please ask it in our chatroom." That is a complete, working `SUPPORT.md`. Do not write more than your project needs.*

---

## Where to get help

*A ranked list of channels, each with what it is actually for. Rank them — an unordered list of five links is not routing.*

*Name the specific destination, not the platform. Kubernetes names `#kubernetes-users` and `#kubernetes-novice` inside its Slack, because "join our Slack" tells a beginner nothing. Node.js gives a pre-built search URL across the whole organisation's issues rather than telling people to search.*

> **Documentation** — {link}. Start here for how-to questions.
> **Discussions** — {link}. Ask here if you are not sure whether your problem affects everyone.
> **Stack Overflow** — the `{tag}` tag. Best for questions with a self-contained code example.

*Say which channels the project staffs and which it does not. Node.js splits them explicitly: search the official venues first, then "try these **unofficial** resources". A user who waits three days in a channel no maintainer reads is worse off than one who was told nobody is listening.*

*Homebrew routes on the user's uncertainty rather than their intent — "Not sure if your issue affects everyone reproducibly?" That gives the reader a test they can apply, instead of asking them to classify their own problem correctly.*

## What the issue tracker is for

*The boundary, stated positively. Say what the tracker **is** for, then what it is not.*

*Go leads with the deviation from the norm, which is the right order because users arrive with an expectation:*

> Unlike many projects on GitHub, the Go project does not use its bug tracker for general discussion or asking questions. We only use our bug tracker for tracking bugs and tracking proposals going through the Proposal Process.

*Write this without scolding. Kubernetes opens by thanking people: "This isn't the right place to get support for using Kubernetes, but the following resources are available below, thanks for understanding."*

*This rule will also appear in your contributing guide, and that is correct. The two files are read by different people arriving from different places. Do not deduplicate it.*

## What is supported

*Which versions, platforms or configurations you will help with. Delete this if the answer is "the latest release" and nothing else.*

*One sentence can do it. Node.js: "Node.js contributors have limited availability to address general support questions. Please make sure you are using a currently-supported version of Node.js." A question about a dead version is answered before it is asked.*

*Three shapes, depending on what you ship:*

- ***A rule with a worked example.** Go: "We support the past two Go releases (for example, Go 1.17.x and Go 1.18.x when Go 1.18.x is the latest stable release)." A rule plus one instance never goes stale.*
- ***A dated table with named phases,** if you run an LTS. Node.js publishes Current, Active LTS, Maintenance and End-of-life with a content commitment for each, keeps the end-of-life rows rather than deleting them, publishes the same data as JSON so tooling and humans cannot diverge, and writes `Dates are subject to change.` under the table so it is not read as a contract.*
- ***Tiers with guarantees attached,** if you support many platforms. Rust's tiers are defined by the CI activity behind them — tier 1 is "guaranteed to work" because it builds and passes tests on every change; tier 2 is "guaranteed to build" and says plainly that tests are not always run. Defining a tier by what you actually do makes the claim falsifiable and stops it drifting into marketing.*

*If you ship a rolling release, say so. That is a complete answer, not a gap.*

## What to expect

*How much attention a question realistically gets, and from whom. This is where you prevent the interaction that ends badly.*

*Node.js states the social contract in two sentences worth copying:*

> The open source license grants you the freedom to use Node.js. It does not guarantee commitments of other people's time. Please be respectful and manage your expectations.

*Almost every unhappy support exchange in open source traces to a user who believed the licence included the maintainer's attention. Saying otherwise once, in writing, costs nothing.*

*curl goes further and documents the outcomes where nothing happens, under headings named `Not reproducible`, `Unresponsive`, `Lack of time/interest` and `Closing off stalled bugs`, including: "Bugs that are filed and are understood can unfortunately end up in the 'nobody cares enough about it to work on it' category." Most projects document only the happy path. Naming the failure modes is unusual and it is honest.*

## What paid support covers

*Delete this unless you sell it or someone else does.*

*If a company offers commercial support for your project, name it and say what it covers. curl points at wolfSSL and lists customisation, porting, feature development, bug fixing and compliance assistance.*

*If you include it, state what the free project still guarantees — otherwise the paid list reads as everything you have withdrawn.*

---

## Notes on using this template

*Delete this section too.*

**Do not claim this file reduces your support load.** Nobody has measured that — not question volume, not maintainer time. Write it because it tells a confused person where to go in one sentence. That courtesy is real and you can verify it by reading the file.

**The stronger lever is `contact_links`, not this file.** `.github/ISSUE_TEMPLATE/config.yml` puts named destinations inside the issue-creation flow itself, and `blank_issues_enabled: false` removes the blank-issue path entirely. This file is a sidebar link the user may not click; the config is a fork in the road they cannot avoid. Use both — the file states the policy, the config enforces the routing.

**Split this out of your contributing guide only under two conditions:** you get support questions in the tracker often enough for it to be a burden, and you have a real non-tracker channel to send them to. If either is false, a "Getting help" section in `README.md` or the contributing guide is better. Two files means two channel lists to keep alive, and a stale channel list is worse than none.

**If you split, make the two files name each other.** Bootstrap is the clean example: its `SUPPORT.md` has a `Bug reports` section whose entire content is a pointer to the contributing guidelines, and its contributing guide says "Please **do not** use the issue tracker for personal support requests" and links Discussions. No overlap, no contradiction, no orphaned advice.

**Where this lives:** in the repository, as `SUPPORT.md`. GitHub checks the `.github` folder first, then the root, then `docs` — so `.github/SUPPORT.md` beats a root copy. Use all caps and the `.md` extension; that is the form GitHub documents. It appears as a link under "Helpful resources" on the new-issue page, which is the moment of highest leverage. GitHub concedes the file is easy to miss and recommends linking it from your README as well. An organisation can put one copy in its public `.github` repository and have every repo inherit it.

---

## Related documents

- [`contributing-guide.md`](contributing-guide.md). The other half of the boundary — for people giving something rather than asking for something
- [`bug-report.md`](bug-report.md). Where a question goes once it turns out to be a defect
- [`troubleshooting-guide.md`](../user-documentation/troubleshooting-guide.md). The answers themselves, which this file only points at
- [`service-readme.md`](service-readme.md). Where a short "getting help" section lives if you decide not to split
- [`security.md`](security.md). The separate, private route for anything that is a vulnerability
