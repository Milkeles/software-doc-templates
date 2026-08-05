# Risk Register

> The list of things that could go wrong, each with an owner and something to watch for.
>
> **Also called:** Risk Log.
>
> **Read this before you build a 5×5 matrix.** Scoring risks as High, Medium and Low does far less than it looks. Two risks land in the same cell when one is ten times the size of the other, a smaller risk can come out coloured red while a larger one stays amber, and where likelihood and severity pull against each other the ranking can be worse than picking at random. This is settled and has never been credibly disputed, which is why the matrix is the part of this document to trust least.
>
> **So the score is not the document.** Make **owner**, **trigger** and **response** the load-bearing fields. If you score, use real numbers, not 1 to 5. Section 4 explains why that alone avoids most of the problem.
>
> **This is a record, not a baseline.** In PRINCE2's classification it changes continuously and is not under change control. Do not put it through an approval process; put it through a review cadence.
>
> **Where it lives.** Wherever it will actually be updated weekly. A wiki page or a tracker, not a document that needs a pull request. The *policy* on how you treat risk belongs elsewhere; the register is data.
>
> **Delete this block before publishing.**

---

## 1. Fields

Ordered by how much each one changes an outcome.

| Field | Why it earns its place |
|---|---|
| **ID** | Stable, never reused, so a decision record can cite it |
| **Risk statement** | Causal form. See section 2 |
| **Owner** | A named person. PMBOK 7 lists "the person responsible for managing the risk" first |
| **Response type and action** | Avoid, reduce, transfer, accept. Then the specific action. The only field that changes the future |
| **Trigger or early-warning indicator** | The observable that says this is happening now |
| **Probability** | A number or an explicit range: "15%", "10 to 20%". Not "medium" |
| **Impact** | Native units: three weeks, £40k, 12,000 users. Not "high" |
| **Status and date last reviewed** | A register nobody re-reads is a liability |
| **Did it occur?** | Closed after the fact. Almost never present, and the only thing that would make your estimates improve |

That last field is the one to fight for. Risk work never corrects itself, because the thing you predicted arrives months later and nobody goes back to check the guess. Without a column recording what actually happened, a team can score risks badly for a decade and never find out.

**Keep the register separate from the risk report.** PMBOK 7 defines both: the register holds individual risks, the report holds overall project risk. Merging them produces a document that is too long to update and too coarse to act on.

---

## 2. Write risks as causal statements

Most scoring disagreements are description problems wearing a scoring costume. Krisper's ambiguity problem is that "the scales are often not defined precisely, and therefore can be argued and judged differently based on the experts' opinion", but the same is true of the risk text itself.

Use a fixed form:

> **Because** [fact about the world], **[event] may happen**, **leading to** [consequence in units].

> Because the payment provider contract expires on 30 June and renegotiation has not started, we may lose card processing for a period, leading to zero revenue for the duration of the outage.

Compare: "Payment provider risk. High." Two people rating the second will not agree. Two people rating the first are arguing about the world rather than about words.

---

## 3. Review cadence
A register written once at kickoff is decoration.

- Review on a fixed cadence, short and boring. Fifteen minutes, whoever owns each open risk.
- Close risks explicitly, with the reason. "No longer relevant because the contract was signed."
- Add the outcome when a risk fires. This is the calibration loop.
- Escalate on the trigger, not on the score. The trigger is observable; the score is an opinion.

---

## 4. If you score, score honestly

Scoring is not forbidden. What fails is the ordinal kind: a 1-to-5 rating, multiplied, then coloured. Three cheap changes remove most of the problem.

**Use numbers, not categories.** "15% likely" and "costs three weeks" cannot be squashed into the same band as something ten times bigger, cannot be flipped by a colouring scheme, and multiply into an expected value that means something. This costs nothing and is the single highest-value change available.

