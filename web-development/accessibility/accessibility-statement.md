# Accessibility Statement

> A public page on your own site saying how accessible it is, what is not accessible, and how to complain.
>
> **This is the one document in this repository that a law may require you to publish, in a format a law specifies.** EU public sector bodies have owed one since 2019 under the Web Accessibility Directive (EU) 2016/2102 Article 7, in the model form set out by Commission Implementing Decision (EU) 2018/1523. UK public sector bodies owe one under the Public Sector Bodies Accessibility Regulations 2018.
>
> **Not a public sector body?** Write one anyway. It is short, it is the fastest way to give disabled users a route to reach you, and if the European Accessibility Act applies to your service it is how you demonstrate you have thought about this at all.
>
> **Where it lives.** A public URL on the site itself, linked from somewhere persistent such as the footer. The Directive requires it to be published and reachable. A statement in your private wiki satisfies nothing.
>
> **Delete this block before publishing.**

---

## Structure

The section order below follows the Annex to Commission Implementing Decision (EU) 2018/1523. If you are in scope of the Directive, keep the order and keep every mandatory section, even where the answer is short. If you are not in scope, the same structure is still the clearest one available, so use it.

Write it in plain language at the level of the rest of your site. A statement a disabled user cannot read is a joke at their expense.

---

## 1. Commitment statement

One or two sentences naming the organisation and the commitment.

> Acme Council is committed to making its website accessible, in accordance with the Public Sector Bodies (Websites and Mobile Applications) (No. 2) Accessibility Regulations 2018.

Name the actual legal instrument that applies to you. Do not write "we are committed to accessibility for all" and stop; it is the sentence every non-compliant statement opens with.

---

## 2. Scope

Say exactly what this statement covers. A URL, or a list of them, or an app name and platform.

> This statement applies to www.example.gov.uk. It does not cover the separate booking system at book.example.gov.uk, which has its own statement.

If subdomains, apps, or third-party embedded services are excluded, say so here. Silence reads as coverage.

---

## 3. Compliance status

One of three, and you must pick one:

| Status | Means |
|---|---|
| **Fully compliant** | Meets the standard with no exceptions |
| **Partially compliant** | Meets most of it; exceptions listed in section 4 |
| **Non-compliant** | Does not meet the standard |

Name the standard and the level. In the EU this is EN 301 549. In the UK, gov.uk now states WCAG 2.2 Level AA.

> This website is partially compliant with WCAG 2.2 Level AA, due to the non-compliances listed below.

**"Fully compliant" is a strong claim and rarely true.** If you have not tested against every criterion on every page and template, you cannot say it. Partially compliant with an honest list is more credible and legally safer than a full-compliance claim a regulator can disprove in an afternoon.

---

## 4. Non-accessible content

The substance of the document. Split into three subsections, because the legal consequences differ.

### 4.1 Non-compliance with the accessibility standard

Things that are simply broken and that you intend to fix.

For each: **what fails, which criterion, and when you will fix it.**

> Some PDFs published before September 2018 are not tagged, so screen readers cannot read them in order. This fails WCAG 2.2 success criterion 1.3.1 (Info and Relationships). We plan to replace these with accessible HTML pages by December 2026.

A date is what makes this section useful. "We are working to fix this" with no date is what regulators and complainants read as no plan.

### 4.2 Disproportionate burden

Content you have assessed as too costly to fix relative to the benefit, and are claiming an exemption for.

This is a legal assessment, not a shrug. It requires you to have weighed the cost against the size of your organisation, your resources, and the benefit to disabled users, and to be able to show that working.

**Lack of time or knowledge is explicitly not a valid reason.** UK government guidance states this directly. Neither is "the vendor has not fixed it", unless you can show what you did about the vendor.

Reassess it. A burden that was disproportionate in 2024 may not be after a platform migration.

> [Content item]. We assessed the cost of remediation as disproportionate under [regulation], because [the specific weighing]. We will reassess this by [date].

If you have nothing to claim here, write "We have not made any disproportionate burden claims." Do not delete the heading.

### 4.3 Content not within scope of the legislation

Content the law does not reach. The exemptions vary by regime; common ones include pre-recorded time-based media published before the regulations applied, live audio, archives that are not updated, and third-party content you neither fund nor develop nor control.

> Live video streams do not have captions. Live video is exempt under regulation 4(2)(e).

Cite the exemption. An uncited scope claim is an unsupported claim.

---

## 5. Preparation of this statement

Three facts, all required.

- **The date this statement was prepared.**
- **The date of the last review or evaluation.**
- **How the assessment was done:** self-assessment, or evaluation by a third party. If third party, name them.

> This statement was prepared on 12 May 2026. It was last reviewed on 12 May 2026. The website was tested by [organisation] using a representative sample of pages selected per WCAG-EM 2.0.

**Review at least annually**, and after any significant change to the site. The Directive requires periodic review. A statement four years old dated to the week you launched is evidence you stopped looking.

---

## 6. Feedback and contact information

How a person tells you something is inaccessible, and how they get the content another way.

Give at least two routes. Not everyone who needs this can use a web form.

> If you cannot access part of this site, or need information in a different format such as accessible PDF, large print, easy read, audio recording or braille:
>
> - email accessibility@example.org
> - call 0300 000 0000
>
> We will reply within 5 working days.

**State a response time and meet it.** A feedback mechanism nobody answers is worse than none, because it converts a fixable problem into evidence of indifference.

The mechanism must be accessible itself. A contact form failing WCAG in an accessibility statement is the most common self-inflicted wound in this document.

---

## 7. Enforcement procedure

Where to escalate if your response is unsatisfactory. Required, and this is where the statement stops being a marketing page.

Link to the actual national enforcement body. It differs by country: in the UK, the Equality and Human Rights Commission, or the Equality Commission for Northern Ireland. In EU member states, the body designated under Article 9 of the Directive.

> If you are not happy with our response, contact the Equality and Human Rights Commission (EHRC) via the Equality Advisory and Support Service: [link].

---

## Optional: what we are doing to improve

Not required by the Directive, and useful anyway.

A short statement of the plan: an audit schedule, training, procurement rules requiring an ACR from vendors. Keep it to commitments with dates. Aspirations without dates weaken everything above them.

---

## Common failures in this document

- **Published, then never touched.** The most common failure by a wide margin, and the easiest for a regulator to detect from the preparation date alone.
- **"Fully compliant" with no evidence.** One disprovable claim discredits the whole statement.
- **Non-accessible content section left empty** while the compliance status says partially compliant. The two contradict.
- **Disproportionate burden used as a bin** for anything expensive, with no assessment behind it.
- **No enforcement link.** Removes the only route a user has when you do not reply.
- **The statement itself is inaccessible.** Test it like any other page.

---

## Related documents

- [`accessibility-conformance-report.md`](accessibility-conformance-report.md). The buyer-facing report. Same findings, different reader and different format. The statement is for users of your site; the ACR is for organisations deciding whether to buy it
- [`accessibility-test-plan.md`](accessibility-test-plan.md). Produces the findings this statement summarises
