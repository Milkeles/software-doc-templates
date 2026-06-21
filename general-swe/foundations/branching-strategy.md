# Branching Strategy

> Which branches exist, how long they live, and how a change reaches production.
>
> **Also called:** branching model, Git workflow.
>
> **This is a coordination decision, not a technical one.** The named strategies are reasoned positions published by vendors and practitioners, not findings from studies. They disagree with each other, and two of the four most-cited ones have been quietly changed or withdrawn by their own publishers. Section 6 covers what is actually measured.
>
> **Write it down because the cost of ambiguity is merge conflicts and failed releases**, both of which are expensive and both of which a half-page document prevents.
>
> **Where it lives.** In the repository it governs, next to the branch protection rules and CI config it describes. It changes when the pipeline changes.
>
> **Delete this block before publishing.**

---

## 1. Choose by how you release, not by what is popular

The release model decides the strategy. Everything else follows.

| If you release | Then you need | Which points to |
|---|---|---|
| Continuously, many times a day, one version in production | One long-lived branch, very short branches off it | Trunk-based, or GitHub Flow |
| On a cadence, one version in production at a time | One long-lived branch plus a release branch per release | Trunk-based with release branches |
| Explicit versions your users choose to install, several supported at once | A maintained branch per supported version | git-flow, or a release-branch-per-version scheme |
| To fixed environments you promote through | Environment branches merged downstream only | GitLab Flow's environment-branch pattern |

```
   TRUNK-BASED                        RELEASE-BRANCH

   o---o---o---o---o---o  main        o---o---o---o---o---o  main
        \     \     \                      \           \
         o     o     o   <2 days            o-o-o       o-o-o
        (merged same or next day)          release/1.4  release/1.5
                                                |            |
   deploy from main                        deploy, then cherry-pick
                                           fixes back to main
```

The second shape costs you one thing the first does not: every fix now has to land in two places, and the discipline about which direction it flows is the whole game. Pick it only if you genuinely support more than one version at a time.

---

## 2. Name the branches

One table. If it takes longer than a table, the scheme is too complicated.

| Branch | Purpose | Lifetime | Who may push | Protected |
|---|---|---|---|---|
| `main` | Always releasable | Permanent | Nobody directly | Yes |
| `feature/*` | One change by one person | 2 days | The author | No |
| `release/x.y` | Stabilise and ship a version | Until end of support | Release owner | Yes |
| `hotfix/*` | Production fix that cannot wait | Hours | Whoever is on call | No |

State the naming convention and the deletion rule in one line each. Branches nobody deletes become the archaeology that makes a repository unreadable.

---

## 3. Set a number for branch lifetime

The single most useful line in this document is a number, because "short-lived" is not enforceable and "two days" is.

Trunk-based development states the operational test plainly: "the branch should only last a couple of days. Any longer than two days, and there is a risk of the branch becoming a long-lived feature branch", and "the developer count should stay at one (or two if pair-programming)". Two days, one developer. If a change cannot be finished in that window, it needs to be split, or hidden behind a flag and merged incomplete.

Below roughly sixteen developers, trunk-based advocates committing straight to the trunk. Above it, they advocate short-lived branches with CI on every one. Write down which side of that line your team is on.

**The corresponding rule for long-lived branches is a merge cadence.** If you keep a release branch, say how often it takes changes from `main` and in which direction fixes flow. GitLab's environment-branch pattern permits merges downstream only, so that nothing exists in production that was never in `main`.

---

## 4. Say how a change gets in

Four decisions, each one line.

- **Merge method.** Merge commit, squash, or rebase. Squash gives one commit per change and a readable history; merge commits preserve the working history. Pick one and configure the host to enforce it, because a repository with all three is a repository with no history at all.
- **Required checks.** Which CI jobs must pass. This is where the strategy becomes real; everything above it is naming.
- **Required reviews.** How many, and whether code owners are required. Cross-reference the code review guidelines rather than restating them.
- **Who can push to protected branches**, and what the break-glass procedure is when production is down.

---

## 5. Say what happens when production is broken

The path most teams have never written down and always need at the worst moment.

State: where the hotfix branches from, what the minimum review is, whether checks can be skipped and who may authorise that, and how the fix gets back into `main` so the next release does not reintroduce the bug. That last step is the one teams forget, and it is how a fixed bug reappears two weeks later.

---

## 6. What the evidence actually says

Worth knowing before anyone argues from authority.

**The named strategies are positions, not results.** Vincent Driessen, who published git-flow in 2010, added a note of reflection on 5 March 2020 saying it "has been widely adopted" but that "people have started treating it like a standard of sorts, but unfortunately also as a dogma or panacea". His actual advice: "If your team is doing continuous delivery of software, I would suggest to adopt a much simpler workflow (like GitHub flow)", but "if, however, you are building software that is explicitly versioned, or if you need to support multiple versions of your software in the wild, then git-flow may still be as good of a fit". That is not a retraction, and anyone telling you git-flow was deprecated by its author is overstating a note that ends "consider your own context".

Two more publisher facts worth having: **GitHub's current documentation has dropped the two deployment rules** that defined GitHub Flow when Scott Chacon described it in 2011 ("anything in the master branch is deployable" and deploy before merging); the final step in GitHub's version today is "delete your branch". And **GitLab has removed its GitLab Flow documentation entirely**, with the redirect deleted in November 2025. If you are quoting either, know which year's text you are quoting.

**The correlational evidence.** DORA's 2017 State of DevOps report found high performers had branch lifetimes and integration times "typically lasting hours" against "days" for low performers, and reported the differences as statistically significant. Take the strength of that carefully. The research uses non-probability snowball sampling, self-reported Likert measures for both the predictor and the outcome, and correlation-based structural equation modelling. Jez Humble, a co-author, put the limit precisely: "we can use words like 'drives', 'predicts', and 'impacts', but not 'causes' since we're not performing a randomized, controlled experiment."

**The one repository-mining result, and it is about a different variable.** Shihab, Bird and Zimmermann mined post-release failure data from Windows Vista and Windows 7 for ESEM 2012 and found that "misalignment of branching structure and organizational structure is associated with higher post-release failure rates", with increases up to 59 percent on Vista and 70 percent on Windows 7. Their conclusion is that "branching structures should not only align according to architectural structure, but also according to its organizational structure."

The practical reading: **the strongest available evidence is not about which named strategy you pick, it is about whether your branches match your teams.** A branch two teams both work in is the shape the data flags, whatever you call your workflow.

---

## Common failures in this document

- **A named strategy copied without the release model behind it.** git-flow on a team that deploys twice a day is pure overhead.
- **"Short-lived" with no number.** Write two days, or three, or one. An adjective enforces nothing.
- **No hotfix path.** Written during the incident, at the worst possible time.
- **No rule for merging fixes back to `main`.** This is how a fixed bug ships again.
- **Three merge methods enabled.** The history becomes unreadable and the strategy is fiction.
- **A branch per team on a component every team edits.** The one pattern with measured failure data behind it.
- **Cited as evidence-based.** These are reasoned positions. Say so.

---

## Related documents

- [`code-review-guidelines.md`](code-review-guidelines.md). What has to happen on the pull request before the merge
- [`contributing-guide.md`](contributing-guide.md). Where an outside contributor learns this scheme exists
- [`changelog.md`](changelog.md). What each release branch produces
- [`release-notes.md`](release-notes.md). The same release, for people who do not read the changelog
- [`test-strategy.md`](test-strategy.md). Which checks are required, and why those
- [`runbook.md`](runbook.md). Where a rollback procedure belongs, and it is not here
