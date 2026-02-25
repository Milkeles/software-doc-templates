# Brand and Visual Guidelines

> What the brand looks like and how to use it correctly, for designers, marketers, agencies and partners.
>
> **On the name.** This document goes by several: brand guidelines, visual identity guidelines, brand book, or (IBM) a design language. There is no standard name. Avoid calling it a "style guide" alone: in a web team that usually means the *editorial* style guide, the A-to-Z of word choice and grammar. GOV.UK, for example, uses "style guide" exclusively for editorial guidance and calls this document "brand guidelines". Mozilla's `/styleguide/` URL now redirects to `brand.mozilla.com`.
>
> **Not the same as your [design system guide](design-system-guide.md).** That one is implementation: components, tokens, contribution, versioning, read by developers importing components. This one is direction, and much of its audience never opens a code editor.
>
> **Where it lives.** Somewhere designers, agencies and partners can reach without a repository account. Usually a public or shared page. Docs-as-code is the wrong home for a document whose primary readers are outside engineering.
>
> **Delete this block before publishing.**

---

## Where the boundary with the design system falls

Published organisations that maintain both keep them separate, and the split is consistent enough to copy.

| Organisation | Brand document | Design system |
|---|---|---|
| GDS | GOV.UK brand guidelines | GOV.UK Design System. Contains **no logo guidance at all** |
| IBM | IBM Design Language, covering "software products, digital and traditional marketing, hardware, advertising, events, physical spaces" | Carbon, "IBM's open source design system for products and digital experiences" |
| Salesforce | Brand Central, plus separate legal trademark guidelines | Lightning Design System, no logo or trademark rules |
| Shopify | Separate | Polaris. No brand, logo or trademark section |

**Atlassian merges them**, putting Logos inside Foundations alongside tokens and typography, and linking a separate Brand kit for external partners. So the boundary there is in-product logo use inside the system, partner permission rules outside it. The split below is a strong convention, not a rule.

The workable line:

```
   BRAND AND VISUAL GUIDELINES          DESIGN SYSTEM GUIDE
   everything the brand appears on      what ships in code

   logo and logo system                 components
   trademark and permissions            token names and structure
   photography, illustration            contribution process
   graphic devices                      versioning and deprecation
   print, social, video, events         theming
   partner and co-branded marketing

              colour and typography appear in BOTH
              brand:  the palette, the typeface, what they mean
              system: token names, contrast pairings, the type scale
```

Duplication of colour and type across the two is normal and correct, because they are stated at different resolutions. What must not happen is disagreement. Name one of them the source of truth for values, and have the other reference it.

---

## 1. Brand foundation

Short. Two or three paragraphs on what the brand stands for and who it speaks to.

This is the only section where adjectives are legitimate, and it still needs discipline. "Confident, plain-spoken, never clever for its own sake" is usable, because a reviewer can point at a design and say it is not that. "Innovative, dynamic and human-centred" is not, because nothing fails it.

**Test each adjective by writing its opposite.** If no organisation would ever claim the opposite, the adjective is doing no work and should go.

---

## 2. Logo

The section people actually open this document to find, and the one most often violated.

Cover:

**The variants.** Primary, secondary, monochrome, reversed, and the icon or mark alone. Say which to use when, not just that they exist.

**Clear space.** Expressed as a multiple of an element of the logo itself, such as the cap height or the width of the mark, so it scales. **There is no cross-organisation standard for the value**; each brand sets its own. Pick one and draw it.

```
   +--------------------------------------+
   |                 x                    |     x = the height of the mark
   |         +----------------+           |
   |    x    |   [ LOGO ]     |    x      |     clear space on all sides
   |         +----------------+           |     is 1x, and nothing may
   |                 x                    |     enter it
   +--------------------------------------+
```

**Minimum size.** In pixels for screen and millimetres for print. Below it, the mark stops being legible and you have no way to argue with anyone who used it small.

**Misuse.** The highest-value part of the whole document, and it must be shown rather than described. Stretching, recolouring, rotating, adding effects, placing on insufficient contrast, reconstructing the lockup, using the wordmark and mark separately when they should be together. A list of prohibited transformations with examples of each prevents more damage than any amount of prose.