**If you must have a matrix, label the axes geometrically.** Real likelihoods and costs span orders of magnitude, so linear bands compress the top end into one cell. Axes that step by powers — 1%, 10%, 100% rather than Low, Medium, High — measurably help people read the thing. Put the definitions on the axes themselves rather than in a separate key, and accept that plain sentences often communicate a risk better than any grid.

**Never allocate budget by the composite score.** The number is not accurate enough to divide money with. Use it to decide what to talk about, then decide spending on the individual risk.

Two more things worth telling your team once:

**Two people scoring the same risk will not agree**, and more training does not close the gap. A score is a conversation starter, not a measurement. Treat a disagreement about a score as the useful part, not as noise to be averaged away.

**Most hand-drawn colour schemes are inconsistent.** There is no way to colour a small grid so that the colours never contradict the underlying arithmetic, and for the standard 5×5 there are only two schemes that work. The one your organisation drew freehand is almost certainly not one of them, which is another reason not to let the colour make the decision.

---

## 5. When the matrix is mandatory

Regulated and safety-critical contexts often require one. IEC 31010:2019 catalogues the consequence/likelihood matrix at §B.10.3, so if a certifying body expects it, produce it.

Note what that standard actually is: Annex B summarises **41 techniques** with their uses, strengths and limitations. The matrix is one entry in a catalogue, presented with its limits, not an endorsement. Cox's own conclusion is similarly moderate: matrices "should be used with caution, and only with careful explanations of embedded judgments". He does not say never.

The defensible position is that **the burden of proof is on the matrix**, not on the alternative. Produce one where required, keep the numeric fields alongside it, and drive decisions from the numbers.

---

## 6. Language to avoid
Almost every risk document opens with a failure statistic, and the usual one does not survive checking.

The Standish CHAOS success and failure percentages are artefacts of Standish's definitions rather than measurements. Eveleens and Verhoef examined 5,457 forecasts across 1,211 real projects for *IEEE Software* in 2010 and concluded the definitions "are misleading, one-sided, pervert the estimation practice, and result in meaningless figures". Their sharpest demonstration: taking a real organisation with a 6% Standish success rate and flipping the sign of every deviation produced an identical fictitious organisation with a **94%** success rate and exactly the same forecasting quality. In their sample the organisation with the worst forecasts had the highest Standish success rate.

Standish's own response to the authors was that its reports "should be considered Standish opinion and the reader bears all risk in the use of this opinion", a disclaimer the authors noted had never appeared in the reports themselves. Robert Glass, Magne Jørgensen and Nicholas Zvegintzov had raised related objections earlier.

If you need a number, use forecast-to-actual data from your own projects. If you do not have any, that is worth saying, and it is a better argument for a register than a borrowed statistic.

---

## Common failures in this document

- **The score is the document.** Owner, trigger and response are what change outcomes.
- **Ordinal 1 to 5 scales multiplied together.** Range compression and risk inversion follow.
- **Budget allocated by rating.** Cox says explicitly this cannot be done.
- **Vague risk text.** Most scoring disagreements are description disagreements.
- **Written at kickoff, never reviewed.** Decoration.
- **No outcome column.** The estimates never improve because nobody ever finds out.
- **Register and risk report merged.** Too long to maintain, too coarse to act on.
- **Opens with a CHAOS statistic.** Refuted in *IEEE Software* in 2010.

---

## Related documents

- [`project-charter.md`](project-charter.md). Where overall project risk is stated once, at a level a sponsor reads
- [`../foundations/threat-model.md`](../foundations/threat-model.md). The same discipline for security specifically
- [`../security-and-compliance/data-protection-impact-assessment.md`](../security-and-compliance/data-protection-impact-assessment.md). Risk to people rather than to the project
- [`../foundations/incident-postmortem.md`](../foundations/incident-postmortem.md). Where a risk that fired gets examined
- [`stakeholder-register.md`](stakeholder-register.md). Several of your largest risks are people, not systems
