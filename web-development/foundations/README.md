# Foundations

The six documents a web team needs regardless of methodology, product or stack.

| Document | Write it when |
|---|---|
| [`browser-support-policy.md`](browser-support-policy.md) | Always. One page, and the cheapest document here by a wide margin |
| [`api-design-guide.md`](api-design-guide.md) | Anyone consumes your API. Before the second version, not after |
| [`frontend-architecture.md`](frontend-architecture.md) | The front end is large enough that a new developer cannot infer the rules from the code |
| [`brand-and-visual-guidelines.md`](brand-and-visual-guidelines.md) | Anyone outside your team produces work in your brand. Agencies, marketing, partners |
| [`design-system-guide.md`](design-system-guide.md) | You have a shared component library used by more than one team |
| [`rollout-plan.md`](rollout-plan.md) | Per risky change. Not standing documentation, and finished when the flag is removed |

None of these replaces [`general-swe/foundations/`](../../general-swe/foundations/). A web team still writes architecture decision records, runbooks and postmortems. These six sit on top.

---

## The pattern underneath all of them

Five of the six exist to write down a decision that would otherwise be re-made, differently, by each person who encounters it.

That is the whole mechanism, and it is worth naming because it tells you when to skip a document. A rule that is genuinely obvious to everyone does not need writing down. A rule that produced an argument last month does.

```
   an implicit decision                 the document that fixes it

   "which browsers do we care about"    browser-support-policy
   "is it safe to retry this POST"      api-design-guide
   "where does this new file go"        frontend-architecture
   "is this the right blue"             brand-and-visual-guidelines
   "should I build my own dropdown"     design-system-guide
   "how do we know this is going wrong" rollout-plan
```

Each of those questions has a correct answer in your organisation today. It is held by two or three people, it is not written anywhere, and everyone else guesses. The document does not create the answer; it publishes one that already exists.

---

## Why these two are separate, and why that surprises people

**Brand and visual guidelines** and the **design system guide** describe the same visual product. Keeping them apart is deliberate and mirrors how game studios split an Art Bible from an art technical document: direction in one, buildable constraints in the other, because the readers are different people.

Published practice supports the split. GDS keeps GOV.UK brand guidelines on a different site from the GOV.UK Design System, and the Design System contains no logo guidance at all. IBM keeps the Design Language separate from Carbon. Salesforce, Mozilla and Shopify do the same; Shopify's Polaris has no brand, logo or trademark section anywhere in it.

**Atlassian merges them**, placing logos inside Foundations alongside tokens and typography, with a separate brand kit for marketplace partners. So this is a strong convention, not a law. If you have one small team and no external partners, one document is fine, and you should say in it that it covers both.

Colour and typography appear in both, at different resolutions. That duplication is normal. **Disagreement is not.** Name one document the source of truth for values and have the other reference it.

---

## Why these documents work, and how good the evidence is

### The browser support policy works because it converts a recurring judgement into a lookup. Evidence: none needed, and none exists

Nobody has studied this and nobody needs to. The policy replaces "does anyone still care about Safari 15" asked five times a year by five people with a table. The value is not insight; it is that the question stops being asked.

The one non-obvious part is the failure mode. A policy that disagrees with the `browserslist` config is worse than no policy, because the config silently wins and the document confidently misleads. Keeping them in the same directory is not tidiness, it is the enforcement mechanism.

### The API design guide works because your consumers cannot ask you. Evidence: the structure of the problem, not a study

Internal code can change a function signature and fix the callers. A published API cannot. That asymmetry is the entire argument and it does not need research behind it.

What it does need is honesty about disagreement. Google's AIP-185 mandates a major version in the URI path. Zalando's Rule 115 states you MUST NOT use URI versioning. Both are published, both are followed by serious organisations, and no RFC settles it. **A guide that presents one house style as the industry standard will be contradicted by the first consumer who has read a different one.** State your choice and your reason; do not claim consensus that does not exist.

### The frontend architecture document works because code shows what, not why. Evidence: design reasoning

A reader can derive structure from the repository. They cannot derive intent. Without the document, every existing pattern looks equally deliberate, so a developer either preserves an accident or overrides a decision, and cannot tell which they did.

The section that makes it work is "known problems". A document that lists what is wrong is trusted on what is right. One with no known problems reads as marketing, and readers discount all of it.

### The design system works because you fix a component once instead of a page at a time. Evidence: arithmetic, not research

**There is no peer-reviewed literature on design system effectiveness**, and none on brand guideline effectiveness either. This area rests on practitioner writing and on published exemplars.

The mechanism is nonetheless real and does not need a study: a fix applied in a component propagates to every page importing it. That is why the [accessibility test plan](../accessibility/accessibility-test-plan.md) pushes testing toward the component layer, and it is the largest single lever available on an accessibility backlog.

