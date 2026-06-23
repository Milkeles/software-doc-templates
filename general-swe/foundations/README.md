# Foundations

Documents every software team needs, whatever it builds and however it plans work.

These twenty-five templates do not assume sprints, WIP limits, or stage gates. A Scrum team, a Kanban team, and a team building to a fixed contract all need to record why they chose PostgreSQL, what to do when the queue backs up, and what "reviewed" means.

Start here before adopting anything from a methodology group.

---

## Why write any of this down

Three reasons, and none of them is "process requires it."

**Memory of *why* decays faster than memory of *what*.** Code records what you built. Nothing records what you rejected. Six months on, the constraint that ruled out the obvious approach is gone, and the next engineer reintroduces it. This is the single strongest argument for architecture decision records, and it is why an ADR that omits the alternatives is half a document.

**Writing exposes the gaps in your own understanding.** You cannot write a clear problem statement for a problem you have not understood. Toyota's A3 sheet works this way on purpose: the paper is one size, and if the analysis will not fit, you do not yet know the problem well enough. Shape Up's fixed appetite does the same job. A design doc that took an hour to write and revealed nothing was probably not needed.

**Under stress, recall fails and checklists do not.** At 3am an on-call engineer who has been awake for twenty minutes is not the same engineer who built the system. A runbook does not exist because people are forgetful; it exists because degraded conditions degrade people. The same logic drives blameless postmortems: hindsight makes the right action look obvious, so a written timeline of what people actually knew at each moment is the only defence against rewriting history.

A fourth, quieter reason: documents move load from synchronous to asynchronous. Every question answered in a document is a question not asked in a meeting.

---

## The four properties that decide whether a document survives

Every credible source demands the same four things, whichever medium it recommends. AWS Well-Architected, Microsoft's Azure Well-Architected Framework, and *Software Engineering at Google* each independently require all four:

1. **A named owner.** Not a team. A person.
2. **A last-reviewed date visible in the document.**
3. **A review cadence**, so the date means something.
4. **One discoverable location**, so nobody has to guess which copy is current.

A document missing these will rot regardless of how well it was written. Pick the medium that makes these four cheapest for that document's audience and edit frequency. Everything in the "where it lives" column below follows from that.

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [Architecture decision record](architecture-decision-record.md) | A choice constrains future work and the reasoning will not be obvious from the code | The decision is reversible in an afternoon | Repo |
| [Technical design document](technical-design-document.md) | A change is large enough that getting the approach wrong is expensive | The solution is unambiguous | Wiki, outcome extracted to an ADR |
| [RFC](rfc.md) | A proposal needs named approvers and a decision deadline | Nobody outside the team is affected | Repo or wiki, by who must review |
| [Architecture overview](architecture-overview.md) | A newcomer, an auditor, or an incident responder needs the shape of the system | The system is one service with one datastore | Repo |
| [Service README](service-readme.md) | Always, for every deployable component | Never | Repo root |
| [Runbook](runbook.md) | An alert can fire and a human must act | The response is deterministic (automate it instead) | Repo, rendered where on-call can reach it |
| [Incident postmortem](incident-postmortem.md) | Users were affected, data was lost, or a human had to intervene | Nothing was learned and nothing was affected | Wiki or incident tool |
| [Test strategy](test-strategy.md) | The team disagrees about what to test where | One person writes all the tests | Repo |
| [Test cases](test-case-specification.md) | A person executes the check, or someone outside the team must see what was checked | The test is automated. The code is the specification | Repo, or a test management tool |
| [Bug report](bug-report.md) | Always, as a form the tracker enforces | Never | Issue tracker, template in `.github/` |
| [Test summary report](test-summary-report.md) | Someone must decide whether to ship, and it is not the person who ran the tests | The pipeline is the decision | Wiki or the release ticket |
| [Code review guidelines](code-review-guidelines.md) | Reviews are inconsistent or slow, or the team is growing | Two people who already agree | Repo |
| [Branching strategy](branching-strategy.md) | More than one person merges, or you support more than one released version | One person, one branch | Repo, beside the CI config |
| [Coding standards](coding-standards.md) | A tool cannot enforce the rule and the argument keeps recurring | The formatter already settled it | Repo, beside the lint config |
| [Contributing guide](contributing-guide.md) | People outside the team send changes | Nobody outside the team can push | Repo, as `CONTRIBUTING.md` |
| [Onboarding guide](onboarding-guide.md) | You will hire again | You will not | Split: setup in repo, org context in wiki |
| [Changelog](changelog.md) | Anyone consumes your releases, including other teams | Nothing outside the repo depends on you | Repo root |
| [Release notes](release-notes.md) | Non-technical users need to know what changed | Your only users read the changelog | Product site or in-app |
| [Threat model](threat-model.md) | You handle credentials, money, personal data, or untrusted input | A prototype with no real data | Repo, beside the design |
| [Glossary](glossary.md) | The same word means different things to different teams | Everyone shares vocabulary already | Repo |
| [Deprecation plan](deprecation-plan.md) | Someone depends on something you intend to remove | Nobody outside the team calls it | Repo, announced widely |
| [Deployment plan](deployment-plan.md) | A release is irreversible, coordinated, or needs a window | The pipeline deploys on green | The release ticket |
| [Configuration management plan](configuration-management-plan.md) | You cannot say what is running in production and who approved it | Tooling already answers that | Repo, or wiki for a programme |
| [Interface control document](interface-control-document.md) | An interface crosses a boundary you cannot change unilaterally | Both sides are yours | Repo both parties read, beside the schema |
| [Data model](data-model.md) | People disagree about what an entity means, or two services write the same table | One service, one obvious schema | Repo, beside the migrations |

