# Privacy ledger: {Game or product}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Controller** | *The legal entity, not the studio name if they differ* |
| **Data protection contact** | |
| **Last reviewed** | YYYY-MM-DD |
| **Owner** | *Legal or compliance, not engineering alone. Engineering feeds this document; it should not be the only author of it* |

*This document exists because a live game is close to the case Article 30 of the GDPR was written for. Article 30(5) exempts organisations under 250 employees from keeping this kind of record, but only if processing is occasional, poses no risk to data subjects' rights, and involves no special-category data. A live game processing player behaviour continuously, at scale, almost never qualifies: "not occasional" alone rules most live products out. Treat this as close to a legal requirement, not as optional documentation discipline.*

*This is a record of what you do, not the compliance program itself. It does not replace legal advice, and it does not substitute for the technical and organisational controls it describes; it is the place someone, inside the company or a regulator, can go to find out what those controls are supposed to be.*

---

## 1. Processing activities

*One row per purpose, following GDPR Article 30(1)'s required fields directly.*

| Purpose | Categories of data subjects | Categories of personal data | Lawful basis | Recipients | Third-country transfer | Retention | Security measures |
|---|---|---|---|---|---|---|---|
| *Account creation and login* | *Registered players* | *Email, username, hashed password* | *Contract (Art. 6(1)(b))* | *None outside controller* | *None* | *Duration of account plus 30 days* | *Encrypted at rest, access-logged* |
| *Gameplay telemetry for balance and matchmaking* | *All active players* | *Session events, in-game actions, device ID* | *Legitimate interest (Art. 6(1)(f))* | *Internal analytics team* | *US region processing, SCCs in place* | *18 months, then aggregated* | *Pseudonymised at collection* |
| *Ad-funded monetisation* | *Free-tier players who have not opted out* | *Advertising ID, IP-derived region* | *Consent (Art. 6(1)(a))* | *{Ad network name}* | *{Per the network's own DPA}* | *Per network's stated retention* | *Consent recorded with timestamp* |

**Lawful basis, one of six, always named.** *Consent, contract necessity, legal obligation, vital interests, public task, or legitimate interest, per Article 6(1). "Legitimate interest" needs the closest scrutiny in a game: the article itself singles out cases "where the data subject is a child" as one where legitimate-interest reasoning gets overridden more easily. If your player base plausibly includes children, do not lean on legitimate interest for anything beyond what is strictly necessary to run the game.*

---

## 2. Children and teens

*The age line is not one number, and the obligations above and below it are not the same as each other.*

| | |
|---|---|
| **EU: age requiring parental consent** | *Under 16 by default; a member state may lower this to no less than 13. State which age applies in each market you operate in, or use 16 as the conservative default if you do not track this per country* |
| **US (COPPA): under 13** | *Applies to any service directed to children under 13, or where you have actual knowledge a user is under 13* |
| **Teens 13-17** | *Not covered by COPPA. State your own policy here explicitly; do not rely on "we comply with COPPA" to imply teen protections it does not include* |

**COPPA's 2025 amendments** *require, for a service in scope: separate verifiable parental consent specifically for disclosing a child's data to a third party for a purpose not integral to the game itself (consenting to play the game is not consent to ad-tech sharing), a written information security program, and a written data retention policy. If this game is directed at or knowingly used by children under 13, confirm each of these three exists and is current, not just that a general privacy policy is published.*

**Why the teen age band gets its own row.** *A 2022 FTC settlement, the largest COPPA penalty on record at $520 million total, arose partly from a gap between what COPPA required for under-13s and what the product actually did for older teens: default-on voice and text chat with no separate protection for 13-17 year olds. Treat "COPPA-compliant" and "safe for teens" as two different claims that need two different answers.*

---

## 3. Per-SDK data inventory

*Every third-party SDK collects something. App Store privacy nutrition labels and Google Play's Data safety section already force this disclosure at the platform level; keep the underlying record here so the platform-facing labels are generated from something true rather than filled in from memory at submission time.*

| SDK / third party | Purpose | Data collected | Shared with the vendor? | Linked to identity? |
|---|---|---|---|---|
| | | | | |

---

## 4. Data subject rights

*How a deletion, access, or correction request is actually fulfilled, including how it propagates to every recipient in section 1's table. This is the same problem the [interface control document](../../general-swe/foundations/interface-control-document.md) template asks about deletion propagation across a system boundary, applied to every third party in this ledger.*

| Right | How fulfilled | Propagates to |
|---|---|---|
| *Erasure* | | *Every third-party recipient listed above* |
| *Access* | | |
| *Portability* | | |

---

## Notes on using this template

*Delete this section too.*

**This document has an owner outside engineering.** Engineering knows what the code actually does; legal or compliance knows what the law requires it to say and do. Neither alone produces a trustworthy ledger.

**Do not treat the small-organisation exemption as a default.** A live game processing behavioural telemetry continuously very rarely qualifies for Article 30(5), whatever your headcount. Check the three conditions in the paragraph at the top of this document before assuming you are exempt.

**Legitimate interest is not a free pass, especially with a young player base.** The GDPR names children explicitly as a case requiring extra scrutiny of legitimate-interest processing. If in doubt, use consent.

**Review this on a real cadence, not once.** A new SDK, a new monetisation partner, or a new analytics vendor changes this document the moment it ships, not at the next scheduled audit.

**Where this lives:** wherever your legal or compliance function keeps controlled records, referenced from engineering documentation rather than duplicated into it. This is closer to a regulatory filing than to a technical design document.

---

## Related documents

- [`age-rating-compliance-record.md`](age-rating-compliance-record.md). The parallel compliance record for content and monetisation disclosure rather than data
- [`../../general-swe/foundations/interface-control-document.md`](../../general-swe/foundations/interface-control-document.md). Where the general version of "how deletion propagates across a boundary" is documented
- [`../../general-swe/security-and-compliance/`](../../general-swe/security-and-compliance/). The general-purpose security and compliance documents this ledger sits alongside
