# Accessibility

Documents that record what your product does for people who cannot use it the way you do.

For most teams reading this, one of these documents is a legal obligation and the deadline has already passed. That is unusual for this repository, and it changes the tone of the group: elsewhere a skipped document costs you clarity, here it can cost you a procurement or produce a finding.

---

## First: the dates, because they decide whether this is optional

| Regime | Who it binds | Standard | From |
|---|---|---|---|
| **European Accessibility Act**, Directive (EU) 2019/882 | Private companies selling listed products and services to EU consumers | EN 301 549, which routes to WCAG | 28 June 2025 |
| **Web Accessibility Directive**, (EU) 2016/2102 | EU public sector bodies | EN 301 549 | Sites 2019, apps 2021 |
| **UK** PSBAR 2018 | UK public sector bodies | gov.uk now states WCAG 2.2 AA | 23 September 2018 |
| **ADA Title II**, 28 CFR Part 35 | US state and local government | WCAG 2.1 AA | 26 April 2027, or 2028 for small entities |
| **Section 508** | US federal agencies and their suppliers | Revised 508, which routes to WCAG | Long standing |

Two details people get wrong. The EAA covers **services sold to consumers**, including e-commerce, consumer banking, e-books and transport booking, not only products, so a great many private companies are in scope who assumed they were not. And the ADA Title II rule adopts **WCAG 2.1**, not 2.2, with dates that the Department of Justice extended by a year in an interim final rule effective 20 April 2026. Build to 2.2 anyway, but cite 2.1 when you are claiming conformance under that rule.

If none of these binds you, the documents here are still worth writing. They are just no longer urgent.

---

## What WCAG actually requires, since almost every summary gets this wrong

**Current version: WCAG 2.2.** W3C Recommendation 5 October 2023, revised 12 December 2024, and published as ISO/IEC 40500:2025. It added nine success criteria and removed one, 4.1.1 Parsing, which is now marked obsolete. If a policy still requires WCAG 2.0 or 2.1, you may have to keep testing and reporting 4.1.1 even though 2.2 dropped it.

**WCAG 3.0 is not a conformance target.** W3C describes it as "currently an incomplete draft" that is "not expected to be a completed W3C standard for a few more years", with many parts "in an exploratory or developing phase". Do not put it in a plan.

**Conformance is per page, not per site, and there are five requirements, not one.** This is the part that shapes every document here:

1. **Conformance level.** A, AA, or AAA, all criteria at that level and below.
2. **Full pages.** You cannot conform "except for the video player".
3. **Complete processes.** If checkout is five pages and one fails, the process does not conform.
4. **Only accessibility-supported ways of using technologies.** Relying on something no assistive technology actually implements does not count.
5. **Non-interference.** Content that fails may not block access to the rest of the page.

Requirements 2 and 3 are why an honest report is mostly "Partially Supports". They are also why sampling matters, and why the test plan below spends its effort on choosing pages rather than on running tools.

**Do not target AAA across a site.** W3C says so directly: "It is not recommended that Level AAA conformance be required as a general policy for entire sites because it is not possible to satisfy all Level AAA success criteria for some content." The same document is candid about the ceiling: "even content that conforms at the highest level (AAA) will not be accessible to individuals with all types, degrees, or combinations of disability, particularly in the cognitive, language, and learning areas." AA is the target every regulation names. Treat individual AAA criteria as improvements you choose, not a level you claim.

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [Accessibility conformance report](accessibility-conformance-report.md) | Anyone buys from you, especially the public sector | Nobody procures your product | A public URL procurement can reach |
| [Accessibility statement](accessibility-statement.md) | You are an EU or UK public sector body, or want the goodwill | You are not in scope and have no public users | A public page on the site itself |
| [Accessibility test plan](accessibility-test-plan.md) | You are going to claim conformance and need it to be true | You have not started testing at all | Docs-as-code |

Three documents, three different readers. The report is for a buyer comparing vendors. The statement is for a user who just hit a barrier. The test plan is for your own team. Merging any two produces a document that serves neither, which is the single most common failure in this group.

---

## What the conformance table actually looks like

Every other group in this repository has a working surface: a board, a hill, a trace chain. Here it is a table, and its columns are the whole argument.

```
  WCAG 2.2 Level AA

  Criteria                          Level  Conformance         Remarks
  --------------------------------- -----  ------------------  ------------------
  1.1.1 Non-text Content              A    Partially Supports  Charts on the
                                                               reporting page have
                                                               no text alternative.
                                                               Fix planned Q3 2026.
  1.4.3 Contrast (Minimum)           AA    Supports
  2.4.11 Focus Not Obscured (Min)    AA    Does Not Support    Sticky header covers
                                                               focused fields in the
                                                               settings form.
  2.5.8 Target Size (Minimum)        AA    Supports
  3.3.8 Accessible Authentication    AA    Partially Supports  Login requires solving
                                                               a puzzle CAPTCHA with
                                                               no alternative.
```

