# Project Brief

> The short document that gets a project taken seriously enough to plan properly.
>
> **Say which brief you mean, because there are at least three.** They have different authors, different audiences and opposite lifecycles, and a template that does not pick one is useless for all three.
>
> | Sense | Written by | Written for | Purpose | Lifecycle |
> |---|---|---|---|---|
> | **PRINCE2 Project Brief** | Project manager | Project board | Get approval to spend on *planning* | Discarded once the PID exists |
> | **RIBA Project Brief** | Client with the design team | Design team | Requirements detailed enough to start design | Superseded at the end of Stage 2 |
> | **Creative or agency brief** | The client | The delivery team | Direct the work | Live for the whole engagement |
>
> **This template is the first sense**, adapted for software: written by the team that would do the work, for whoever controls the money, to earn the right to plan. Section 6 covers what to change if you meant one of the others.
>
> **It authorises nothing.** That is the difference from a [charter](project-charter.md). PMBOK 7 lists brief and charter as separate strategy artifacts, and the charter's definition contains "formally authorizes" and "authority" while the brief's contains neither. If your brief is used to approve spend, you have written a charter and should call it one.
>
> **Not necessarily short.** PMBOK 7 says a brief gives "a high-level overview". RIBA says it holds "detailed requirements… to enable the design team to begin design work". Those are directly contradictory, and the RIBA brief is the more detailed document. Do not assume brief means brief.
>
> **Where it lives.** Wiki. Short-lived, widely read, edited by people outside the repo.
>
> **Delete this block before publishing.**

---

## 1. The problem

Start here, not with the solution. One paragraph on what is wrong today, for whom, and what it costs.

Write it so someone could disagree with it. "Onboarding is slow" is not disagreeable. "New customers take 11 days on average to reach first successful API call, and 40% never do" is.

---

## 2. Why now

The question a funder actually asks and most briefs skip. Something changed: a contract, a deadline, a competitor, a cost that crossed a threshold, a dependency going end of life.

If nothing changed, say so honestly. "Nothing has changed, this has been broken for two years and we think it is now the highest-value thing available" is a legitimate answer and a more credible one than an invented urgency.

---

## 3. What we think we would build

A paragraph and a rough shape. Not a design.

The point is to let the reader judge scale, not approach. If two approaches are genuinely open, name both and say the choice is part of what planning would settle.

---

## 4. What is out of scope

Longer than section 3, usually, and more useful. Every reader silently assumes their own favourite adjacent problem is included.

---

## 5. What we are asking for

The ask, stated concretely. This is the section that makes it a brief rather than an essay.

> **We are asking for:** two engineers for three weeks to produce a plan and a firm estimate.
> **We are not yet asking for:** approval to build.
> **The decision we want from you:** yes or no by [date].

Naming the decision and the date is what converts a document into a gate. Without it a brief circulates indefinitely.

**Keep the justification thin on purpose.** PRINCE2 puts an *outline* business case in the brief, at a level "sufficient only to justify spending on initiation". Building a full business case before you are funded to think is the cost the two-gate structure exists to avoid.

---

## 6. Adapting this template

**If the brief comes from the client rather than the team**, the direction of travel reverses and the sections change: the client states outcomes, constraints, mandatories and success measures, and the team responds. Getting this backwards is the most common template error, because "project brief" is used for both directions in different industries.

**If you are briefing design work**, RIBA's four elements are the best-specified version available and transfer well: project outcomes, sustainability outcomes, quality aspirations and spatial requirements. Two pieces of RIBA guidance are worth stealing verbatim. On quality: aspirations "can be conveyed by written statements but are better expressed using images from similar exemplar projects". On outcomes: the challenge is "how success can be measured. This requires objective data, but any information-gathering exercise is likely to yield highly subjective responses."

RIBA also does something almost nobody else does and everybody needs: it defines **Project Brief Derogations**, a record used "to identify and agree where aspects of the design do not need to comply with the Project Brief". A named, agreed mechanism for the brief turning out to be wrong beats silent divergence. Add one.

---

## 7. Why the brief is worth getting right

RIBA states the case more plainly than any software source: "It is foolhardy to believe that where the outcomes from one stage are poor, they can be recovered in the next stage. For example: a poor Project Brief is likely to lead to poor design outcomes."

There is also a measured reason to distrust your own judgement of your brief. The BetterBriefs Project surveyed over 1,700 marketers and agency staff across more than 70 countries, launched at IPA EffWorks Global in October 2021. **80% of the people writing briefs said they wrote good ones. 10% of the people receiving them agreed.** On whether briefs give clear strategic direction the split was 78% against 5%; on clear, concise language, 83% against 7%. Around 70% of both groups reported frequent rebriefing.

The practical conclusion is not that briefs are bad. It is that **the author cannot assess their own brief**, which is the argument for a template with explicit acceptance criteria and a named reader who signs it off.

The same study's widely quoted claim that 33% of marketing budget is wasted through poor briefs is a **self-reported estimate by survey respondents**, not a measurement, and the "$200bn" headlines derived from it are a further extrapolation that is not in the research. The perception gap is the defensible finding. Use that.

---

## Common failures in this document

- **Used to approve spend.** Then it is a [charter](project-charter.md) and should say so.
- **Direction of travel unclear.** Team-to-funder and client-to-team briefs are different documents.
- **A full business case.** Defeats the purpose of a cheap first gate.
- **No named decision and no date.** Circulates instead of resolving.
- **Out of scope missing.** Every reader assumes their own pet problem is included.
- **Self-assessed as good.** 80% of authors think so; 10% of readers agree.
- **No mechanism for being wrong.** RIBA's derogations record is the model.

---

## Related documents

- [`project-charter.md`](project-charter.md). The document that does authorise, and what it must contain
- [`../requirements/vision-and-scope.md`](../requirements/vision-and-scope.md). Where this grows into a real scope statement if approved
- [`stakeholder-register.md`](stakeholder-register.md). Who needs to see the brief before it is decided
- [`../lean/`](../lean/). If the honest answer is "we do not know whether this is worth building"
- [`../shape-up/`](../shape-up/). If you fix time and vary scope, the shaped pitch is this document's closest relative
