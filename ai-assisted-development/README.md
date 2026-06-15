# AI-assisted development

Documents for a team whose work is built with, and sometimes by, a coding agent or language model.

This sits on top of [`general-swe/`](../general-swe/), not instead of it. A team using a coding agent still writes architecture decision records, technical design documents, and runbooks. This area covers what's genuinely new: a document meant to be read by a model as well as, or instead of, a person, and the practice of checking whether the model's output is actually good enough to ship.

This is the newest area in the repository, and it will date faster than the others. The specific file names and tool syntax below (`AGENTS.md`, hooks, a given vendor's permission model) will likely be superseded. The underlying disciplines they encode, such as saying what you'd tell a new teammate, separating the plan from the work, and defining what "good enough" means before you grade it, will not.

---

## Groups

| Group | Use it when |
|---|---|
| [`foundations/`](foundations/) | Any codebase where a coding agent works regularly. What it needs to know every session, and what it should work on next. |
| [`specification/`](specification/) | A single feature or task is complex or ambiguous enough that handing it to an agent without a written spec would be guessing. |
| [`evaluation/`](evaluation/) | You need to know, in more than a gut feeling, whether agent-produced work or an agent-driven feature is actually good enough. |

There is no methodology split here. The practice is too new and too fast-moving for a Scrum-versus-Kanban-style fork to mean anything yet.

---

## What makes this documentation different

Two things distinguish this area from the rest of the repository.

**The reader is a probabilistic process, not a person.** A human who reads a runbook either follows it or deviates for a reason you can ask about afterward. A model's adherence to written instructions is empirically partial: Anthropic's own guidance on Claude Code puts advisory instruction-following at roughly 70%, with a hook (a script that runs deterministically, outside the model's discretion) as the mechanism for a rule that has to hold every time. That gap between "the model was told" and "the model did it" doesn't exist for a human-facing runbook in the same way, and the documents in this area have to be written with it in mind: short and specific enough that the instructions actually get followed, with anything non-negotiable enforced outside the document rather than left to the document alone.

**The document doubles as the interface.** An architecture decision record explains a choice to a future engineer; an `AGENTS.md` file is read, verbatim, at the start of every agent session and shapes what the agent does next. Getting it wrong doesn't just confuse a reader later, it changes the agent's behavior immediately, which is why the guidance in this area leans harder on concrete length limits and explicit include/exclude lists than most of the rest of the repository does.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| Agent instructions file | Docs-as-code, at the repository root (and in nested package roots for a monorepo) | Coding agents read it directly from the working tree; a copy anywhere else is invisible to the agent |
| Task plan | Docs-as-code, next to the agent instructions file | Same reason: it has to be in the tree an agent actually reads |
| Agent task specification | Docs-as-code for the lifetime of the task, deleted or archived once the task ships | Written to be read by an agent in a single session; no value once the work is merged |
| Evaluation plan | Wherever the team already tracks engineering methodology, reviewed on a set cadence | Defines a standing method, not a single result |
| Eval run log | Wherever the team already tracks recurring engineering work | A rolling record of results over time, not a durable reference |

---

## What to write first

1. **Agent instructions file**, the moment more than one person points a coding agent at the repository. Without it, every session re-derives context that a five-minute file would have supplied for free.
2. **Task plan**, once the instructions file exists and there's more than a single task in flight. A plan turns "the agent guessed what to build" into "the agent built what was asked."
3. **Agent task specification**, for any task where you'd want to interview a new hire before they started, not just hand them a one-line ticket.
4. **Evaluation plan and eval run log**, once agent-produced output starts reaching production, or once a feature's whole value proposition depends on a model's judgment rather than deterministic code. Before that point, ordinary code review and the testing documents in [`general-swe/foundations/`](../general-swe/foundations/) already cover it.
