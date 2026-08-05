# Frontend Architecture

> How the front end is put together and why, for someone who has to change it.
>
> **What it is for.** A new developer can read the code and work out what it does. They cannot work out what was deliberate. This document separates the structure someone chose from the structure that accumulated, so a change either respects a decision or knowingly overrides it.
>
> **Where it lives.** Docs-as-code. It describes the code and rots faster than anything else in this area when separated from it. Review it in the same pull request that changes the structure it describes.
>
> **How long.** Under 2000 words. Beyond that it stops being read, and an unread architecture document is worse than none because people cite it without checking.
>
> **There is no standard section set for this document.** No frontend-specific architecture documentation standard exists. ISO/IEC/IEEE 42010:2022 covers architecture description generally and is paywalled. arc42 offers a twelve-section practitioner template. The C4 model gives a way to draw systems at four zoom levels. All three are general-purpose; applying them to a front end is convention, not compliance. The headings below borrow from arc42 and C4 where they help and drop what does not apply. If your organisation already uses arc42, use arc42 — consistency across your documents beats matching this file.
>
> **Delete this block before publishing.**

---

## 1. What this application is

Three or four sentences. What it does, who uses it, and the one constraint that shaped everything else.

> Customer-facing storefront. Anonymous browsing, authenticated checkout. Roughly 400,000 sessions a week, 78% mobile. Server-rendered because organic search is the primary acquisition channel and first-load speed is the metric the business tracks.

The last sentence is the one worth the effort. **State the dominant constraint**, because every decision below either serves it or trades against it, and a reader who does not know it cannot evaluate any of them.

---

## 2. Rendering strategy

The largest decision in a front end and the one most often left implicit.

State which of these applies, and where. Most real applications mix them, and the mixing rule is what needs writing down.

| Strategy | Use here for |
|---|---|
| Server-side rendering | Pages that must be indexed or must paint fast on a cold cache |
| Static generation | Content that changes less often than it is requested |
| Client-side rendering | Authenticated, interactive views behind a login |
| Streaming / partial hydration | Pages with a fast-critical top and a slow tail |

Then state the rule:

> Marketing and product pages are statically generated and revalidated hourly. Search results are server-rendered. Everything under `/account` is client-rendered, because it is behind a login and never indexed.

**Say what you gave up.** A reader who sees only the benefit will assume the trade-off was not considered and will re-litigate it.

---

## 3. Structure

How the code is organised, and the rule that decides where a new file goes.

Draw it. Keep it to one level of detail.

```
   src/
     app/            routes. one directory per route, nothing shared here
     features/       vertical slices. each owns its UI, state and data access
       checkout/
       search/
     shared/         used by two or more features. moving something here is a
                     review decision, not a convenience
     ui/             design system components. no feature knowledge, no data
```

State the dependency rule and make it checkable:

> `features/*` may import from `shared/` and `ui/`. `features/*` may not import from another feature. `ui/` imports nothing from `features/` or `shared/`.

**A dependency rule you do not enforce is a preference.** Name the linter rule or tooling that enforces it. If nothing enforces it, say that too, so a reader knows the rule describes intent rather than reality.

---

## 4. State

The area where undocumented convention causes the most duplicated work, because there are usually four ways to do the same thing and no stated ordering.

Categorise, then assign:

| Kind of state | Held in | Example |
|---|---|---|
| Server state | Data-fetching library cache | Product list, order history |
| URL state | The URL | Filters, page number, selected tab |
| Global client state | Store | Session, theme, feature flags |
| Local component state | Component | Whether a dropdown is open |

Then give the decision rule in one line:

> Default to local. Promote to URL if it should survive a refresh or be shareable. Promote to global only if two unrelated features need it. Server data is never copied into the global store.

The last clause prevents the most common architectural failure in front ends: server data mirrored into a global store, where it desynchronises from the server and every component has to guess which copy is current.

---

## 5. Data access

How the front end talks to the back end.