**The three verdicts have defined meanings and they are not a scale you can round up.** From the US General Services Administration:

- **Supports:** "The functionality of the product has at least one method that meets the criterion without known defects or meets with equivalent facilitation."
- **Partially Supports:** "Some functionality of the product does not meet the criterion."
- **Does Not Support:** "The majority of product functionality does not meet the criterion."

Plus **Not Applicable**, "the criterion is not relevant to the product", and **Not Evaluated**, which may only be used in the Level AAA table.

**The load-bearing fact, stated by GSA and hidden by almost every vendor report: "Partially Supports" means the product is not conformant.** There is no partial credit. A report that is 90 percent "Partially Supports" is a report of a non-conforming product, written in a way that reads like progress.

That tension is what makes the remarks column the real content. A buyer who knows the field skips the verdicts and reads the remarks, because a remark naming a specific broken control on a specific page is evidence somebody tested, and a remark saying "minor issues" is evidence nobody did.

---

## The documents, one by one

### Accessibility conformance report

**When.** Anyone procures your product, and always if you sell to government.

**Why.** The ACR is the document that turns accessibility from a claim into something comparable across vendors. A buyer cannot test five products; they can read five reports in the same format.

**Get the vocabulary right, because it signals whether you know the field.** The **VPAT** is the blank template, published by the Information Technology Industry Council. A VPAT filled in for a specific product is an **ACR**. Saying "here is our VPAT" is saying "here is our blank form". The current template is VPAT 2.5Rev, April 2025, in four editions: WCAG, Revised Section 508, EN 301 549, and INT which covers all three. Pick the edition matching what your buyer must comply with, and check the version before publishing, because ITI revises it.

**Self-assessment is allowed.** There is no rule requiring third-party authorship and no defined evaluator qualification. Anyone claiming otherwise is selling audits. What there is, is a reputational mechanism: a report with vague remarks and universal "Supports" is read as untested by anyone who procures regularly.

**Where.** A public URL, findable without a sales conversation. Buyers screen before they contact you.

### Accessibility statement

**When.** You are an EU or UK public sector body, in which case it is required and its contents are specified. Otherwise when you want users hitting a barrier to have somewhere to go.

**Why.** The statement does something no internal document does: it gives the affected person a named route to a human. Commission Implementing Decision (EU) 2018/1523 sets a model statement, and the mandatory elements are the interesting part, because they are almost all about honesty and recourse rather than about compliance:

- a commitment statement and the scope it covers,
- compliance status, one of fully, partially, or non-compliant,
- the non-accessible content, sorted into non-compliance, disproportionate burden, and out of scope,
- **how the assessment was made**, self-assessment or third-party evaluation,
- a feedback mechanism and a link to it,
- contact details,
- a link to the enforcement procedure.

Review at least annually.

**The disproportionate burden route is real and it is narrow.** You may claim a fix is disproportionate, but you must have done and recorded the assessment. UK government guidance rules out the two excuses teams reach for first: lack of time and lack of knowledge are not valid justifications.

**Where.** A public page on the site, linked from every page. A statement nobody can find has failed at its only job.

### Accessibility test plan

**When.** Before you claim conformance in either of the documents above.

**Why.** Because conformance is a property of full pages and complete processes, and you cannot test every page. The plan is where you decide which pages stand for the rest, and that decision is the one an auditor will question.

**There is an authoritative method, and it is worth following.** W3C's Website Accessibility Conformance Evaluation Methodology, WCAG-EM 2.0, published as a Group Note on 23 July 2026. Five steps: define the evaluation scope, explore the target digital product, select a representative sample, evaluate the sample, report the findings. It is explicitly non-normative and "does not in any way add to or change the requirements defined by the normative WCAG 2 standard", so it is a method for producing a defensible answer rather than a source of requirements.

Note step 5. WCAG-EM produces an **evaluation report**, which is a fourth artefact. The test plan template covers steps 1 to 3 and points at where the output lands. Keep them separate: the plan is stable, the reports accumulate.

**Where.** Docs-as-code. It changes with the product.

---

## Why these documents work, and how good the evidence is

### The problem the documentation solves is absent experience, not carelessness

The reason accessibility defects survive review is not that engineers do not care. It is that a sighted developer using a mouse gets no signal when a focus outline is invisible or a form field has no label. Nothing feels wrong, because nothing is wrong for them.

This is the same structure as the runbook argument in [`general-swe/foundations/`](../../general-swe/foundations/README.md), where a checklist substitutes for recall that degrades at 3am. Here the checklist substitutes for an experience the author cannot have. That is why the criteria are enumerated rather than summarised as a principle: a principle relies on the author noticing, and the author is exactly the person who will not.

This is reasoning about why the format is what it is, not a research finding. Labelled as such.

### Automated testing cannot establish conformance, and the honest number is smaller than vendors imply

