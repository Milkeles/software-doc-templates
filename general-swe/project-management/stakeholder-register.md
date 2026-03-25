# Stakeholder Register

> Who can affect this project or be affected by it, what each one actually wants, and who owns the relationship.
>
> **Why "register" and not "map".** The map is the grid you draw from the register. The register is the data, and it is the part that survives contact with the project. PMBOK 7's definition is one sentence but it sets two obligations: the register "records information about project stakeholders, which includes an **assessment** and **classification**". A list of names satisfies neither.
>
> **The famous grid has no evidence behind it, and it is miscredited.** The power/interest grid is routinely attributed to Mendelow (1981). That paper plots **power against environmental dynamism**, for the purpose of allocating environmental scanning effort, and the word "interest" does not appear in it once. Section 4 covers what to use instead and what the grid is still good for.
>
> **Include people who only think they are affected.** PMBOK's definition of stakeholder ends "or perceive itself to be affected by a decision, activity, or outcome". That clause does real work: a vocal team with no objective stake is still a stakeholder, and leaving them out of the register does not make them go away.
>
> **Where it lives.** Wiki, with restricted access. It contains candid assessments of named colleagues, and it should be written knowing that.
>
> **Delete this block before publishing.**

---

## 1. Fields

| Field | Note |
|---|---|
| **Name and role** | A person, not "Marketing". See section 2 |
| **The specific concern** | What they care about on this project. One row per person-per-concern |
| **Assessment** | Power, legitimacy, urgency. See section 3 |
| **Classification** | Which category your scheme puts them in, and which scheme it is |
| **Current stance** | Supportive, neutral, opposed, unaware |
| **Desired stance** | The gap between this and the previous field is what the engagement plan acts on |
| **Communication preference and cadence** | How and how often. Getting this wrong creates opposition on its own |
| **Relationship owner** | Who talks to them |
| **Date last reviewed** | Stakeholder position is not a fixed property. See section 5 |

**Keep the actions somewhere else.** PMBOK 7 splits this into three: the register records who they are, stakeholder analysis is the method that produces the classification, and the **stakeholder engagement plan** holds "the strategies and actions required to promote productive involvement". Merging the plan into the register produces a table too wide to read.

---

## 2. One row per concern, not per person

The most useful refinement in the research literature. Eesley and Lenox proposed the **stakeholder-request-firm triplet** as the unit of analysis, arguing that the attributes of a specific request drive how managers respond, not the standing of the person making it: "a powerful and legitimate stakeholder might make a claim that is seen by managers not only as not urgent but also as illegitimate".

Applied to software, this is concrete. Your head of sales is high power on pricing and commitments, and has no legitimate claim on the database schema. A single "high power" row loses that and produces bad engagement decisions in both directions.

Related, and the reason for naming people rather than departments: Wolfe and Putler's criticism of stakeholder models is that **priorities within a group vary**. "Support wants X" is usually two people who want opposite things.

---

## 3. Assessment: use the model that was tested

Of the two common models, one has been empirically tested and one has not.

**The salience model** (Mitchell, Agle and Wood, *Academy of Management Review*, 1997) classifies stakeholders on three attributes. PMBOK 7 names it as its only stakeholder classification model and credits the authors directly: "power to influence, legitimacy of the stakeholders' relationships with the project, and the urgency of the stakeholders' claim".

Combinations give the categories:

```
   power only ............ dormant       one attribute:
   legitimacy only ....... discretionary   latent, low priority
   urgency only .......... demanding

   power + legitimacy .... dominant      two attributes:
   power + urgency ....... DANGEROUS       expectant, engage actively
   legitimacy + urgency .. dependent

   all three ............. definitive    act now
```

**"Dangerous" is why this model is worth the extra column.** Power and urgency without legitimacy names the stakeholder who can block you, wants it immediately, and has no proper claim. No power/interest grid has an equivalent cell, and every experienced team recognises the person.

**What the evidence supports.** Agle, Mitchell and Sonnenfeld tested the model against data from CEOs of 80 large US firms in 1999. All three attributes significantly predicted salience, and **urgency was the strongest predictor**. Later studies validated it across manufacturing firms in Spain, sporting event committees and environmental accidents.

