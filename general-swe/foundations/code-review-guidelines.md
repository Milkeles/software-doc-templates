# Code review guidelines

*Also called: pull request (PR) review guidelines, code review checklist.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | *Which repositories or teams.* |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

---

## The standard

*The single sentence that decides whether to approve. Everything else in this document is detail under it.*

*Google's formulation is the clearest available and worth adopting nearly verbatim: approve a change once it definitely improves the overall code health of the system, even if it is not perfect, because there is no such thing as perfect code, only better code.*

*Write your version. Then write its corollary, which is the part that actually changes behaviour: a reviewer may not block a change because they would have written it differently.*

> **Example.** Approve when the change definitely improves the health of the codebase. Perfection is not the bar, and "I would have done it another way" is not an objection.

---

## Response time

*How quickly a review must be started, and what to do when that slips.*

*State the reason alongside the number, or the number will be treated as aspirational. The reason is that review latency is a team cost, not a personal one: an engineer who reviews promptly is individually slower and the team ships faster. Google's rule is a maximum of one business day to respond, where responding may mean a partial review or an explicit "I will get to this at 15:00".*

| | |
|---|---|
| **First response** | *One business day maximum* | 
| **If you cannot** | *Say so in the request and name someone who can* |
| **Urgent** | *Define what qualifies and how to signal it. Keep the bar high or everything becomes urgent.* |

---

## Change size

*A limit, with a reason, and what to do when a change exceeds it.*

*Review quality falls off with size, and past a point reviewers stop finding defects and start approving. Google's guidance is that around 100 lines is comfortable and 1,000 is usually too large. SmartBear's frequently cited figures from a Cisco study of 2,500 reviews suggest 200 to 400 lines per sitting, under 60 minutes, with 70 to 90 percent of defects found in that range. Treat those numbers as directional rather than settled: the study was vendor-funded, is not peer-reviewed, and is twenty years old. The two sources agree on the direction, which is the part you can rely on.*

- *Target: under N lines of substantive change*
- *Split by: refactor first, behaviour second; mechanical rename in its own change*
- *Exempt: generated files, moves with no edits, lock files*

**What the author owes the reviewer.** *A description explaining why, not what. A note on what to look at first. Any part the author is unsure about, flagged explicitly. Passing CI before requesting review.*

---

## What to look for

*The list, roughly in order of importance. A reviewer who runs out of time should have spent it on the top of this list.*

1. **Design.** *Does the change belong in this system, and is it in the right place? The most valuable and the least automatable thing a reviewer does.*
2. **Correctness.** *Does it do what it claims, including at the edges and under concurrency?*
3. **Tests.** *Do they fail if the code is wrong? A test that passes against broken code is worse than none.*
4. **Complexity.** *Could a future reader change this safely? Is it built for a requirement that does not exist?*
5. **Naming and clarity.** *Would a new joiner understand it without the author present?*
6. **Security and data handling.** *Untrusted input, secrets, personal data, permissions.*
7. **Operability.** *Can you tell from logs and metrics whether this works in production?*
8. **Comments and documentation.** *Do the comments explain why? Did the change invalidate a document?*

*Anything a tool can decide, a tool should decide. Formatting, import order and lint rules do not belong in review comments; move them into CI and stop discussing them.*

---

## Review comments
*The mechanics that determine whether review feels like help or like an exam.*

- **Label the ones that do not block.** *Prefix optional comments so the author knows what is required. `Nit:` for trivia, `Optional:` for a suggestion, `FYI:` for information needing no action. Without labels, every comment reads as a demand, and reviews take twice as long.*
- **Comment on the code, not the coder.** *"This is not thread-safe" rather than "you forgot the lock". The grammar matters more than people expect.*
- **Ask rather than assert when you are unsure.** *"What happens if this is empty?" is faster than being wrong loudly.*
- **Explain why, and link.** *A comment that only says what to change teaches nothing and gets repeated next week.*
- **Say what is good.** *Rare enough that it is disproportionately effective, and it is the only signal an author gets about what to keep doing.*

---

## Disagreement

*How an argument ends, decided now rather than during one.*

*Most review conflict is not about the code; it is about not knowing who decides. State the escalation path and the time limit.*

1. *Author and reviewer discuss in the thread.*
2. *If unresolved after N rounds, talk in person or on a call. Text amplifies disagreement.*
3. *If still unresolved, escalate to ... The decision is recorded in the thread.*

*Two principles worth adopting explicitly. Facts and data beat opinions and preferences. And where neither side can produce evidence, the author's approach wins, because consistency is worth less than momentum.*

---

## Approving

*What approval means here, and what it does not.*

- *Approving means: you believe this improves the codebase and you accept shared responsibility for it.*
- *It does not mean you have proved it correct.*
- *Approve with unresolved nits when you trust the author to address them. Blocking on trivia is how review earns a reputation.*

**Who must review.** *How many approvals, and whether a code owner is required for particular paths. Keep the number as low as you can defend; each additional required reviewer adds latency and reduces the felt responsibility of each one.*

---

## Exceptions

*When review is skipped or shortened, agreed in advance so it is not decided under pressure.*

- *Production incident fix: merge with one approval, full review within one working day, recorded in the incident.*
- *Automated dependency bumps: ...*
- *Documentation-only changes: ...*

---

## Notes on using this template

*Delete this section too.*

**Write the parts your team argues about.** If reviews are slow, the response-time and size sections carry this document. If reviews are hostile, the comment-writing and disagreement sections do. The rest can be short.

**Automate everything you can before writing rules about it.** Every style rule enforced by a human is a rule that generates friction, delay and resentment, and it will be enforced inconsistently. Formatters and linters do this work without either.

**Measure latency, not throughput.** Time from review request to first response tells you whether the process is working. Counting comments per review does not, and rewarding it produces worse reviews.

**Where this lives:** in the repository, as `CONTRIBUTING.md` or under `docs/`. It references the style guide, the lint configuration and the CI gates, and must change with them.

---

## Related documents

- [`coding-standards.md`](coding-standards.md). What a tool checks, so a reviewer does not have to
- [`branching-strategy.md`](branching-strategy.md). What has to be true about the branch before a review can start
- [`contributing-guide.md`](contributing-guide.md). The front door that points a new contributor here
