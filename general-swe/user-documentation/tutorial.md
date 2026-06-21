# Tutorial

> A lesson. The reader learns by doing something that works.
>
> **Also called:** Getting Started Guide, Walkthrough, or Quickstart.
>
> **What it is for.** Building basic competence in someone who does not have it yet. Not helping them get a job done. Daniele Procida draws the line sharply: a tutorial's purpose is "to help the pupil acquire basic competence", while a how-to guide's is "to help the already-competent user perform a particular task correctly".
>
> **The rule that makes tutorials hard.** Responsibility for success sits with you. Procida: "In a tutorial, responsibility lies with the teacher. If the learner gets into trouble, that's the teacher's problem." A tutorial that breaks at step 9 has failed completely. The reader cannot diagnose it, and will not trust the rest of your documentation.
>
> **Where it lives.** Docs-as-code, published to the docs site. It breaks when the product changes, so it must be editable in the same pull request as the change that breaks it.
>
> **Delete this block before publishing.**

---

## 1. Title

Name what the reader will have built, not what they will have learned.

> Good: "Build your first pipeline"
> Bad: "Introduction to pipelines"

"Introduction to X" describes your table of contents. "Build your first X" describes the reader's afternoon.

---

## 2. What you will build

One short paragraph and, where it helps, the finished output. A screenshot, a code listing, a terminal transcript.

The reader is deciding whether to spend twenty minutes. Show them the end state so the decision is informed.

State the time it takes. Be honest and measure it rather than guessing; a tutorial advertised as ten minutes that takes fifty is worse than one advertised as fifty.

---

## 3. Prerequisites

What must already be true. Versions, accounts, installed tools, prior tutorials.

**Every prerequisite is a place the reader can fail before starting.** Keep the list as short as the tutorial allows, and link the installation guide rather than restating it.

Give a command that proves each one:

> ```
> node --version   # expect v22 or later
> ```

---

## 4. Steps

Numbered. Each step is one action with one visible result.

Five rules, and the tutorial fails without them.

**One path only.** No options, no "you could also", no branching by platform if you can avoid it. Choices are for readers who know enough to choose. If two platforms genuinely diverge, write two tutorials.

**Every step must work.** Procida: "The tutorial eliminates the unexpected." Pin versions, use a fixed dataset, avoid anything that depends on the network being fast or an external service being up. A contrived setting is correct here, not a compromise.

**Show the expected result after each step.** The reader needs to confirm they are still on track. Without it, an error at step 3 is discovered at step 11.

> ```
> $ pipeline init demo
> Created demo/pipeline.yaml
> ```
>
> You now have a `demo` directory containing one file.

**Do not explain.** The urge to teach the concept behind the step is strong and it is what turns tutorials into unfinishable essays. Link to the explanation instead. One clause of orientation is fine; a paragraph is not.

**Do not make the reader guess.** This is the one point where the standard advice is contested, and the contest resolves against exploration. John Carroll's minimalist instruction includes "guided exploration", where learners induce the correct procedure by trial and error. Thomas Williams and David Farkas challenged exactly that part in *SIGCHI Bulletin* (1992), arguing that "the stated minimalist goal of enabling the learner to accomplish real work while learning a program is often thwarted by the act of compelling that learner to induce, through trial and error, the correct procedures needed to accomplish that work". Procida arrives at the same place from a different direction. Tell the reader what to type.

---

## 5. Checkpoints

At two or three points, give the reader a way to verify state independently of the steps.

> Run `pipeline status`. You should see one pipeline, `demo`, with status `ready`.

Checkpoints are what let a reader recover. Without them, the only recovery is starting over.

---

## 6. What you built

Two or three sentences recapping what now exists and what the reader can now do.

Then links out, in this order: the how-to guides for real tasks, the explanation for why it works, the reference for the full surface. **Do not put a further tutorial first** unless it is genuinely the next lesson.

---

## Testing this document

A tutorial is the only documentation type that can be verified mechanically end to end, and it decays faster than any other. Both facts point the same way.

- Run it on a clean machine or a fresh container before publishing.
- Automate it if you can. A tutorial whose commands run in CI stays true.
- Re-run it on every release that touches the surface it uses.
- Watch someone unfamiliar do it once, in silence. Every place they hesitate is a defect.

**A stale tutorial is worse than no tutorial.** It teaches the reader that your documentation cannot be trusted, and that lesson generalises to everything else you wrote.

---

## Common failures in this document

- **Written for the author's convenience.** Ordered by how the system is built rather than by what the learner can absorb.
- **Explaining mid-step.** The lesson stalls, the reader loses the thread, and the tutorial never gets finished.
- **Options and branches.** The reader must make a decision they lack the knowledge to make.
- **No expected output.** An error at step 3 surfaces at step 11, and the reader blames themselves.
- **Depends on a live external service.** Fails for reasons the reader cannot fix and you cannot see.
- **Never re-run.** The commonest failure by a wide margin. Untested tutorials rot silently.
- **Actually a how-to guide.** If it assumes competence and serves a real goal, it is not a tutorial.

---

## Related documents

- [`how-to-guide.md`](how-to-guide.md). For readers who already have the competence this builds
- [`explanation.md`](explanation.md). Where the concepts behind the steps belong
- [`installation-guide.md`](installation-guide.md). Link it from prerequisites rather than repeating it
- [`README.md`](README.md). Why the four types are separate, and the evidence behind it
