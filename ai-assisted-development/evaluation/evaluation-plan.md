# Evaluation plan: {Feature or agent behavior}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | |
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

*This defines the method: what "good enough" means for this feature and how that gets measured. The record of actually running it belongs in the [eval run log](eval-run-log.md), not here.*

---

## 1. Why this needs an evaluation, not just tests

*State plainly what about this feature depends on a model's judgment rather than deterministic logic, and therefore can't be fully covered by the test templates elsewhere in this repository. If a simpler, non-agentic approach would work as well, say so: adding evaluation overhead for a model call that a plain function would have handled is a cost with no matching benefit.*

---

## 2. What's being measured

| | |
|---|---|
| **Task or behavior under evaluation** | |
| **What "correct" or "good enough" means here** | *Be concrete. "The response is helpful" is not gradable; "the response includes the correct account balance and does not disclose other customers' data" is* |
| **Partial credit?** | *Is this graded pass/fail, or on a scale? A model that gets most of the way there is often meaningfully better than one that fails outright; say whether that distinction matters here* |

---

## 3. Eval set

| | |
|---|---|
| **Sources** | *Real production examples, domain-expert-written cases, synthetic cases, or a mix. State the mix, since an eval set that doesn't resemble real traffic validates the wrong thing* |
| **Edge cases covered** | *Beyond the happy path: unusual input formats, ambiguous or multi-part requests, and adversarial input, at minimum* |
| **Set size** | |
| **Where the set lives** | |

---

## 4. Grading method

| | |
|---|---|
| **Method** | *Deterministic (exact match, string match, an executable check), model-graded (an LLM judge), human review, or a mix* |
| **Why this method** | *Deterministic grading is cheap and reliable but misses nuance; a model judge scales further than a human but needs its own calibration; human review is the highest quality and the slowest. State the tradeoff you're accepting* |

*If any part of this uses an LLM judge, fill in the rest of this section. Otherwise delete it.*

| | |
|---|---|
| **Bias controls** | *Response order (position bias) and response length (verbosity bias) are both documented ways an LLM judge can be misled independent of actual quality. State how each is controlled for* |
| **Human calibration** | *How the judge's agreement with human ratings was checked before trusting it at scale, and how often that check gets repeated* |

---

## 5. Cadence

| | |
|---|---|
| **Runs on** | *Every change, a fixed schedule, or both* |
| **Where results are recorded** | *Link the [eval run log](eval-run-log.md)* |

---

## Notes on using this template

*Delete this section too.*

**Justify the complexity before measuring it.** An evaluation plan is itself evidence for or against using an agent at all. If a simpler workflow would score just as well, that's a valid finding, not a wasted plan.

**Make "good enough" concrete before grading anything.** A vague success criterion produces a vague eval no matter how sophisticated the grading method is. If you can't state what a correct response looks like in one or two concrete sentences, that's the thing to fix first.

**An eval set that doesn't look like production traffic tells you about the eval set, not the system.** Bias in the eval set toward easy or unrepresentative cases is one of the most common ways an evaluation plan produces a false sense of confidence.

**Don't trust an LLM judge without checking it against humans first.** A judge that hasn't been calibrated against human ratings can be confidently wrong in a consistent direction, which is worse than being randomly wrong, since it won't show up as noise.

**Where this lives:** wherever the team already tracks engineering methodology, reviewed on a set cadence alongside the rest of that methodology.

---

## Related documents

- [`eval-run-log.md`](eval-run-log.md). Where the results of actually running this plan accumulate over time
- [`../../general-swe/foundations/test-strategy.md`](../../general-swe/foundations/test-strategy.md). The deterministic-code counterpart to this document
- [`../specification/agent-task-specification.md`](../specification/agent-task-specification.md). Where this plan's verification step originates, for a single task rather than a standing feature
