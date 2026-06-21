# Deprecation: {What is being removed}

*Also called: sunset plan, EOL (end-of-life) plan.*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **What** | *The endpoint, field, library version, service or behaviour. Be exact.* |
| **Replacement** | *What to use instead, with a link. "Nothing" is an answer, but say it.* |
| **Announced** | YYYY-MM-DD |
| **Removal date** | YYYY-MM-DD |
| **Owner** | |
| **Status** | Proposed \| Announced \| Migration \| Removed |

*Consumers have exactly three questions: what replaces this, by when must I move, and what breaks if I do not. The header answers two. Answer the third in the first paragraph.*

---

## Why

*Two or three sentences. The cost of keeping it, or the risk it carries.*

*Consumers absorb the cost of your deprecation, so they are entitled to the reason. "Deprecated" with no justification generates escalation, and rightly.*

---

## Who is affected

*The consumers you found, and how you found them. Access logs, API keys, dependency search, package downloads, support tickets.*

*Do this before announcing. It is the step that changes the plan, because the list is always longer than expected and usually contains someone you did not know existed.*

| Consumer | Usage | Contacted | Migrated |
|---|---|---|---|
| | *Requests per day, or version pinned* | | |

*State plainly how confident you are that the list is complete, and what could hide a consumer from you: a caller without an API key, an internal script, a customer integration you cannot see.*

---

## What breaks if you do nothing

*The failure mode after removal, in the consumer's terms. A 410 response, a build failure, a silently missing field.*

*Silent failures need a longer runway and louder announcements than loud ones, because nobody notices them in a test environment.*

---

## How to migrate

*The actual steps, with before and after. A worked example beats a paragraph of description.*

*Cover the awkward cases: what maps cleanly, what does not, and what has no equivalent. The cases with no equivalent are the ones that generate escalations, and hiding them does not prevent that.*

**Before**

```
```

**After**

```
```

**No direct equivalent.** *What is genuinely lost, and what to do instead.*

**Effort.** *An honest estimate. Consumers schedule against it.*

---

## Timeline

*Dates, with what happens at each. Work backwards from the removal date and check the runway is realistic for a team that has its own roadmap.*

| Date | What happens |
|---|---|
| *2025-03-01* | *Announced. Marked deprecated in the changelog and in the API response headers. Documentation updated.* |
| *2025-04-01* | *Deprecation warnings logged on every call. Consumers with usage contacted directly.* |
| *2025-07-01* | *Brownout: disabled for one hour, twice, at announced times.* |
| *2025-09-01* | *Removed.* |

*Give at least one full release cycle of the slowest consumer, and more when a team must schedule work against a roadmap set months ahead.*

*Brownouts are worth the trouble. A short, announced, deliberate outage before removal finds the consumers who ignored every notice, at a moment when you can still turn it back on.*

---

## How this is announced

*Every channel, with dates. The failure mode of deprecations is not insufficient notice; it is notice delivered where the affected people were not looking.*

- *Changelog, under `Deprecated`, at announcement and under `Removed` at removal*
- *In-band signal: response header, log warning, compiler or runtime warning*
- *Direct contact with each identified consumer*
- *Wherever your consumers already read: a mailing list, a channel, a release email, the developer portal*

*In-band signals reach people who read nothing. They are the only channel with that property, and they are the one most often skipped.*

---

## Rollback

*What you do if removal breaks something you did not anticipate. Whether it can be re-enabled, how quickly, and who decides.*

*Also: the point after which it cannot be undone, and what makes it so. Data written in a new format usually.*

---

## Exit criteria

*What must be true before removal proceeds. State it as a measurement, so the decision is not a judgement call on the day.*

- *Zero requests from unknown callers for 30 consecutive days*
- *All identified consumers confirmed migrated, or explicitly signed off on being broken*
- *Two brownouts completed with no unresolved reports*

*Then decide in advance what happens if the criteria are not met: slip the date, or remove anyway with a named person accountable. Deciding this beforehand is what stops a deprecation running for three years.*

---

## Notes on using this template

*Delete this section too.*

**Find the consumers before you announce.** The list changes the timeline, the channels and sometimes the decision. Announcing first and counting afterwards produces a plan you have to revise in public.

**Deprecation without a removal date is not deprecation.** It is a label. Nobody schedules work against "eventually", so nothing moves, and you keep both the old and the new path forever. Set the date at announcement even if you later move it.

**Say what is lost.** Every migration guide that claims full parity meets a consumer who depended on the one behaviour that changed. Naming it costs you nothing and buys the goodwill you will need when the date arrives.

**Where this lives:** in the repository as the durable record, announced through whatever your consumers already read. Mark it in the [changelog](changelog.md) under `Deprecated` at announcement and under `Removed` at removal, so anyone scanning versions sees both ends.

---

## Related documents

- [`changelog.md`](changelog.md). Where the deprecation is marked at announcement and again at removal
- [`release-notes.md`](release-notes.md). How the same removal is explained to a non-technical user
- [`interface-control-document.md`](interface-control-document.md). The agreement this plan is retiring a version of
- [`data-model.md`](data-model.md). The entity shape this plan may be retiring, if consumers depend on it
