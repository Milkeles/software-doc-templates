# Configuration management plan: {System or programme}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Applies to** | |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |
| **Review cadence** | *At minimum, at the start of each phase or each quarter.* |

*This document answers one question: **at any moment, what exactly is running, where did it come from, and who agreed to it?** If your team can already answer that from tooling, this plan should be one page of links.*

---

## Write this by reference

*The controlling standard says so itself. IEEE Std 828-2012, Annex D, opens: "The CMP shall include the following either by reference to another document that is a CI or within itself."*

*That sentence is the whole strategy. Every section below may be a pointer, provided the thing pointed at is itself version-controlled. "See `.github/workflows/release.yml`" satisfies the requirement and stays true; a prose description of the pipeline does not stay true past the next change to it.*

**So the test for every paragraph you are about to write: does a tool already hold this fact? If yes, link it and move on.**

*A caveat about the standard. IEEE lists 828-2012 as Inactive-Reserved, so do not cite it as current practice. It remains the most complete published statement of what belongs in this plan, which is why the structure below follows it.*

---

## 1. Scope and limits

*What this plan covers and what it does not. Applicability, limitations, and the assumptions the plan rests on.*

*Name the assumptions that would change the plan if false. The standard's own examples are "the degree of customer participation in CM activities or the availability of automated aids", and both still bite: a plan written assuming a shared artefact registry that never gets funded is a plan that quietly stops being followed.*

*Point at the [glossary](glossary.md) rather than defining terms here.*

---

## 2. What is under control

*The configuration items, and the criteria for something becoming one.*

*A configuration item is an "aggregation of work products that is designated for configuration management and treated as a single entity". The size is your choice: it can be an entire system or a single module. Pick the level at which you would want to say "version X of this".*

| Item type | Identified by | Where it lives | Under whose control |
|---|---|---|---|
| *Application source* | *Git commit SHA* | *`org/service-payments`* | *Repo maintainers* |
| *Deployable artefact* | *Semantic version + digest* | *Container registry* | *Release pipeline only* |
| *Infrastructure definition* | *Git commit SHA* | *`org/infra`* | *Platform team* |
| *Runtime configuration* | *Config version* | *Parameter store, changes via pull request* | *Service owners* |
| *Secrets* | *Rotation date* | *Secrets manager* | *Security team* |
| *Database schema* | *Migration number* | *`db/migrations/` in the service repo* | *Service owners* |
| *This plan* | *Document version* | | |

**Criteria for entry.** *What has to be true before something enters the list. Usually: it can affect production behaviour, and more than one person can change it.*

**Say what is deliberately excluded**, *and why. Local developer tooling, scratch environments, generated files. An unstated exclusion reads as an oversight during an audit.*

---

## 3. Baselines

*A baseline is a version "formally reviewed and agreed upon, that thereafter serves as the basis for further development, and that can be changed only through formal change control procedures". Note the second half. If it can be changed without going through the process, it is not a baseline.*

| Baseline | Established when | Contains | Changed how |
|---|---|---|---|
| *Release baseline* | *At tag* | *Source, artefact digest, migrations, config* | *New release only* |
| *Requirements baseline* | *At sign-off* | *The approved SRS version* | *Change request* |

*In a modern repository most of this is a tag plus a lockfile. Say that, if it is true, and stop.*

---

## 4. Who decides

*Responsibilities and authorities. Name organisational units and job titles, not individuals, because individuals change and this document will not keep up.*

| Activity | Who performs | Who approves |
|---|---|---|
| *Merge to main* | *Any engineer* | *One reviewer with write access* |
| *Change a production config value* | *Service owner* | *Second service owner* |
| *Change infrastructure* | *Platform team* | *Platform lead* |
| *Approve a release* | *Release pipeline* | *Named in the [deployment plan](deployment-plan.md)* |

**If you have a change control board**, *state its purpose and objectives, membership, period of effectivity, scope of authority, and operational procedures. If you do not, say that pull request review is the change control mechanism, because that is a legitimate answer and leaving it unstated is what makes auditors ask for a board.*

