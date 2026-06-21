# Patch notes: {Version or date}

*Also called: release notes, changelog.*

*Italic text is guidance. Delete it as you fill each section in.*

*Read the general [release notes](../../general-swe/foundations/release-notes.md) template first: the discipline of writing for the reader, not for yourself, leading with the benefit, holds entirely. This adds two things a typical software release rarely has: a balance section that has to explain a tuning decision to a player who feels it, and a platform-parity note when certification means not everyone gets this patch on the same day.*

---

## In this update

*Two or three sentences on the theme, exactly as the general template asks.*

---

## New content

*As "New" in the general template: what it is, and how to reach it.*

---

## Balance changes

*Every entry here should trace to a [balance log](balance-log.md) entry. Do not restate the reasoning in full; link it. Do state the change itself in terms a player feels, not the raw values a designer sees.*

| Change | Was | Now | Why (short) |
|---|---|---|---|
| *Longbow damage vs. armored targets* | *18* | *22* | *Underperforming against its intended role; see [balance log BL-0091](balance-log.md)* |

*Say why, briefly, even when the honest answer is "usage data showed it underused." Players who feel a nerf or buff and get no explanation assume the worst explanation available. A short, honest reason costs you little and heads off a disproportionate amount of community speculation.*

---

## Fixed

*As the general template: symptoms the player saw, not the code that changed. Skip internal fixes nobody noticed.*

---

## Platform notes

*Delete this section if every platform received this patch simultaneously.*

*State plainly which platforms have this patch and which are still in certification. A player checking patch notes against their own game and not finding the changes reflected, with no explanation, reads as a bug or a broken promise rather than as a certification delay outside your control.*

| Platform | Status |
|---|---|
| *PC (Steam)* | *Live* |
| *PlayStation* | *In certification, expected {date}* |
| *Xbox* | *In certification, expected {date}* |

---

## Known issues

*As the general template.*

---

## Notes on using this template

*Delete this section too.*

**Balance changes need a reason, not just a value.** A patch note that says a weapon's damage changed from 18 to 22 with no explanation reads as arbitrary even when it was carefully measured. State the reasoning in one sentence and link the full record.

**Do not promise simultaneous platform parity you cannot deliver.** If certification means PC gets a fix two weeks before console, say so in the notes rather than letting players discover the gap themselves.

**Where this lives:** the store page, patch notes site, or in-client, same as the general template.

---

## Related documents

- [`../../general-swe/foundations/release-notes.md`](../../general-swe/foundations/release-notes.md). The base template
- [`balance-log.md`](balance-log.md). The full reasoning and measured effect behind every balance change summarised here
- [`deployment-plan.md`](deployment-plan.md). How this release actually reached players, including the certification timeline that drives the platform notes section