**What it does not support**, and this is usually omitted: the same study found **no link between stakeholder salience and financial performance**. The model predicts who managers pay attention to. It does not show that paying attention makes money.

**Known criticisms**, all worth carrying:

- It measures *perceived* salience, not actual salience. Currie, Seaton and Wesley proposed involving less biased third parties in identification for this reason.
- It ignores **fringe stakeholders** who currently hold none of the three attributes but will (Hart and Sharma).
- It is not normative enough to guide prioritisation in a crisis (Pajunen).
- It says nothing about *what strategies to use* once you have classified someone (Jawahar and McLaughlin).
- Salience is **gamed, not observed**. Aaltonen and colleagues catalogued eight strategies stakeholders use to raise their own salience. Urgency in particular is manufacturable.

Note also that the strongest published review of the model is by its own authors, twenty years on. Treat the existence of the validating studies as reliable and the framing as partisan.

---

## 4. The power/interest grid

Use it if it helps a conversation. Do not present it as evidence-based, and do not credit it to Mendelow.

Mendelow's 1981 ICIS paper builds a matrix of **power against dynamism**, and its output is how much environmental scanning effort to spend on each quadrant, not "manage closely" and "keep informed". His own words: "a grid may be constructed using Power and Dynamism as the two axes… The task facing us now is the determination of the most suitable scanning process for each quadrant." The figure is captioned "The Power Dynamism Matrix for Environmental Scanning".

The substitution of interest for dynamism is a real conceptual change, not a synonym. Dynamism is the volatility of the stakeholder's power base, an external property. Interest is an attitude. The power/interest form is most reliably traced to Johnson and Scholes' *Exploring Corporate Strategy*.

Two further corrections worth making once, because they appear in textbooks and consultancy decks:

- The citation "Mendelow, A. (1991), Stakeholder Mapping, Proceedings of the 2nd International Conference on Information Systems" is garbled. The second ICIS was in **1981**, and that is not the paper's title.
- **PMBOK 7 contains no power/interest grid at all.** PMI kept the peer-reviewed model and dropped the popular one.

No study tests whether the grid improves stakeholder outcomes. It is a heuristic, and a genuinely useful one for getting a room to agree on something. Label it as such.

---

## 5. Review it, because power moves

Mendelow's actual contribution is the one part of his paper that everyone skips, and it is the best argument for a dated register: "power is situation specific. Should a substitute be available, the originally powerful sole supplier loses the power base."

Stakeholder position is a function of dependency. When the dependency changes, the position changes, often overnight. Re-review at every phase boundary and whenever a dependency shifts: a vendor replaced, a reorganisation, a budget moved, a person promoted.

---

## 6. Handle it carefully

This document contains written judgements about named colleagues, including whether they are opposed to something and how much power they have.

- Restrict access, and say who has it.
- Write every row as though the person will read it, because eventually one will.
- Assess the position, not the person. "Opposed to the migration because it moves reporting away from their team" is defensible. "Difficult" is not.

---

## Common failures in this document

- **A list of names.** PMBOK requires an assessment and a classification.
- **One row per department.** Priorities inside a group are not uniform.
- **One row per person regardless of topic.** Power is per decision, not global.
- **The grid credited to Mendelow.** He plotted power against dynamism.
- **The grid presented as evidence-based.** Nothing tests it.
- **Salience claimed to improve performance.** The 1999 study found no such link.
- **Written once at kickoff.** Power moves when dependencies move.
- **Engagement actions merged in.** They belong in a separate plan.
- **Written as though nobody named will ever read it.** Someone will.

---

## Related documents

- [`project-charter.md`](project-charter.md). Where the key stakeholder list is first named
- [`project-brief.md`](project-brief.md). Who needs to see it before the decision
- [`risk-register.md`](risk-register.md). An opposed stakeholder with power is a risk, and belongs in both
- [`../requirements/vision-and-scope.md`](../requirements/vision-and-scope.md). Where stakeholder needs become stated scope
- [`../foundations/rfc.md`](../foundations/rfc.md). The mechanism for getting technical stakeholders to disagree in writing and early
