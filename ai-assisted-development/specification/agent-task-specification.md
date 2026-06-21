# Agent task specification: {Task name}

*Also called: a task spec, or a task brief.*

*Italic text is guidance. Delete it as you fill each section in.*

*Written to be handed to an agent in a single session, with no back-and-forth needed to fill gaps. If you find yourself wanting to add a caveat while the agent is already working, that caveat belongs here instead, written in before the session starts.*

| | |
|---|---|
| **Task** | *Link the [task-plan.md](../foundations/task-plan.md) entry this expands on, if there is one* |
| **Owner** | |
| **Status** | *Draft, ready, in progress, done* |

---

## 1. Goal

*What this task builds or fixes, and why, in plain language. Lead with the outcome, not the mechanism.*

---

## 2. Files and interfaces involved

*Name the specific files, functions, modules, or APIs this task touches. An agent working from a named list makes fewer wrong guesses than one working from a general description of the area.*

| File or interface | Role in this task |
|---|---|
| | |

---

## 3. Out of scope

*State plainly what this task does not include, especially anything adjacent that might look like part of the same task. This is the single most commonly missing section in a spec that otherwise looks complete.*

---

## 4. Constraints

*Reuse the three-tier structure from the [agent instructions file](../foundations/agent-instructions-file.md) if this task has boundaries beyond what that file already covers. Leave this section out if it doesn't.*

| Always do | Ask first | Never do |
|---|---|---|
| | | |

---

## 5. Verification

*The end-to-end step that proves the task is actually done. Not "looks right," but a command, a test, or a specific action with an expected result. This is the section that closes the loop; a spec without one leaves "done" as a judgment call.*

| | |
|---|---|
| **How to verify** | *Exact command, test file, or reproducible check* |
| **Expected result** | |

---

## Notes on using this template

*Delete this section too.*

**Self-contained is the whole point.** A reader with no other context should be able to pick this up and know what to build, what not to touch, and how to prove it works. If a section only makes sense to someone who was in the conversation that produced it, rewrite it.

**Write the out-of-scope section even when it feels obvious.** What looks obviously out of scope to the person who wrote the spec is frequently the first thing an agent decides to "helpfully" include, since a request often implies adjacent work that wasn't actually asked for.

**A spec with no verification step isn't finished.** Section 5 is what turns "looks done" into something checkable. Without it, whoever reviews the result is the entire verification loop, and every mistake waits for them to notice it by hand.

**Consider building the spec through a conversation, not from a blank page.** Interviewing about the task before writing it down (implementation approach, edge cases, tradeoffs) surfaces exactly the ambiguity this document exists to remove. Write the spec after that conversation, not instead of it.

**Where this lives:** docs-as-code, for the life of the task. Archive or delete it once the work ships; the merged code is the permanent record from that point on.

---

## Related documents

- [`../foundations/task-plan.md`](../foundations/task-plan.md). The queue entry this specification expands on
- [`../foundations/agent-instructions-file.md`](../foundations/agent-instructions-file.md). Standing conventions this task should already follow without restating them here
- [`../../general-swe/foundations/technical-design-document.md`](../../general-swe/foundations/technical-design-document.md). The document to write instead, when the question is whether to build something at all
