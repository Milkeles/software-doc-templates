# Threat model: {Feature or system}

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Scope** | *The one feature, flow or service this covers. Not the whole platform.* |
| **Participants** | *Who was in the session. Include the engineers who build it.* |
| **Date** | YYYY-MM-DD |
| **Review trigger** | *What obliges a revisit: a new data flow, a new external caller, a change of trust boundary.* |

*The whole activity reduces to four questions: what are we working on, what can go wrong, what are we going to do about it, and did we do a good enough job. The sections below are those four in order.*

*Aim for one page per feature, done at design time, redone when the design changes. A forty-page model produced once is worth less than four one-page models produced as the system grew.*

---

## 1. What are we working on

*The system under analysis, at the level of data flow. What components exist, what data moves between them, and where trust changes.*

**Trust boundaries.** *Every point where data crosses from something you control less into something you control more, or into a different privilege level. The internet to your edge, your service to a third party, an unprivileged user to an admin action, tenant to tenant.*

*Boundaries are where threats concentrate. If a diagram has none marked, the analysis has not started.*

**Assets.** *What an attacker would want, and what you would most regret losing. Credentials, personal data, money, availability, integrity of records.*

| Asset | Where it lives | Why it matters |
|---|---|---|
| | | |

**Assumptions.** *What you are taking as given: the platform is patched, the network is segmented, the identity provider is trusted, the operations team is not hostile.*

*Write these down. Today's assumption is next year's vulnerability, and an unrecorded one cannot be rechecked.*

*Diagram it, roughly. A whiteboard photo with boundaries drawn on it is enough. Waiting for a complete and accurate diagram before starting the analysis is the most common way threat modelling gets abandoned.*

---

## 2. What can go wrong

*Threats, generated systematically rather than by imagination. STRIDE is the usual generator: walk each element or data flow and ask the six questions.*

| Category | The question | Property it breaks |
|---|---|---|
| **S**poofing | *Can someone claim to be another party?* | *Authentication* |
| **T**ampering | *Can data be modified in transit or at rest?* | *Integrity* |
| **R**epudiation | *Can someone deny doing it, and could we prove otherwise?* | *Non-repudiation* |
| **I**nformation disclosure | *Can data reach someone who should not see it?* | *Confidentiality* |
| **D**enial of service | *Can someone make this unavailable?* | *Availability* |
| **E**levation of privilege | *Can someone do something they are not permitted to?* | *Authorisation* |

*Record each threat as a short scenario, not a category name. "Spoofing" is not a threat. "A caller replays a captured webhook signature to post a second refund" is, and it can be tested.*

*Include the abuse cases specific to your domain: the same user opening two sessions, a tenant reading another tenant's data, a partial failure leaving money in two places at once.*

| # | Threat scenario | Category | Existing control | Residual risk |
|---|---|---|---|---|
| 1 | | | | *High \| Medium \| Low* |

*Rate residual risk by impact and likelihood, however crudely. The purpose of the rating is only to sort the next section.*

---

## 3. What are we going to do about it

*One decision per threat. Four options, and three of them are legitimate answers.*

- **Mitigate.** *Add a control that reduces it.*
- **Eliminate.** *Remove the feature or the data that creates it. Often the cheapest answer and the least considered.*
- **Transfer.** *Move it to someone equipped to hold it: a payment processor, an identity provider, an insurer.*
- **Accept.** *Decide it is tolerable. Requires a named person who accepted it and a date.*

| # | Decision | Action | Owner | Ticket | Accepted by |
|---|---|---|---|---|---|
| 1 | *Mitigate* | | | | |
| 2 | *Accept* | *No action* | | | *Name, date* |

*Every row needs an owner and a ticket, or it is a wish. This table is where threat models most often stop being useful: enumerating threats feels like progress and changes nothing.*

---

## 4. Did we do a good enough job

*A short honest assessment, written at the end of the session.*

- *What did we not cover, and why*
- *What are we least confident about*
- *What would change our answers*
- *When do we look at this again*

*"Good enough" is the standard, deliberately. A model that must be complete before it counts will never be finished.*

---

## Notes on using this template

*Delete this section too.*

**Four failure modes to watch for, named by the Threat Modeling Manifesto.**

- *Hero Threat Modeler:* one security specialist does this for everyone. The result is a document the engineers do not believe and do not act on. The people building it must be in the room.
- *Admiration for the Problem:* threats are enumerated in loving detail and nothing is decided. Section 3 is the antidote and is not optional.
- *Perfect Representation:* the diagram must be exhaustive before analysis can begin. Several rough models beat one perfect one.
- *Tendency to Overfocus:* the session disappears into one interesting attack. Timebox it and move on.

**Do it at design time.** A threat model produced after the code ships can only find problems that are now expensive to fix. Attach it to the [design document](technical-design-document.md) while the design can still change cheaply.

**STRIDE is a generator, not a taxonomy to complete.** Carnegie Mellon's SEI, surveying twelve methods, describes it as the most mature. It is well suited to finding technical threats against a data flow. For privacy harms, LINDDUN asks better questions. For business risk weighted by attacker motivation, PASTA does. Use the one that matches what you are afraid of.

**Sixty minutes with the right people beats a week of writing.** The Manifesto values dialogue over documents. This file records a conversation; it does not substitute for one.

**Where this lives:** in the repository, beside the design it covers, so a design change and its threat model move in one commit. Restrict the path if the content is sensitive. Keep the accepted-risk rows findable, because an auditor will ask who accepted what and when.

---

## Related documents

- [`technical-design-document.md`](technical-design-document.md). Where this model should attach, while the design can still change cheaply
- [`configuration-management-plan.md`](configuration-management-plan.md). Why supply chain and access control matter there, answered here
- [`interface-control-document.md`](interface-control-document.md). Where a trust boundary named here usually runs
