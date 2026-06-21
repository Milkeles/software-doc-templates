# Rollout Plan

> One page, written before a risky change reaches users, saying how it gets there, how you will know it is going wrong, and how you turn it off.
>
> **Also called:** a launch plan, or a release plan.
>
> **Short-lived by design.** A rollout plan is finished when the flag is removed. It is not a document you maintain. If you find yourself updating one that is six months old, the rollout stalled and that is the real problem.
>
> **When to write one.** Not for every change. Write one when the change is hard to reverse, touches money or data, changes something users have learned, or you genuinely do not know how it will behave under real traffic. Most deployments need none of this.
>
> **Where it lives.** Wherever the change is tracked: the ticket, the pull request, or a wiki page linked from both. One per rollout.
>
> **Delete this block before publishing.**

---

## 1. What is changing

Two sentences, written for someone paged at 3am who has never seen this work.

> Replacing the checkout address form with a new component that autocompletes from a postcode lookup service. Users see a different form; the submitted data shape is unchanged.

State the blast radius plainly: which users, which pages, which downstream systems.

---

## 2. Why gradually

One sentence. If you cannot write it, you may not need a staged rollout, and staging a change that does not need it costs real time.

The honest general argument is narrower than it is usually stated. Gradual exposure **limits blast radius by construction**: if 1% of users see a broken change, 99% do not. That is a property of the mechanism, not an empirical claim, and it holds regardless of what any study says.

**Claims that progressive delivery reduces incident rates or improves recovery time do not have a locatable primary source.** The figures circulating trace back to vendor blogs and to attributions that cannot be verified against the reports they cite. Argue from blast radius, which is true by construction, rather than from statistics you cannot support.

---

## 3. Stages

The core of the plan. Each stage names who is exposed, for how long, and what has to be true before the next one.

| Stage | Audience | Duration | Proceed when |
|---|---|---|---|
| 1 | Internal staff only | 2 days | No errors reported, form submits end to end |
| 2 | 1% of logged-in users | 3 days | Checkout completion rate within 1 point of control, no new error signatures |
| 3 | 10% | 3 days | Same, plus INP on the checkout page not worse |
| 4 | 50% | 3 days | Same |
| 5 | 100% | | Same, held for 7 days before flag removal |

Three rules make the table useful rather than decorative:

**Every gate is a number, not a feeling.** "No issues" is not a gate; everyone has issues and nobody agrees which count. "Checkout completion rate within 1 point of control" is checkable by someone who was not in the planning meeting.

**Every stage has a minimum duration.** Ramping in a morning means you only see morning traffic on the devices that browse in the morning. Weekly cycles are real and a stage shorter than a day cannot see them.

**Say who decides.** A named role, or the ramp stalls at the first stage where the numbers are ambiguous, which is most of them.

---

## 4. How users are selected

More consequential than it looks, and the part that invalidates the most rollouts.

**Sticky assignment.** A user who is in must stay in. A user who sees the new checkout on Monday and the old one on Tuesday will report a bug you cannot reproduce, and any comparison you run is meaningless.

**Bucketing key.** User ID, session, account, or device. State which. Session-level assignment on a multi-device product means the same person sees both.

**Confounded segments.** Ramping to "internal staff" then "1% of users" is fine. Ramping to "1% of users" where the sampling is by geography, or by anything correlated with behaviour, means stage 2's numbers do not predict stage 5's. Say what the selection is correlated with, or confirm it is random.

**Overrides.** How support puts a specific complaining customer back on the old path without a deploy. Without this, the first serious complaint becomes an emergency rollback of the whole rollout.

---

## 5. What you are watching

Name the metrics, the dashboards, and the alert thresholds. Before the ramp starts, not during.

| Signal | Where | Alert if |
|---|---|---|
| Checkout completion rate | Product analytics dashboard | Treatment more than 1 point below control |
| Error rate, checkout routes | Error tracker, filtered by flag value | Any new error signature, or rate above 0.5% |
| INP, checkout page | RUM | 75th percentile above 200 ms |
| Support tickets mentioning checkout | Support queue tag | Any increase over baseline |

**Split every metric by flag value.** An aggregate metric at 1% exposure cannot move enough to detect anything. If your tooling cannot break down by flag, that limitation is worth knowing before you start rather than during.

**Include at least one qualitative channel.** Support tickets and session recordings catch the failures no metric was defined for, which is most of the ones that matter.

---

## 6. Rollback

The section that determines whether the plan was worth writing.

**How.** The exact action. "Set `checkout-address-v2` to 0% in the flag console." A named action someone can take without understanding the change.

**How long it takes to take effect.** Flag evaluation is not always instant, and cached or server-rendered pages can serve the old decision for minutes. Know the number before you need it.

**Who can do it.** Ideally anyone on call, with no approval. A rollback that needs a decision meeting is not a rollback.

**What does not roll back.** The part people forget and the reason rollouts turn into incidents. Database migrations, data written in the new shape, emails sent, payments taken, third-party state changed. **List these explicitly.** If the change writes data the old code cannot read, the flag does not save you and the plan needs a different design: expand the schema first, migrate, then contract.

> The flag reverts the UI. Addresses saved through the new form are stored in the same shape and remain valid. No migration is involved, so rollback is complete.

If rollback is not complete, say so at the top of the plan, not here.

---

## 7. Cleanup

The step that is skipped, and the reason codebases accumulate dead flags that nobody dares remove.

Set it as a commitment with a date and an owner:

> Flag removed and the old component deleted by 2026-04-15. Owner: [name]. Ticket: [link].

Two flags in a codebase is four code paths, and nobody tests all four. **A flag left in place after the rollout succeeded is technical debt with a specific, known removal cost**, which makes it the cheapest kind to pay off and the easiest to forget.

If your flag platform reports flag age, use it. OpenFeature, a CNCF Incubating project since 21 November 2023, provides a vendor-neutral SDK interface if you want the option of changing platform later without rewriting call sites.

---

## 8. Communication

Who needs to know, and when.

- **Support**, before stage 2. They will receive the tickets and need to know the flag exists and how to check which variant a customer is on.
- **The wider team**, at start and at 100%.
- **Users**, only if the change alters something they have learned. A silent UI change to a workflow people use daily generates support load in proportion to how confident you were that it was an improvement.

---

## Common failures in this document

- **Written after the ramp started.** Becomes a record rather than a plan, and the gates get set to whatever the numbers happened to be.
- **Gates that are opinions.** "Looks fine" ramps changes that were not fine.
- **No irreversible-effects list.** The flag flips back, the data does not, and the rollout becomes an incident.
- **Non-sticky assignment.** Produces unreproducible bug reports and meaningless comparisons.
- **Metrics not split by flag.** Nothing detectable at low exposure, so early stages tell you nothing.
- **No cleanup date.** The flag outlives the person who added it.

---

## Related documents

- [`api-design-guide.md`](api-design-guide.md). If the rollout changes an API contract, the guide's versioning and deprecation rules apply and a flag does not exempt you
- [`../../general-swe/foundations/incident-postmortem.md`](../../general-swe/foundations/incident-postmortem.md). Where this goes if the rollback list was incomplete
- [`../../general-swe/foundations/deprecation-plan.md`](../../general-swe/foundations/deprecation-plan.md). For removing something rather than replacing it
