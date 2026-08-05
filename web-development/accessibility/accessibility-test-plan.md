# Accessibility Test Plan

> How you will find out whether your product is accessible, written down before you start testing rather than reconstructed after.
>
> **Why it exists.** Accessibility testing without a plan converges on whatever the tooling reports, because that is the path of least resistance. The plan is what forces the manual and assistive technology testing to happen, and what makes two evaluations six months apart comparable.
>
> **The spine is WCAG-EM 2.0**, the W3C Website Accessibility Conformance Evaluation Methodology (W3C Group Note, 23 July 2026, superseding the 2014 version). It is non-normative and says so: "This document does not in any way add to or change the requirements defined by the normative WCAG 2 standard." It is a method for evaluating, not a standard to conform to. Use it because it gives sampling a defensible basis, not because anyone requires it.
>
> **Where it lives.** Docs-as-code. It is a test plan; it belongs with the tests.
>
> **Delete this block before publishing.**

---

## 1. Scope

WCAG-EM step 1. Get this wrong and everything downstream is wrong.

State four things:

**What is being evaluated.** The set of pages or screens. Define it by rule, not by list: "all pages under www.example.com, excluding the legacy help centre at help.example.com". A boundary a reader can apply themselves survives new pages being added.

**The conformance target.** Which standard, which level. WCAG 2.2 Level AA is the usual answer, and the one most regulation now points at. State it explicitly rather than assuming.

**Accessibility support baseline.** Which browser and assistive technology combinations you consider supported. WCAG conformance requirement 4 ("Only Accessibility-Supported Ways of Using Technologies") depends on this, and almost every test plan skips it. Without a baseline, "does it work with a screen reader" has no answer.

> Supported: NVDA (latest) with Firefox ESR and Chrome stable; JAWS (latest) with Chrome stable; VoiceOver with Safari on macOS and iOS; TalkBack with Chrome on Android.

**Whether you are testing additional requirements.** Organisational rules beyond WCAG, if you have them. Say so, and keep them in a separate list so a reader can tell what is standard and what is yours.

---

## 2. Explore the product

WCAG-EM step 2. Done before sampling, because you cannot sample a thing you have not surveyed.

Record:

| What to identify | Why it matters for sampling |
|---|---|
| Common pages and page types | Templates repeat; one bad template is a hundred bad pages |
| Essential functionality | Anything a user must complete. These become complete processes |
| Types of content | Text, images, video, data tables, PDFs, generated documents |
| Technologies relied upon | Frameworks, component libraries, embedded third parties |
| Variations | Responsive breakpoints, themes, logged-in versus anonymous, locales |

This step produces an inventory, not a judgement. Keep it in the plan; it is what a later evaluator uses to check your sample was fair.

---

## 3. Sample

WCAG-EM step 3, and the section that determines whether the evaluation means anything.

Testing every page is not possible above trivial size, so you sample and defend the sample.

### Structured sample

Chosen deliberately to cover the exploration inventory. Include:

- The home page and the primary entry points.
- One page of **each distinct template or page type**.
- **Complete processes end to end.** WCAG conformance requirement 3 is that if a page is part of a process, every page in the process must conform. Testing checkout step 2 in isolation tells you nothing about the checkout.
- Pages with each content type identified in step 2: the video page, the data table page, the PDF.
- Each state variation that changes the DOM: logged out and logged in, error states, empty states.
- Any page known or reported to be problematic.

### Random sample

A small set chosen at random from outside the structured set, typically around 10% of the total sample. Its job is to catch what the structured sample's assumptions missed. If the random sample finds issue types the structured sample did not, your structured sample was wrong and you extend it.

### Sample record

List every page in the plan with its URL and the reason it is included. "Because it was on the list" is not a reason; "represents the article detail template" is.

The sample list is the single most contested part of an accessibility evaluation. A buyer, a regulator, or a complainant will ask whether you tested the thing that failed. A recorded, reasoned sample answers that.

---

## 4. Methods

How each criterion gets checked. Three layers, and all three are required. This section is where the plan earns its existence, because layers two and three are the ones teams skip.

### Automated

Fast, cheap, runs in CI, catches a minority of problems.

Name the tool and version, where it runs, and what fails the build.

**Be honest about the ceiling.** The UK Government Digital Service tested 13 automated tools against a page with 142 deliberately injected barriers. The best tool detected 40% outright, and 50% counting issues it flagged for human review. Treat automation as removing noise before manual testing, not as evidence of conformance.

