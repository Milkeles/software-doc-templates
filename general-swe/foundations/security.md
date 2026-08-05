# Security policy for {project}

*Also called: SECURITY.md, vulnerability disclosure policy, responsible disclosure policy.*

*Italic text is guidance. Delete it as you fill each section in.*

*This file answers one question for a stranger who has found a flaw in your software: where do I send this, and what happens next? Everything else is optional — ISO/IEC 29147:2018 makes that literal, requiring only a preferred contact mechanism.*

*A stale contact is worse than no contact. RFC 9116 says so directly: "Not having a 'security.txt' file may be preferable to having stale information in this file." The same applies here. If you cannot keep an address alive, do not publish it.*

| | |
|---|---|
| **Last reviewed** | YYYY-MM-DD |
| **Applies to** | *Which repositories, packages, and hosted services. Say it explicitly — Rust's file covers two whole GitHub organisations, and says so.* |
| **Escalation** | *Where to go if you get no reply. Delete if you have nowhere above you.* |

---

## Reporting a vulnerability

*The one section you cannot skip. Name exactly one preferred private channel, and link it directly.*

*Pick one of three:*

- ***GitHub private vulnerability reporting.** Deep-link the form rather than describing it, as Electron does: `https://github.com/{org}/{repo}/security/advisories/new`. Enable it first under Settings → Advanced Security.*
- ***A security mailbox.** `security@example.com`. Preferably a list, not a person — Laravel routes to one named individual, which is unambiguous and a bus factor of one.*
- ***A bounty platform.** React and Angular are three-line redirects into their parent company's programme. If someone else runs your disclosure process, say so and stop writing.*

*Then say what not to do, by name. Kafka's version works because reporters think in terms of the tool in front of them:*

> Do **not** open public GitHub issues or pull requests, file public JIRA tickets, or post to mailing lists for unpatched vulnerabilities.

*If you enable GitHub's private reporting, name a human fallback too. GitHub only notifies maintainers who are watching the repository for all activity or subscribed to security alerts — the button does not guarantee anyone reads the report.*

## Report contents

*A short list of what makes a report actionable. HashiCorp's is three lines: steps to reproduce or a proof of concept, the tools used including versions, and the tool output. That is enough.*

*Do not demand a CVSS score or a suggested patch. You are asking someone doing you a favour to fill in a form.*

## Our response

*The response you commit to, in order, with numbers. Vague reassurance sets no expectation and cannot be broken, which is the problem with it.*

*Commit to two milestones: time to acknowledge receipt, and a default disclosure deadline. CERT/CC reports that 24–48 hours is common for acknowledgement and 45–90 days for public disclosure.*

*Node.js is the clearest worked example, and its trailing caveat is the honest part:*

> Normally, your report will be acknowledged within 5 days, and you'll receive a more detailed response to your report within 10 days indicating the next steps in handling your submission. These timelines may extend when our triage volunteers are away on holiday, particularly at the end of the year.

*A timeline is optional, and publishing one you miss costs more than publishing none. Skip this section rather than promise a response you cannot staff.*

*Say whether you will request a CVE and whether you will credit the reporter. On GitHub both are mechanically supported — GitHub is a CVE Numbering Authority, and the advisory form has a credit field — so this is a promise you can actually keep.*

## Supported versions

*Which versions get security fixes. Write a rule with a worked example so it never goes stale.*

*Go's is the best in the sample:*

> We support the past two Go releases (for example, Go 1.17.x and Go 1.18.x when Go 1.18.x is the latest stable release).

*If you ship continuously, say that instead. Homebrew: "Homebrew is a rolling release package manager… only the latest release and latest commit on the `main` branch are supported."*

*Delete this section if you have one supported version, which is the honest answer for most projects. A table listing one row of `1.x ✅` communicates nothing.*

## Out of scope

*The highest-value optional section: it saves triage time on reports you were never going to accept.*

*Two ways to write it, and the first is better:*

***As a rule.** Homebrew states a security boundary and then defines a vulnerability as its negation — "defects in Homebrew-maintained code or infrastructure that let an attacker violate those guarantees without already controlling the user's account, local machine, maintainer account, command line, environment, configuration, third-party tap, mirror, wrapper or repository." A rule decides cases you did not anticipate. A list does not.*

