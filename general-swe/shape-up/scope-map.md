# Scope map: {Project}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Project** | *Link the pitch.* |
| **Cycle** | *Number and end date.* |
| **Team** | |
| **Scopes discovered** | YYYY-MM-DD |

*Scopes are the parts of a project that can be finished independently. A few days each. They come from real interdependencies in the work, which is why you cannot write them before starting.*

> "Scope mapping isn't planning. You need to walk the territory before you can draw the map."

*Fill this in at the end of week one, once the team has been in the code. Filling it in on day one is a work breakdown structure with different vocabulary.*

*Then move it into your tracker as list names. This file is a scaffold for the conversation, not a document to maintain for six weeks.*

---

## 1. Scopes

*One row each. Name them the way a person would say them out loud, because their whole purpose is to give the team language for talking about progress without listing tasks.*

*Names come from the problem domain, not the codebase. "Reassign" and "Move to another project" are scopes. "API layer" and "Frontend" are layers, and layers are the failure mode below.*

| Scope | What is done when it is done | Uphill or downhill | Owner |
|---|---|---|---|
| | | | |

*"Uphill" means unknowns remain: you are still working out how. "Downhill" means it is known and the rest is execution. Move it when the understanding changes, not when the work feels good.*

> **Example.**
> | Scope | Done when | Position | Owner |
> |---|---|---|---|
> | *Switcher menu* | *A user with two companies can switch and land on the right dashboard* | *Downhill* | *Ana* |
> | *Session scoping* | *A switched session reads and writes only the chosen company's data* | *Uphill, still unsure about cached queries* | *Ben* |

---

## 2. Chowder

*Loose tasks that do not belong to any scope. Keep them in one list and keep it short.*

- *...*

*Three to five items is normal at the end. A long chowder list is a signal, not a problem in itself: it usually means the scopes were drawn along the wrong seams and you have not found the real structure yet. Redraw rather than adding a sixth item.*

---

## 3. Nice-to-haves

*Mark anything optional with a tilde. That mark is the whole mechanism.*

*A tilde is a decision, made now, that this can be dropped when the deadline gets close. Making it early is what leaves the choice available. Marking things in week five is triage.*

- *~ Keyboard shortcut for the switcher*
- *~ Remember the last company on next login*

---

## 4. When you redraw

*Scopes are wrong at first, and that is expected. Redraw when any of these show up.*

**Signs you have it right:**

- You can talk about the project in these terms without listing tasks
- Each scope could be finished and shipped without the others being done
- A scope is a few days, not two weeks

**Signs to redraw:**

- Every scope named after a layer or a team: "backend", "API", "design". Progress on one tells you nothing about whether anything works
- A scope that stays half done for a week. It is probably two scopes with a dependency inside it
- Chowder growing past five items
- A scope nobody can say the "done when" for

---

## Notes on using this template

*Delete this section too.*

**Do not write this before the cycle starts.** Every property that makes a scope useful comes from interdependencies you can only see from inside the work. A scope map written during shaping is a plan, and the method deliberately does not produce one.

**Instability in week one is the process working, not failing.** Expect the first draft to be wrong. If it is still moving in week four, that is different: it means the shaping was wrong, and the answer is scope hammering rather than more redrawing.

**Scope hammering is done by the team building.** They are the only people who know which cuts are cheap. The questions to ask, from chapter 14: is this a must-have for version one, what is the cost of not doing it, can we simplify rather than remove, what happens if we let people work around it, is this a new problem or one that already existed, is there a way to make it a different scope.

**Two shapes to recognise.** A *layer cake* splits the work horizontally, front end and back end. The book allows it where the layers are genuinely thin and independent, so treat it as a judgement call rather than a rule. An *iceberg* is a scope with a small visible piece over far more hidden work, and that one is a warning: it will not finish when it looks like it should.

**Where this lives:** your tracker, as list names. Move it there as soon as the scopes hold for two days. A Markdown copy will diverge from the tracker within a week, and then you have two answers to the same question.

---

## Related documents

- [`pitch.md`](pitch.md). What the project row links to; the map names the parts, the pitch shaped the whole
- [`kick-off-message.md`](kick-off-message.md). What put this project's team on the cycle the scope map is drawn during
- [`cool-down-guide.md`](cool-down-guide.md). A scope stuck uphill or chowder that keeps growing is what the shaping review there looks back on
