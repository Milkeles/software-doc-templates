# Requirements traceability matrix: {System}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Baseline** | *Which [specification](software-requirements-specification.md) version this traces.* |
| **Generated from** | *The tools the links live in. If the answer is "typed by hand", read the warning below first.* |
| **Generated on** | YYYY-MM-DD |
| **Owner** | *Who is accountable for the traces being true, not for the file existing.* |

*The spine of plan-driven work. Gotel and Finkelstein's definition, still the one everyone cites, is "the ability to describe and follow the life of a requirement, in both a forward and backward direction."*

*Read the warning in the last section before you build this as a spreadsheet.*

---

## What this matrix is for

*State it, because a matrix built without a stated purpose gets built to the wrong shape.*

*Two directions, two different questions, two different faults found.*

| Direction | Question | Finds |
|---|---|---|
| **Forward** | *Is every requirement designed, built and verified?* | *Gaps. Requirements nobody implemented.* |
| **Backward** | *Why does this code or test exist?* | *Scope creep, gold-plating, orphaned code.* |

*Both, maintained together, is what standards mean by "bidirectional". One direction is half a control.*

**Pre-specification traceability.** *The axis teams skip. Forward from a requirement into design and code is post-specification traceability. Backward from a requirement to its origin, its rationale and the person who asked for it is pre-specification, and it is the one that decays first, because the origin is a conversation and the conversation is not in a tool.*

*The cost of skipping it arrives two years later, when nobody can say whether a requirement is load-bearing, so nothing can safely be removed and the system only grows.*

---

## The trace chain

*Name the levels you trace through, and how many you need. Not every project needs all of them.*

*A defensible chain for a regulated system:*

```
stakeholder need
  → system requirement
    → software requirement
      → design element
        → code unit
          → test case
            → test result
              → defect
      ↑
   hazard / risk control measure
```

*Trace every level you have, and be honest about the ones you do not. A chain with a missing link is not a chain, and the missing link is exactly where an assessor will look.*

**Which levels apply here.** *List them. Delete the ones you do not use rather than leaving empty columns, which read as unfinished work.*

---

## The matrix

*One row per requirement. Every cell either has a link or a stated reason for being empty.*

| Req ID | Requirement | Source | Design element | Code | Test case | Result | Status |
|---|---|---|---|---|---|---|---|
| *SRS-014* | *Account locks after 5 failed attempts* | *StRS-007, SEC-3* | *DE-07* | *auth/lockout.go* | *TC-091* | *Pass, build 442* | *Verified* |
| *SRS-015* | *Lock notifies the account owner* | *StRS-007* | *DE-07* | | *TC-092* | *Not run* | *In progress* |

**Status** *is the column people read. Keep the vocabulary small and fixed: Not started, In design, Implemented, Verified, Deferred, Waived. Free text here defeats the purpose, because the value of the matrix is being able to count.*

**Empty cells are findings, not gaps in the paperwork.** *A requirement with no test case is a requirement nobody is going to check. A code unit with no requirement is work nobody asked for. The matrix earns its cost by making both countable.*

---

## Coverage summary

*The numbers a gate review actually needs. Generate them; do not count by hand.*

| Measure | Count | Target | Status |
|---|---|---|---|
| *Requirements in baseline* | | | |
| *With a design element* | | *100%* | |
| *With at least one test case* | | *100%* | |
| *Verified and passing* | | | |
| *Deferred, with an approved [change request](change-request.md)* | | | |
| *Waived, with a recorded justification* | | | |
| *Test cases tracing to no requirement* | | *0* | |
| *Code units tracing to no requirement* | | | |

*The last two rows are the backward direction, and they are the rows most matrices omit. A test that traces to nothing is either testing an undocumented requirement or testing nothing that matters, and both are worth knowing.*

---

## Waivers and deferrals

*Requirements not being met in this baseline, with a decision recorded against each. Never leave one implicit.*

*An implicit deferral is discovered at acceptance testing, when it is a defect. An explicit one is agreed in advance, when it is a decision.*

| Req ID | Deferred or waived | Justification | Approved by | Date | Revisit |
|---|---|---|---|---|---|
| | | | | | |

---

## Hazard and risk traceability

*Only if you have a safety or security risk analysis. Delete this section if you do not.*

*IEC 62304 clause 7.3.3 requires traceability from the hazardous situation to the software item, from the item to the specific software cause, from the cause to the risk control measure, and from the measure to its verification. Four links, and the fourth is the one commonly missing: a risk control with no verification is an intention.*

| Hazard | Software item | Software cause | Risk control | Verified by |
|---|---|---|---|---|
| | | | | |

---

## Where traceability is genuinely mandatory

*Delete whichever of these do not apply. Keep the one that does, with its clause, so a reader knows why this document exists.*

| Standard | What it requires | Applies at |
|---|---|---|
| *IEC 62304 §5.7.4* | *Traceability between software requirements and their tests or other verification* | *All safety classes, including Class A* |
| *IEC 62304 §7.3.3* | *Hazard traceability through to risk control verification* | *Classes B and C* |
| *IEC 62304 §8.2.4* | *Records linking change request, problem report and approval* | *All safety classes* |
| *DO-178C §5.5, §6.5* | *Bidirectional traceability across system requirements, high and low level requirements, code and verification. Trace data is itself a life cycle data item that must be verified* | *Rigour scales with DAL A to E* |
| *ISO 26262 Part 8 Cl. 6, Part 6* | *Safety requirement management and bidirectional traceability to test cases* | *Rigour scales with ASIL* |
| *FDA GPSV* | *Traceability analysis in every phase, "(and vice versa)" throughout* | *Medical device software* |
| *GAMP 5* | *URS to FS to DS to IQ/OQ/PQ* | *Computerised systems in life sciences* |

*Check the clause against the current edition before citing it in a submission. These are pointers, and standards move.*

---

## Notes on using this template

*Delete this section too.*

**Generate it. Do not maintain it.** This is the single most important line on the page. No standard mandates a spreadsheet; they mandate recorded, maintainable, bidirectional trace relationships. A hand-kept matrix is accurate on the day it is written and wrong within a month, because every requirement change, test rename and refactor invalidates a cell that nobody updates. A stale matrix is worse than none: it is an audit finding, and it is evidence you were not doing the thing you claimed.

The maintainable version is typed links in the tools where the artefacts already live: requirement identifiers in test case metadata, requirement identifiers in commit messages or code annotations, a report that assembles them. Then the matrix is a view, and views cannot go stale.

**Build it at the start.** Retrofitting traces onto a finished project is the most expensive mistake available in this group. The links have to be reconstructed from memory by people who were not there, which produces a document that is complete and untrue.

**Trace to identifiers, never to titles.** Titles get edited. If your matrix points at "the login requirement", it points at nothing the moment someone renames it.

**Retire identifiers, never reuse them.** A deleted requirement's ID stays dead. Reusing it silently reattaches every historical trace, test result and defect to a different requirement.

**One matrix per baseline.** Traceability against "the latest requirements" is not traceability, because it cannot be reproduced. Freeze it with the baseline it belongs to.

**Where this lives:** generated from your requirements and test management tools, published as a report at each [phase gate](phase-gate-review.md). If you have no tooling, the honest answer is to buy some or to reduce the number of trace levels until manual maintenance is genuinely feasible. Do not pretend a spreadsheet updated quarterly is a control.