---

## How these documents feed each other

Twenty-five documents is enough to duplicate badly. The defence is one rule: **every fact lives in exactly one document, and the others link to it.** The map below is where the facts live.

**A decision, from proposal to current state.**

```
   technical design doc  \
                          >---> ADR ------------> architecture overview
   RFC                   /       |                        |
                                 |                        |
                        why we chose it,          what the system is
                        one per decision,         now, edited freely,
                        never edited after        no history kept
                        it is accepted
```

The design doc and the RFC are working documents that stop mattering the day the decision is made. The ADR is the residue: the constraint, the alternatives, the reason. The overview describes the result. Those last two split along tense, and that split is the whole reason both exist. An ADR is a dated statement about the past and is superseded rather than rewritten. An overview is a statement about the present and is wrong the moment it is stale.

**An ADR with no matching overview update leaves the overview lying.** An overview with no ADRs behind it can describe the system but cannot explain it, which is the state most teams are actually in.

**A running service, from ship to incident and back.**

```
   architecture overview ---> service README ---> runbook
                                                     |
                                       alert fires   |
                                                     v
                                                 incident
                                                     |
                                                     v
                                                postmortem
                                        /            |             \
                                       v             v              v
                                  runbook           ADR         test strategy
                                new or fixed   if the fix     if the gap was
                                    step       overturns a      coverage
                                               decision
```

The arrows out of the postmortem are the part teams skip, and skipping them is what makes postmortems feel like paperwork. A postmortem whose actions live only inside the postmortem has changed nothing. The finding belongs in whichever document would have prevented the incident, and the postmortem links to it.

**Anything anyone else depends on.**

```
   deprecation plan ---> changelog ---> release notes
        |                                    |
   for consumers you            for people who did not
   can name and must            read the changelog and
   warn directly                should not have to
```

The changelog is a fact record for people integrating with you. Release notes are written for someone who does not know your internals. Same event, two audiences, two documents, and merging them produces one that serves neither.

**How a change gets in.** Four documents describe one path, and each answers a different question about it.

```
   contributing guide ---> branching strategy ---> coding standards
        |                        |                       |
   where do I start,      what do I branch        what will the
   who do I ask,          from, how long          checks reject
   what is the rule       may it live
                                 \                      /
                                  v                    v
                            code review guidelines
                                        |
                            what a human decides,
                            and the bar for approval
```

The split is by enforcement. The coding standards hold what a tool checks; the review guidelines hold what only a person can. Merging them produces a document where nobody can tell which rules block a merge. The branching strategy holds the mechanics, and the contributing guide is the front door that links to all three without repeating any of them.

**What testing produces.** Four documents, and the split is by tense.

```
   test strategy ------> test cases -------> test summary report
        |                     |                      |
   standing rules,      what we decided        what we found,
   written once,        to check, before       written after,
   argued rarely        the run                read once
                              |
                        a case fails
                              |
                              v
                        bug report ---> incident postmortem
                                        if it reached production
```

The strategy is durable and answers "what do we test". The cases are the checks themselves. The summary report is a record of one cycle and is never edited afterwards. A team that keeps only the strategy has rules nobody executed; a team that keeps only reports has a history with no reason behind it.

**The bug report is the odd one.** It is the only document here that people outside the team write, often in a hurry, often once. That is why its design is a tracker form rather than a page, and why the measured way to improve reports is to change the form rather than to ask people to try harder.

**How a change reaches production.** The change is in; this is what carries it out.

```
   configuration management plan
      what counts as a release,
      what is under control,
      who may approve
              |
              v
      deployment plan ------> changelog ------> release notes
      one release, once           |
              |                   v
              |             interface control document
              |             if the release changes an
              |             agreement someone relies on
              v
        incident postmortem
        when it does not go well
```

The configuration management plan is standing and answers "what is a release here". The deployment plan is single-use and answers "how does this one go out". Teams that write only the second re-derive the first every time, inconsistently.

**The two documents that describe structure rather than events.** The data model and the interface control document say what the system's data means and what crosses its boundaries. Both are consulted rather than read, both go stale silently, and both are worth writing only where more than one team has an opinion.

**The two that sit outside every flow.** The glossary and the code review guidelines are not produced by any event. They exist because a disagreement kept recurring, and they are written the second or third time it recurs, not in advance.

---

## Four modes, and why mixing them ruins a document

Daniele Procida's [Diátaxis](https://diataxis.fr/) framework splits documentation along two axes: practical against theoretical, and study against work. That gives four modes.

| | Practical | Theoretical |
|---|---|---|
| **At study** | Tutorial: learning | Explanation: understanding |
| **At work** | How-to guide: a goal | Reference: information |

Diátaxis was written for product documentation, not for internal engineering artefacts. The extension below is ours, not Procida's, but it explains the most common failure in this group.

- **Explanation:** architecture decision records, the rationale sections of an RFC, the lessons in a postmortem. Answers *why*.
- **Reference:** architecture overviews, API contracts, glossaries. Consulted, not read.
- **How-to:** runbooks, onboarding setup steps. For someone already competent, trying to finish something.
- **Tutorial:** a guided first change for a new hire. Rare, and its absence is usually the real onboarding problem.

