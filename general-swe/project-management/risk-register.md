# Risk Register

> The list of things that could go wrong, each with an owner and something to watch for.
>
> **Also called:** Risk Log.
>
> **Read this before you build a 5×5 matrix.** The peer-reviewed evidence against ordinal risk matrices is strong, mathematical, and has never been refuted. Cox's 2008 analysis in *Risk Analysis* found they "can correctly and unambiguously compare only a small fraction (e.g., less than 10%) of randomly selected pairs of hazards", can "mistakenly assign higher qualitative ratings to quantitatively smaller risks", and for risks with negatively correlated frequency and severity can be "worse than useless, leading to worse-than-random decisions". Thirteen years later, Sutherland and colleagues still opened their randomised study by noting "there has been little empirical work on their effectiveness in supporting understanding and decision making".
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

That last field is the one to fight for. Krisper's survey of problems with risk matrices names the reason bad risk practice never self-corrects: the outcome "eventually occurs, hence there is no immediate feedback". Without a column recording what actually happened, a team can score risks badly for a decade and never find out.

**Keep the register separate from the risk report.** PMBOK 7 defines both: the register holds individual risks, the report holds overall project risk. Merging them produces a document that is too long to update and too coarse to act on.

---

## 2. Write risks as causal statements

Most scoring disagreements are description problems wearing a scoring costume. Krisper's ambiguity problem is that "the scales are often not defined precisely, and therefore can be argued and judged differently based on the experts' opinion", but the same is true of the risk text itself.

Use a fixed form:

> **Because** [fact about the world], **[event] may happen**, **leading to** [consequence in units].

> Because the payment provider contract expires on 30 June and renegotiation has not started, we may lose card processing for a period, leading to zero revenue for the duration of the outage.

Compare: "Payment provider risk. High." Two people rating the second will not agree. Two people rating the first are arguing about the world rather than about words.

---

## 3. Review, or do not bother

A register written once at kickoff is decoration.

- Review on a fixed cadence, short and boring. Fifteen minutes, whoever owns each open risk.
- Close risks explicitly, with the reason. "No longer relevant because the contract was signed."
- Add the outcome when a risk fires. This is the calibration loop.
- Escalate on the trigger, not on the score. The trigger is observable; the score is an opinion.

---

## 4. If you score, score honestly

Scoring is not forbidden. Ordinal scoring, multiplied and coloured, is what the evidence attacks. Three cheap changes remove most of the problem.

**Use numbers, not categories.** Cox's proofs are about ordinal categorisation. A probability of "15%" and an impact of "three weeks" are not subject to range compression, cannot be inverted by a colouring scheme, and can be multiplied to give an expected value that actually means something. This costs nothing and is the single highest-value change available.

**If you must have a matrix, use geometric axis labels.** Levine argued in 2012 that logarithmically scaled axes reduce range compression, because real likelihoods and consequences span orders of magnitude. Sutherland and colleagues tested this: in two randomised online experiments with **2,699 participants** they found "a nonlinear/geometric labeling scheme helps matrix comprehension", and that comprehension "might be enhanced by integrating further details about the likelihood and impact onto the axes of the matrix rather than putting them in a separate key". They also found risk matrices "are not always superior to text for the presentation of risk information".

**Never allocate budget by the composite score.** Cox is explicit: "Effective allocation of resources to risk-reducing countermeasures cannot be based on the categories provided by risk matrices."

Two more findings worth telling your team once:

**Scores are not reproducible.** Ball and Watt found that "different risk assessors may assign vastly different ratings to the same hazard" and that "even following lengthy reflection and learning scatter remains high". Training did not fix it. Their context was public leisure activities rather than software, so do not overstate the transfer, but the mechanism is human rather than domain-specific. A score is a conversation starter, not a measurement.

**Consistent colouring is mathematically constrained.** Cox proves there is no consistent colouring for a 2×2 or 3×3 matrix, and only very restricted ones above that. For the standard 5×5 there are two, and the one your organisation drew freehand is almost certainly not one of them.

---

## 5. When the matrix is mandatory

Regulated and safety-critical contexts often require one. IEC 31010:2019 catalogues the consequence/likelihood matrix at §B.10.3, so if a certifying body expects it, produce it.

Note what that standard actually is: Annex B summarises **41 techniques** with their uses, strengths and limitations. The matrix is one entry in a catalogue, presented with its limits, not an endorsement. Cox's own conclusion is similarly moderate: matrices "should be used with caution, and only with careful explanations of embedded judgments". He does not say never.

The defensible position is that **the burden of proof is on the matrix**, not on the alternative. Produce one where required, keep the numeric fields alongside it, and drive decisions from the numbers.

---

## 6. What not to say about project risk

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
