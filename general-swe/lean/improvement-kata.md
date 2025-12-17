# Improvement kata: {Process being improved}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Learner** | *The person running the cycles.* |
| **Coach** | *The person asking the five questions. The routine needs both.* |
| **Process** | *One process. Not a team, not a goal.* |
| **Current target condition set** | YYYY-MM-DD |
| **Achieve by** | YYYY-MM-DD |

*Four steps: understand the direction, grasp the current condition, establish the next target condition, iterate toward it. Sections 1 to 3 are set once and revisited rarely. Section 4 is the working part and runs daily or every few days.*

*Rother's reason for having a written routine rather than a shared understanding is worth keeping in mind: "Concepts or coarse steps alone don't change mindset and behavior."*

---

## 1. Direction

*The longer-term challenge this serves. Not achievable soon, and that is the point: it says which way is forward when a target condition is met and you need the next one.*

*One or two sentences. It should still be true in a year.*

> **Example.** Any engineer can ship a change to production on the day they finish it, without asking anyone.

---

## 2. Current condition

*How the process operates today. Facts, gathered by observation.*

*Describe the process, not the outcome. "Deploys take four days" is an outcome. "A deploy requires a release ticket, a manual QA pass, and an approval from one of two people, in that order, and the QA queue is checked twice a day" is a condition, and only the second one shows you where to intervene.*

| | |
|---|---|
| **How it runs now** | *The actual steps and who does them.* |
| **Measured** | *Numbers, and how you got them.* |
| **Observed on** | YYYY-MM-DD |

*Go and look. A current condition assembled from what people say the process is will describe the documented process, which is not the one running.*

---

## 3. Next target condition

*How the process will operate at a date you name. Not a number you want.*

*This distinction is the whole method. A target is an outcome. A target condition is a description of the process working differently, and the difference matters because you can list the obstacles between here and a described process. You cannot list the obstacles between here and a number.*

*The step is officially called "Establish the **Next** Target Condition." The word is in the name. This is one in a series, not a destination, so make it close: weeks, not quarters.*

| | |
|---|---|
| **The process will operate like this** | |
| **Which should produce** | *The measure you expect to follow.* |
| **Achieve by** | YYYY-MM-DD |

> **Example.** Merging to main triggers a deploy with no ticket and no manual approval, for changes touching only the service layer. Expected: those changes reach production within an hour of merge.

---

## 4. Obstacles

*What stands between the current condition and the target condition. One list, added to as you find more.*

*Work on one at a time. The list is a parking area, not a plan, and the discipline of picking a single obstacle is what stops this becoming a project.*

| Obstacle | Status |
|---|---|
| | *Not started / Working on it now / Cleared / Not an obstacle after all* |

*Keep the ones that turned out not to be obstacles, marked as such. Knowing what you were wrong about is most of what this record is for.*

---

## 5. Experiment cycles

*The working record. One block per cycle, newest at the top. Each is small enough to run in a day or two.*

*The first two fields are filled in before, the last two after. Doing them in that order is what makes this a record of learning rather than a log of activity.*

### Cycle {N}, YYYY-MM-DD

| | |
|---|---|
| **Obstacle being addressed** | |
| **Step taken** | *What you did.* |
| **What we expected** | *Written before running it.* |
| **What actually happened** | |
| **What we learned** | |

*If the expected and actual match every time, the steps are too safe to be teaching you anything. A cycle that surprises you is the one that was worth running.*

---

## Notes on using this template

*Delete this section too.*

**The five coaching questions are the routine, and they are short enough to memorise.** What is the target condition. What is the actual condition now. What obstacles do you think are preventing you from reaching the target condition, and which one are you addressing now. What is your next step, and what do you expect. When can we go and see what we have learned from taking that step.

The second question comes with four follow-ups that are the best-specified experiment structure in this whole group: what did you plan as your last step, what did you expect, what actually happened, what did you learn. Section 5 is those four questions.

**The coach asks questions and does not supply answers.** The routine collapses immediately without this. If the coach knows the answer and gives it, the learner has been told something and practised nothing, and the point of a kata is the practice.

**Set target conditions close.** Far enough out and you cannot see the obstacles, which means you cannot take a next step, which means the routine stops. Guidance on a maximum horizon varies between sources and I could not verify a specific number against Rother's own text, so use the practical test instead: if you cannot list the obstacles, it is too far away.

**PDCA or PDSA.** Rother's material says PDCA throughout, so this template does too. Deming objected to the term, on the grounds that "check" means "to hold back" and that the acronym was not his. That history is in the [group README](README.md) rather than here, because it is a naming argument and this is a working document.

**Where this lives:** version control or a wiki. Sections 3 and 5 hold expectations recorded before the outcome was known, and their only value is that someone can go back and compare. A physical board next to the team works well for the daily cycles, provided the completed cycles get transcribed somewhere they survive.
