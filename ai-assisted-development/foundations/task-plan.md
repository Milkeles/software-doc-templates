# Task plan: {Repository, package, or workstream}

*Italic text is guidance. Delete it as you fill each section in.*

*The [agent instructions file](agent-instructions-file.md) says how the project works. This says what to actually work on. Keep the two separate: standing conventions belong in one, the current queue belongs in the other, and mixing them makes both harder to keep short.*

| | |
|---|---|
| **Covers** | |
| **Last reviewed** | YYYY-MM-DD |

---

## 1. The queue

*Group by priority if the volume warrants it (P0-P3, or high/medium/low). For a short queue, a flat list is enough.*

```
## P0

- [ ] {One task, one sentence. If it takes more than one sentence to describe, it's two tasks.}
- [ ] {...}

## P1

- [ ] {...}
```

*Each task should be small enough that "done" is unambiguous. "Improve error handling" is not a task; "return a 400 with a message when the request body fails validation" is.*

---

## 2. Dependencies

*Where one task can't start until another finishes, say so explicitly rather than leaving it to be discovered mid-task.*

| Task | Blocked by |
|---|---|
| | |

---

## 3. Completion

*State the convention this queue follows, so it's consistent: delete a task once it's done and let commit history be the record, or check it off and leave it as a log. Either works; pick one and say which.*

| | |
|---|---|
| **Convention** | *Delete on completion, or check off and keep* |

---

## Notes on using this template

*Delete this section too.*

**One task, one sentence.** If a task needs a paragraph to describe, split it. A queue of small, unambiguous items is easier for an agent to pick up correctly than a queue of a few large, vague ones, for the same reason a well-groomed backlog is easier for a human team to pull from than a pile of epics.

**State blockers explicitly rather than relying on task order.** A queue read top to bottom looks ordered whether or not it actually is. A stated "blocked by" is unambiguous; a task's position in the list is not.

**This is not the [product backlog](../../general-swe/agile-scrum/product-backlog-item.md) or [sprint backlog](../../general-swe/agile-scrum/sprint-backlog.md) template.** Those carry sprint cadence, story points, and a product owner's prioritization built for a human team's ceremonies. This is flatter and shorter-lived: a working queue for whatever an agent is actively executing, often scoped to a single session, a single day, or a single small workstream, not a sprint.

**Richer per-task fields exist if the work justifies them.** Some teams add fields like acceptance criteria, a verification command, an estimate, or a stable ID for cross-referencing blockers. These are useful past a certain queue size and add overhead below it. Start with the plain checklist above and add structure only once the plain version is genuinely running into ambiguity.

**Where this lives:** docs-as-code, next to the agent instructions file. An agent reading its task queue needs it in the working tree, the same as the instructions file itself.

---

## Related documents

- [`agent-instructions-file.md`](agent-instructions-file.md). Standing project knowledge, as distinct from this file's current work queue
- [`../specification/agent-task-specification.md`](../specification/agent-task-specification.md). The full brief for a single queue item complex enough to need one
