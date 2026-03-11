# User Documentation

Documents written for the people who use your software, rather than the people who build it.

| Document | Write it when |
|---|---|
| [`tutorial.md`](tutorial.md) | Someone new needs to become competent. One per product, sometimes two. Not more |
| [`how-to-guide.md`](how-to-guide.md) | A competent user has a goal. Most of your documentation is this |
| [`reference-page.md`](reference-page.md) | There is a surface to describe. Generate it wherever you can |
| [`explanation.md`](explanation.md) | The same "but why does it work that way" keeps arriving |
| [`installation-guide.md`](installation-guide.md) | Always. It is the first thing anyone reads and the highest-ranked gap in the research |
| [`troubleshooting-guide.md`](troubleshooting-guide.md) | The same problems reach support twice |
| [`documentation-style-guide.md`](documentation-style-guide.md) | More than two people write documentation |

---

## The split, and where it comes from

The first four come from **Diátaxis**, by Daniele Procida, at [diataxis.fr](https://diataxis.fr/). It is the most widely adopted structure for user documentation and the reasoning behind it is unusually careful.

It derives four document types from two axes rather than listing them. **Get the axis names right**, because the popularised version is wrong. Procida's axes are **action/cognition** and **acquisition/application**, not "theory/practice" and "study/work". Those are his glosses inside the definitions, not the axes themselves.

```
                        ACQUISITION                 APPLICATION
                        the user is at study        the user is at work

    ACTION              TUTORIAL                    HOW-TO GUIDE
    knowing how,        "Can you teach me to...?"   "How do I...?"
    what we do          a lesson                    a recipe
                        serves learning             serves a goal

    COGNITION           EXPLANATION                 REFERENCE
    knowing that,       "Why...?"                   "What is...?"
    what we think       discursive explanation      dry description
                        serves understanding        serves information

            the type is decided by the reader's situation,
            not by the subject matter.
```

Procida's own cooking analogy fixes all four at once: teaching a child to cook, a recipe in a cookery book, the information on the back of a food packet, and an article on culinary social history.

**The distinction that gets lost is tutorial versus how-to guide**, and Procida is precise about it. A tutorial's purpose is "to help the pupil acquire basic competence"; a how-to guide's is "to help the already-competent user perform a particular task correctly". A tutorial "eliminates the unexpected" and "responsibility lies with the teacher". A how-to guide "must prepare for the unexpected" and "the user has responsibility". Same steps, different contract.

**The blur is predicted by the framework, not caused by your carelessness.** Procida names it: adjacent types share a property and tend to merge. Tutorials and how-to guides both guide action. Reference and how-to guides both serve application. Reference and explanation both carry propositional knowledge. Tutorials and explanation both serve acquisition. Knowing which neighbour a document is drifting toward is more useful than trying to prevent drift.

---

## What Diátaxis does not cover

Three of the seven templates here sit outside the four-type model, deliberately.

**Installation guide.** Procedural, so nominally a how-to guide, but it is the first document anyone reads and the reader has no competence to assume. In practice it needs its own rules and its own testing discipline.

**Troubleshooting guide.** No clean home. A how-to guide starts from a goal; a troubleshooting reader knows only a symptom. Reference describes the working system. The Good Docs Project ships `troubleshooting` as a separate template, which is the same conclusion reached independently.

**Quickstart.** Not a template here, but worth naming. It sits between tutorial and how-to: too goal-shaped to be a lesson, too pedagogical to assume competence. The Good Docs Project ships it separately from `tutorial`. If you write one, decide consciously which contract it offers.

Genres serving no practitioner-skill need at all sit outside the derivation rather than badly inside it: release notes, changelogs, status pages, legal notices. Those live in [`../foundations/`](../foundations/). Procida is explicit that "the original context for the Diátaxis approach was limited to software product documentation".

**Four types is one taxonomy, not the only one.** Red Hat's modular documentation model uses three: **concept, procedure, reference**. It descends from DITA topic types rather than from Diátaxis, has no tutorial type, and folds explanation into concept. The Good Docs Project names the fourth type `concept` too. GitLab uses its own topic types. If your team already says "concept", use that word; the need is identical and the vocabulary is not settled.

---

## Why these documents work, and how good the evidence is

The evidence is thinner than the field's confidence suggests, but it is not absent, and what exists points somewhere useful.

### What is measured

**Documentation failures are content failures, not presentation failures.** Uddin and Robillard surveyed 323 IBM software professionals for *IEEE Software* (2015) and concluded that "the three severest problems were ambiguity, incompleteness, and incorrectness of content" and that "the most pressing problems were related to content, as opposed to presentation". Six of the ten problems were rated blockers that pushed developers to a different API. Aghajani and colleagues reached a compatible conclusion at *ICSE 2019* by mining 878 documentation-related artefacts from mailing lists, Stack Overflow, issue trackers and pull requests, a method chosen specifically to avoid the bias of asking developers. **Two opposite methods agreeing is stronger than either alone.** The practical consequence: spend your effort on correctness and completeness, not on styling.

**Brief, task-focused, error-aware instruction beats a comprehensive manual for learning.** This is the strongest result in the field and it is genuinely experimental. Carroll, Smith-Kerker, Ford and Mazur-Rimetz, "The Minimal Manual", *Human-Computer Interaction* 3(2), 1987, ran two controlled experiments in a simulated office with measured learning time and task success. The minimal manual won on learning time and on the specific dimensions its design targeted. Note the limits: 19 and 32 participants, 1987, clerical users on a word processor, one research group. The book is *The Nurnberg Funnel* (MIT Press, 1990).

**READMEs systematically omit purpose and status.** Prana and colleagues, *Empirical Software Engineering* 24, 2019, manually annotated 4,226 sections from 393 randomly sampled GitHub repositories: "information discussing the 'What' and 'How' of a repository is very common, while many README files lack information regarding the purpose and status of a repository". Random sampling makes this stronger than most work here. It is the best argument for the [explanation](explanation.md) template.

**Installation instructions are the top-ranked gap.** Aghajani and colleagues at *ICSE 2020* surveyed 146 practitioners: missing installation, deployment and release instructions were rated important by 68%, ahead of user documentation at 65% and developer guidelines at 60%. The authors themselves flag a 9.5% response rate, self-selection bias, and that 125 of 146 came from one company. Perceived importance, not measured outcome.

**Incomplete or outdated documentation is pervasive in open source.** The GitHub Open Source Survey (2017) sampled 5,500 respondents randomly across more than 3,800 repositories and released the data under CC0: "Incomplete or outdated documentation is a pervasive problem, observed by 93% of respondents." It is nine years old, and it means 93% of *respondents encountered the problem*, not that 93% of documentation is bad. That misreading is everywhere.

### What is reasoning, not evidence

**Nobody has empirically validated Diátaxis.** No controlled study, no measured outcome, no peer-reviewed evaluation. Procida is candid that this is not his aim: he writes that Diátaxis "aims to place documentation practice on a more rigorous theoretical footing", which is a claim about theory, not evidence. The site's "proven in practice" is an adoption claim. Adopt the framework because the reasoning is good and the vocabulary is shared, not because it is validated.

**"Diátaxis is used by hundreds of projects" is the author's self-report**, and he states he stopped tracking. Attribute it to him.

### The argument that holds without a study

Two people arrive at your documentation. One is learning, one is stuck mid-task. They want opposite things: the learner wants a controlled path with nothing surprising; the worker wants the shortest route through a mess they already have. **A document that tries to serve both serves neither**, and that is a structural fact rather than an empirical finding.

Carroll and Rosson named the reason people at work will not read the lesson: the *production bias*, which pushes users to act rather than study, and the *assimilation bias*, which makes them read new systems through familiar ones. That is the properly sourced version of "nobody reads the documentation", and it is what justifies the how-to guide as a separate genre.

### Two arguments you should not use

**Any percentage for how much time developers spend reading documentation.** No traceable primary source. The adjacent figures that do circulate, the 70% reading and the 10:1 read-to-write ratio, are about *code* and trace to *Clean Code* asserting them without a study.

**Any ROI or cost-per-ticket figure for documentation.** No primary source exists for any of them. Uddin and Robillard say the opposite and it is worth quoting because it concedes the objection: "creating and maintaining it is costly, and predicting the payoff is difficult."

---

## The standards, and why they will not help you much

**ISO/IEC/IEEE 26511 to 26515** cover this territory, split by role rather than by reader need:

| Standard | Covers | Edition |
|---|---|---|
| 26511:2018 | Managers of information for users | Second |
| 26512:2018 | Acquirers and suppliers | Second |
| 26513:2017 | Testers and reviewers | Second |
| 26514:2022 | Design and development. The "how to write it" one | First |
| 26515:2018 | Developing information for users in an agile environment | Second |

Two details almost every secondary source gets wrong. **The series was renamed**: current editions say "information for users", not "user documentation". Citing "ISO/IEC/IEEE 26514, Requirements for designers and developers of user documentation" cites a withdrawn 2008 document. And **26514:2022 says "First edition" on its title page** despite superseding ISO/IEC 26514:2008, because the earlier one was ISO/IEC and the current one is jointly ISO/IEC/IEEE.

All five are paywalled, and none can be quoted at length. Their real value is the role-based cut, which is a genuinely different question from Diátaxis's need-based cut. There is no evidence of meaningful adoption in general software practice, so do not present them as standard practice.

---

## Reference material worth borrowing from

**The Good Docs Project** ([thegooddocsproject.dev](https://www.thegooddocsproject.dev/)) publishes template sets under **MIT No Attribution**, which permits reuse and adaptation with no obligation to credit. Version 1.6.0 was tagged 11 June 2026 on a roughly six-monthly cadence. Their set covers tutorial, how-to, reference, concept, quickstart, installation guide, troubleshooting and style guide, plus README, changelog, release notes and contributing guide. Credit them anyway; it costs nothing.

**Write the Docs** is a community, not a standards body. It publishes conferences, talks, a Slack and a documentation guide, and no normative rules. Cite it for shared practice, never as an authority for a specific rule.

---

## Where these documents live

All of them: **docs-as-code**, in the repository, published to a docs site by the build.

This is the opposite of the [requirements group](../requirements/), and the reason is the same in both cases: **put the document where its authors already work.** Requirements are co-authored with business stakeholders who cannot open a pull request, so they live on a wiki. User documentation is written by the people who change the code, and it breaks when the code changes.

| Document | Home | Why |
|---|---|---|
| Tutorial | Docs-as-code, tested in CI | Breaks on any change to the flow it teaches. Must be fixable in the same pull request |
| How-to guide | Docs-as-code | Same. Also the largest set, so it needs review tooling |
| Reference | Generated from source, in the same file as the code | A separate copy diverges silently. Docstrings and schema descriptions do not |
| Explanation | Docs-as-code | Changes when the design changes, which happens in pull requests |
| Installation guide | Docs-as-code, run in CI | The commands are testable. Test them |
| Troubleshooting guide | Docs-as-code, indexed by search | Error codes should link straight to the entry |
| Style guide | Docs-as-code, enforced by a linter | It has to be linkable from a review comment |

**The rule that makes this work: documentation changes ship in the pull request that made them necessary.** A separate documentation ticket is a documentation ticket that closes late or never. This is the single highest-value process decision in the group, and it is only available because the documents live next to the code.

---

## What to write first

1. **Installation guide.** The first thing read, the top-ranked gap in the research, and cheap to verify.
2. **Reference**, generated. Do not hand-write what the compiler already knows.
3. **One tutorial.** One good one beats four stale ones.
4. **How-to guides**, added as real tasks appear. Do not plan the set in advance.
5. **Troubleshooting entries**, added the second time a problem is reported.
6. **The style guide**, once more than two people write.
7. **Explanation**, when a question has arrived three times.

---

## Sources

- Daniele Procida, *Diátaxis*, [diataxis.fr](https://diataxis.fr/), CC BY-SA 4.0. Continuously revised with no version numbers, so cite with an access date
- The earlier Divio documentation system (2014 to 2021), which Procida wrote and has partly disavowed: "I still agree with most of it, though there are several aspects that I now think I got wrong." The phrase "The Grand Unified Theory of Documentation" belongs to David Laing, not Procida
- The Good Docs Project templates, MIT No Attribution, v1.6.0, 11 June 2026
- ISO/IEC/IEEE 26511:2018, 26512:2018, 26513:2017, 26514:2022, 26515:2018. All paywalled
- Google developer documentation style guide, CC BY 4.0. Microsoft Writing Style Guide, which replaces the *Microsoft Manual of Style*. Red Hat supplementary style guide, layered on the IBM Style Guide. GitLab documentation style guide. Apple Style Guide, June 2026
- Uddin and Robillard, "How API Documentation Fails", *IEEE Software* 32(4), 2015
- Aghajani et al., "Software Documentation Issues Unveiled", *ICSE 2019*, and "Software Documentation: The Practitioners' Perspective", *ICSE 2020*
- Prana et al., "Categorizing the Content of GitHub README Files", *Empirical Software Engineering* 24, 2019
- Carroll, Smith-Kerker, Ford and Mazur-Rimetz, "The Minimal Manual", *Human-Computer Interaction* 3(2), 1987. Carroll, *The Nurnberg Funnel*, MIT Press, 1990
- Williams and Farkas, "Minimalism Reconsidered: Should We Design Documentation for Exploratory Learning?", *SIGCHI Bulletin*, 1992, for the critique of guided exploration
- Carroll and Rosson, "Paradox of the Active User", in *Interfacing Thought*, MIT Press, 1987. A theoretical synthesis, not an experiment
- GitHub Open Source Survey, 2017, data under CC0

**On sourcing.** Quoted material is verbatim from the sources named. Where a claim is reasoning rather than evidence, it is labelled as such. Statistics widely repeated without a traceable source, including documentation reading-time percentages and documentation ROI figures, are named above and left out.
