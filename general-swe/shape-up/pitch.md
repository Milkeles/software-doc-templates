# Pitch: {What this would do}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Shaped by** | *Whoever did the shaping. Usually one or two people.* |
| **Date** | YYYY-MM-DD |
| **Appetite** | *Small batch (1 to 2 weeks) or big batch (6 weeks). Nothing else.* |
| **Status** | *Draft / Circulating / Bet on for cycle {N} / Passed on* |

*Title it as the thing itself, not as a problem area. A person scanning six pitches before a betting table should know what each one would build.*

*Five ingredients, and the book names all five: problem, appetite, solution, rabbit holes, no-gos. They are below in that order. Do not add a sixth.*

---

## 1. Problem

*The raw idea, a use case, or something you saw that makes this worth working on. One specific case beats a category.*

*Name a person and what happened to them. "Users want better filtering" is a category and it justifies anything. "A customer with 4,000 contacts cannot find one without scrolling" is a problem, and it rules things out, which is the useful property.*

*If you only have a solution and no problem, stop. There is no way to argue about whether a solution is good without one.*

> **Example.** Customers who run more than one company on their account have to log out and log back in to switch. Support gets this weekly. One customer described keeping two browsers open permanently.

---

## 2. Appetite

*How much time this is worth, decided before you designed anything.*

*This is a budget, not a prediction. It constrains the solution rather than describing it. If the design does not fit the appetite, cut the design, not the appetite.*

*Say what makes it worth that much and no more. An appetite with no reasoning behind it is a number someone will negotiate.*

> **Example.** Two weeks. It affects a small share of accounts, but it is the top support complaint from the largest ones. Not worth six.

---

## 3. Solution

*The core elements, in a form someone understands immediately.*

*Rough, solved, bounded. All three, and they pull against each other, which is why shaping is work.*

**Rough.** *Deliberately unfinished, so the team can see where their judgement belongs. Fat marker sketches, breadboards, prose. Not mockups. Specific work is harder to estimate, not easier, because the hidden complexity sits in the details you drew.*

**Solved.** *Every main element is present at the macro level and they connect. Not a task list. A reader must be able to say what the finished thing does.*

**Bounded.** *It is clear what is inside and where it stops.*

*Two ways to draw this, both from the book:*

- **Breadboard**, for anything mostly about flow. Places (screens or dialogs), affordances (things you can click or type into), and lines connecting an affordance to the place it leads. No layout. It stays about what connects to what.
- **Fat marker sketch**, for anything where an arrangement matters. Drawn thick enough that you cannot add detail. That is the point of the marker.

> **Example (breadboard).**
> ```
> Account menu ---> Switch company (list of companies)
>                        |
>                        v
>                   Dashboard, now scoped to chosen company
> ```

*Then the elements in prose, one line each. If you cannot say what an element does in a line, it is not solved yet.*

---

## 4. Rabbit holes

*The holes you already filled in while shaping, and how you filled them.*

*This is the ingredient people get wrong. It is not a risk register handed to the team. It is the record of the hard parts you thought through so nobody spends week three discovering them.*

*Where a rabbit hole is deep enough, dictate the answer. Prescribing one technical detail is legitimate here even though the rest of the pitch is deliberately rough.*

*The test: would a competent person hit this and lose days? If yes, it belongs here with an answer next to it.*

> **Example.** Switching must not invalidate the current session. Reuse the existing session and swap the account scope on it rather than re-authenticating. Re-authenticating drags in the SSO path and that is a project of its own.

---

## 5. No-gos

*What is explicitly excluded, so nobody builds it and nobody asks whether it is missing.*

*Two kinds, and both are worth listing. Things you decided against, and things you cut to make the appetite work.*

*This is what makes a pitch bounded. Without it, everyone reading fills the gaps differently and each of them reads a larger project than you shaped.*

> **Example.** No cross-company reporting. No copying data between companies. No changes to invitations or permissions. Any of these turns two weeks into six.

---

## Notes on using this template

*Delete this section too.*

**Circulate it before the betting table, not at it.** People read it and comment asynchronously, and the comments are for poking holes and adding missing information, not for voting. A pitch first seen in the meeting is a pitch nobody checked.

**Problem and solution ship together or not at all.** A solution with no problem gives nobody grounds to judge it. A problem with no solution is unshaped work, and handing it to a build team pushes exploration into the six weeks that were meant for building.

**A pitch that does not get bet on is not a backlog item.** It stays where it is. If the idea matters it will come back, and if it does not, the shaping was cheap. Do not build a queue of unbet pitches and review it monthly. That is the thing Shape Up removed.

**Freeze it once it is bet on.** From that point the pitch is the input the team was given, and rewriting it destroys the record of what was actually agreed. Changes during the cycle are the team's scope decisions and belong in [the scope map](scope-map.md).

**Where this lives:** a wiki or document tool. It holds sketches, non-engineers read it, it is frozen after the bet, and none of it versions with code.