Widely used percentage claims about automated coverage ("automated tools catch 57%") come from vendor marketing with no published method. Do not repeat them in your plan.

### Manual

A human working through criteria that no tool can decide: whether alt text is meaningful, whether heading structure reflects the content, whether an error message tells you how to fix the error, whether focus order matches visual order.

State who does it, against what checklist, and how findings are recorded.

**Keyboard-only testing is the highest-yield single activity here.** Unplug the mouse and complete each process in the sample. It surfaces focus traps, invisible focus indicators, unreachable controls and skipped landmarks faster than anything else, and it needs no specialist tooling.

### Assistive technology

Testing with real screen readers, magnification, and speech input on the combinations in your support baseline.

State the combinations and who runs them. Testing with one screen reader on one browser is normal for small teams and should be stated as a limitation rather than presented as coverage.

**Testing with disabled users is not the same as testing with assistive technology, and it is better.** If you can fund it, say here how participants are recruited and compensated. If you cannot, say that too. An unstated absence reads as an untested claim.

---

## 5. Recording findings

One issue per finding, and each one carries:

| Field | Content |
|---|---|
| Where | URL and the specific element |
| What happens | Observed behaviour, not the criterion number |
| Criterion | The WCAG success criterion and level |
| Severity | How much it blocks, not how hard it is to fix |
| Steps to reproduce | Including browser and assistive technology used |
| Evidence | Screenshot, recording, or the DOM fragment |

**File findings where your other bugs live.** An accessibility issue tracker separate from the main backlog is how accessibility work stops being prioritised against everything else, and therefore stops happening.

Severity should reflect user impact: does this block a task entirely, make it substantially harder, or make it worse but usable. Do not let effort estimates leak into severity; that is a prioritisation decision made later, by someone else.

---

## 6. Cadence

What runs when. The plan is worth little if it only executes before an audit.

| Trigger | What runs |
|---|---|
| Every pull request | Automated checks on changed pages, plus linting |
| Every new component | Keyboard and screen reader test before it enters the design system |
| Every release | Automated across the sample, manual on anything changed |
| Quarterly, or per major release | Full manual pass on the structured sample |
| Annually | Full evaluation, and refresh the statement and the ACR |

Adjust the intervals to your release rate. Keep the principle: **component-level testing catches the problem once, page-level testing catches it as many times as the component is used.** Pushing effort to the component library is the largest available saving.

---

## 7. Reporting

WCAG-EM step 5 produces an evaluation report. It is a separate output from this plan, and this plan should name where it goes.

State which of these each evaluation feeds:

- The [accessibility statement](accessibility-statement.md), if you publish one.
- The [accessibility conformance report](accessibility-conformance-report.md), if buyers ask for one.
- The backlog.

Aggregation matters: an ACR row says "Partially Supports" and needs a remark, which comes from grouping individual findings by criterion. Plan for that grouping rather than handing an auditor a raw bug list.

---

## 8. Roles

Who owns what. Short, and the reason the plan does not stall.

| Role | Owns |
|---|---|
| Accessibility lead | The plan, the sample, sign-off on the annual evaluation |
| Developers | Automated checks passing, keyboard testing their own work |
| Designers | Contrast, focus states, target sizes, at design time |
| QA | Manual passes against the sample |
| Content authors | Alt text, heading structure, link text, document accessibility |

**Content authors are the most commonly omitted row and the most frequent source of new failures**, because they add content daily and never see a build pipeline. If your CMS lets authors publish untagged PDFs and empty alt attributes, no amount of engineering rigour holds the line.

---

## Common failures in this document

- **Automation only.** Ships a plan that cannot detect most barriers, and produces a false sense of conformance.
- **No sample.** Testing "the main pages" gives no basis for a conformance claim and no way to repeat the evaluation.
- **Processes tested page by page.** Misses exactly the failures that block a user from finishing.
- **No accessibility support baseline.** Makes half the findings unarguable, because there is no agreed target.
- **Annual audit as the only cadence.** Findings arrive after the code that caused them is a year old.
- **Separate accessibility backlog.** Guarantees the work loses every prioritisation call.

---

## Related documents

- [`accessibility-conformance-report.md`](accessibility-conformance-report.md). What buyers receive
- [`accessibility-statement.md`](accessibility-statement.md). What users receive
- [`../foundations/design-system-guide.md`](../foundations/design-system-guide.md). Where component-level accessibility gets fixed once instead of everywhere