The claims to avoid are the numbers. Design token adoption percentages circulating as industry data come from a vendor survey of roughly 300 self-selected professionals. Consistency and revenue uplift figures are consultancy publications with no stated method. Argue the arithmetic, measure your own adoption, and cite nothing you cannot trace.

### The rollout plan works because 1% of users is not 100% of users. Evidence: true by construction, and the statistics are not

Gradual exposure limits blast radius. That is a property of the mechanism and needs no evidence.

**Claims that progressive delivery reduces incident rates or improves recovery time do not have a locatable primary source.** The figures in circulation resolve to vendor blogs or to attributions that cannot be checked against the reports they name. Make the blast-radius argument, which is unassailable, and leave the statistics alone.

### One argument you should not use

**"Fixing it later costs more."** The cost-of-change curve attributed to Boehm's 1981 work is widely used to justify writing all of these documents up front. A 2017 study in *Empirical Software Engineering* examined 171 projects from 2006 to 2014 and found no evidence for the delayed issue effect. See [`../../general-swe/waterfall/`](../../general-swe/waterfall/) for the detail. Write these documents because they stop questions being re-answered, not because of a curve that did not replicate.

---

## Where these documents live

| Document | Home | Why |
|---|---|---|
| API design guide | Docs-as-code | Reviewed alongside the API it governs. A guide the API can drift from is not a guide |
| Frontend architecture | Docs-as-code | Describes the code, and rots faster than anything else here when separated from it |
| Browser support policy | Docs-as-code, in the same directory as `.browserslistrc` | The prose and the machine-readable version must not disagree, and proximity is the only thing that reliably prevents it |
| Design system guide | Published with the component library, versioned with the same releases | Its readers are importing the components. They should not have to look in a second place |
| Brand and visual guidelines | A page designers, agencies and partners can reach without a repository account | Most of its readers never open a code editor. Docs-as-code makes it invisible to the people who need it |
| Rollout plan | With the change: the ticket, the pull request, or a page linked from both | Short-lived. It is done when the flag is removed, and it should disappear with the work |

The general rule in this repository is that documents changing with the code belong in the repository. **Brand guidelines are the clean exception, and the reason is the audience, not the change rate.** A document whose primary readers are outside engineering belongs where they already are.

---

## The document control block

The templates here carry no version number, author list or revision history, and that is deliberate for the docs-as-code ones. Git supplies all of it, more accurately than a table anyone maintains by hand.

For the two documents that live outside the repository, the block is worth adding at the top:

```
   Document ID      ACME-BRAND-2026-03-14
   Version          2.1
   Date             2026-03-14
   Organisation     Acme
   Team             Design
   Author(s)        [name]
   Reviewer(s)      [name]
   Confidentiality  Public | Internal | Confidential
```

Followed by a revision history table and a table of contents.

**Add it only where the hosting platform does not supply the same information.** A wiki page with poor history needs it. A Markdown file in git does not, and a hand-maintained version number in a git-tracked file will be wrong within two releases.

---

## What to write first

1. **Browser support policy.** An afternoon, and it settles an argument that otherwise recurs monthly.
2. **API design guide**, if anyone consumes your API. The cost of writing it rises with every consumer who has already integrated.
3. **Frontend architecture**, once a new developer's first pull request keeps landing in the wrong place. That symptom is the signal.
4. **Design system guide**, when the second team starts importing your components. Before that you can just talk to each other.
5. **Brand and visual guidelines**, when the first person outside your team produces something in your brand.
6. **Rollout plans**, per change, and only for changes that warrant one.

---

## Sources

- OpenAPI Specification 3.2.0 (19 September 2025); OpenAPI Initiative statements on 3.x and Moonwalk
- RFC 9110, 9111, 9112, 9113, 9114 (June 2022); RFC 9457 (July 2023); RFC 9745; RFC 8594
- Google API Improvement Proposals, AIP-185; Azure REST API Guidelines; Zalando RESTful API Guidelines, rules 113 to 115 and 176
- Web Platform Baseline, W3C WebDX Community Group; `browserslist`
- Design Tokens Format Module 2025.10, Design Tokens Community Group (28 October 2025)
- WAI-ARIA Authoring Practices Guide, W3C Group Note; WCAG 2.2
- GOV.UK brand guidelines and GOV.UK Design System; IBM Design Language and Carbon; Atlassian Design System Foundations; Shopify Polaris; Mozilla Brand Portal and Trademark Guidelines; Salesforce Trademark and Copyright Usage Guidelines
- Peltonen, Mezzalira and Taibi, "Motivations, benefits, and issues for adopting Micro-Frontends", *Information and Software Technology* (2021)
- OpenFeature, CNCF Incubating project since 21 November 2023

**On sourcing.** Where a claim in these templates comes from a specification, it is cited to the specification. Where a widely repeated claim has no traceable primary source, the templates say so instead of repeating it. That applies to progressive delivery incident statistics, design token adoption percentages, and design system return-on-investment figures.
