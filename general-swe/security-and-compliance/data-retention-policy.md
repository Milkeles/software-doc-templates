# Data Retention Policy

> How long you keep each thing, and why that number and not another.
>
> **The GDPR contains no retention periods.** Not one. Article 5(1)(e) says data must be "kept in a form which permits identification of data subjects for no longer than is necessary for the purposes for which the personal data are processed". Any template that ships with default periods has invented them. The numbers in your policy come from your purposes and from sector law, and you have to derive them.
>
> **The wording gives you a second option.** The obligation is on keeping data *in a form which permits identification*. Anonymise the record and the clock stops without deleting the row. That is the escape hatch for analytics, and it is worth designing for.
>
> **Why this exists as a document at all.** Article 5(2) accountability: you must be able to demonstrate compliance. A retention rule that lives only in a cron job cannot be demonstrated, and nobody can tell whether it is still right.
>
> **Where it lives.** Wiki, owned jointly by Legal and Engineering. The enforcement lives in code; the decision does not.
>
> **Delete this block before publishing.**

---

## 1. How a period gets decided

Work in this order for every category of data. Record the answer, because the reasoning is the compliance artefact.

1. **What purpose is this data serving?** Take it from the [ROPA](record-of-processing-activities.md).
2. **When does that purpose end?** Account closure, contract end, ticket resolution, the last transaction.
3. **Does a law require you to keep it longer?** Tax, accounting, employment, sector regulation.
4. **Does a limitation period apply?** How long can someone still sue, and do you need the record to defend yourself.
5. **Take the longest, and say which rule produced it.**

A period without a stated reason is unmaintainable. Nobody can safely shorten it later because nobody knows what it was protecting.

---

## 2. The schedule

The whole document, really. Everything else supports it.

| Category | Trigger | Period | Basis | Then what | Owner |
|---|---|---|---|---|---|
| Account and profile | Account closure | 30 days | Purpose ends. Grace period for accidental deletion | Hard delete | Platform |
| Order and invoice records | End of financial year | 6 years | Accounting and tax law | Hard delete | Finance |
| Support tickets | Ticket closure | 24 months | Recurrence context, dispute defence | Hard delete | Support |
| Application logs with IPs and user IDs | Write | 12 months | Security investigation, PCI DSS 10.5.1 where in scope | Hard delete | Platform |
| Product analytics | Collection | 14 months identifiable | Year-on-year comparison | **Anonymise**, then keep indefinitely | Data |
| Unsuccessful job applications | Decision | 6 months | Discrimination claim window | Hard delete | People |
| Backups | Creation | 35 days | Recovery objective | Expire the whole snapshot | Platform |

Four columns carry the weight, and they are the ones most often missing:

**Trigger, not just period.** "Two years" is meaningless without saying two years from what. Most retention bugs are trigger bugs.

**Basis.** Which of the five steps in section 1 produced this number.

**Then what.** Deletion and anonymisation are different outcomes with different engineering.

**Owner.** The person who answers when the number is challenged.

---

## 3. Backups

The part that quietly makes the rest untrue.

You cannot selectively delete one person's data from an immutable snapshot without restoring and rewriting it. The accepted approach is to let backups age out on their own schedule and to state plainly that erasure requests are executed against live systems immediately and against backups by expiry.

Two conditions make that defensible, and you should write both down:

- The backup retention window is **short and fixed**, so "by expiry" is a bounded promise.
- A restored backup is **reconciled against the deletion log** before it returns to service, so a restore does not resurrect deleted records.

Without the second condition, a restore silently undoes every erasure since the snapshot.

---

## 4. Where retention conflicts with itself

Real schedules contain contradictions. Name them rather than letting each team resolve them privately.

**Logs against storage limitation.** PCI DSS v4.0.1 requirement 10.5.1 requires audit log history for at least 12 months, with at least the most recent three months immediately available. Those logs contain IP addresses and user identifiers, which are personal data. The requirement to keep and the requirement to minimise both apply. The usual resolution is to scope the 12-month rule to the cardholder data environment only and keep everything else shorter, but write down which resolution you chose.

**Legal hold against erasure.** When litigation is reasonably anticipated, evidence must be preserved. The GDPR recognises the purpose: Article 17(3)(e) exempts erasure needed "for the establishment, exercise or defence of legal claims", and Articles 9(2)(f) and 21(1) point the same way. The conflict is therefore not whether you may hold, but **how wide and how long**. A hold that covers whole systems indefinitely is not supported by those provisions.

We found no EDPB guidance resolving the scope question. State the tension in your policy, keep holds narrow and dated, and log every one.

**Sector law against everything.** Examples whose existence is well established, though you should read the statute rather than a summary table: UK Companies Act 2006 s.388 (accounting records, three years for a private company and six for a public one), HMRC guidance requiring six years for tax records, HIPAA §164.316(b)(2)(i) requiring six years for policy documentation, and EU anti-money-laundering rules at around five years. None of these are GDPR periods; they are the external constraints GDPR tells you to respect.

---

## 5. Enforcement

A policy nobody enforces is worse than none, because it documents an intention you are demonstrably failing.

- **Every row in section 2 maps to a mechanism.** A TTL, a scheduled job, a lifecycle rule on the bucket. Name it in the row or in a companion table.
- **Alert on the job, not on the data.** A deletion job that silently stops failing open is the common failure.
- **Measure the oldest record per category** and publish it. If the oldest support ticket is four years old, the 24-month rule is fiction.
- **Test erasure end to end.** Submit a request against a test account and check every store, including the search index, the analytics warehouse, the cache and the third-party processors. Erasure requests fail in the systems nobody remembered.

The EDPB's 2025 Coordinated Enforcement Framework action targeted the right to erasure specifically. Launched on 5 March 2025 across 32 authorities, it covered 764 controllers and produced 9 formal investigations plus 23 fact-finding exercises, with the report published in February 2026. Erasure is where the attention currently is.

---

## 6. Anonymisation as an alternative to deletion

Article 5(1)(e) constrains data "in a form which permits identification". Genuinely anonymous data falls outside the GDPR entirely, so anonymising ends both the clock and the obligation.

The bar is high and the word is used loosely. Removing a name is not anonymisation when the remaining fields identify a person. Pseudonymised data, where a key still exists somewhere, is explicitly still personal data under Article 4(5).

Where you claim anonymisation, say what technique was used and why re-identification is not reasonably possible. Where you cannot say that, call it pseudonymisation and keep applying the schedule.

---

## Common failures in this document

- **Invented default periods.** The GDPR supplies none; yours must be derived.
- **Periods with no trigger.** "Two years" from what.
- **Backups ignored.** Makes every stated period untrue.
- **No restore reconciliation.** A restore resurrects deleted records.
- **Conflicts left unresolved.** Each team resolves PCI against minimisation differently.
- **Indefinite legal holds.** Article 17(3)(e) supports the purpose, not unlimited scope.
- **Never verified.** Publish the oldest record per category and the fiction is visible.
- **"Anonymised" used for pseudonymised data.** Article 4(5) still calls it personal data.

---

## Related documents

- [`record-of-processing-activities.md`](record-of-processing-activities.md). Where the purposes that drive each period are recorded
- [`data-protection-impact-assessment.md`](data-protection-impact-assessment.md). Relies on these periods when assessing risk
- [`incident-response-plan.md`](incident-response-plan.md). Retention decides what was still there to lose
- [`../foundations/runbook.md`](../foundations/runbook.md). Where the deletion and restore procedures are written
- [`../foundations/test-strategy.md`](../foundations/test-strategy.md). Erasure needs an end-to-end test like any other requirement
