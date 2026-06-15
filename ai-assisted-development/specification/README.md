# Specification

One document, for the tasks complex enough that handing them to an agent without a written brief would mean guessing.

## The document

| Document | Answers |
|---|---|
| [`agent-task-specification.md`](agent-task-specification.md) | For this one task: what to build, what's explicitly out of scope, and how to prove it's done. |

## When to use it

**Any task where you'd want to interview a new hire before they started, not just hand them a one-line ticket.** A typo fix or a small, obvious change doesn't need one; the task-plan entry is the whole spec. A feature that touches several files, has a non-obvious edge case, or where "done" isn't self-evident earns one.

**Before starting the session that implements the task, not during it.** The value of this document comes from resolving ambiguity up front. Writing it while the agent is already mid-implementation defeats the purpose: by then, guesses have already been made.

## Why we use it

Anthropic's own guidance for Claude Code names the property that makes a spec like this work: it has to be self-contained, name the specific files and interfaces involved, state plainly what's out of scope, and end with a verification step that proves the feature actually works. Each of those is checkable: a reader can look at a finished spec and say whether it has them, which is exactly what makes "write a good spec" into something more than advice.

The underlying reasoning is the same as running a discovery conversation before a human engineer starts a ticket: most of the cost of ambiguity is paid during implementation, in the form of a wrong guess that has to be found and redone. Paying that cost once, up front, in a conversation or a written spec, is cheaper than paying it after the code is already written the wrong way. A separate analysis of thousands of real agent configuration files found the same failure mode from the other direction: most specs that don't work fail because they're vague, not because they're wrong. "Build me something cool" gives an agent nothing to anchor on, no matter how capable the agent is.

A recommended way to arrive at this document: have the agent interview you about the feature first, covering implementation approach, edge cases, UI details, and tradeoffs, and only write the spec once that conversation has actually surfaced the ambiguity. Then start a fresh session against the finished spec, so implementation begins with a clean, focused context instead of the exploratory back-and-forth that produced it.

This is not the same document as the [technical design document](../../general-swe/foundations/technical-design-document.md) already in this repository. A TDD is written for human reviewers who are deciding whether to build something and sanity-checking the approach before anyone writes code. This document assumes the decision to build is already made, and is written to be handed directly to an agent that will execute it with less human judgment standing between the document and the resulting code, which is exactly why it needs the extra discipline of an explicit scope boundary and a built-in way to check the result.

## Where it lives

**Docs-as-code, for the life of the task.** It has to be in the working tree for the agent implementing it to read. Once the task ships, archive it or delete it. Like the task plan, it's a working document for a specific piece of work, not a durable reference; the merged code and its commit message are the permanent record.
