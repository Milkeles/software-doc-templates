# Foundations

The two documents almost every agent-assisted codebase ends up needing: what the agent should know every session, and what it should work on next.

## The documents

| Document | Answers |
|---|---|
| [`agent-instructions-file.md`](agent-instructions-file.md) | What does an agent need to know about this codebase before it touches anything? |
| [`task-plan.md`](task-plan.md) | What's actually being worked on, in what order, and what's blocking what? |

## When to use each

**Agent instructions file: any codebase where a coding agent works more than once.** The first session, an agent can discover build commands and conventions by reading around. The second session, and every one after, it's re-deriving the same context for free if nobody wrote it down. The break-even point is roughly one session.

**Task plan: any codebase with more than one task in flight, or any task complex enough that jumping straight to code would mean guessing at scope.** A single, small, unambiguous task doesn't need a plan file; the prompt is the plan. A body of work with more than one piece, or dependencies between pieces, does.

## Why we use them

The two files split on a simple line: one is standing knowledge, the other is a work queue. The open, cross-vendor `AGENTS.md` convention (read natively by more than twenty coding-agent tools as of this writing) draws exactly this line and calls the instructions file "a README for agents": the human `README.md` stays short and welcoming, and the build steps, test commands, and conventions an agent needs but a new human contributor mostly infers from the code move into their own file. Splitting it out keeps both documents doing one job instead of one document doing two badly.

The task plan exists for a more basic reason: an agent given a vague or multi-part instruction will make scope decisions on its own, and those decisions are guesses. Writing the queue down first is the same discipline as writing a sprint backlog down before a human team starts a sprint, for the same reason: it forces the ambiguity to surface before the work starts, not during it.

Neither document is the same as the [product backlog](../../general-swe/agile-scrum/product-backlog-item.md) or [sprint backlog](../../general-swe/agile-scrum/sprint-backlog.md) templates already in this repository. Those carry ceremony-specific structure (story points, sprint cadence, a product owner's prioritization) built for a human team's rhythm. A task plan here is flatter and shorter-lived: a queue for whatever an agent is actively working through, often for a single session or a single day, not a sprint.

## Where these live

**Docs-as-code, at the root of the repository (or the root of each package, in a monorepo), for both documents.** This is not a preference; it is close to a hard requirement. A coding agent reads its instructions and its task queue directly from the working tree at the start of a session. A copy of either file kept in a wiki is, from the agent's point of view, a file that does not exist.
