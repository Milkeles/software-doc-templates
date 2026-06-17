# Age rating and compliance record: {Game}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | *All storefronts and territories this game ships to* |
| **Owner** | *Legal, compliance, or the person who submits ratings, not engineering alone* |
| **Last reviewed** | YYYY-MM-DD |

*This record tracks two different kinds of obligation, and they carry different weight. Age ratings themselves (ESRB, PEGI, and the rest) are industry self-regulation: no statute requires a rating board's approval before you ship. Loot box law, where it exists, is a real statute with real penalties. Keep both in one record because they both change when your content does, but do not present one as having the legal force of the other.*

---

## 1. Rating submissions

*One row per rating body per platform. A rating is not permanent: content updates can trigger a re-rating requirement, tracked in section 4.*

| Body | Territory | Questionnaire answers reflect | Descriptors assigned | Submitted rating | Current rating | Last submitted |
|---|---|---|---|---|---|---|
| *ESRB* | *US, Canada* | | | | | |
| *PEGI* | *EU, UK* | | | | | |
| *IARC* | *Digital storefronts (Google Play, Nintendo eShop, Microsoft Store)* | | | | | |
| *CERO* | *Japan* | | | | | |
| *USK* | *Germany* | | | | | |
| *ACB* | *Australia* | | | | | |

**Two rating bodies can disagree in good faith.** A 2023 study measuring ESRB-PEGI consistency on the same physical release found a 39.4% overall agreement rate, rising to 83.9% once each body's retroactivity policy is accounted for: a body does not always re-rate a game retroactively when its own standards shift, so an older title carries an older-standard rating even as newer titles are rated more strictly. A gap between your ESRB and PEGI rating is not automatically an error in either.

---

## 2. In-game purchases and random items label

*ESRB and PEGI introduced an "In-Game Purchases (Includes Random Items)" label in 2020 for any paid randomised in-game transaction; IARC adopted the same label. This is industry self-regulation. No law requires the label. Track it here as a commitment your studio has made, not as a legal filing.*

| | |
|---|---|
| **Does this game contain paid randomised transactions?** | *Yes / no. If yes, every body above needs this label* |
| **Label applied on** | *List each storefront and confirm the label is live, not just submitted* |
| **Last verified against the live build** | *Date someone actually checked the storefront listing, not the submission form* |

**Self-regulation without enforcement produces low compliance, and this is measured, not assumed.** The same 2023 study checked 100 mobile games on Google Play already confirmed to contain loot boxes, each independently verified by replaying it for up to an hour. Only 29 of the 100 displayed the required label. Storefront rating questionnaires are not a reliable substitute for your own check: verify the label against the live build yourself, on a real cadence, rather than trusting that an automated IARC questionnaire keeps itself current as your content changes.

---

## 3. Loot box and gambling-adjacent mechanics by territory

*Legal status of paid randomised mechanics varies by territory and is not settled EU-wide or globally. State status, not conclusions; consult local counsel for anything you plan to ship into a territory with an unclear or adverse position. This table is a tracking record, not a legal opinion.*

| Territory | Status as tracked | Last reviewed |
|---|---|---|
| *Belgium* | *Belgian Gaming Commission ruled in April 2018 that paid loot boxes containing tradeable items are illegal gambling under the 1999 Gambling Act; non-compliance carries criminal penalties. Do not ship tradeable paid random items into this territory without counsel's sign-off* | |
| *Netherlands* | *Dutch gambling authority fined EA over FIFA Ultimate Team packs in 2019; reversed by the Council of State in March 2022, which held the packs could not be assessed as a standalone game of chance separate from the wider game. Contested, not settled* | |
| *United Kingdom* | *Government review (2020-2022) concluded the evidence base was still emerging and chose industry self-regulation over new legislation. No UK loot box statute exists as tracked here* | |
| *{Other territory}* | | |

**Belgium and the Netherlands reached opposite legal conclusions on functionally similar mechanics.** Treat this as a real, current split in EU practice, not as a gap in your research. A mechanic cleared in one EU territory is not automatically cleared in another.

---

## 4. Re-rating triggers

*What content change requires going back to a rating body before it ships. Missing this is how a rating goes stale without anyone deciding it should.*

| Trigger | Which bodies need re-review | Applies to this game? |
|---|---|---|
| *New paid randomised mechanic added* | *All bodies with a random-items label scheme* | |
| *New violence, drug, or sexual content descriptor threshold crossed* | *All* | |
| *Voice or text chat added or changed* | *Bodies with an interactive-elements descriptor* | |
| *New territory launch* | *That territory's body* | |

---

## Notes on using this template

*Delete this section too.*

**The label scheme is voluntary; loot box law, where it exists, is not.** Keep this distinction visible in the record itself. A team that treats "we have the label" as equivalent to "we are legally compliant in every territory" has misread what the label is for.

**A rating disagreement between bodies is not automatically a mistake.** Check whether it traces to a retroactivity policy difference before treating it as an error to fix.

**Verify the label against the live build, not the submission.** The 29% compliance rate Xiao (2023, *Royal Society Open Science*) measured among games already confirmed to have the mechanic exists precisely because studios treated submission as the finish line.

**Where this lives:** the same controlled location as the [privacy ledger](privacy-ledger.md), typically owned by legal or compliance and referenced from engineering documentation rather than duplicated into it.

---

## Related documents

- [`privacy-ledger.md`](privacy-ledger.md). The parallel compliance record for player data rather than content and monetisation disclosure
- [`release-notes.md`](release-notes.md). Where a content change that triggers section 4 gets announced to players, after this record confirms the re-rating is done
