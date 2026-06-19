# Postmortem: {What broke, in the words a user would use}

*Italic text is guidance. Delete it as you fill each section in.*

*Title by user-visible effect, not by cause. "Checkout unavailable for 43 minutes" beats "Redis connection pool exhaustion". People search by what they saw.*

| | |
|---|---|
| **Incident** | *ID and link to the incident channel or ticket.* |
| **Date** | YYYY-MM-DD |
| **Duration** | *Detection to resolution, and user impact window if different.* |
| **Severity** | |
| **Authors** | |
| **Status** | Draft \| In review \| Reviewed \| Closed |
| **Responders** | *Everyone who worked it. Credit, not blame.* |

---

## Summary

*Five sentences at most: what users experienced, for how long, what caused it, what fixed it, what stops it recurring.*

*Most people read only this. Write it so that is enough. Write it last.*

> **Example.** Checkout returned errors for 43 minutes on 12 March. A config change reduced the connection pool to 10 while normal load needs 60. Reverting the change restored service. Pool size is now validated against measured load in CI, and the deploy pipeline surfaces config diffs in the change summary.

---

## Impact

*Quantified, from the user's side. Requests failed, orders lost, customers affected, revenue, support tickets, SLO error budget consumed.*

*Use real numbers or say you do not have them. "Minimal impact" is not a measurement, and it is usually wrong.*

*Also record what did not break. Scope is as informative as damage.*

---

## Timeline

*What happened and, more importantly, what was known at each point. Timestamps in one timezone, stated.*

*Record the state of knowledge, not the state of the world. "14:12 believed the database was the cause, began failover" is the useful entry. "14:12 the database was fine" is hindsight, and it makes the responders look careless for reasons they could not have known.*

*Include: the change or event that started it, the first signal, first human response, each hypothesis and what it was based on, each action and its effect, the point of understanding, resolution.*

*Dead ends belong here. A hypothesis that took twenty minutes to rule out is a signal about your observability, and deleting it hides that.*

| Time | What happened | What responders knew |
|---|---|---|
| *13:47* | *Config change deployed to production* | *Routine deploy, no signal yet* |
| *13:52* | *Error rate alert fires* | *Errors rising, cause unknown* |
| | | |

---

## Trigger

*The specific event that started this. One or two lines. Kept separate from the factors below on purpose: the trigger is what made it happen now, not why it was possible.*

---

## Contributing factors

*Everything that had to be true for this incident to happen and to last as long as it did. Technical, procedural and organisational.*

*Prefer "how" questions to "why" questions. "How was it possible to set a pool size below measured demand?" produces a system answer. "Why did they set it wrong?" produces a person, and stops the analysis one step early.*

*Cover, where they apply:*

- *The condition that made the failure possible*
- *What allowed it to reach production*
- *What delayed detection*
- *What delayed diagnosis*
- *What delayed recovery*

*If a factor is "a person made a mistake", keep going. The question is what made that mistake easy to make and hard to catch. Everyone involved was doing what looked reasonable with the information they had; a factor that does not respect that is not finished.*

**On the words.** *This template uses "contributing factors" rather than "root cause". PagerDuty made the same change, arguing that incidents in complex systems have several causes and that treating one as the root leads to shallow fixes. Google's template keeps "root causes", plural. If your organisation prefers the older phrase, keep it, but keep the plural and keep asking how.*

---

## What went well

*Genuinely. Detection that worked, a runbook that held up, a rollback that was fast, someone who escalated early.*

*Not morale filler. These are the controls you already paid for, and knowing which ones worked tells you where to invest next.*

---

## What went badly

*The controls that failed or were missing. An alert that fired late or not at all, a dashboard that misled, a runbook that was wrong, a dependency nobody knew existed.*

---

## Where we got lucky

*What would have made this much worse but did not happen. Off-peak hours, an engineer who happened to be online, a second failure that did not coincide.*

*This section finds the incidents you have not had yet. Each piece of luck is a control you are relying on without knowing it.*

---

## Action items

*What changes, who owns it, and the tracking number. Nothing without all three.*

*Keep the work in your issue tracker and this table as an index. Action items left in a document body are not scheduled, and unscheduled work does not happen.*

*Prefer changes that remove the possibility over changes that ask people to be careful. "Add a validation rule" survives turnover; "remind the team to check" does not. Sort so the highest-leverage item is first.*

| Action | Type | Owner | Priority | Ticket |
|---|---|---|---|---|
| | *Prevent \| Detect \| Mitigate \| Process* | | | |

*Each action should be measurable: someone must be able to say whether it is done. "Improve monitoring" fails that test; "alert when pool utilisation exceeds 80% for 5 minutes" passes.*

---

## Supporting detail

*Graphs, log extracts, queries, links to the incident channel. Anything a reader might want to check for themselves. Keep it out of the narrative above.*

---

## Notes on using this template

*Delete this section too.*

**Blameless means the analysis assumes people acted reasonably given what they knew.** It does not mean avoiding names or pretending nothing went wrong. Name people as responders and authors; explain actions by the information available at the time. The moment a postmortem can damage someone's standing, the honest detail stops arriving, and you lose the only data that makes the exercise worth running.

**Decide the triggers in advance.** User-visible degradation past a stated threshold, any data loss, any manual intervention such as a rollback or traffic reroute, resolution beyond a set duration, or a monitoring failure. Anyone may also request one. Without agreed triggers, every postmortem starts as a negotiation about whether to hold one.

**Publish within a week, and publish widely.** The value is in the reading. A postmortem seen only by the team that had the incident teaches only that team, and every other team keeps its version of the same gap.

**Review it with people who were not there.** They ask the questions the responders have stopped being able to see.

**Where this lives:** a wiki or incident management tool, not the repository. This is a dated record with a lifecycle, a review meeting, comment threads and a company-wide readership. Git versions text; it does not support discussion or discovery. Keep them all in one searchable place so the next responder can find the last time this happened.

---

## Related documents

- [`runbook.md`](runbook.md). Where an action item becomes a new or fixed step
- [`architecture-decision-record.md`](architecture-decision-record.md). Where an action item goes if the fix overturns a decision
- [`test-strategy.md`](test-strategy.md). Where an action item goes if the gap was coverage
- [`bug-report.md`](bug-report.md). What this document becomes when the failure stayed contained instead of reaching users