**A document that tries to be all four is bad at all four.** A runbook interrupted by paragraphs explaining the architecture is a worse runbook, because at 3am the reader is scanning for the next command. An architecture overview that drifts into justifying past choices stops being consultable. This is exactly why arc42 puts architecture decisions in their own chapter instead of scattering rationale through the structural chapters.

When a section feels wrong, check whether it belongs to a different mode. Usually it does. Link to it instead of inlining it.

---

## The documents, one by one

### Architecture decision record

**When.** Write one when a decision constrains what future engineers can do and the reasoning will not survive in the code. Choosing a database, a message format, an auth model, a directory convention that everyone must follow. The test is not importance, it is *irreversibility*: if undoing it costs a week, record it.

**Why.** Code shows the chosen path. It cannot show the three paths you rejected or the constraint that eliminated them. Without that, later engineers either repeat the analysis or, worse, "fix" the decision and rediscover the constraint in production. ADRs are also the cheapest onboarding document per minute spent: a new engineer reading twelve ADRs in order learns more about a system than from any overview, because they learn the tensions rather than the shape.

**Where.** In the repository, `docs/decisions/`. Michael Nygard specified the repo in the [original 2011 formulation](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions), and ThoughtWorks put lightweight ADRs in the Adopt ring of its Technology Radar specifically recommending source control "rather than wikis or websites," so the record stays in sync with the code. ADRs are short and append-only, which is what git handles best and what wikis handle worst.

One caveat: a decision spanning many repositories has no natural home in any one of them. Keep a central decision log for those and link to it.

### Technical design document

**When.** Before writing code for a change where getting the approach wrong is expensive. Roughly ten to twenty pages for a large project, one to three for anything smaller. If the design has no trade-offs worth discussing, you are writing an implementation manual and should stop.

**Why.** The value is in the review, not the artefact. A design doc puts the combined experience of the organisation in front of a decision while changing it is still cheap. It also forces the author to state non-goals, which is where most scope disputes actually live.

