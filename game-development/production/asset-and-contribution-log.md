# Asset and contribution log: {Project}

*Italic text is guidance. Delete it as you fill each section in.*

*A game's configuration items are not only code. A character model, a music track, a sound effect, and a piece of concept art are all configuration items in the same sense the [configuration management plan](../../general-swe/foundations/configuration-management-plan.md) means the term: work products designated for control, with an owner and a known state. Code has Git to answer "who wrote this and under what licence." Art and audio, especially once a contractor, a vendor, or a stock library is involved, usually have nothing playing that role. This document is that role.*

---

## The log

| Asset ID | Name | Category | Status | Contributor | Rights | Source | Last updated |
|---|---|---|---|---|---|---|---|
| *AST-0142* | *Frost golem, base model* | *Character* | *Approved* | *Outsource vendor: Northwind Studios* | *Work for hire, full transfer, contract #2026-014* | *Commissioned* | *2026-03-02* |
| *AST-0143* | *Title theme* | *Music* | *Licensed* | *J. Alvarez (composer)* | *Exclusive sync licence, game use only, contract #2026-009* | *Commissioned* | *2026-02-14* |
| *AST-0144* | *Ambient forest loop* | *Audio* | *Licensed* | *Freesound.org, user "biotic"* | *CC0* | *Stock* | *2026-01-30* |

**Status values:** *Concept / WIP / Final / Approved / Rejected / Retired. Pick the set that matches your pipeline and use it consistently; the value of the column is entirely in everyone using the same words for the same state.*

**Rights, always.** *Every row states what right you actually have, not an assumption that you have one. "Work for hire, full transfer" and "exclusive sync licence, game use only" are not interchangeable, and the difference is the one a publisher's legal review or a platform certification process will actually check. "CC0" and "attribution required" are not interchangeable either; if attribution is required, record where it is fulfilled.*

---

## Contributor register

*Everyone who has produced an asset, once, with the terms that apply to everything they contribute unless a specific asset states otherwise.*

| Contributor | Role | Agreement type | Contract or reference | Territory or use limits |
|---|---|---|---|---|
| | | | | |

*This table exists so a rights question about a specific asset does not require re-reading a contract from scratch. It also catches the case a per-asset log misses: a contributor whose agreement has expired, been revoked, or never covered the use you are now making of their work.*

---

## Flags

*Assets with an open question. This is the section someone actually reads before a release, not the full log above.*

| Asset ID | Issue | Blocks | Owner | Opened |
|---|---|---|---|---|
| *AST-0146* | *Rights confirmation not yet returned from vendor* | *Cannot ship in this build* | | *2026-03-20* |

---

## Notes on using this template

*Delete this section too.*

**Record the right, not your confidence in the right.** "We're pretty sure this is fine" is not a value for the Rights column. If the contract is unclear, the row belongs in Flags, not in the main log marked Approved.

**One row per asset, not per file.** A character model with a base mesh, three texture variants, and a rig is one configuration item with one rights story, even if it is several files. Track file-level detail in your asset pipeline tool; track the row here at the level a rights question would actually be asked.

**Stock and CC-licensed assets need this table as much as commissioned ones do.** A permissive licence still has terms: attribution, non-commercial restrictions, share-alike requirements. "We downloaded it for free" is not the same as "we have the right to use it the way we are using it."

**This is a control, not paperwork.** The reason it earns its place is the same reason the [configuration management plan](../../general-swe/foundations/configuration-management-plan.md) exists: at any moment, you should be able to answer what is in the build, where it came from, and who agreed to it, without asking a person who might be unavailable, or might have left.

**Where this lives:** docs-as-code, a spreadsheet linked from the wiki, or your asset pipeline tool, whichever one your team will actually keep current. The requirement is not the format; it is that exactly one place answers "do we have the rights to this," and everyone knows where it is.

---

## Related documents

- [`../foundations/art-bible.md`](../foundations/art-bible.md). The standard an asset is produced against, as distinct from its status and rights
- [`../../general-swe/foundations/configuration-management-plan.md`](../../general-swe/foundations/configuration-management-plan.md). The general version of the control this document implements for art and audio
- [`../../general-swe/foundations/changelog.md`](../../general-swe/foundations/changelog.md). The equivalent record for code