**Placement on backgrounds.** Which variant on light, on dark, on photography. State the minimum contrast the background must provide.

---

## 3. Colour

Where taste ends and checkable rules begin, so specify rather than describe.

For each colour give: name, hex, RGB, and CMYK or Pantone if you print. Then state the rules that can be verified:

| Rule | Source |
|---|---|
| Body text against its background: contrast ratio at least **4.5:1** | WCAG 2.2 success criterion 1.4.3 (AA) |
| Large text (18pt, or 14pt bold): at least **3:1** | WCAG 2.2 1.4.3 (AA) |
| UI components and meaningful graphics against adjacent colours: at least **3:1** | WCAG 2.2 1.4.11 (AA) |
| Colour is never the only means of conveying information | WCAG 2.2 1.4.1 (A) |

**Publish the approved pairings, not just the palette.** A palette lets a designer combine any two colours, and some of those combinations fail. A table of which foreground is permitted on which background, with the measured ratio, removes the judgement call.

> | Foreground | Background | Ratio | Use |
> |---|---|---|---|
> | `#1A1A1A` | `#FFFFFF` | 17.4:1 | Body text |
> | `#FFFFFF` | `#1D4ED8` | 7.0:1 | Text on primary action |
> | `#1D4ED8` | `#FFFFFF` | 7.0:1 | Links |
> | `#6B7280` | `#FFFFFF` | 4.8:1 | Secondary text. Not for text under 16px |

State semantic meaning too: which colour means error, success, warning. A brand that uses its primary colour for destructive actions has a problem no component library can fix.

---

## 4. Typography

Typefaces, licences, and the rules.

**The typefaces**, with weights and the licence you hold. Licensing is not a footnote: a typeface licensed for print and not for web embedding is a legal problem discovered at launch.

**Fallback stacks**, in order, and what happens when the web font fails to load. This is a brand decision, not a technical one, because a fallback that shifts layout produces the layout shift your [performance budget](../performance/performance-budget.md) measures.

**The type scale.** Sizes, line heights, weights, and what each level is for. Keep it small; a scale with fourteen levels is fourteen opportunities to pick the wrong one.

**Minimum sizes**, and the accessibility rules that constrain them:

- Text must resize to **200%** without loss of content or functionality (WCAG 2.2 1.4.4, AA).
- The design must survive user-applied text spacing: line height 1.5×, paragraph spacing 2×, letter spacing 0.12×, word spacing 0.16× of the font size (WCAG 2.2 1.4.12, AA).

That second one is the reason to avoid fixed-height containers around text, and it is worth stating here rather than discovering it in an audit.

---

## 5. Iconography

Style, grid, stroke weight, corner radius, and how a new icon gets made or approved.

State whether icons carry meaning alone. An icon-only control needs an accessible name, and the [design system guide](design-system-guide.md) should say which component enforces that. If a set of icons must always appear with a label, this is where that rule lives.

---

## 6. Photography and illustration

The most subjective section, and the one where adjectives fail hardest.

**Show, do not describe.** A grid of approved images beside a grid of rejected ones, each rejection annotated with the reason, teaches the rule. "Authentic, warm, never staged" teaches nothing, because everyone believes their choice was authentic.

Then state what is checkable:

- Whether text may be placed on images, and the contrast the image must provide behind it.
- Whether images may carry information that appears nowhere else. If yes, the alt text requirement is not optional.
- Licensing and model releases, and who holds them.
- Where the approved library lives.

---

## 7. Motion

Include this if your brand has a motion identity. Skip it if not, rather than inventing one. GOV.UK's brand guidelines have no motion section.

Cover duration, easing, and what motion is for: orienting the user, confirming an action, expressing personality.

Two hard rules apply and both are worth stating here rather than leaving to the implementation:

- Motion that starts automatically and lasts more than **five seconds** must be pausable, stoppable or hideable (WCAG 2.2 2.2.2, Level A).
- Honour `prefers-reduced-motion`. Motion triggered by interaction should be disableable unless it is essential (WCAG 2.2 2.3.3, Level AAA). `prefers-reduced-motion` is specified in Media Queries Level 5, which as of February 2026 remains a **W3C Working Draft**, not a Recommendation. It is broadly implemented regardless.

