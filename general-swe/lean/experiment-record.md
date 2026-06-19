# Experiment: {What we think is true}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | |
| **Written** | YYYY-MM-DD *(before running it, or this document does nothing)* |
| **Decided** | YYYY-MM-DD |
| **Outcome** | *Confirmed / Refuted / Inconclusive* |

*Sections 1 to 5 are written before the experiment runs. Sections 6 and 7 after. The order is the entire mechanism: a prediction recorded after the result is not a prediction.*

*Why bother. Microsoft's experimentation team reported that "only about 1/3 of ideas improve the metrics they were designed to improve", splitting roughly one third good, one third flat, one third negative. Their own caveat is worth keeping with the number: teams run experiments when they are unsure, so there is selection bias. Even so, most confident ideas do nothing. You will not remember which of yours were which unless you wrote them down first.*

---

## 1. Belief

*What you think is true, stated so that it could turn out false.*

*Write the belief, not the feature. "Users abandon signup at the payment step because they do not trust an unfamiliar processor" is a belief. "Add PayPal" is a plan, and a plan cannot be wrong, only unfinished.*

*If you cannot imagine the result that would make you drop this, you do not have a hypothesis yet.*

---

## 2. What we already know

*The evidence you have now, and how strong it is.*

*Separate what you measured from what you were told from what you assume. Most experiments that waste a month test something the existing data already answered.*

---

## 3. Prediction

*What you expect to happen, with a number and a direction.*

| | |
|---|---|
| **Measure** | *One primary measure. Name it precisely enough that two people compute it the same way.* |
| **Current value** | *Measured, not estimated. If you do not know it, that is the first experiment.* |
| **Predicted value** | *A number. Guess if you must.* |
| **Guardrail measures** | *What must not get worse. Latency, error rate, support volume, revenue.* |

*Guardrails are how you find out that your improvement moved the cost somewhere else. An experiment with no guardrail can only succeed.*

---

## 4. Method

*What you will do, on whom, for how long.*

| | |
|---|---|
| **Change** | |
| **Who sees it** | *Population, and how they are split.* |
| **Duration or sample** | *Decided in advance.* |
| **How the split works** | *Randomised, by cohort, before and after. Say which, because it decides what you may conclude.* |

*Fix the duration before starting. Stopping when the numbers look good is the most common way a team produces a result that does not survive shipping.*

*A before and after comparison is a legitimate method when a split is impossible. It is also much weaker, because anything else that changed in the period is inside your result. Say so here rather than reporting it later as if it were a controlled test.*

---

## 5. What we will do about it

*Both answers, written before you know which one you get.*

| | |
|---|---|
| **If confirmed** | |
| **If refuted** | |
| **If inconclusive** | *The most likely outcome and the one nobody plans for.* |

*Deciding this in advance is what stops a refuted result being reinterpreted into a partial success. It will be, otherwise. Everyone does it and nobody notices doing it.*

**Stop condition.** *The result that would make you abandon this direction entirely, not just this experiment. Optional, and not part of any standard method. It is here because the alternative is running variations of the same idea until something crosses a threshold by chance.*

---

## 6. What happened

*The result. Numbers first.*

| Measure | Predicted | Actual |
|---|---|---|
| | | |

*Include the guardrails. Include the measures that did not move.*

*Report what happened before interpreting it. Keeping the two separated is what makes this document useful to someone reading it in a year.*

---

## 7. What we learned

*What you now believe that you did not believe before.*

*The valuable case is the miss. If the prediction was wrong, say by how much and what you think you misunderstood. A record showing only confirmed hypotheses is a record of experiments that were not needed.*

**Decision.** *What is happening as a result, per section 5.*

---

## Notes on using this template

*Delete this section too.*

**If it is not written before the result, it is not an experiment.** This is the only rule here that cannot be relaxed. Everything else on the page is a convenience.

**One primary measure.** With five measures and a normal amount of noise, something will move, and you will believe it. Pick the one the belief is about and treat the rest as guardrails.

**Refuted is a good outcome and needs saying out loud.** If two thirds of ideas do nothing or harm, then finding out cheaply is the value being produced. A team that treats refutation as failure will stop running experiments it might lose, which are the only informative ones.

**Keep the weak experiments distinguishable from the strong ones.** A randomised split with a preset duration and a before-and-after eyeball are both recorded here, and they support very different conclusions. Section 4 exists so a later reader can tell which they are looking at.

**Where this lives:** version control or a wiki, and it must survive. This document's entire value is retrospective. Unlike the [A3](a3.md) and the [value stream map](value-stream-map.md), where the making is the point and the artefact is disposable, here the artefact is the point: it is a prediction preserved past the moment it could be quietly revised.

---

## Related documents

- [`a3.md`](a3.md). Section 5 of the A3 predicts a number the same way this document does; both fail the same way if the prediction is written after the result is known
- [`value-stream-map.md`](value-stream-map.md). The future-state changes in section 6 are predictions about a queue or handoff; write them up here once tested rather than trusting memory of what was expected
- [`improvement-kata.md`](improvement-kata.md). Section 5's cycle blocks are this same discipline embedded in a daily routine; use this document on its own when the prediction does not belong to an ongoing kata
