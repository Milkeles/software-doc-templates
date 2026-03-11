# Troubleshooting Guide

> Organised by what went wrong, not by what the reader was trying to do.
>
> **Why it needs its own template.** Diátaxis has no clean home for it. A how-to guide starts from a goal the reader already knows; a troubleshooting reader knows only a symptom. Reference describes the working system, not the broken one. The Good Docs Project ships `troubleshooting` as a separate template, which is a practical acknowledgement of the same gap.
>
> **The organising principle.** Entries are indexed by **what the reader sees**, in the exact words they see it. Not by subsystem, not by cause, not by severity. A reader with an error message will paste that message into a search box, and the document either matches it or does not exist.
>
> **Where it lives.** Docs-as-code, published to the docs site and indexed by search. If your product emits error codes, link each code from the error output straight to its entry.
>
> **Delete this block before publishing.**

---

## 1. How to find your problem

Open with a way in. For a short guide, a symptom list. For a long one, an error-code table.

| You see | Section |
|---|---|
| `ERR_AUTH_EXPIRED` | [Authentication expires immediately](#) |
| `409 in_use` when rotating a key | [Key rotation blocked by a live deployment](#) |
| Requests succeed locally, time out in staging | [Timeouts in one environment only](#) |

The third row matters. **Not every symptom has an error code.** Behavioural symptoms need entries too, and they are the ones readers give up on first.

---

## 2. Entry format

Same five parts, every time. Consistency is what makes the page scannable under stress.

> ### Authentication expires immediately after sign-in
>
> **Symptom.** Sign-in succeeds, then the next request returns `401` with `ERR_AUTH_EXPIRED`. Reproduces on every request, not intermittently.
>
> **Confirm it.** Run `acme auth debug`. The reported `token_issued_at` is later than `server_time`.
>
> **Cause.** The client clock is ahead of the server. Tokens are rejected as issued in the future.
>
> **Fix.** Enable NTP on the client host. On Ubuntu: `sudo timedatectl set-ntp true`. Sign in again.
>
> **If that does not fix it.** Skew below 30 seconds is tolerated, so a working clock rules this out. See [token audience mismatch](#).

**Symptom** in the reader's words, including the literal message.
**Confirm it** so the reader distinguishes this from the three symptoms that look identical.
**Cause** in one or two sentences. Enough to make the fix make sense.
**Fix** as concrete steps.
**If that does not fix it** pointing onward, so the entry is never a dead end.

The confirm step is the one most often skipped and the one that does most of the work. Without it, readers apply the wrong fix, break something else, and lose trust in the whole document.

---

## 3. What to include

**Only failures that have actually happened.** Source this document from support tickets, incident reviews, and repeated questions. An imagined failure mode wastes the reader's time and crowds out the real ones.

Keep a note of frequency. The commonest three go first regardless of how interesting the others are.

---

## 4. Getting more information

A short section on diagnosis in general, so a reader whose symptom is not listed is not stranded.

- Where the logs are, and how to raise the level.
- The one diagnostic command worth running first, and what its output means.
- How to tell a client problem from a server problem.
- What to collect before opening a support ticket.

**This section is what makes the document useful for the failures you did not anticipate**, which is most of them.

---

## 5. Where to get help

The support channel, the issue tracker, and what to include in a report. Link the [bug report template](#) if you have one.

Say what you need: version, platform, exact error text, steps to reproduce, and the diagnostic output from section 4. Asking here saves a round trip on every ticket.

---

## Keeping it alive

A troubleshooting guide is the one document with a natural, cheap source of truth: your support queue.

- Add an entry the second time a problem is reported. Once is an accident.
- When you fix the underlying bug, mark the entry with the version that fixed it rather than deleting it. Readers on older versions still need it.
- Delete entries whose cause no longer exists in any supported version.
- Review after each release.

**Prefer fixing the product.** A troubleshooting entry is a permanent workaround for a temporary decision. If an entry gets read a thousand times a month, the error message is wrong, the default is wrong, or the validation is missing. Documenting a confusing error is second best to making it unconfusing.

---

## Common failures in this document

- **Organised by subsystem.** The reader does not know which subsystem failed. That is why they are here.
- **Symptoms paraphrased.** The literal error string is the search term. Print it exactly.
- **No confirmation step.** Readers apply fixes for problems they do not have.
- **Cause without fix.** Explains the failure and leaves the reader stuck.
- **Dead ends.** No onward link when the fix does not work.
- **Written from imagination.** Long, plausible, and matching nothing anyone has hit.
- **Never pruned.** Fixed bugs stay listed and the real entries get buried.

---

## Related documents

- [`how-to-guide.md`](how-to-guide.md). For readers who know their goal
- [`installation-guide.md`](installation-guide.md). Carries its own install-time failures
- [`reference-page.md`](reference-page.md). Every error code should be documented there and linked from here
- [`../foundations/runbook.md`](../foundations/runbook.md). The internal equivalent, for operators
- [`../foundations/incident-postmortem.md`](../foundations/incident-postmortem.md). A recurring symptom here is a candidate for a real fix
