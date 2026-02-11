# Accessibility Conformance Report

> An ACR is a completed VPAT. The VPAT is a blank template published by the Information Technology Industry Council (ITI); once you fill it in with findings about your product, the result is an Accessibility Conformance Report.
>
> **Who reads this.** Procurement officers and accessibility reviewers at organisations deciding whether to buy your product. Not your engineers. Write it for someone who has your competitor's ACR open in the next tab.
>
> **Which edition.** VPAT 2.5Rev (April 2025) ships four editions: WCAG, Section 508 (US federal), EU (EN 301 549), and INT (all three combined). Pick the smallest one that covers the markets you sell into. INT is longer to fill in and longer to read.
>
> **Self-assessment is allowed.** No authority requires a third party to write your ACR, and no standard defines evaluator qualifications. But you must say which you did in Evaluation Methods, and buyers weight that.
>
> **Delete this block before publishing.**

---

## 1. Product information

State the exact thing you tested. A buyer who cannot tell whether the report covers the version they are buying will treat it as covering nothing.

| Field | Content |
|---|---|
| Name of product / version | Include the version number. "Acme Portal 4.2" not "Acme Portal" |
| Report date | Month and year. Findings decay; a date lets the reader judge how far |
| Product description | Two sentences on what it does and who uses it |
| Contact information | A monitored address for accessibility questions, not a general sales inbox |
| Notes | Anything that changes how the tables should be read. Optional |
| Evaluation methods used | See section 2 |

**Scope belongs here too.** If the report covers the customer-facing web app but not the admin console, say so in Notes. An ACR that quietly covers a subset is the single most common complaint buyers raise.

---

## 2. Evaluation methods used

Free text, one paragraph, and the part experienced reviewers read first.

Say:
- **Who evaluated.** Internal team, named third party, or both.
- **What was tested.** Which pages or flows, and how you chose them. If you sampled, say you sampled.
- **How.** Automated tooling plus manual testing plus assistive technology testing, named. Automated tooling alone is not a WCAG evaluation and a reviewer will spot it.
- **On what.** Browser and screen reader combinations, with versions. "NVDA 2025.1 with Firefox 128, VoiceOver with Safari 18 on macOS 15."
- **When.** The test window, if it differs from the report date.

One line example:

> Evaluated by Acme's internal accessibility team in April 2026 against a 12-page representative sample selected per WCAG-EM 2.0, using axe DevTools 4.10 for automated checks followed by manual keyboard and screen reader testing with NVDA 2025.1 / Firefox 128 and VoiceOver / Safari 18.

Avoid "tested with industry-standard tools". It says nothing and reads as evasion.

---

## 3. Applicable standards and guidelines

List what you evaluated against, with links. For a WCAG edition:

- Web Content Accessibility Guidelines 2.2, W3C Recommendation, Level A and Level AA.

WCAG 2.2 became a W3C Recommendation on 5 October 2023 and was revised on 12 December 2024. It is also published as ISO/IEC 40500:2025.

**Do not claim WCAG 3.0.** It is an incomplete W3C draft, not a conformance target, and a claim against it tells a reviewer you do not know the landscape.

**On 4.1.1 Parsing.** WCAG 2.2 removed success criterion 4.1.1. It appears in the VPAT tables marked "(Obsolete and removed)". If a buyer's policy still requires WCAG 2.0 or 2.1, you may need to keep testing and reporting it. Leave the row in and mark it, rather than deleting it.

---

## 4. Conformance tables

One table per level: Level A, Level AA, and Level AAA if you report it.

### Format

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

### The four terms, used exactly as defined

These definitions come from the GSA. Do not paraphrase them and do not invent a fifth term.

| Term | Definition |
|---|---|
| **Supports** | The functionality of the product has at least one method that meets the criterion without known defects or meets with equivalent facilitation |
| **Partially Supports** | Some functionality of the product does not meet the criterion |
| **Does Not Support** | The majority of product functionality does not meet the criterion |
| **Not Applicable** | The criterion is not relevant to the product |
| **Not Evaluated** | Only permitted in the Level AAA table |

Two things follow that people get wrong:

**"Partially Supports" means the product is not conformant.** GSA states this directly. It is not a passing grade with an asterisk. If most of your rows say Partially Supports, your report says you do not conform, however encouraging the word looks.

**"Not Evaluated" is only valid for Level AAA.** You cannot use it to skip an A or AA criterion you did not test. Test it or report Does Not Support.

### Remarks

Required on every row that is not "Supports". A Partially Supports with an empty Remarks column is the reason a procurement reviewer bins a report.

A useful remark names three things: **what fails, where, and what happens next.** "Charts on the reporting page have no text alternative. Fix planned Q3 2026." Not "some images may lack alternative text."

Do not use Remarks to argue the criterion is unfair or that assistive technology should handle it. Buyers read that as a product that will not be fixed.

### The nine criteria new in WCAG 2.2

If you are updating a WCAG 2.1 report, these rows are new and are the ones a reviewer checks first, because an untouched 2.1 report relabelled as 2.2 is easy to spot.

| Criterion | Level |
|---|---|
| 2.4.11 Focus Not Obscured (Minimum) | AA |
| 2.4.12 Focus Not Obscured (Enhanced) | AAA |
| 2.4.13 Focus Appearance | AAA |
| 2.5.7 Dragging Movements | AA |
| 2.5.8 Target Size (Minimum) | AA |
| 3.2.6 Consistent Help | A |
| 3.3.7 Redundant Entry | A |
| 3.3.8 Accessible Authentication (Minimum) | AA |
| 3.3.9 Accessible Authentication (Enhanced) | AAA |

---

## 5. Level AAA

Optional, and usually omitted.

WCAG itself says: "It is not recommended that Level AAA conformance be required as a general policy for entire sites because it is not possible to satisfy all Level AAA success criteria for some content."

Report AAA only where a buyer asked or where you genuinely meet specific criteria worth advertising. "Not Evaluated" is permitted throughout this table and is the honest answer for criteria you did not test.

---

## 6. Legal disclaimer

One short paragraph, if your legal team wants one. Standard practice, and buyers ignore it.

Keep it to the report's scope and date. Do not use it to disclaim the findings themselves; a disclaimer that undercuts the tables makes the whole document worthless to the reader.

---

## Common failures in this document

- **Reporting against WCAG 2.1 and labelling it 2.2.** The nine new criteria give it away.
- **Every row says Supports.** No product of any size conforms fully. A perfect report reads as untested, not as excellent.
- **Automated tooling only.** The best tool in the GDS audit of 13 tools caught 40% of 142 injected barriers outright. A tool-only evaluation misses most of what is wrong.
- **No version number.** The report becomes unusable the moment you ship.
- **Stale.** An ACR older than your last major release describes a product that no longer exists. Refresh on major versions.

---

## Related documents

- [`accessibility-statement.md`](accessibility-statement.md). The public-facing statement. Different audience, different legal basis, overlapping content
- [`accessibility-test-plan.md`](accessibility-test-plan.md). How you produce the findings this report publishes