**Where.** A wiki or collaborative document tool, then link it from the repository. This is the one document in this group where the primary source points away from the repo. Google keeps design docs in Google Docs because the value concentrates in comment threads during review, and, as Malte Ubl [describes](https://www.industrialempathy.com/posts/design-docs-at-google/), they are usually not updated after the system ships. A document that stops tracking the code has no reason to sit next to it.

Extract the durable decisions into ADRs in the repo. Leave the deliberation in the wiki.

### RFC

**When.** A proposal affects people outside the team, or needs a decision by a date, or needs a record that specific people agreed. Rust's process is the clearest public model: a template, a set of named approvers, and a ten-day final comment period.

**Why.** An RFC differs from a design doc in one respect that matters: it has a **defined decision procedure and a defined set of deciders**. A design doc has reviewers. An ADR records a decision made elsewhere. If your "RFC process" has no named approvers and no time limit on comments, you have a design doc with a fashionable name, and it will stall.

Note that the naming is not settled in the industry. Several well-known engineering organisations use "RFC" and "design doc" interchangeably. Define the term inside your own organisation and stop worrying about it.

**Where.** Either, decided by who must participate. Rust and Oxide run entirely in git pull requests and get versioning, line comments, and an auditable approval trail free. That only works if every required reviewer uses pull requests. If product, legal, or design must sign off, use the wiki. The tool is not the important part; the named approvers and the deadline are, and no tool supplies those.

### Architecture overview

**When.** The system has more than a couple of moving parts and someone outside it needs to understand the shape: a new hire, an auditor, an incident responder, a team that wants to integrate.

**Why.** Everyone builds a mental model of the system anyway. Without a shared picture, each model is different, and the differences only surface during an incident. This document also gives ADRs somewhere to attach: arc42 reserves chapter 9 for architecture decisions rather than defining a decision format, which is exactly the right split. The overview holds the structure; ADRs hold the reasoning.

**Where.** In the repo, as text, rendered to HTML in CI. Diagrams belong in a text format (Structurizr DSL, PlantUML, Mermaid) for the same reason: an exported PNG in a wiki cannot be diffed, cannot be reviewed alongside the change that invalidated it, and will never be regenerated.

### Service README

**When.** Every deployable component, from day one.

**Why.** It is the first thing anyone reads and the last thing anyone updates. A service README that answers "what is this, how do I run it, who owns it, where does it break" removes the majority of interruptions a team receives. It is the cheapest document in this group by a wide margin.

**Where.** Repository root. Nowhere else is defensible.

**Note.** This template assumes a team-owned service with on-call behind it. A public library or tool needs a different shape: install steps, a usage example, and a license, not an owner-and-tier table. See the note at the top of the template.

### Runbook

**When.** An alert can fire and a human must decide something. If every alert has a documented response, on-call becomes a job that can be handed over. If it does not, on-call is a job only the author can do.

**Why.** Google reports roughly a threefold improvement in mean time to recovery from having procedures recorded in advance rather than improvising, though that figure is a company claim with no published method. The mechanism is not in dispute: under time pressure and sleep deprivation, people skip steps and misremember thresholds.

Two honest caveats. First, if the runbook is a deterministic list of commands, delete it and automate it. Second, there is real disagreement here: Charity Majors argues that in modern distributed systems you rarely see the same failure twice, so observability beats pre-written procedure for the unknown cases. The counterargument is that runbooks are how institutional knowledge survives on-call turnover. Both are right about different failures. Write runbooks for the recurring and the procedural; invest in observability for the rest.

**Where.** Source in the repo so it versions with the system and passes through review. Render it somewhere on-call can reach without the systems it describes. Link the rendered page directly from the alert. A runbook you can only reach through the service that is down is not a runbook.

Also: update it during the incident, while you still remember. A second person should be able to execute it without asking you anything. If they cannot, it is not finished.

### Incident postmortem

**When.** User-visible degradation past a threshold you set in advance, any data loss, any human intervention such as a rollback or traffic reroute, a resolution time above a threshold, or a monitoring failure. Any stakeholder can also request one. Decide the triggers before you need them, or every postmortem becomes a negotiation.

**Why.** Two forces work against learning from incidents, and the document exists to counter both.

Hindsight bias makes the correct action look obvious after the fact, which makes the responders look careless. A timeline recording what was known at each moment, not what was true, is the defence.

The fundamental attribution error pushes readers to explain the outcome by the character of the people involved rather than the conditions they faced. This is why "root cause" is contested. PagerDuty removed the phrase from its template in favour of **contributing factors**, arguing that "very rarely is the mistake rooted in a human performing an action." Google keeps the heading but pluralises it and simultaneously talks about contributing causes. John Allspaw goes further and rejects the causal model itself, arguing that asking "why?" repeatedly leads to "who?", and proposing "how?" prompts instead.

The template here defaults to *contributing factors* with *trigger* kept separate, and explains the disagreement rather than hiding it.

**Where.** A wiki or incident management tool. Not the repo. A postmortem is a dated record with a lifecycle (draft, in review, reviewed, closed), a scheduled meeting, comment threads, and a company-wide readership. Git does versioning; it does not do discussion or discovery. Action items live in the issue tracker with an owner and a number, not in the document body, where nobody will look at them again.

Publish within a week. A postmortem published four months later is an archive entry, not a learning tool.

### Test strategy

**When.** The team disagrees about what belongs at which level, or new joiners keep writing the wrong kind of test, or the suite is slow and nobody knows which layer to cut.

**Why.** The strategy exists to make one argument explicit: what a test at each level costs and what confidence it buys. The famous shapes are downstream of that argument, not upstream. Martin Fowler states the pyramid's premise plainly, that broad-stack tests are "expensive, slow, and brittle compared to more focused tests," and adds "while this is usually true, there are exceptions." Kent C. Dodds' testing trophy pushes weight toward integration tests, and scopes his own claim narrowly to front-end JavaScript, where tooling made those tests fast and stable.

This is a context dispute, not a contest between universal truths. The template asks your team to write down its own cost and confidence assumptions instead of copying a shape.

Note also that a test strategy and a test plan are different documents. In [ISTQB](https://istqb-glossary.page/test-strategy/) terms, a strategy is organisation- or programme-wide and durable; a plan is project-scoped and carries a schedule and resources. The schedule is the cleanest way to tell them apart. The plan lives in `waterfall/`, where fixed scope makes it useful.

**Where.** In the repo it governs. A test strategy constrains CI configuration and must change with the pipeline.

### Test cases

**When.** A person executes the check by hand, or someone outside the team must later see what was checked. Automated tests do not get a second description in prose; the code is the specification and a copy of it will drift.

**Why.** Not to find more defects, because the evidence says they do not. Itkonen and Mantyla ran a controlled replication with 51 participants on the jEdit editor, having previously run it with 79, and confirmed three findings: "there is no difference in the defect detection effectiveness between ET and TCT", exploratory testing "is more efficient by requiring less design effort", and predesigned test cases "produce more false-positive defect reports". Time spent designing cases in advance buys no additional defects.

The reason to write them anyway is in the same paper: "we recognize that TCT has other benefits over ET in managing and controlling testing in large organizations." Cases exist so that testing can be delegated, audited, repeated on a schedule, and handed over when a person leaves. Those are real needs, and none of them is defect detection.

Which makes the honest instruction unusual: write as few as you can justify, and charter exploratory sessions for everything else. The template's first section is a decision table for exactly that.

The failure mode the same study names is abstraction level. Cases pinned to button positions break on every redesign and stop being run; cases written as "try an invalid input" are executed differently by two people, so a pass means nothing.

**Where.** In the repo beside the tests if they are executable or heading for automation. In a test management tool if results must be recorded per build and shown to someone outside the team. Split across both, the two lists disagree within a release.

### Bug report

**When.** Always, and as a form the tracker enforces rather than a page people are asked to read.

**Why.** This is the best-measured document in the group. Bettenburg and colleagues surveyed 466 people across Apache, Eclipse and Mozilla for FSE 2008, then mined 150,000 reports. Developers ranked steps to reproduce highest at 83 percent, stack traces at 57 percent, test cases at 51 percent. Reporters ranked test cases hardest to supply at 75 percent, steps to reproduce at 51 percent.

The finding that should change your behaviour is the correlation between what developers consider important and what reporters actually provide: **-0.035**, which the authors call a huge gap. But the correlation between what developers consider important and what reporters *believe* is important is **0.839**. Their conclusion: "ignorance of reporters is *not* a reason for the aforementioned information mismatch [...] to a large extent, lacking tool support causes this mismatch."

So the intervention is the form, not the etiquette guide. Make the field required, attach the trace automatically, and stop writing prose asking people to try harder.

Two received ideas do not survive the same study. Duplicates were named a problem by only 10 percent of developers, against 79 percent for errors in the steps to reproduce; the authors write that "duplicates are not really problems. They often add useful information." And report quality is statistically independent of time to fix, at correlations between 0.002 and 0.068, so time-to-close cannot be used as a quality measure.

**Where.** The issue tracker, with the template file in `.github/ISSUE_TEMPLATE/` so the form versions with the code.

### Test summary report

**When.** A person who did not run the tests has to decide whether to ship. If the pipeline makes that decision, you do not need this document.

**Why.** To convert activity into a decision. The report's real content is not counts but claims: which areas you now have confidence in, on what basis, and which have none. The rows that read "not covered" are the ones the reader needs, because an area with no row is read as an area that passed.

Two numbers must be handled carefully. Coverage is not a quality target: Inozemtseva and Holmes generated 31,000 test suites over five systems of up to 724,000 lines, evaluated them by mutation testing, and concluded that coverage "should not be used as a quality target because it is not a good indicator of test suite effectiveness". And session metrics are gameable, which Jonathan Bach said first when he introduced them: a biased manager or a "silver-tongued tester" can distort both the sheets and the debrief.

Where exploratory testing is the main activity, session-based test management gives this report a unit. A session is "an uninterrupted block of reviewable, chartered test effort", roughly ninety minutes, about three per tester per day. Bach's measured breakdown on real work is the number worth carrying into any plan: 61 percent of time went to non-session work, 28 percent to testing, and the rest to setup, bug investigation and opportunity testing.

**Where.** The wiki or the release ticket. It is written once, read around a decision, and then consulted as a record. Its readers frequently do not clone the repository.

### Code review guidelines

**When.** Reviews take days, or block on style arguments, or vary wildly by reviewer. Also whenever the team is about to grow, because unwritten norms do not scale past the people who invented them.

**Why.** Most review friction comes from an unstated question: what is the bar? Google answers it directly: approve once the change "definitely improves the overall code health of the system," even if it is not perfect, "because there is no such thing as perfect code, there is only better code." Writing that down converts an argument about taste into an argument about a stated principle, which is a much shorter argument.

The second thing guidelines buy is speed, and speed is a team property. Google's rule is that one business day is the maximum time to respond, and its stated reason is that it optimises team velocity over individual velocity. An engineer who reviews quickly is slower personally and the team ships faster.

On review size, the most cited numbers come from a Cisco study of 2,500 reviews published by SmartBear: 200 to 400 lines per sitting, no more than 60 minutes, defect discovery of 70 to 90 percent in that range. Treat those with the caveat attached. The study is vendor-funded, not peer-reviewed, and twenty years old. It is nonetheless directionally consistent with Google's independent guidance that 100 lines is reasonable and 1,000 is usually too large.

**Where.** In the repo under `docs/`, linked from `CONTRIBUTING.md` rather than pasted into it. The guidelines reference the coding standards and the lint configuration, and must move with them.

### Branching strategy

**When.** More than one person merges to the same repository, or you support more than one released version at a time. Below that, the strategy is "commit to main" and does not need a document.

**Why.** The named strategies are reasoned positions from vendors and practitioners, not results, and treating them as more than that is how teams end up running git-flow while deploying twice a day. Vincent Driessen said as much about his own model in 2020: people "started treating it like a standard of sorts, but unfortunately also as a dogma or panacea", and his advice was to use something simpler under continuous delivery and keep git-flow only for explicitly versioned software.

The strongest available evidence is not about which model you pick. Shihab, Bird and Zimmermann mined post-release failure data from Windows Vista and Windows 7 for ESEM 2012 and found that misalignment between branching structure and *organisational* structure was associated with higher failure rates, by up to 59 and 70 percent respectively. DORA's correlation between short branch lifetimes and delivery performance is real but self-reported and non-causal; Jez Humble, a co-author, states the limit himself.

So the document's job is to fix a number for branch lifetime, name a hotfix path, and make sure no branch is shared by two teams. Those are the parts that pay.

**Where.** In the repo, next to the branch protection settings and CI configuration it describes.

### Coding standards

**When.** A rule cannot be enforced by a formatter or a linter, and the argument about it keeps recurring. If a tool can settle it, configure the tool and write nothing.

**Why.** Almost every rule in a style guide is a coordination convention rather than a finding, and Google says so about its own: the conventions are "sometimes arbitrary". That is not a weakness, since coordination is genuinely worth paying for, but a guide that claims evidence it does not have loses the argument with the first person who checks.

Very little survives checking. The recommendation of 2 to 4 space indentation traces to a single 1983 Pascal study, and the one modern eye-tracking replication found no effect. Comments help by between negative 30 and positive 34 percent depending on the snippet. Developers' stated preferences and their measured reading effort point in opposite directions in both recent studies. Two rules do hold up: **descriptive full words beat abbreviations**, measured on professionals doing defect-finding, and **restyling old code is not worth it**, which the eye-tracking work states directly.

There is also a real disagreement to resolve rather than paper over. PEP 8 says consistency within a module beats consistency with the guide. Google says the opposite, and gives a mechanism: at 100 million lines, uniformity is what makes automated refactoring possible. Which one is right for you depends on whether you run automated changes across repositories.

**Where.** In the repo, in the same commit as the lint configuration. Separated, they drift within a quarter.

### Contributing guide

**When.** People who do not work on the project every day send changes. That includes other teams inside your company, not only outside contributors.

**Why.** It is a router. All five of kubernetes, rust, node, django and Homebrew keep the file between 1 and 4 KB and use it to point at the real documentation, because a complete guide in this position does not get read.

Be careful about what it achieves. No study measures whether adding the file converts more first-time contributors. What is measured is narrower: Steinmacher and colleagues found 58 distinct newcomer barriers, most of them not documentation, and their guided portal "played an important role in guiding newcomers and in lowering barriers related to the orientation and contribution process, whereas it was not effective in lowering technical barriers". Write it to answer "what happens next and who do I ask", and expect nothing from it on the difficulty of the code itself.

The filename matters more than it should. GitHub only shows the Contributing link on the issue and pull request pages when the file is named `CONTRIBUTING`, in the root, `.github/`, or `docs/`.

**Where.** The repository root by default, because that is where people look without being told.

### Onboarding guide

**When.** Before the next hire, not during. The best moment to fix an onboarding document is the first time someone uses it, so make "improve the doc you just followed" an explicit first-week task.

**Why.** The Microsoft study of onboarding in software teams (An Ju et al., ICSE 2021, 32 new developers and 15 managers interviewed, plus 226 survey responses) found the newcomer's experience is driven by the **tasks** they are given, working through learning, confidence, and socialisation, not by the reading material. That is the argument for a first-task section rather than a link farm.

A first-week production change is a test of the document, not a rite. If a new hire cannot reach production by following your instructions, the instructions are broken, and you now know it in week one instead of month three. Google separates the onboarding mentor from the reporting line deliberately, so that admitting confusion carries no cost.

**Where.** Split it. Environment setup, first-change walkthrough, and the architecture tour go in the repo, where they pass through review and break loudly when the build changes. Team norms, who to ask, and organisational context go in the wiki, where they change without a pull request.

### Changelog

**When.** Anything outside the repo consumes your releases, including other teams inside your company.

**Why.** [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) states the point in one line: "Changelogs are for humans, not machines." A generated commit log is not a changelog, because it is full of merge commits, obscure titles, and documentation-only changes. The curation is the work.

The convention names six categories: Added, Changed, Deprecated, Removed, Fixed, Security. Use those names exactly. Consumers who know the convention can scan for the two that matter to them.

Note that Keep a Changelog describes itself as its author's considered opinion and answers "is there a standard changelog format?" with "not really." It is a very widely adopted convention, not a standard. It also pairs with [Semantic Versioning](https://semver.org/), which has a precondition most teams skip: SemVer requires a declared public API. Without one, "backward incompatible" has no meaning and your major version numbers are decoration.

**Where.** `CHANGELOG.md` at the repository root, generated at release time from the repo.

### Release notes

**When.** Non-technical people need to know what changed. Customers, support staff, sales, internal users of a platform.

**Why.** A changelog and release notes have different readers and therefore different content. The changelog says what changed. Release notes say what you can now do and why you would care. Support staff reading a changelog cannot answer a customer question; customers reading a changelog do not know which entries affect them.

There is no normative source for this split, only consistent industry practice. The defensible chain is: git log, curated into a changelog, curated again into release notes.

**Where.** Product site, documentation portal, in-app, or email. Not the repo, because the audience is not in the repo and the content needs images and review by people who do not write code.

### Threat model

**When.** The system handles credentials, money, personal data, or input from anyone you do not control. Do it at design time, per feature, and again when the design changes.

**Why.** The [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org/) reduces the whole activity to four questions: what are we working on, what can go wrong, what are we going to do about it, and did we do a good enough job. That framing matters because it makes the exercise finishable. Most threat models fail by trying to be complete.

The Manifesto names the failure modes directly. **Perfect Representation** is the belief that the diagram must be exhaustive before analysis can start. **Admiration for the Problem** is enumerating threats without deciding responses. **Hero Threat Modeler** is one specialist doing it for everyone, which produces a document the team does not believe.

Use STRIDE to generate the threats. Carnegie Mellon's SEI, surveying twelve methods, calls it "currently the most mature threat-modeling method." Alternatives exist (LINDDUN for privacy, PASTA for risk-centric work) and the template names them.

One page per feature, revisited at each design change, beats a forty-page artefact produced once. The Manifesto values "dialog over documents"; the document records the dialog, it does not replace it.

**Where.** In the repo, beside the design it covers, so that a design change and its threat model move in one commit. Restrict access to the path if the content is sensitive.

### Glossary

**When.** The same word means different things to different teams. "Account", "user", "order", "active", and "delivered" are the usual offenders.

**Why.** Ambiguous vocabulary produces bugs that look like logic errors. Two services agree they exchange an "order" and disagree about whether a cancelled one still counts. The glossary is cheap insurance and doubles as the shared language the domain model should use. arc42 makes it chapter 12 for this reason.

**Where.** In the repo, next to the architecture overview. It is reference material and must move with the model it describes.

### Deprecation plan

**When.** You intend to remove something someone else depends on. An endpoint, a field, a library version, a whole service.

**Why.** Deprecations fail for a predictable reason: the announcement reaches people who were not looking for it. A plan forces you to answer the three questions consumers actually have, which are what replaces this, by when must I move, and what breaks if I do not. It also forces you to find out who depends on you, which is usually the moment the plan changes.

**Where.** In the repo as the durable record, and announced through whatever channel your consumers already read. Mark the deprecation in the changelog under `Deprecated` at announcement and under `Removed` at removal, so a consumer scanning versions sees both.

### Deployment plan

**When.** Rarely, and that is the point. Write one when a release contains something irreversible, needs coordination with another party, requires a window, or must be approved outside engineering. If you ship on green several times a day, the pipeline is the plan.

**Why.** To make three decisions while everyone is calm: what has to be true before starting, what counts as failure, and who may call a rollback without asking permission. Under pressure those decisions get made badly or not at all.

The section that earns the document is the list of things that cannot be rolled back. Code rolls back. Data, sent emails and third-party state do not. A team that has not written that list believes it has a rollback plan when it has half of one.

Where canarying is used, be specific. Google's SRE workbook names three requirements, and the one teams miss is "integration of the canary evaluations into the release process": a canary judged by a person glancing at a dashboard is not integrated into anything. Two of its warnings are worth carrying: compare against a concurrent control rather than yesterday, because "time is one of the biggest sources of change in observed metrics", and keep the metric list short, because "too many metrics can bring diminishing returns".

**Where.** With the release ticket. It is dated and single-use. The repeatable procedure it references is a runbook and belongs in the repo.

### Configuration management plan

**When.** You cannot answer, from tooling alone, what is running in production and who approved it. Also whenever a contract or regulator requires the answer in writing.

**Why.** IEEE Std 828-2012 is the most complete published statement of what belongs in this plan, and its most useful sentence is the first line of the normative annex: "The CMP shall include the following either by reference to another document that is a CI or within itself." Everything may be a link, provided the linked thing is itself version-controlled. That is a licence to write one page instead of forty, and it is the difference between a plan that stays true and one that describes a pipeline as it was two years ago.

Treat the standard as a checklist of questions rather than a document structure. Most teams need three of its sections: what is under control, who approves changes, and how anyone finds out what is running.

The gap worth naming is runtime configuration. Traditional configuration management was built for source and deliverables, while the thing that most often changes production behaviour unnoticed is a config value or a feature flag toggled in a console. If those are not in the plan, it is not describing your system.

Note that IEEE lists 828-2012 as Inactive-Reserved. Use it for its content, not as a current mandate.

**Where.** In the repo when it governs one team, because it must change in the same commit as the branch protection and pipeline it describes. In the wiki when it spans several teams and suppliers. Never both.

### Interface control document

**When.** An interface crosses a boundary you cannot change unilaterally: another team with its own roadmap, another company, a contract, or consumers you cannot enumerate. Between two services owned by one team, the schema is enough.

**Why.** IEEE 828 states the reason better than any modern source: "Interfaces represent 'agreements' between different development efforts [...] each interface represents at least three CIs: the interface specification itself, and components on either side of the interface." The specification is a versioned artefact owned jointly, not documentation belonging to the provider. Teams that treat it as the provider's own reference are the teams whose consumers find out about breaking changes in production.

Write the machine-readable schema first. This document holds only what a schema cannot express: who owns each side, what each error means and whether retrying is safe, ordering and delivery guarantees, rate limits, how much notice a breaking change gets, and what happens to the data. Those are what actually break integrations.

On verification, know the boundary. Consumer-driven contract testing is the better mechanism where you can enumerate your consumers, and its authors scope it exactly that way: it "is applicable in the context of either a single enterprise or a closed community of well-known services". If your consumers are anyone with an API key, you cannot collect their contracts, and a published document with a real notice period is the mechanism you have.

**Where.** A repository both parties can read, versioned with the schema, published where consumers actually look. Behind your own SSO, for an external consumer, is the same as unwritten.

### Data model

**When.** People disagree about what an entity means, or two services write the same table, or a newcomer cannot tell which of four tables is authoritative.

**Why.** The migrations already hold the columns. What they cannot hold is meaning, and meaning is what the arguments are about.

Chen's 1976 paper is still the clearest guide to keeping the levels apart. He separates "information concerning entities and relationships which exist in our minds" from the information structure that represents them, and from access-path-dependent storage. Most data modelling disputes are two people arguing at different levels, one asking what a customer is and the other asking about an index.

Two of Chen's smaller points settle recurring arguments. Attributes can belong to a relationship rather than to either entity, and his example is the one teams still get wrong. And whether something is an entity or a relationship "is a decision which has to be made by the enterprise administrator [...] so that the distinction is suitable for his environment", not a fact to be discovered. Recording which way you decided ends the argument permanently.

The section teams omit is what is currently mid-change. Evolutionary database design handles a breaking change with a transition phase where "the database supports both the old access pattern and the new ones simultaneously". During that window the model has two shapes, and a document showing one of them is wrong.

**Where.** In the repo beside the migrations, because it is only true relative to a schema version. Render a copy where analysts and support staff can read it without cloning.

---

## What to write first

If you have none of these, write them in this order:

1. **Service README**, for each service. An hour each, and it stops the most interruptions.
2. **Runbook**, for your noisiest alert. One alert, not all of them.
3. **Architecture decision record**, starting with the next decision you make, not the backlog of past ones. Retrofitting ADRs is a project; adopting them is free.
4. **Incident postmortem**, the next time something breaks.

Everything else can wait until you feel its absence. A document written before anyone missed it is a guess about what people will need.

---

## Sources

The claims above come from these. Where they disagree, the disagreement is stated rather than resolved.

- Nygard, [Documenting Architecture Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) (2011); [MADR](https://adr.github.io/madr/); ThoughtWorks Technology Radar, [Lightweight ADRs](https://www.thoughtworks.com/radar/techniques/lightweight-architecture-decision-records)
- Ubl, [Design Docs at Google](https://www.industrialempathy.com/posts/design-docs-at-google/); [Rust RFC process](https://github.com/rust-lang/rfcs); [Oxide RFD 1](https://rfd.shared.oxide.computer/rfd/0001)
- [arc42](https://arc42.org/overview); Brown, [C4 model](https://c4model.com/); Procida, [Diátaxis](https://diataxis.fr/)
- [Google SRE Book](https://sre.google/sre-book/table-of-contents/) and [SRE Workbook](https://sre.google/workbook/table-of-contents/), on runbooks, postmortems, and on-call onboarding
- [PagerDuty incident response documentation](https://response.pagerduty.com/)
- AWS Well-Architected [OPS07-BP03](https://docs.aws.amazon.com/wellarchitected/latest/framework/ops_ready_to_support_use_runbooks.html) and [OPS07-BP04](https://docs.aws.amazon.com/wellarchitected/latest/framework/ops_ready_to_support_use_playbooks.html); [Azure Well-Architected OE:02](https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/formalize-operations-tasks)
- Allspaw, [The Infinite Hows](https://www.oreilly.com/radar/the-infinite-hows/)
- Winters, Manshreck and Wright, *Software Engineering at Google*, chapters [3](https://abseil.io/resources/swe-book/html/ch03.html), [10](https://abseil.io/resources/swe-book/html/ch10.html) and [11](https://abseil.io/resources/swe-book/html/ch11.html)
- [Google engineering practices](https://google.github.io/eng-practices/) on code review
- Fowler, [TestPyramid](https://martinfowler.com/bliki/TestPyramid.html); Vocke, [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html); Dodds, [The Testing Trophy](https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications)
- Ju, Sajnani, Kelly and Herzig, [A Case Study of Onboarding in Software Teams](https://arxiv.org/abs/2103.05055), ICSE 2021
- [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); [Semantic Versioning](https://semver.org/)
- [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org/); [OWASP Threat Modeling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html); SEI, [Threat Modeling: 12 Available Methods](https://www.sei.cmu.edu/blog/threat-modeling-12-available-methods/)
- Driessen, [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) and its March 2020 note; Hammant, [Trunk Based Development](https://trunkbaseddevelopment.com/); Chacon, [GitHub Flow](https://scottchacon.com/2011/08/31/github-flow.html) (2011), against GitHub's current [flow documentation](https://docs.github.com/en/get-started/using-github/github-flow)
- Shihab, Bird and Zimmermann, "The Effect of Branching Strategies on Software Quality", ESEM 2012, 301-310; DORA, [2017](https://dora.dev/research/) and 2019 State of DevOps reports, read with their methodology appendices
- Steinmacher, Conte, Gerosa and Redmiles, "Social Barriers Faced by Newcomers Placing Their First Contribution in Open Source Software Projects", CSCW 2015; Steinmacher, Conte, Treude and Gerosa, "Overcoming Open Source Project Entry Barriers with a Portal for Newcomers", ICSE 2016; [GitHub Open Source Survey 2017](https://opensourcesurvey.org/2017/)
- [PEP 8](https://peps.python.org/pep-0008/); [Google Style Guides](https://google.github.io/styleguide/); [Linux kernel coding style](https://www.kernel.org/doc/html/latest/process/coding-style.html); [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/about.html); [Developer Certificate of Origin 1.1](https://developercertificate.org/)
- Binkley, Davis, Lawrie, Maletic, Morrell and Sharif, "The impact of identifier style on effort and comprehension", *Empirical Software Engineering* 18(2) (2013), 219-276; Miara, Musselman, Navarro and Shneiderman, "Program indentation and comprehensibility", *CACM* 26(11) (1983), 861-867; Bauer, Siegmund, Peitek, Hofmeister and Apel, "Indentation: Simply a Matter of Style or Support for Program Comprehension?", ICPC 2019
- Bettenburg, Just, Schröter, Weiss, Premraj and Zimmermann, "What Makes a Good Bug Report?", FSE-16 (2008), 308-318
- Itkonen and Mäntylä, "Are Test Cases Needed? Replicated Comparison between Exploratory and Test-Case-Based Software Testing", *Empirical Software Engineering* 19(2) (2014), 303-342; Itkonen, Mäntylä and Lassenius, "Defect Detection Efficiency: Test Case Based vs. Exploratory Testing", ESEM 2007
- Inozemtseva and Holmes, "Coverage Is Not Strongly Correlated With Test Suite Effectiveness", ICSE 2014, 435-445
- Bach, J., "Session-Based Test Management", *STQE* 2(6) (November 2000), 32-37
- [ISO/IEC/IEEE 29119-3:2021](https://www.iso.org/standard/79429.html), read as far as the free preview allows; IEEE Std 829-2008, front matter; Bach, J. (James), [How Not to Standardize Testing](https://www.satisfice.com/blog/archives/1464) (2014) and Bolton, [ISO 29119 FAQ](https://developsense.com/blog/2014/09/iso-29119-questions-and-answers) (2014), for the objections to it
- IEEE Std 828-2012, *Standard for Configuration Management in Systems and Software Engineering*, read in full, including the normative Annex D. Listed by IEEE as Inactive-Reserved
- [Google SRE Workbook, "Canarying Releases"](https://sre.google/workbook/canarying-releases/); [Google SRE Book, "Release Engineering"](https://sre.google/sre-book/release-engineering/)
- Robinson, [Consumer-Driven Contracts: A Service Evolution Pattern](https://martinfowler.com/articles/consumerDrivenContracts.html) (2006)
- Chen, "The Entity-Relationship Model, Toward a Unified View of Data", *ACM Transactions on Database Systems* 1(1) (March 1976), 9-36; Ambler and Sadalage, [Evolutionary Database Design](https://martinfowler.com/articles/evodb.html)
