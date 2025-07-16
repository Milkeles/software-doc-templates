# Glossary

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Owner** | |
| **Last reviewed** | YYYY-MM-DD |

*One term per row. Alphabetical, so it can be scanned rather than read.*

*Define a term here when it means different things to different people, or when a competent outsider would guess wrong. Do not define words that carry their ordinary meaning: a glossary padded with obvious entries stops being consulted.*

---

## Domain terms

| Term | Means | Does not mean | Used in |
|---|---|---|---|
| *Account* | *A billing relationship with one payment method. One customer may have several.* | *A login. That is a User.* | *`billing`, `accounts-api`* |
| *Delivered* | *Carrier confirmed handover to the recipient.* | *Dispatched from the warehouse. That is Shipped.* | *`fulfilment`* |

*The "does not mean" column is what makes this document earn its place. Ambiguity is rarely about a missing definition; it is about two plausible ones. Naming the wrong reading is what stops the bug.*

*The "used in" column ties vocabulary to code. If a term is defined here and the code calls it something else, one of the two is wrong, and this is where you find out.*

---

## Statuses and lifecycles

*Where a term names a state, define the whole set and what moves between them. Individual state definitions given in isolation are where the disagreements hide.*

**Order status.** *`draft` → `placed` → `paid` → `shipped` → `delivered`, with `cancelled` reachable before `shipped` and `refunded` after `paid`.*

*Then the questions people actually ask: does a cancelled order count in daily totals, is a refunded order still delivered, what is an "active" order.*

---

## Metrics

*Any number reported to anyone. Name, definition, exact filter, source system, owner.*

*Two teams reporting different figures for the same metric is the normal state of affairs, and it is always a definition problem, not a data problem.*

| Metric | Defined as | Excludes | Source | Owner |
|---|---|---|---|---|
| *Active user* | *Signed in at least once in the last 28 days* | *Service accounts, staff logins* | | |

---

## Abbreviations and internal names

*Acronyms, service codenames, legacy names still in the code.*

*Include the ones that are obvious to you. They are the ones a new joiner cannot search for, because they do not know they are abbreviations.*

| Short | Full | Note |
|---|---|---|
| | | |

---

## Terms we deliberately do not use

*Words banned because they caused confusion, with what to say instead.*

*Short and unusually effective. It is the only section that changes what people write.*

| Avoid | Use | Why |
|---|---|---|
| *Client* | *Customer, or API caller* | *Meant both, in the same sentence, in a postmortem* |

---

## Notes on using this template

*Delete this section too.*

**Add a term when it causes a misunderstanding, not before.** A glossary written up front is a guess. One grown from real confusion contains only entries that earned their place, and people trust it accordingly.

**One definition, not one per team.** If two teams genuinely need different meanings, they need different words. Recording both under one heading preserves the problem in writing.

**Make it the language of the code.** A definition nobody implements is a preference. When this document and the model disagree, treat it as a defect in one of them and fix it, rather than maintaining a translation layer in everyone's head.

**Where this lives:** in the repository, beside the [architecture overview](architecture-overview.md). It is reference material about the model and must move with it. arc42 makes the glossary chapter 12 for the same reason.
