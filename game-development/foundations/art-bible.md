# Art bible: {Game name}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Locked since** | YYYY-MM-DD *When direction stopped being negotiable. Blank if still concept-stage* |
| **Art director** | |
| **Last reviewed** | YYYY-MM-DD |
| **Applies to** | *Which project or which sub-team, if a studio runs several* |

*This is a production reference, not a pitch. Concept art made to sell a visual direction internally or to a publisher belongs in the [business plan](business-plan.md) or the [game design document](game-design-document.md)'s aesthetics section. This document starts once that direction is locked, and its job is narrower and more precise: let two different artists, or an outsourcing vendor who has never spoken to the art director, produce work that looks like it came from the same game.*

*The web-development area solves the identical problem for a different medium: [`brand-and-visual-guidelines.md`](../../web-development/foundations/brand-and-visual-guidelines.md) and [`design-system-guide.md`](../../web-development/foundations/design-system-guide.md) lock a visual language so a distributed team ships one coherent product. Read this as that same document, adapted for a production pipeline that includes outsourced art and per-asset review rather than a component library.*

---

## Visual pillars

*Two to four short phrases, the visual equivalent of the design pillars in the game design document. Every asset gets checked against these before it gets checked against anything more specific.*

| Pillar | Means | Rules out |
|---|---|---|
| | | |

---

## Palette

*The colours in use, and the rule for when each applies. A palette without a rule is a swatch, not a standard: two artists reading "warm autumn tones" will not converge, but two artists reading "hostile zones use desaturated red-orange, safe zones use saturated blue-green" will.*

| Context | Palette | Rule |
|---|---|---|
| | | |

---

## Proportions and silhouette

*The rules that keep a character, creature, or prop recognisable at a glance and consistent across artists. State the rule, not just an example: "player-controlled characters read at 7 heads tall, enemies at 6 or fewer, so silhouette alone signals threat versus ally" is a rule an artist can apply to a character nobody has drawn yet.*

---

## Per-category standards

*The table an artist or a vendor checks before starting work. Fill in every category your project actually produces; delete the rest.*

| Category | Polycount budget | Texture resolution | Naming convention | Reviewed by |
|---|---|---|---|---|
| *Player character* | | | | |
| *Enemy, standard* | | | | |
| *Enemy, boss* | | | | |
| *Environment prop* | | | | |
| *UI element* | | | | |
| *VFX* | | | | |

---

## Material and rendering treatment

*Shader rules, lighting approach, post-processing. What makes a correctly modelled, correctly coloured asset still look wrong if it ignores this section: cel-shaded outlines, a specific roughness range, a rule against pure black or pure white in albedo textures.*

---

## Reference and inspiration

*Real-world and media references that anchor the pillars above, so "military sci-fi but grounded" has an example an artist can hold up next to their own work.*

*This section is where most of the actual content of an art bible lives, and it is almost entirely images. Keep the images in your shared drive or digital asset manager and link them from here; do not try to make this file the source of truth for visual reference. See the notes below on where this document lives.*

---

## Do and don't

*Paired examples, described precisely enough to apply without seeing an image. A rule an artist can misread is a rule that will be misread.*

| Do | Don't | Why |
|---|---|---|
| | | |

---

## Cultural and regional review

*Delete this section if your game ships to one territory. Keep it if you localise or distribute internationally.*

*Imagery, symbols, colours, and gestures carry different meanings in different markets. Name who reviews new asset categories for this before they ship, and what the review checks for.*

---

## What is currently changing

*Direction changes even after it is locked. This section is what keeps the document honest about it, the same way the [data model](../../general-swe/foundations/data-model.md) template tracks an in-progress schema change instead of pretending the schema is settled.*

| Change | Old direction | New direction | Applies from | Owner |
|---|---|---|---|---|
| | | | | |

---

## Notes on using this template

*Delete this section too.*

**This is not the concept art.** Concept art that explores options belongs to pre-production and to the pitch. This document is what is left once the exploring is done: a small number of decided rules, stated precisely enough to hand to someone who was not in the room.

**Written because verbal direction does not scale to a contractor.** An in-house artist sitting near the art director absorbs correction constantly and informally. An outsourcing vendor gets none of that, and every rule they were not given, they will guess, inconsistently. This document is what you hand them instead of a guess.

**A locked pillar is still a pillar someone can challenge.** Locking direction stops daily renegotiation, not the possibility that the direction is wrong. Route a real challenge to the art director and record the decision in the "what is currently changing" table; do not let it get relitigated asset by asset.

**Keep the rules, not the debate.** This document states what was decided. Why it was decided, and what else was considered, belongs in an [ADR](../../general-swe/foundations/architecture-decision-record.md)-style record if you want that history kept at all.

**Where this lives:** a shared drive or digital asset management tool that handles images well, linked from the wiki. This repository, and Git generally, handle binary images and large media poorly; do not force this document into a text-only home just for consistency with the rest of this area.

---

## Related documents

- [`game-design-document.md`](game-design-document.md). States the aesthetic and emotional intent this document turns into an executable standard
- [`business-plan.md`](business-plan.md). Where pitch-stage concept art belongs, before direction locks
- [`../../web-development/foundations/brand-and-visual-guidelines.md`](../../web-development/foundations/brand-and-visual-guidelines.md). The same problem, solved for a website
- [`../../web-development/foundations/design-system-guide.md`](../../web-development/foundations/design-system-guide.md). The same problem, solved for a component library
- [`../production/asset-and-contribution-log.md`](../production/asset-and-contribution-log.md). Where an individual asset's status and rights are tracked, as distinct from the standard it must meet
