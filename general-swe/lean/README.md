# Lean

Documents for teams that treat improvement as a discipline: find where the time actually goes, change one thing, predict what will happen, and check.

---

## First: there are two Leans, and they share almost nothing but the word

**Lean from Toyota.** Ohno's *Toyota Production System* (1988), Womack and Jones's *Lean Thinking* (1996), Rother and Shook's *Learning to See* (1999), Shook's *Managing to Learn* (2008), Rother's *Toyota Kata* (2009). It is about flow, waste and a repeatable improvement routine. It assumes you are already making something and want to make it better.

**Lean Startup.** Ries (2011) and Blank (2005, 2013). It is about testing whether anyone wants the thing at all. Blank's definition of a startup is exact: "a temporary organization designed to search for a repeatable and scalable business model." The distinction he builds on is that "while existing companies execute a business model, start-ups look for one."

Blank names the lineage himself: he credits his own customer development work, Osterwalder and Pigneur's business model canvas, and then writes, "Eric dubbed the combination of customer development and agile practices the 'lean start-up.'" So the two are related by naming, not by derivation.

They answer different questions. Toyota lean asks whether you are building it well. Lean Startup asks whether you should be building it. A team with a delivery problem and a team with a demand problem both reach for "lean" and get different books.

**This group holds four documents covering both, and they are not equally well evidenced.** That is stated below rather than smoothed over.

---

## The manufacturing analogy, and the best argument against it

Every lean-in-software text rests on one move: treat development as a production process, then apply production thinking. It is worth knowing the strongest objection before adopting anything here.

Jack Reeves made it in 1992, a decade before lean software development existed. His argument in "What Is Software Design?" is that **source code is the design, and the compiler and linker are the manufacturing step.** If that is right, software is cheap to build and expensive to design, manufacturing is nearly free, and optimising the production line is a category error. The entire cost sits in design, which is the one activity lean manufacturing does not address.

The Poppendiecks concede the shape of this themselves, contrasting development as an exercise in discovery with manufacturing as an exercise in reducing variation.

The honest position: lean's diagnostics work in software where the problem is queues and handoffs, which are real and everywhere. They work less well where the problem is that the thinking is hard. Use the tools on the first kind of problem.

---

## Ohno's seven wastes, in his words

Reproduced because almost every version you will meet is a paraphrase. Ohno introduces the list with "The preliminary step toward application of the Toyota production system is to identify wastes completely":

1. Waste of overproduction
2. Waste of time on hand (waiting)
3. Waste in transportation
4. Waste of processing itself
5. Waste of stock on hand (inventory)
6. Waste of movement
7. Waste of making defective products

**Overproduction is first on purpose.** Ohno calls it "our worst enemy" because it hides the others. Build more than is needed and the queue absorbs every problem downstream of it, so nothing surfaces.

Two notes on vocabulary that will save an argument later.

"TIMWOOD" is a later mnemonic, not Ohno's list and not his ordering. Using it silently reorders his priorities.

The three Ms are more fragile than they look. Ohno's authorised 1988 English translation renders them as waste (muda), **inconsistency** (mura) and **unreasonableness** (muri). The now-standard "unevenness" and "overburden" are later Lean Enterprise Institute vocabulary. The concepts survive the translation, the words are downstream. And they appear together exactly once in the whole book, inside a clause about kanban rules, not as a headline framework. "Ohno defined three categories of waste" overstates one sentence.

---

## Poppendieck's principles, and why you will find two lists

This causes real confusion, because the list most often reproduced online is from the 2003 book while the citation next to it points at the 2006 one. The Poppendiecks renamed five of the seven and said so: "Some readers may notice that the wording of some principles has changed a bit, but the intent remains the same."

| 2006 (*Implementing Lean Software Development*) | 2003 (*Lean Software Development*) |
|---|---|
| Eliminate Waste | Eliminate Waste |
| Build Quality In | Build Integrity In |
| Create Knowledge | Amplify Learning |
| Defer Commitment | Decide as Late as Possible |
| Deliver Fast | Deliver as Fast as Possible |
| Respect People | Empower the Team |
| Optimize the Whole | See the Whole |

Use the 2006 wording. If you quote the 2003 wording, cite the 2003 book.

Their seven wastes of software, from 2006: partially done work, extra features, relearning, handoffs, task switching, delays, defects. Their claim about the first among these mirrors Ohno's: "Just as Taiichi Ohno called overproduction the worst waste in manufacturing, unused features are the worst kind of waste in software development."

**One number to handle carefully.** Their widely quoted figure that only about 20 percent of features are used regularly comes from a Standish Group presentation, and they hedge it themselves: it came from a limited study, they checked it informally against audiences, and they claim only that it is "in the right ballpark." Standish data is separately criticised as unreproducible. Quote the hedge with the number or leave both out.

