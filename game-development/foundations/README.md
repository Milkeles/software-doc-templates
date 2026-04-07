# Foundations

The three documents almost every game project writes, regardless of genre, platform, or methodology. They answer three separate questions that get tangled together if you let them: what the game is, what it looks like, and why anyone should pay for it.

## The documents

| Document | Answers |
|---|---|
| [`game-design-document.md`](game-design-document.md) | What are we building, and what should it feel like to play? |
| [`art-bible.md`](art-bible.md) | What does it look like, precisely enough that two different artists produce the same thing? |
| [`business-plan.md`](business-plan.md) | Why does this get funded, and on what terms? |

## When to use each

**Game design document: from the first pitch, and continuously after.** Start it before you can answer every section. A design document that waits for certainty never gets written, because a game does not have certainty until it is finished.

**Art bible: once direction is locked and more than one person is producing art.** A solo developer or a two-person team communicating by looking at the same screen does not need this. The moment you add a contractor, an outsourcing vendor, or a second artist who was not in the room when a decision was made, verbal direction stops scaling and this document starts paying for itself.

**Business plan: when you need someone outside the founding team to say yes.** A publisher, an investor, a platform holder deciding whether to feature you, or your own studio's leadership deciding whether to greenlight the next milestone. A self-funded solo project answerable to nobody can reasonably skip it.

## Why these three, and not one combined document

Each is written for a different reader who wants a different thing from it, and combining them serves none of the three well.

A designer wants the game design document to hold still long enough to build against, but wants to keep changing it as the game teaches you what it actually is. An artist wants the art bible to be a precise, stable reference they can match without asking someone. A publisher wants the business plan to answer "will this make money and can this team ship it" in the time it takes to read a few pages, because that is roughly all the time a first-pass pitch review gets. A document trying to satisfy all three compromises on all three: too unstable for the artist, too detailed for the publisher, too commercial for the designer.

## Where these live

None of these three belong in the source repository, and that puts this group at odds with most of `general-swe/foundations/`. The reason is the same one, three times over: the value of each document is either in ongoing discussion (the design document), in image content Git handles badly (the art bible), or in a readership that does not use a code editor (the business plan). See the area [README](../README.md) for the full table.
