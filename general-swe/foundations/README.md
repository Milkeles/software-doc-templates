# Foundations

Documents every software team needs, whatever it builds and however it plans work.

These fifteen templates do not assume sprints, WIP limits, or stage gates. A Scrum team, a Kanban team, and a team building to a fixed contract all need to record why they chose PostgreSQL, what to do when the queue backs up, and what "reviewed" means.

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
| [Code review guidelines](code-review-guidelines.md) | Reviews are inconsistent or slow, or the team is growing | Two people who already agree | Repo |
| [Onboarding guide](onboarding-guide.md) | You will hire again | You will not | Split: setup in repo, org context in wiki |
| [Changelog](changelog.md) | Anyone consumes your releases, including other teams | Nothing outside the repo depends on you | Repo root |
| [Release notes](release-notes.md) | Non-technical users need to know what changed | Your only users read the changelog | Product site or in-app |
| [Threat model](threat-model.md) | You handle credentials, money, personal data, or untrusted input | A prototype with no real data | Repo, beside the design |
| [Glossary](glossary.md) | The same word means different things to different teams | Everyone shares vocabulary already | Repo |
| [Deprecation plan](deprecation-plan.md) | Someone depends on something you intend to remove | Nobody outside the team calls it | Repo, announced widely |

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

### Code review guidelines

**When.** Reviews take days, or block on style arguments, or vary wildly by reviewer. Also whenever the team is about to grow, because unwritten norms do not scale past the people who invented them.

**Why.** Most review friction comes from an unstated question: what is the bar? Google answers it directly: approve once the change "definitely improves the overall code health of the system," even if it is not perfect, "because there is no such thing as perfect code, there is only better code." Writing that down converts an argument about taste into an argument about a stated principle, which is a much shorter argument.

The second thing guidelines buy is speed, and speed is a team property. Google's rule is that one business day is the maximum time to respond, and its stated reason is that it optimises team velocity over individual velocity. An engineer who reviews quickly is slower personally and the team ships faster.

On review size, the most cited numbers come from a Cisco study of 2,500 reviews published by SmartBear: 200 to 400 lines per sitting, no more than 60 minutes, defect discovery of 70 to 90 percent in that range. Treat those with the caveat attached. The study is vendor-funded, not peer-reviewed, and twenty years old. It is nonetheless directionally consistent with Google's independent guidance that 100 lines is reasonable and 1,000 is usually too large.

**Where.** In the repo, as `CONTRIBUTING.md` or under `docs/`. The guidelines reference the style guide and lint configuration and must move with them.

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
