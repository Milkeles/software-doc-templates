# Template index

Every template in the repository, with what each one is for. Use this when you know the document you want and not where it lives.

If you don't know what you need yet, start from the [README](README.md) and read the group README for your area — it tells you which documents earn their place and which to skip.

Areas: [General software engineering](#general-software-engineering) · [Web development](#web-development) · [Game development](#game-development) · [Data engineering](#data-engineering) · [Platform engineering](#platform-engineering) · [AI-assisted development](#ai-assisted-development)

---

## General software engineering

Documents any software team needs, whatever the domain. → [`general-swe/`](general-swe/)

### Foundations — methodology-agnostic

→ [`general-swe/foundations/`](general-swe/foundations/)

| Document | What it's for |
|---|---|
| [Architecture decision record](general-swe/foundations/architecture-decision-record.md) | Record one significant decision, the options weighed, and why this one won. |
| [Architecture overview](general-swe/foundations/architecture-overview.md) | Explain how the system fits together to someone who has never seen it. |
| [Branching strategy](general-swe/foundations/branching-strategy.md) | State how code moves from a developer's machine to production. |
| [Bug report](general-swe/foundations/bug-report.md) | Describe a defect so someone else can reproduce and fix it. |
| [Changelog](general-swe/foundations/changelog.md) | Tell users what changed in each release, in their terms. |
| [Code review guidelines](general-swe/foundations/code-review-guidelines.md) | Set what reviewers look for, so review stops being personal taste. |
| [Coding standards](general-swe/foundations/coding-standards.md) | Settle the style arguments once, in writing. |
| [Configuration management plan](general-swe/foundations/configuration-management-plan.md) | Define what is version-controlled, how it's identified, and who can change it. |
| [Contributing guide](general-swe/foundations/contributing-guide.md) | Tell outside contributors how to make a change you'll accept. |
| [Data model](general-swe/foundations/data-model.md) | Document the entities, their fields, and the rules connecting them. |
| [Deployment plan](general-swe/foundations/deployment-plan.md) | Set out the steps, checks, and rollback for a specific release. |
| [Deprecation plan](general-swe/foundations/deprecation-plan.md) | Retire something without stranding the people using it. |
| [Glossary](general-swe/foundations/glossary.md) | Fix what the team's domain words mean, so two people don't use one word differently. |
| [Incident postmortem](general-swe/foundations/incident-postmortem.md) | Learn from an outage without assigning blame. |
| [Interface control document](general-swe/foundations/interface-control-document.md) | Pin down the contract between two systems built by different teams. |
| [Onboarding guide](general-swe/foundations/onboarding-guide.md) | Get a new engineer to their first useful change. |
| [Release notes](general-swe/foundations/release-notes.md) | Announce a release to the people affected by it. |
| [RFC](general-swe/foundations/rfc.md) | Propose a change and gather informed disagreement before building it. |
| [Runbook](general-swe/foundations/runbook.md) | Give the on-call engineer the steps to fix this at 3am. |
| [Service README](general-swe/foundations/service-readme.md) | Answer, in one file, what a service does and how to run it. |
| [Technical design document](general-swe/foundations/technical-design-document.md) | Work out how something will be built before building it. |
| [Test case specification](general-swe/foundations/test-case-specification.md) | Write a test someone else can run and get the same result. |
| [Test strategy](general-swe/foundations/test-strategy.md) | Set how the team tests, at what level, and what it deliberately doesn't test. |
| [Test summary report](general-swe/foundations/test-summary-report.md) | Say what was tested, what was found, and whether it's fit to ship. |
| [Threat model](general-swe/foundations/threat-model.md) | Find what an attacker would go for, before they do. |

### Requirements

→ [`general-swe/requirements/`](general-swe/requirements/)

| Document | What it's for |
|---|---|
| [Non-functional requirements](general-swe/requirements/non-functional-requirements.md) | Make speed, availability, and security testable instead of aspirational. |
| [Product requirements document](general-swe/requirements/product-requirements-document.md) | State what to build and why, before anyone designs it. |
| [Use case specification](general-swe/requirements/use-case-specification.md) | Describe one goal a user achieves, step by step, including what goes wrong. |
| [Vision and scope](general-swe/requirements/vision-and-scope.md) | Agree what the product is for and where its edges are. |

### Agile / Scrum

→ [`general-swe/agile-scrum/`](general-swe/agile-scrum/)

| Document | What it's for |
|---|---|
| [Definition of done](general-swe/agile-scrum/definition-of-done.md) | Agree what "finished" means, so it stops being negotiated per item. |
| [Product backlog item](general-swe/agile-scrum/product-backlog-item.md) | Describe one piece of work well enough to plan and accept it. |
| [Product goal](general-swe/agile-scrum/product-goal.md) | Name the single objective the backlog is working toward. |
| [Sprint backlog](general-swe/agile-scrum/sprint-backlog.md) | Hold the sprint goal and the plan for reaching it. |
| [Sprint retrospective](general-swe/agile-scrum/sprint-retrospective.md) | Turn what the team noticed into one change it will actually make. |
| [Sprint review notes](general-swe/agile-scrum/sprint-review-notes.md) | Record what was shown, what stakeholders said, and what it changes. |
| [Team working agreement](general-swe/agile-scrum/team-working-agreement.md) | Write down how the team works together, so new members don't guess. |

### Kanban

→ [`general-swe/kanban/`](general-swe/kanban/)

| Document | What it's for |
|---|---|
| [Blocker log](general-swe/kanban/blocker-log.md) | Track what stops work, so repeat causes become visible. |
| [Definition of workflow](general-swe/kanban/definition-of-workflow.md) | State what each column means and when an item may move. |
| [Flow review](general-swe/kanban/flow-review.md) | Look at the flow metrics and decide what to change. |
| [Kanban system design](general-swe/kanban/kanban-system-design.md) | Design the board, its limits, and its policies deliberately. |
| [Work item types](general-swe/kanban/work-item-types.md) | Define the kinds of work on the board and how each is handled. |

### Lean

→ [`general-swe/lean/`](general-swe/lean/)

| Document | What it's for |
|---|---|
| [A3](general-swe/lean/a3.md) | Fit a problem, its cause, and the fix onto one sheet. |
| [Experiment record](general-swe/lean/experiment-record.md) | State the prediction before the change, so the result can't be reinterpreted after. |
| [Improvement kata](general-swe/lean/improvement-kata.md) | Move toward a target condition one obstacle at a time. |
| [Value stream map](general-swe/lean/value-stream-map.md) | See where the time actually goes between idea and production. |

### Shape Up

→ [`general-swe/shape-up/`](general-swe/shape-up/)

| Document | What it's for |
|---|---|
| [Cool-down guide](general-swe/shape-up/cool-down-guide.md) | Protect the weeks between cycles from being filled with new work. |
| [Kick-off message](general-swe/shape-up/kick-off-message.md) | Hand a shaped pitch to a team with the context it needs. |
| [Pitch](general-swe/shape-up/pitch.md) | Present a shaped idea with its appetite and its limits attached. |
| [Scope map](general-swe/shape-up/scope-map.md) | Break work into scopes the team discovers, not ones assigned upfront. |

### Waterfall / plan-driven

→ [`general-swe/waterfall/`](general-swe/waterfall/)

| Document | What it's for |
|---|---|
| [Change request](general-swe/waterfall/change-request.md) | Get a change to a baselined document assessed and approved. |
| [Master test plan](general-swe/waterfall/master-test-plan.md) | Plan testing across the whole project, not one release. |
| [Phase gate review](general-swe/waterfall/phase-gate-review.md) | Decide, on evidence, whether the project may enter the next phase. |
| [Requirements traceability matrix](general-swe/waterfall/requirements-traceability-matrix.md) | Prove every requirement is designed, built, and tested. |
| [Software design description](general-swe/waterfall/software-design-description.md) | Describe the design that satisfies the requirements specification. |
| [Software requirements specification](general-swe/waterfall/software-requirements-specification.md) | Specify what the system must do, in a form you can test against. |
| [User acceptance test plan](general-swe/waterfall/user-acceptance-test-plan.md) | Define what the customer must see to accept delivery. |

### Project management

→ [`general-swe/project-management/`](general-swe/project-management/)

| Document | What it's for |
|---|---|
| [Project brief](general-swe/project-management/project-brief.md) | Get enough agreement to justify planning the project at all. |
| [Project charter](general-swe/project-management/project-charter.md) | Authorise the project and name who can decide what. |
| [Risk register](general-swe/project-management/risk-register.md) | Track what could go wrong, how likely, and who owns the response. |
| [Stakeholder register](general-swe/project-management/stakeholder-register.md) | Know who cares about this project and what each of them needs. |

### Security and compliance

→ [`general-swe/security-and-compliance/`](general-swe/security-and-compliance/)

| Document | What it's for |
|---|---|
| [Data protection impact assessment](general-swe/security-and-compliance/data-protection-impact-assessment.md) | Assess a high-risk processing activity before it starts, as the GDPR requires. |
| [Data retention policy](general-swe/security-and-compliance/data-retention-policy.md) | Say how long each kind of data is kept and what happens after. |
| [Incident response plan](general-swe/security-and-compliance/incident-response-plan.md) | Decide who does what during a breach, before there is one. |
| [Record of processing activities](general-swe/security-and-compliance/record-of-processing-activities.md) | Keep the Article 30 record of what personal data you process and why. |
| [Security review checklist](general-swe/security-and-compliance/security-review-checklist.md) | Check a change for the failures that actually cause breaches. |

### User documentation

→ [`general-swe/user-documentation/`](general-swe/user-documentation/)

| Document | What it's for |
|---|---|
| [Documentation style guide](general-swe/user-documentation/documentation-style-guide.md) | Make documentation written by many people read as one voice. |
| [Explanation](general-swe/user-documentation/explanation.md) | Give the reader the understanding behind the instructions. |
| [How-to guide](general-swe/user-documentation/how-to-guide.md) | Take a competent user through one real task. |
| [Installation guide](general-swe/user-documentation/installation-guide.md) | Get the software running on the reader's machine. |
| [Reference page](general-swe/user-documentation/reference-page.md) | Describe one thing precisely, for someone who already knows what they want. |
| [Troubleshooting guide](general-swe/user-documentation/troubleshooting-guide.md) | Match a symptom to a cause and a fix. |
| [Tutorial](general-swe/user-documentation/tutorial.md) | Teach a beginner by getting them a working result. |

---

## Web development

Browser and API-facing work. → [`web-development/`](web-development/)

### Foundations

→ [`web-development/foundations/`](web-development/foundations/)

| Document | What it's for |
|---|---|
| [API design guide](web-development/foundations/api-design-guide.md) | Make separately built endpoints feel like one API. |
| [Brand and visual guidelines](web-development/foundations/brand-and-visual-guidelines.md) | Keep the product looking like itself across surfaces. |
| [Browser support policy](web-development/foundations/browser-support-policy.md) | Say which browsers you support, so testing and bug triage have an answer. |
| [Design system guide](web-development/foundations/design-system-guide.md) | Document the components so people use them instead of rebuilding them. |
| [Frontend architecture](web-development/foundations/frontend-architecture.md) | Explain how the client application is structured and why. |
| [Rollout plan](web-development/foundations/rollout-plan.md) | Ship a change to users gradually, with a way back. |

### Accessibility

→ [`web-development/accessibility/`](web-development/accessibility/)

| Document | What it's for |
|---|---|
| [Accessibility conformance report](web-development/accessibility/accessibility-conformance-report.md) | Report conformance against WCAG success criteria, claim by claim. |
| [Accessibility statement](web-development/accessibility/accessibility-statement.md) | Tell users where the product stands and how to report a barrier. |
| [Accessibility test plan](web-development/accessibility/accessibility-test-plan.md) | Plan the manual and automated checks that find real barriers. |

### Performance

→ [`web-development/performance/`](web-development/performance/)

| Document | What it's for |
|---|---|
| [Performance budget](web-development/performance/performance-budget.md) | Set the numbers a change must not exceed, and what happens if it does. |
| [Performance review](web-development/performance/performance-review.md) | Look at real user metrics and decide what to fix. |

---

## Game development

Games and interactive media. → [`game-development/`](game-development/)

### Foundations

→ [`game-development/foundations/`](game-development/foundations/)

| Document | What it's for |
|---|---|
| [Art bible](game-development/foundations/art-bible.md) | Give artists one visual target so the game looks coherent. |
| [Business plan](game-development/foundations/business-plan.md) | Show how the game makes money and what it costs to make. |
| [Game design document](game-development/foundations/game-design-document.md) | Hold the design the team is actually building, as it changes. |

### Production

→ [`game-development/production/`](game-development/production/)

| Document | What it's for |
|---|---|
| [Asset and contribution log](game-development/production/asset-and-contribution-log.md) | Track where every asset came from and what licence it carries. |
| [Cycle retrospective](game-development/production/cycle-retrospective.md) | Review a milestone or cycle and change one thing about the next. |

### Live operations

→ [`game-development/live-operations/`](game-development/live-operations/)

| Document | What it's for |
|---|---|
| [Age rating compliance record](game-development/live-operations/age-rating-compliance-record.md) | Keep the evidence behind your PEGI, ESRB, or IARC rating. |
| [Balance log](game-development/live-operations/balance-log.md) | Record what was tuned, why, and what the numbers did after. |
| [Deployment plan](game-development/live-operations/deployment-plan.md) | Ship a build to a live game with players in it. |
| [Live-ops plan](game-development/live-operations/live-ops-plan.md) | Plan the events and content the live game runs on. |
| [Privacy ledger](game-development/live-operations/privacy-ledger.md) | Track what player data every SDK in the build collects. |
| [Release notes](game-development/live-operations/release-notes.md) | Tell players what changed, especially when it affects how they play. |

---

## Data engineering

Pipelines, warehouses, and models. → [`data-engineering/`](data-engineering/)

### Foundations

→ [`data-engineering/foundations/`](data-engineering/foundations/)

| Document | What it's for |
|---|---|
| [Data contract](data-engineering/foundations/data-contract.md) | Make the producer's promise to consumers explicit and enforceable. |
| [Data pipeline design document](data-engineering/foundations/data-pipeline-design-document.md) | Work out how data moves and what happens when it doesn't. |
| [Dataset catalog entry](data-engineering/foundations/dataset-catalog-entry.md) | Let someone find a dataset and know whether to trust it. |

### Governance

→ [`data-engineering/governance/`](data-engineering/governance/)

| Document | What it's for |
|---|---|
| [Data classification and access policy](data-engineering/governance/data-classification-and-access-policy.md) | Decide what's sensitive and who may see it. |
| [Data lineage record](data-engineering/governance/data-lineage-record.md) | Show where a field came from and what breaks if it changes. |
| [Data quality specification](data-engineering/governance/data-quality-specification.md) | Define the checks that decide whether data is fit to use. |

### Operations

→ [`data-engineering/operations/`](data-engineering/operations/)

| Document | What it's for |
|---|---|
| [Backfill and reprocessing plan](data-engineering/operations/backfill-and-reprocessing-plan.md) | Rerun history without corrupting what's already downstream. |
| [Freshness and SLA log](data-engineering/operations/freshness-and-sla-log.md) | Track whether data arrived when consumers were promised it would. |
| [Pipeline runbook](data-engineering/operations/pipeline-runbook.md) | Give whoever gets paged the steps to fix a failed run. |

---

## Platform engineering

Infrastructure and operations. → [`platform-engineering/`](platform-engineering/)

### Foundations

→ [`platform-engineering/foundations/`](platform-engineering/foundations/)

| Document | What it's for |
|---|---|
| [Platform onboarding guide](platform-engineering/foundations/platform-onboarding-guide.md) | Get a team from nothing to a running service on your platform. |
| [Service catalog entry](platform-engineering/foundations/service-catalog-entry.md) | Answer who owns a service and how to reach them, at a glance. |

### Reliability

→ [`platform-engineering/reliability/`](platform-engineering/reliability/)

| Document | What it's for |
|---|---|
| [Error budget policy](platform-engineering/reliability/error-budget-policy.md) | Agree in advance what happens when reliability runs out. |
| [SLO document](platform-engineering/reliability/slo-document.md) | Set a reliability target users would actually notice. |
| [Toil log](platform-engineering/reliability/toil-log.md) | Make repetitive manual work visible enough to justify automating. |

### Resilience

→ [`platform-engineering/resilience/`](platform-engineering/resilience/)

| Document | What it's for |
|---|---|
| [Capacity plan](platform-engineering/resilience/capacity-plan.md) | Know when you run out of headroom, before you do. |
| [Disaster recovery plan](platform-engineering/resilience/disaster-recovery-plan.md) | Recover from the failure you hope never happens. |

---

## AI-assisted development

Working with coding agents and language models. → [`ai-assisted-development/`](ai-assisted-development/)

### Foundations

→ [`ai-assisted-development/foundations/`](ai-assisted-development/foundations/)

| Document | What it's for |
|---|---|
| [Agent instructions file](ai-assisted-development/foundations/agent-instructions-file.md) | Tell a coding agent the project conventions it can't infer. |
| [Task plan](ai-assisted-development/foundations/task-plan.md) | Agree the approach with an agent before it writes code. |

### Specification

→ [`ai-assisted-development/specification/`](ai-assisted-development/specification/)

| Document | What it's for |
|---|---|
| [Agent task specification](ai-assisted-development/specification/agent-task-specification.md) | Specify a task precisely enough that the result can be checked. |

### Evaluation

→ [`ai-assisted-development/evaluation/`](ai-assisted-development/evaluation/)

| Document | What it's for |
|---|---|
| [Evaluation plan](ai-assisted-development/evaluation/evaluation-plan.md) | Decide how you'll measure whether the system is good enough. |
| [Eval run log](ai-assisted-development/evaluation/eval-run-log.md) | Record what was evaluated, against which version, and what it scored. |