***As named exclusions with reasons.** Vue gives the reasoning and an analogy in two sentences:*

> We do not consider XSS via template expressions a valid attack vector, because it can only happen if the user intentionally uses untrusted content as template compilation source. This is similar to knowingly pasting untrusted scripts into a browser console.

*Node.js names CWE numbers on both sides of the line, which makes the boundary checkable by someone other than you. Also carve out what you do not own — Electron: "Report security bugs in third-party modules to the person or team maintaining the module."*

## Legal safe harbour

*Whether you commit not to pursue legal action against a reporter who follows this policy. Delete the section if you are not making that commitment — do not gesture at it.*

*Be aware of how rare a real grant is. Many projects publish the mirror image instead — duties on the reporter (avoid privacy violations, no data destruction, only test accounts you own) with no grant of authorisation in return. That is not safe harbour, and calling it that misleads people.*

*If you do grant it, do not draft the wording yourself. disclose.io's `dioterms` are CC0-1.0, so you can copy them without attribution. Reproduce the limit clause verbatim, because it is the part that is true regardless of what you promise:*

> Note that the Safe Harbor applies only to legal claims under the control of the organization participating in this policy, and that the policy does not bind independent third parties.

*Publishing this file does not by itself authorise anyone to test your systems. RFC 9116 §5.5 is explicit that researchers "shouldn't assume that the presence or absence of a 'security.txt' file grants or denies permission for security testing". If you want to permit or forbid testing, say it here.*

## AI-assisted reports

*Whether you accept reports drafted with an LLM, and on what terms. Delete this section until you are receiving the reports that make you want it.*

*Homebrew's is the clearest, and it leads their file rather than trailing it:*

> AI and LLM tools may help with security research but you remain fully responsible for everything you submit: treat their output as a fallible first draft and verify its correctness yourself before reporting.

*They then ask for brevity for a stated reason — "we are volunteers reading every word, and a concise report is a faster fix." A rule with a reason attached gets followed more often than a rule without one.*

---

## Notes on using this template

*Delete this section too.*

**Decide which of two jobs this file is doing.** Job A is instructions to someone reporting a vulnerability: where to send it, what happens, what is in scope. Job B is guidance to someone deploying your software safely: threat model, unsafe configurations. Most projects merge the two without noticing. If your software has a non-obvious threat model, write it in [`threat-model.md`](threat-model.md) and link to it rather than growing this file.

**A pointer beats a policy that drifts.** Roughly half of major projects delegate the substance to a canonical page elsewhere — Django's entire file is a title and one URL, 80 bytes, and Django has one of the most detailed disclosure policies in open source. A short file that resolves to a maintained page beats a long file nobody updates.

**Private reporting and this file are not substitutes.** GitHub's private-reporting button is a channel and carries no policy content — no scope, no timeline, no expectations. A project with it enabled still needs this file.

**Only publish an escalation route if you have somewhere to escalate to.** Electron and Node.js, both under the OpenJS Foundation, name two thresholds: no acknowledgement within 6 business days, or acknowledgement then silence for 14 days. An unaffiliated project has no higher authority to name — leave the row out rather than invent one.

**Where this lives:** in the repository, as `SECURITY.md`. GitHub checks three locations in this order — the `.github` folder, the repository root, then `docs` — so `.github/SECURITY.md` wins over a root copy, which catches people out. Use all caps and the `.md` extension; GitHub documents that form and does not document any other. It backs the Security policy page at `github.com/{owner}/{repo}/security/policy`. An organisation can put one copy in its public `.github` repository and have every repo inherit it, but inherited files do not appear in clones, packages or downloads — so a distributed library is better off with its own copy in the tree, while 200 internal services are better off with the org default. If you also run a website, publish `/.well-known/security.txt` per RFC 9116 with a `Policy:` field pointing back at this file, and set the mandatory `Expires` field.

---

## Related documents

- [`threat-model.md`](threat-model.md). What an attacker can do and what you have decided to defend — the detail this file should link to rather than absorb
- [`incident-postmortem.md`](incident-postmortem.md). What you write after a report turns into an incident
- [`bug-report.md`](bug-report.md). The public route, for everything that is not a vulnerability
- [`support.md`](support.md). Where to send people who are not reporting a flaw
- [`release-notes.md`](release-notes.md). Where the fix becomes visible to users who need to upgrade