Vestibular disorders make this a health matter, not a preference. Say so once, briefly, so nobody treats the reduced-motion path as a nice-to-have.

---

## 8. Voice and tone

Optional here, and often better as a separate editorial style guide. GOV.UK keeps them apart; Atlassian keeps tone inside its Foundations as "Content".

If you keep it here, keep it to the visual-adjacent parts: capitalisation in interface labels, sentence case versus title case, how the brand name is written, whether you use the ampersand. The full editorial guide, spelling, grammar and the A-to-Z of preferred terms, is a different document with a different reader.

---

## 9. Applications

"Brand in use" in most published guidelines, and near-universal across them.

Worked examples of the brand applied: a page header, a social post, a slide, a business card, a stand. This is where a reader checks whether they have understood the preceding sections, and it is the section agencies use most.

---

## 10. Trademark and permissions

**Situational.** Include it if third parties use your marks: partners, resellers, marketplace developers, open-source forks. Omit it if the brand is used only by your own staff. GOV.UK's brand guidelines carry no trademark chapter, because Crown branding is governed by separate policy.

If you include it, cover: which marks are registered, what nominative or compatibility use is permitted, what modification is prohibited, and the address for permission requests.

The open-source case is the strictest, and Mozilla states the principle more clearly than most:

> Open source licensing applies to code, not branding.

Mozilla requires prior written permission for uses beyond stating compatibility, forbids modifying, abbreviating or combining its marks, and rules that a significantly modified Firefox "may not use Mozilla or Firefox in its name". Salesforce's guidelines, addressed to "partners, resellers, customers, developers, consultants, publishers, and other third parties", forbid lookalike marks. Atlassian requires that Marketplace partners "must not incorporate any elements of Atlassian's brand".

If you have an ecosystem and no such section, you have no basis to object when someone ships a product that looks like yours.

---

## Where to send someone who wants an exception

Name a person or team, and give a turnaround time.

Every guideline document generates exception requests. Without a stated route, the requester either guesses or asks whoever is nearest, and the answer differs by who they asked. That is how a brand fragments.

---

## How good is the evidence for any of this

Weak, and worth saying plainly.

**There is no peer-reviewed research on brand guideline effectiveness**, and none on design system adoption in an established venue. This area rests entirely on practitioner literature and on published exemplars from organisations that maintain these documents in public. The strongest available evidence is that large, design-mature organisations, including GDS, IBM, Salesforce and Mozilla, all maintain one and maintain it separately from their design system. That is convergent practice, not measurement.

Two claims to avoid:

- **Design token adoption percentages.** The widely repeated "56% to 84% in a year" comes from a vendor industry survey of roughly 300 self-selected professionals. Not a finding.
- **Consistency or revenue uplift figures.** Attributed to consultancies, with no published method.

The honest argument is the mechanism: a rule written once and shown with examples is cheaper to apply and easier to review than a judgement made repeatedly by different people. That is enough. It does not need a statistic.

---

## Common failures in this document

- **Adjectives instead of examples.** "Bold and human" is unreviewable. Side-by-side do and don't is not.
- **A palette with no approved pairings.** Guarantees combinations that fail WCAG 1.4.3, and the failure surfaces in an accessibility audit rather than in design review.
- **Disagrees with the design system.** Two sources of truth for the same hex value, and nobody knows which is current.
- **Locked in a PDF behind a login.** The agency you hired cannot read it, so they guess.
- **No misuse examples.** People violate rules they were never shown.
- **No exception route.** Requests get answered inconsistently, and the inconsistency becomes precedent.
- **Typeface licensing omitted.** Discovered at launch, and expensive.

---

## Related documents

- [`design-system-guide.md`](design-system-guide.md). The implementation of this direction in code
- [`../accessibility/accessibility-conformance-report.md`](../accessibility/accessibility-conformance-report.md). Colour and typography decisions made here appear as findings there
- [`../../general-swe/foundations/glossary.md`](../../general-swe/foundations/glossary.md). If you maintain an editorial style guide, that is where terminology belongs, not here
