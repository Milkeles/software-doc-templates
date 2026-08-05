# How-To Guide

> A recipe. The reader already knows how to cook.
>
> **Also called:** task topic (the DITA standard's term), procedure, or how-to article.
>
> **What it is for.** Getting a competent user to a result. Procida: "A how-to guide directs the user's work" and "serves the work of the already-competent user, whom you can assume to know what they want to do, and to be able to follow your instructions correctly."
>
> **The difference from a tutorial, in one line.** A tutorial is written for someone at study; a how-to guide for someone at work. The tutorial controls the environment and takes responsibility for the outcome. The how-to guide meets the reader in the real world, where "the user has responsibility for getting themselves in and out of trouble".
>
> **Why most documentation should be this.** People arrive at documentation mid-task, with a goal already in mind, unwilling to stop and learn. Carroll and Rosson named this the paradox of the active user: a *production bias* that pushes people to act rather than read, and an *assimilation bias* that makes them interpret the new through the familiar. How-to guides are the format that survives both.
>
> **Where it lives.** Docs-as-code, published to the docs site.
>
> **Delete this block before publishing.**

---

## 1. Title

Start with "How to" and name the goal in the reader's words.

> Good: "How to rotate a signing key"
> Bad: "Key rotation" · "Working with keys" · "Key management overview"

The title is the whole search interface. A reader typing "rotate key" into a search box must land here, and the noun-phrase versions above do not match how anyone describes their problem.

**One goal per guide.** "How to configure authentication" is a chapter, not a guide. Split it: how to add an OIDC provider, how to require MFA, how to set session lifetime.

---

## 2. Overview

One or two sentences on the situation this addresses, and if there is a near neighbour, which one the reader wants.

> Use this to replace a key on a schedule. To replace one you believe is compromised, see [how to revoke a compromised key](#), which does not wait for the grace period.

This costs two lines and prevents the reader from doing the almost-right thing.

---

## 3. Before you start

What must be true. Permissions, state, tools, access.

Keep it to what actually blocks the task. A how-to guide that opens with a full environment setup has absorbed the installation guide and should link it instead.

---

## 4. Steps

Numbered, imperative, one action each.

**Assume competence.** No explanation of what a key is. No teaching the CLI. If the reader needs that, they need the [tutorial](tutorial.md) or the [explanation](explanation.md), and a link is the correct response.

**Handle the unexpected.** This is where a how-to guide differs most from a tutorial. Procida: "The how-to guide must prepare for the unexpected, alerting the user to its possibility." The reader is on their own machine with their own state, and things will not be clean.

> 4. Run `keyctl rotate --id <key-id>`.
>
>    If the key is in use by a running deployment, the command exits with `409 in_use`. Drain the deployment first, or pass `--force` to accept a short window of failed requests.

**Make it adaptable.** Procida again: "A how-to guide needs to be adaptable to real-world use-cases. One that is useless for any purpose except *exactly* the narrow one you have addressed is rarely valuable." Use placeholders, name the variable parts, and say what changes if the reader's situation differs.

**Do not pin to a contrived example the reader must mentally translate.** Show `<key-id>`, not `demo-key-1`, unless the literal value matters.

---

## 5. Verify

How the reader confirms it worked. A command, an expected response, a place in the interface.

> ```
> keyctl list --id <key-id>
> ```
> The new key shows `state: active`. The previous key shows `state: retiring` with an expiry timestamp.

**A how-to guide with no verification step is not finished.** The reader is at work and needs to know whether to move on. Without this, the guide ends in ambiguity at precisely the moment certainty matters.

---

## 6. Troubleshooting
Two or three of the likeliest failures, each with a cause and a fix. Not an exhaustive list; link the [troubleshooting guide](troubleshooting-guide.md) for that.

The test for what belongs here: it is a failure caused by *this procedure*, not a general symptom of the system.

---

## 7. Related tasks

Links to the neighbouring guides. What comes before, what comes after, what the reader might have confused this with.

---

## Common failures in this document

- **Titled as a noun phrase.** Unfindable by anyone searching for their actual problem.
- **Teaching mid-procedure.** Turns a five-minute task into a lecture the reader skims and misreads.
- **Too narrow to reuse.** Solves exactly one contrived case and nothing adjacent.
- **No verification.** The reader cannot tell whether they are done.
- **No failure modes.** The guide assumes a clean environment. Real environments are not clean.
- **Several goals in one guide.** The reader scrolls past four irrelevant sections to reach theirs.
- **Actually a tutorial.** If it assumes no prior competence and controls the environment, it belongs in [`tutorial.md`](tutorial.md).

---

## Related documents

- [`tutorial.md`](tutorial.md). For readers who do not yet have the competence this assumes
- [`reference-page.md`](reference-page.md). Link every flag and parameter rather than describing it here
- [`explanation.md`](explanation.md). Where the reasoning behind the procedure belongs
- [`troubleshooting-guide.md`](troubleshooting-guide.md). Symptom-first, for readers who do not know which task they need
- [`../foundations/runbook.md`](../foundations/runbook.md). The same shape, aimed at operators during an incident
