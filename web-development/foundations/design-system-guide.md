# Design System Guide

> How to use the component library, how to contribute to it, and what happens when it changes.
>
> **Also called:** a pattern library, the older term for much of the same ground.
>
> **Not the same as your component reference.** Storybook or a docs site shows each component's props and renders it. This document covers what a props table cannot: which component to reach for, when to build your own instead, how a change gets in, and what a version bump means for the twelve teams importing it.
>
> **Not the same as your [brand and visual guidelines](brand-and-visual-guidelines.md).** Those carry direction: logo, palette, type, imagery. This carries implementation: components, tokens, contribution, versioning. Different readers. A marketing designer needs the first and will never open this. GDS, IBM, Salesforce, Mozilla and Shopify all keep the two apart; the GOV.UK Design System contains no logo guidance at all.
>
> **Where it lives.** Published with the component library itself, on the same docs site, versioned with the same releases. Its readers are the people importing the components, and they should never have to look in a second place.
>
> **Delete this block before publishing.**

---

## 1. What this system is for

Two or three sentences on what it covers and what it deliberately does not.

> Components for internal product surfaces. Covers forms, tables, navigation, and feedback. Does not cover marketing pages, which use a separate stack, or data visualisation, which uses [library].

**Naming what is out of scope is more useful than naming what is in.** It is the answer to half the questions the maintainers receive.

---

## 2. Design tokens

The layer everything else is built from, and the part that most teams get structurally wrong by having only one level.

### Structure

Three tiers, and the middle one is the point:

| Tier | Example | Who uses it |
|---|---|---|
| **Primitive** | `color.blue.600 = #1D4ED8` | Nobody, directly. Raw values with no meaning |
| **Semantic** | `color.action.primary = {color.blue.600}` | Component authors and product developers |
| **Component** | `button.primary.background = {color.action.primary}` | The component itself. Optional |

**Consumers use semantic tokens only.** A product team that writes `color.blue.600` has hard-coded a value you cannot rebrand or theme. A team that writes `color.action.primary` gets the new value for free. State this as a rule and enforce it with lint if you can.

### Format

The **Design Tokens Format Module**, from the W3C Design Tokens Community Group, reached its first stable version, 2025.10, announced on 28 October 2025.

**It is a Community Group report, not a W3C Standard, and not on the W3C Standards Track.** Community Group reports carry no W3C endorsement. That does not make it a bad choice, and it is the closest thing to a common interchange format that exists, but say what it is when you cite it. Tooling support is growing and uneven; check that your specific pipeline supports it before committing to it.

### What to document

- Where the source of truth lives, and which direction it flows. Design tool to code, or code to design tool. **One direction, stated.** Two-way sync sounds appealing and produces conflicts nobody can resolve.
- How a token gets added or changed, and who approves.
- How theming works: which tokens vary by theme and which are fixed.
- Deprecated tokens and their replacements.

---

## 3. Components

### The index

A table, not prose. Name, one-line purpose, status, and a link to the full reference.

| Component | Use for | Status |
|---|---|---|
| `Button` | Actions | Stable |
| `LinkButton` | Navigation styled as a button | Stable |
| `IconButton` | Icon-only actions. Requires `aria-label` | Stable |
| `Dropdown` | Selecting one option from under 15 | Deprecated. Use `Select` |
| `Select` | Selecting one or more options | Beta |

**The "use for" column does the work.** Most misuse is not people ignoring the system; it is people picking the wrong component because the names are similar and nothing distinguished them.

### Status labels

Define them, because consumers plan around them.

| Status | Means |
|---|---|
| **Beta** | Usable, API may change without a major version. Say so in the release notes |
| **Stable** | API changes only in a major version |
| **Deprecated** | Works, will be removed. Named replacement and removal version required |

A deprecated component without a named replacement is an instruction to invent something, which is what the system existed to prevent.

---

## 4. When not to use the system

The section that decides whether developers trust the system or route around it silently.

State the rule for building something custom:

> Build your own when the need is genuinely specific to one feature and will not recur. Do not rebuild an existing component because it is 90% right; raise an issue instead, because your 10% is probably someone else's too.

And say what to do when a component is close but wrong. If the answer is "open an issue and wait three weeks", people will copy the source and modify it, and you will have a fork you do not know about. An escape hatch you designed is better than one they improvise: a documented `className` override, a slot, or a documented lower-level primitive.

