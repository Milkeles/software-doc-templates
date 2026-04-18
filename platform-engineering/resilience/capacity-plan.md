# Capacity plan: {System or service}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Covers** | |
| **Owner** | |
| **Forecast horizon** | *How far ahead this plan projects* |
| **Last revisited** | YYYY-MM-DD |

*Industry guidance on the right amount of headroom above peak measured usage genuinely disagrees, from roughly 10% to 50% depending on the source and the risk tolerance assumed. There is no single correct number to borrow here. State your own target and the reasoning behind it, informed by how bursty your actual demand is and how fast your team can react, rather than citing someone else's rule of thumb as if it were a standard.*

---

## 1. Current state

| Resource | Current peak usage | Current capacity | Headroom |
|---|---|---|---|
| | | | |

*Based on actual historical data and real observed performance, not on assumption. A capacity plan built on what the system was specified to handle, rather than what it has actually handled under real load, is measuring the wrong thing.*

---

## 2. Forecast

| Resource | Expected demand at horizon | Basis for forecast | Capacity needed |
|---|---|---|---|
| | | *Growth trend, known upcoming launch, seasonal pattern* | |

---

## 3. Headroom target and reasoning

| | |
|---|---|
| **Target headroom** | *Your own number, stated as a percentage above peak* |
| **Why this number** | *Tied to your own burstiness and reaction time, not a borrowed industry rule of thumb* |
| **Action threshold** | *Utilization level that triggers scaling action, stated ahead of time rather than decided live* |

---

## 4. Gap and plan to close it

| Resource | Gap (forecast demand minus current capacity) | Action | By when |
|---|---|---|---|
| | | | |

---

## Notes on using this template

*Delete this section too.*

**Do not borrow a headroom percentage as if it were a standard.** Sources disagree substantially, and the right number depends on facts specific to your system: how fast demand can spike, and how fast your team can actually react. State your own reasoning instead of citing a number you found in a blog post.

**Revisit this on a schedule, not when it becomes urgent.** A forecast checked against actual outcomes on a set cadence catches drift early. A forecast written once and left alone is a snapshot of a moment that has already passed.

**Base current state on real observed behavior.** What a system is specified or provisioned to handle and what it has actually handled under real, bursty, production load are frequently different numbers, and the second one is the one that matters here.

**Where this lives:** wiki or the tracker already holding the forecast, revisited on a set cadence. This is a living document; keep the update cost low enough that revisiting it actually happens.

---

## Related documents

- [`disaster-recovery-plan.md`](disaster-recovery-plan.md). Whether an alternate site has enough capacity to absorb full load during a failover
- [`../reliability/slo-document.md`](../reliability/slo-document.md). The reliability target this system's capacity has to sustain under load