- **Which APIs**, and where their contracts live. Link the OpenAPI file or the [API design guide](api-design-guide.md).
- **Where fetching happens.** In a data layer per feature, in route loaders, or in components. Pick one; mixing means nobody can find where a request originates.
- **Whether types are generated** from the schema or handwritten. Generated is the stronger position and the reason is worth stating: a handwritten type that disagrees with the API compiles cleanly and fails at runtime.
- **Caching and revalidation.** How long, and what invalidates it.
- **Error and loading conventions.** Which errors surface to the user, which retry silently, and what a loading state looks like. Without a convention every feature invents its own and the application feels inconsistent for reasons users cannot name.

---

## 6. Boundaries and third parties

What you depend on that you do not control, and what happens when it fails.

| Dependency | Used for | If it is slow or down |
|---|---|---|
| Payment provider SDK | Checkout | Checkout blocked. Show a specific message, not a generic error |
| Analytics tag | Product analytics | Loaded async, failures ignored |
| Consent platform | Cookie banner | Blocks all other tags by design |

Third-party scripts are the largest single lever on the numbers in your [performance budget](../performance/performance-budget.md), and the one most often outside engineering's control. Listing them here creates a place where someone can see the total.

---

## 7. Micro-frontends, if you have them

Skip this section if you do not, and be honest that you probably should not.

The published evidence is a 2021 multivocal literature review in *Information and Software Technology* (Peltonen, Mezzalira and Taibi) covering 43 sources. It documents real motivations and real costs. The frequently quoted adoption percentages come from self-reported adopter surveys with obvious selection bias, so treat them as what adopters say rather than as measured outcomes.

If you have them, document what only this document can tell a reader:

- Where the split runs and why. Team boundaries, not technical ones, if the point was independent deployment.
- The composition method: build-time, server-side, or runtime.
- Shared dependency policy. Which libraries are shared, which are duplicated, and what a version conflict does.
- Cross-application communication and routing ownership.
- Shared styling and design token strategy, which is where micro-frontends visibly fail first.

---

## 8. Accessibility and browser support

Two short cross-references, not a restatement.

- Accessibility is fixed at the component layer. See [`design-system-guide.md`](design-system-guide.md) and [`../accessibility/accessibility-test-plan.md`](../accessibility/accessibility-test-plan.md).
- The browsers this architecture assumes are in [`browser-support-policy.md`](browser-support-policy.md). Say here if any architectural decision depends on it, for example a build target that excludes a browser the policy claims to support. That contradiction is common and expensive.

---

## 9. Known problems

The section that makes the document trustworthy.

List what is wrong, what it costs, and whether anyone plans to fix it.

> The legacy `LegacyDataTable` component is used on four pages and is not keyboard-accessible. Replacement is scheduled for Q4 2026.

> Two state management libraries are in use. The older one is confined to `features/reporting/`. No migration is planned; do not add to it.

**Without this section, readers assume the document is aspirational and stop trusting the rest.** With it, "do not add to it" is an instruction someone can follow.

---

## 10. Decisions

Do not explain reasoning here. Link it.

> - Server-side rendering over a single-page application: [ADR-012](../../general-swe/foundations/architecture-decision-record.md)
> - Vertical feature slices over layered directories: ADR-019
> - Generated API types: ADR-023

This document says **what the architecture is now**. Architecture decision records say **why, at the time, with the alternatives considered**. Keeping the reasoning here means editing history every time the structure changes, and the reasoning gets rewritten to match the outcome.

---

## Common failures in this document

- **Written once at project start.** Describes an application that no longer exists, and is cited as though it does.
- **Lists the tech stack and stops.** `package.json` already does that. The value is the rules and the trade-offs.
- **No known problems section.** Reads as marketing, so readers discount all of it.
- **State management undocumented.** Guarantees four approaches and duplicated server data.
- **Reasoning inlined instead of linked.** The document becomes long, and the history becomes unrecoverable.
- **Contradicts the browser support policy.** Usually discovered by a user on a browser you claimed to support.

---

## Related documents

- [`api-design-guide.md`](api-design-guide.md). The contract this front end consumes
- [`design-system-guide.md`](design-system-guide.md). The component layer this architecture sits on
- [`browser-support-policy.md`](browser-support-policy.md). The runtime this architecture targets
- [`../../general-swe/foundations/architecture-overview.md`](../../general-swe/foundations/architecture-overview.md). The system this front end is one part of