**A design system with no escape hatch gets forked.** Deciding where the hatch is, is a design decision. Pretending there is none is not.

---

## 5. Accessibility

What the system guarantees, and what it cannot.

**What components handle.** Keyboard interaction, focus management, ARIA roles and properties, focus indicators, target sizes. Be specific per component where behaviour is non-obvious: "`Modal` traps focus, returns it on close, and closes on Escape."

**What consumers must supply.** Accessible names for icon-only controls, correct heading levels, meaningful alt text, form labels associated with inputs. List these, because they are the failures that appear in an accessibility audit against pages built entirely from accessible components.

**What is tested, and how.** Automated checks in CI, keyboard testing per component, screen reader testing on which combinations.

**On the ARIA Authoring Practices Guide.** The APG is widely used for interaction patterns and is a **W3C Group Note, explicitly non-normative and "not endorsed by W3C or its Members"**. It stopped being versioned on 17 May 2022. The normative documents are WAI-ARIA itself and WCAG. Follow the APG for patterns, conform to WCAG.

The economics are the argument for putting effort here: **fixing a component fixes every page that uses it.** Fixing pages fixes one page each. This is the single largest lever available on an accessibility backlog, which is why the [accessibility test plan](../accessibility/accessibility-test-plan.md) pushes testing toward the component layer.

---

## 6. Contributing

How a change gets in. Vague here means the system stalls or fragments.

State:

- **How to propose.** An issue first, describing the need rather than the solution. Two teams asking for slightly different things usually need one component, and you only see that if the issue describes the need.
- **What a contribution must include.** Implementation, tests, accessibility tests, documentation, and a token-aligned appearance. Say it as a checklist so nobody is surprised in review.
- **Who reviews and what they check.** A named team or rotation.
- **How long it takes.** An honest number. If it is three weeks, say three weeks; people plan around a known wait and route around an unknown one.
- **Whether product teams can contribute at all**, or only request. Both models work. An unstated model produces contributions that get rejected after the work is done, and that happens once per contributor.

---

## 7. Versioning and change

Consumers have to plan upgrades, so the rules have to be legible.

- **Scheme.** Semantic versioning is the usual answer. State what you consider breaking: removing a prop, changing a default, changing visual output beyond a stated tolerance. **Visual change is the contested one.** Decide whether a restyled button is a major version, and write it down before the argument.
- **Release cadence**, and whether patches are backported.
- **How many major versions you support at once**, and for how long.
- **Migration guides**, one per major version, with codemods where you can supply them. A codemod is the difference between an upgrade that happens and one that is deferred for two years.
- **Deprecation notice period.** Match it to your consumers' release cycles, not yours.

---

## 8. Adoption

Optional, and worth it if the system is meant to spread rather than exist.

Track and publish: which products are on which version, and what fraction of UI is built from system components.

**Publish the number even when it is bad.** A system claiming success while three teams have quietly forked it is a system whose maintainers are the last to know.

**Do not quote a return-on-investment figure.** Every number in circulation traces back to a vendor or a consultancy with no published method, and the first person who checks will find that out. You do not need one. The argument is the mechanism: a problem solved once instead of once per team, and accessibility fixed once instead of once per page. Make that case, then measure your own adoption and quote that instead.

---

## Common failures in this document

- **Duplicates the component reference.** Rots against the generated docs, and the generated docs win.
- **No "when not to use it".** Developers route around the system silently and you find out during an audit.
- **One flat token layer.** Consumers bind to raw values, and theming or rebranding becomes a find-and-replace across every product.
- **Contribution process undocumented.** The system becomes a bottleneck, and the bottleneck becomes a fork.
- **Accessibility claimed, not specified.** Consumers assume components handle what they must supply themselves.
- **Breaking changes undefined for visual output.** Every restyle becomes an argument about the version number.

---

## Related documents

- [`brand-and-visual-guidelines.md`](brand-and-visual-guidelines.md). The direction this system implements
- [`frontend-architecture.md`](frontend-architecture.md). Where the system sits in the application structure
- [`browser-support-policy.md`](browser-support-policy.md). The components must work where the policy says they work
- [`../accessibility/accessibility-test-plan.md`](../accessibility/accessibility-test-plan.md). Component-level testing is the cheapest accessibility work available