The best primary source is the UK Government Digital Service tool audit. They injected **142 known accessibility barriers** into a page and ran **13 automated tools** over it. The best tool found **40 percent** outright, and **50 percent** counting issues it merely flagged for human review.

Two caveats belong with that number. It was last updated in April 2018 and the tools have changed. And it measures detection of injected barriers, not of the barriers real sites have.

**The percentages you will see quoted, usually 30 or 57 percent, come from vendor marketing and have no published methodology.** Use the GDS figure with its date and its method, or use no number and say plainly that automation cannot establish conformance. Do not repeat a bare percentage from a tool's own website in a document whose purpose is credibility.

The practical consequence for the test plan: automation is a regression guard that runs on every commit and catches the same class of error repeatedly. It is not evidence. The evidence is manual testing against a sample you chose deliberately, with assistive technology, by someone who knows how it is actually used.

### Two claims to leave out

**"15 percent of people, or one billion, have a disability."** This is the WHO's 2011 World Report figure and it has been superseded. The current WHO position, from March 2023, is "an estimated 1.3 billion people experience significant disability. This represents 16% of the world's population, or 1 in 6 of us." Note the qualifier: that is significant disability, not any impairment. Quote the current figure with its qualifier, or quote neither.

**Lawsuit counts.** The circulating numbers come from a defence law firm and an accessibility vendor, neither of whom publishes a reproducible method, and there is no official court or DOJ count. Beyond the sourcing problem, there is a strategic one: an accessibility case built on fear of litigation collapses the moment somebody calculates that the expected cost of a lawsuit is lower than the cost of the work. Build the case on the regulations, which have dates, and on the procurement mechanism, which loses you deals you can name.

---

## What to write first

1. **The test plan**, because both other documents assert things that must be true.
2. **The conformance report**, if you sell to anyone who procures.
3. **The statement**, immediately if you are a public sector body, since the deadline has passed.

Write the report last of the two published documents. A report written before the testing is a guess with a version number on it.

---

## Sources

- [WCAG 2.2](https://www.w3.org/TR/WCAG22/), W3C Recommendation 5 October 2023, revised 12 December 2024, also ISO/IEC 40500:2025. Source of the five conformance requirements and the 4.1.1 removal
- [Understanding Conformance](https://www.w3.org/WAI/WCAG22/Understanding/conformance), W3C. Source of both AAA quotations
- [WCAG 3 status](https://www.w3.org/WAI/standards-guidelines/wcag/wcag3-intro/), W3C. Latest draft 3 March 2026, explicitly not a conformance target
- [WCAG-EM 2.0](https://www.w3.org/TR/WCAG-EM/), W3C Group Note, 23 July 2026. Non-normative, five steps
- [VPAT](https://www.itic.org/policy/accessibility/vpat), Information Technology Industry Council. Version 2.5Rev, April 2025, four editions. **Check the current version before publishing a report**
- [Section508.gov ACR guidance](https://www.section508.gov/sell/vpat/), US General Services Administration. Source of the verbatim conformance term definitions and the statement that "Partially Supports" means non-conformant
- [Directive (EU) 2019/882](https://eur-lex.europa.eu/eli/dir/2019/882/oj), European Accessibility Act. Obligations from 28 June 2025
- [Directive (EU) 2016/2102](https://eur-lex.europa.eu/eli/dir/2016/2102/oj) Article 7, and [Commission Implementing Decision (EU) 2018/1523](https://eur-lex.europa.eu/eli/dec_impl/2018/1523/oj) setting the model accessibility statement
- EN 301 549 V3.2.1, ETSI, March 2021, aligned to WCAG 2.1. Draft V4.1.0 dated 2025-11 aligns clauses 9, 10 and 11 to WCAG 2.2
- [ADA Title II web rule](https://www.ada.gov/resources/2024-03-08-web-rule/), 28 CFR Part 35, published 24 April 2024, adopting WCAG 2.1 AA. Compliance dates extended by a DOJ interim final rule effective 20 April 2026
- UK Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018, and [gov.uk accessibility guidance](https://www.gov.uk/guidance/accessibility-requirements-for-public-sector-websites-and-apps)
- [GDS accessibility tool audit](https://alphagov.github.io/accessibility-tool-audit/), UK Government Digital Service. 142 injected barriers, 13 tools, best result 40 percent. Last updated April 2018
- [WHO, Disability and health](https://www.who.int/news-room/fact-sheets/detail/disability-and-health), 7 March 2023. 1.3 billion, 16 percent, significant disability

**On sourcing.** Regulatory dates here are taken from the legislation itself or the enforcing agency, never from a compliance vendor's summary, because those summaries have a commercial interest in the dates being sooner and the obligations broader. Three things could not be verified and are stated as unknown rather than guessed: when EN 301 549 V4.x will be cited in the Official Journal, whether any authority defines who may author an ACR, and any general figure for what proportion of accessibility issues automated tools detect.