---

## The document map

| Document | Write it when | Skip it when | Home |
|---|---|---|---|
| [A3](a3.md) | A problem is big enough to need thinking through and small enough for one person to own | The cause is known and the fix is a commit | Paper, then a photograph in the wiki |
| [Value stream map](value-stream-map.md) | You suspect the delay is in the queues, not the work | You have not walked the flow yourself | Paper, drawn during the walk |
| [Experiment record](experiment-record.md) | You are changing something and predicting an outcome | You are not predicting anything, in which case it is not an experiment | Version control or a wiki |
| [Improvement kata](improvement-kata.md) | You want a repeatable improvement routine rather than occasional pushes | You have one problem to fix and then stop | Version control or a wiki |

---

## Where lean documents live, and why two of them belong on paper

This group splits cleanly, and the split is the most useful thing on this page.

**Value is in the making: the A3 and the value stream map.** These are thinking aids. The artefact is a by-product of somebody understanding something, and a tidy artefact produced without that understanding is worthless while looking better. Keep them cheap, physical and disposable. Archive a photograph and the resulting plan, not the map.

This is not nostalgia and it is not my inference. Rother and Shook give it a page with a bare imperative heading, **"Always draw by hand in pencil"**, and then argue it:

> "Resist the temptation to use a computer."

> "Drawing by hand means that you can **do it yourself**, which is key to understanding the material and information flows."

> "Drawing by hand means you will focus on understanding the flow, instead of on how to use the computer. **The point of value stream mapping is not the map, but understanding the flow of information and material.**"

And they extend it to division of labour: "Map the whole value stream yourself, even if several people are involved... If different people map different segments, then no one will understand the whole."

The claim is epistemic. Tooling and delegation both improve the artefact and destroy the thing it was for.

The A3's constraint is the same kind of constraint. It is named for the paper it is written on, one sheet of A3 or 11 by 17 inches. That is the largest sheet a small group can read together around a table and the smallest that forces you to cut. Both traditions independently landed on the same sheet: Rother and Shook tell the mapper to use "11" x 17" ledger size paper, called 'A-3' in Europe and Japan," and Sobek and Jimmerson define the A3 report as one "written on an A3 sized paper (metric equivalent of 11" x 17")."

I would not push the A3 as far as "must be handwritten." The sourced claims are that it is size-constrained and that it is deliberately incomplete when circulated. Those two are the point.

**Value is in the keeping: the experiment record and the improvement kata.** These carry a prediction made before the outcome was known. Their entire worth is that someone can retrieve them afterwards and check whether the prediction held. Version them, in the repository or a wiki, wherever they will survive.

The test is simple. If the document's job is done the moment it is finished, keep it cheap. If its job starts the moment it is finished, keep it safe.

---

## The documents, one by one

### A3

**When.** A problem worth several days of somebody's attention.

**Why.** The A3 forces a sequence people skip: state the problem, establish what is actually happening now, find the cause, only then propose something. Most improvement proposals arrive as a solution with a problem reverse-engineered onto the front, and the format makes that visible because the current-condition box will be thin.

There is one finding that argues directly for having a real template rather than a blank page. Sobek and Jimmerson analysed 18 cases and reported that participants who followed each step consistently achieved excellent results, and that "skipping even one step dramatically reduced the likelihood of success." That is 18 cases, not a controlled trial, and it comes from a university engineering department rather than a consultancy. Treat it as the best available evidence, which it is, rather than as proof.

**The layout is doctrinal, and it means something.** Items flow top to bottom down the left side, then top to bottom down the right. Left is what is true. Right is what to do about it. A reader can tell at a glance whether you spent your effort on understanding or on advocating.

**The results box is blank when you write it.** An A3 that arrives complete has skipped the process it exists to impose.

**Note the section lists disagree.** Sobek and Jimmerson use eight boxes, Shook's *Managing to Learn* uses seven, and a 2013 *PLOS ONE* paper describes a ten-step variant. The template here follows Sobek and Jimmerson because their section names are the ones I could verify verbatim. Do not treat any of the three as a standard.

**Where.** Paper. Photograph into the wiki when it is done.

### Value stream map

**When.** You suspect the delay is in the waiting rather than the working, and you are prepared to go and look.

**Why.** The map's job is one comparison: total elapsed time against the time anyone was actually working. Rother and Shook expect that comparison to be unpleasant, and their worked example makes the point better than any benchmark. At Acme Stamping, 188 seconds of processing time sat inside a 23.6 day lead time.

**Read the limitations before using this in software, because they are real.** Three come straight out of the primary text:

- The authors call it "a pencil and paper tool" in the definition itself, and describe it as **qualitative**: "Numbers are good for creating a sense of urgency or as before/after measures." A VSM turned into a metrics dashboard is being misused by its authors' account.
- It is scoped to **one product family, door to door.** A map covering everything a software team does violates the method.
- It assumes a repeating flow you can time with a stopwatch. "Bring your stopwatch and do not rely on standard times." Software work items are heterogeneous and mostly non-repeating, so per-step cycle time in the original sense often has no stable meaning.

The usable translation: in software a VSM is a **queue and handoff diagnostic**, not a production diagnostic. It shows you where work waits and who hands it to whom. That is worth knowing and it is less than the manufacturing version delivers.

**One column on the template is not from the original.** Percent complete and accurate, the share of work arriving downstream that is usable without rework, was introduced by Keyte and Locher in 2004 for office and administrative processes. The phrase appears nowhere in Rother and Shook. It is arguably the most useful column on a software map, which is why it is there, but attribute it correctly.

**Where.** Paper, drawn while walking the flow. The wiki gets a photograph and the value stream plan.

### Experiment record

**When.** You are about to change something and you have a prediction.

**Why.** Because your prediction is probably wrong, and you will not remember that unless you wrote it down.

The number that makes this argument is from Microsoft's experimentation platform team, and it is worth quoting exactly:

> "only about 1/3 of ideas improve the metrics they were designed to improve"

with the split: "about 1/3 be good, 1/3 flat, and 1/3 negative." Kohavi's own caveat belongs with it, because it strengthens the claim rather than weakening it: there is selection bias, since teams experiment when they are unsure. He also notes Bing's success rate is lower.

Two thirds of confident ideas do nothing or harm. That is the case for writing the prediction down before you find out.

**Where.** Version control or a wiki. Its value is entirely retrospective.

### Improvement kata

**When.** You want improvement to be a routine rather than an event.

**Why.** Rother's argument for a written pattern is that understanding is not enough: "Concepts or coarse steps alone don't change mindset and behavior." The four steps are named in his handbook as Understand the Direction, Grasp the Current Condition, Establish the **Next** Target Condition, and Iterate Toward the Target Condition. The word "next" is in the official step name and carries the meaning. Target conditions come in a series.

The distinction that does the work is target versus **target condition**. A target is an outcome, a number you want. A target condition describes how the process operates once you get there. You can enumerate the obstacles between here and a target condition. You cannot enumerate the obstacles between here and a number.

The reflection questions from the Coaching Kata are the best-sourced experiment structure available anywhere in this group: what did you plan as your last step, what did you expect, what actually happened, what did you learn. Four questions, and the second only works if the expectation was recorded before the fact.

**Where.** Version control or a wiki.

---

## PDCA, PDSA, and why Deming disowned the acronym

Small piece of history, worth carrying because it explains a naming inconsistency you will hit.

Deming objected to "PDCA" on two counts. The word: he "warned Western audiences that the plan, do, check, and act version is inaccurate because the English word 'check' means 'to hold back.'" And the attribution. Asked in 1980 how the quality-circle PDCA related to the Deming Circle, he answered: "They bear no relation to each other." In a 1990 letter he wrote, "be sure to call it PDSA, not the corruption PDCA." In a 1991 letter: "How the PDCA ever came into existence I know not."

Lineage: Shewhart (1939), Deming's 1950 Japan lectures, Japanese PDCA, Deming reintroducing the Shewhart cycle in 1986, and PDSA as "the Shewhart cycle for learning and improvement" in 1993.

Practical consequence: Rother's material uses PDCA throughout, so the kata template does too. The history is here rather than as a correction to him.

---

## Womack and Jones's five principles, and their own complaint about them

The five names are certain: **value, value stream, flow, pull, perfection.** Their own sentence containing all five:

> "We are putting the entire value stream for specific products relentlessly in the foreground and rethinking every aspect of jobs, careers, functions, and firms in order to correctly specify value and make it flow continuously along the whole length of the stream as pulled by the customer in pursuit of perfection."

The imperative-verb version you will see everywhere ("specify value, identify the value stream, make value flow...") varies between sources and I could not verify it against the book. Use the names.

More useful than the principles is their complaint about how people apply them. In their foreword to *Learning to See* they reproduce their own five-step action plan and single out the step everyone skips:

> "Yet the overlooked Step Four is actually the most critical"

Step four is mapping the value stream. What they see instead is "companies rushing headlong into massive muda elimination activities, kaizen offensives or continuous improvement blitzes." Waste elimination without mapping first is the standard failure, named by the authors.

---

## What to write first