*Cross-reference the [change request](../waterfall/change-request.md) process where baselined requirements are involved, and the [code review guidelines](code-review-guidelines.md) for everything else.*

---

## 5. Status accounting

*How anyone finds out what version is where, without asking a person.*

| Question | Answered by |
|---|---|
| *What is running in production right now* | *Deployment dashboard, link* |
| *What changed between two versions* | *Changelog and commit range* |
| *Which environments run which version* | *Same dashboard* |
| *Who approved a given change* | *Pull request record* |

*The failure mode here is a status report that is compiled by hand once a week. It is stale on publication and nobody trusts it. If the tool cannot answer the question, fixing the tool is the work; writing the report is not.*

---

## 6. Audits

*How you verify that what is recorded matches what exists.*

| Audit | Checks | Frequency | Who |
|---|---|---|---|
| *Configuration* | *The running artefact digest matches the one recorded for the release* | *Every deploy, automated* | *Pipeline* |
| *Drift* | *Deployed infrastructure matches the definitions in the repository* | *Daily* | *Platform team* |
| *Access* | *Who can bypass the controls above* | *Quarterly* | *Security* |

*The third one is the one people forget, and it is the one that determines whether the other two mean anything.*

---

## 7. Third-party and supplier items

*Anything you did not build and cannot change: dependencies, vendor components, contracted deliverables.*

*Record how they are identified and pinned, how updates are evaluated, and where the licence and provenance record lives. If you produce a software bill of materials, name it here and link the [threat model](threat-model.md).*

*The standard permits omitting this section entirely if no suppliers provide configuration items. That is the only omission it allows, so if you drop it, say why.*

---

## 8. Releases

*A release is "a version of software or a system under CM that is made formally available to a wider community", which explicitly includes internal releases to another team or to QA. State the release types you actually have and who receives each.*

*Everything about executing a release belongs in the [deployment plan](deployment-plan.md) and the [branching strategy](branching-strategy.md). This section names the types and points there.*

**Archiving.** *What happens when a release reaches end of life: where it is archived, how it is withdrawn from normal channels, and how the record is marked. Teams that skip this discover during an incident that the version a customer is still running cannot be rebuilt.*

---

## 9. Maintaining this plan

| | |
|---|---|
| **Who monitors it** | |
| **Update frequency** | |
| **How changes are approved** | |
| **How changes are communicated** | |

*Keep a change history in the document. A configuration management plan with no version history is the clearest possible demonstration that it is not being followed.*

---

## Notes on using this template

*Delete this section too.*

**Most teams need three sections, not nine.** What is under control, who approves changes, and how anyone finds out what is running. The rest applies when you have suppliers, baselined requirements, or an auditor. Delete what does not apply rather than filling it with "N/A", which reads as unconsidered.

**The plan describes the system, it does not replace it.** If the plan says changes require review and the repository allows direct pushes to main, the repository wins and the plan is a liability. Check the settings before you write the sentence.

**Name the branching model.** The standard's own worked example expects it: the CM authority should "ensure that software developers on the project understand the selected branching model and how to use the toolset to implement it". Link the [branching strategy](branching-strategy.md) rather than describing it twice.

**Runtime configuration is the gap.** Traditional CM was built for source and deliverables. The thing that most often changes production behaviour without anyone noticing is a config value or a feature flag toggled through a console. If those are not in section 2, this plan is not describing your system.

**Where this lives:** in the repository if the team it governs is the team that reads it, because it must change in the same commit as the pipeline and branch protection it describes. In the wiki if it is a programme-level document covering several teams and suppliers, where its readers include people with no repository access. Do not keep both copies.

---

## Related documents

- [`deployment-plan.md`](deployment-plan.md). Executing a single release under these rules
- [`branching-strategy.md`](branching-strategy.md). How changes reach a baseline
- [`changelog.md`](changelog.md). Status accounting for consumers
- [`../waterfall/change-request.md`](../waterfall/change-request.md). The formal route for changing a baselined item
- [`threat-model.md`](threat-model.md). Why supply chain and access control matter here
- [`glossary.md`](glossary.md). Where the terms belong instead of in section 1