1. **One A3**, on a problem you actually have. It is the cheapest of these and it teaches the sequence the rest depend on.
2. **One value stream map**, if and only if you are willing to walk the flow yourself. Otherwise skip it, because a map drawn from a meeting room is a fiction with numbers.
3. **The experiment record**, as soon as anyone proposes a change with a predicted outcome.
4. **The improvement kata**, once the first three have happened at least once and you want them to keep happening.

---

## Where the evidence is strong and where it is not

Stated plainly, because the four documents here are not equal and treating them as equal is how people get burned.

**Strongest.** Online controlled experimentation. Kohavi's one-third finding is quantified, industrial, replicated across companies and published. If you take one thing from this group, take the experiment record.

**Solid but narrow.** The A3. Decades of documented Toyota practice, primary-source arguments for its specific design constraints, and real academic study, though that study is dominated by healthcare case work and practitioner surveys. There is no controlled comparison of A3 against another structured format.

**Well documented, poorly translated.** The value stream map. Superb as a manufacturing method, described in detail by its authors, and resting on assumptions that do not hold in software. Worth using with the limitations above stated.

**Weakest.** Lean Startup as a management methodology. Multiple independent systematic reviews converge on a thin empirical base, isolated case settings, mixed findings, and no review concluding it demonstrably improves outcomes. Note the asymmetry carefully: the strength of the experimentation evidence does not transfer to the methodology built around it. They are separate claims and the literature treats them very differently.

**On lean in software generally.** Pernståhl, Feldt and Gorschek's review found lean software research "in its nascent state" for large-scale development with "very little support available for practitioners." That was 2013 and it remains the citation for the gap between the enthusiasm and the evidence.

---

## Sources

- Ohno, *Toyota Production System: Beyond Large-Scale Production*, Productivity Press, 1988. The seven wastes, the three Ms, and "All we are doing is looking at the time line"
- Womack and Jones, *Lean Thinking*, Simon & Schuster, 1996. The five principles
- Rother and Shook, [*Learning to See*](https://www.lean.org/store/book/learning-to-see/), Lean Enterprise Institute, v1.2, 1999. Value stream mapping, the hand-drawing argument, the Acme figures
- Shook, *Managing to Learn*, Lean Enterprise Institute, 2008. The A3 as a dialogue between mentor and mentee
- Sobek and Jimmerson, "A3 Reports: Tool for Organizational Transformation," *Proceedings of the 2006 Industrial Engineering Research Conference*. The verified eight-section structure and the 18-case finding
- Rother, [*The Improvement Kata Handbook*](http://www-personal.umich.edu/~mrother/Handbook/), and *Toyota Kata*, McGraw-Hill, 2009
- Poppendieck and Poppendieck, *Implementing Lean Software Development: From Concept to Cash*, Addison-Wesley, 2006, and *Lean Software Development: An Agile Toolkit*, 2003
- Keyte and Locher, *The Complete Lean Enterprise*, Productivity Press, 2004. Origin of percent complete and accurate
- Reeves, ["What Is Software Design?"](https://www.developerdotstar.com/mag/articles/reeves_design.html), *C++ Journal*, 1992. The strongest argument against the manufacturing analogy
- Ries, ["Minimum Viable Product: a guide"](http://www.startuplessonslearned.com/2009/08/minimum-viable-product-guide.html), 2009, and *The Lean Startup*, Crown, 2011
- Blank, "Why the Lean Start-Up Changes Everything," *Harvard Business Review* 91(5), 2013
- Kohavi, Crook, Longbotham et al., "Online Experimentation at Microsoft," 2009. The one-third finding
- Kohavi, Deng, Frasca et al., ["Online controlled experiments at large scale"](https://doi.org/10.1145/2487575.2488217), KDD '13
- Fagerholm, Sanchez Guinea, Mäenpää and Münch, ["The RIGHT model for Continuous Experimentation"](https://doi.org/10.1016/j.jss.2016.03.034), *Journal of Systems and Software* 123, 2017
- Pernståhl, Feldt and Gorschek, ["The lean gap"](https://doi.org/10.1016/j.jss.2013.06.035), *Journal of Systems and Software* 86(11), 2013
- Moen and Norman, ["Evolution of the PDCA Cycle"](https://deming.org/), and Moen, "Foundation and History of the PDSA Cycle." Deming's objections, with dates and letters

**On sourcing.** The Toyota material is primary and old, and its software translation is the weak joint throughout. Where a claim comes from the manufacturing source it is quoted; where it comes from the software adaptation it is attributed to the adapter. Two things frequently stated as lean facts are not sourced anywhere we could find: a typical flow efficiency percentage for knowledge work, and any definition of validated learning or innovation accounting in Ries's own words beyond his 2009 MVP post. Both are omitted rather than hedged.
