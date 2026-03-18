# Record of Processing Activities

> The inventory of what personal data you hold and why. Required by GDPR Article 30.
>
> **Call it by its legal name.** "Record of processing activities", "ROPA", or "Article 30 record". A supervisory authority asking for your Article 30 record will not recognise an invented internal name, and neither will a customer's security questionnaire.
>
> **You probably need two records, not one.** Article 30(1) covers what you do as a **controller**, Article 30(2) what you do as a **processor**, and they require different fields. A SaaS company is almost always both: controller for its own staff and customers, processor for the data its customers put into the product.
>
> **The small-business exemption almost never applies.** See section 5 below before assuming it does.
>
> **This is the first document opened during a breach.** It answers "whose data was in that system", which is the question that starts the 72-hour clock. That, more than the legal duty, is why it should be accurate.
>
> **Where it lives.** Wiki or a structured store that non-engineers can edit. Legal, privacy and support all maintain entries.
>
> **Delete this block before publishing.**

---

## 1. Controller record: the seven required items

Article 30(1). Every processing activity you decide the purposes and means of.

| # | Item | Notes |
|---|---|---|
| a | Name and contact details of the controller, any joint controller, the representative and the DPO | Roles, not individuals, plus a working address |
| b | The purposes of the processing | One row per purpose. "Running the business" is not a purpose |
| c | Categories of data subjects and categories of personal data | Customers, employees, applicants, children. Contact data, location, health |
| d | Categories of recipients, including recipients in third countries or international organisations | Includes your processors |
| e | Transfers to a third country, with the identification of that country and, for Article 49(1) second-subparagraph transfers, the documented suitable safeguards | Name the mechanism |
| f | Where possible, the envisaged time limits for erasure of the different categories of data | Link the [retention policy](data-retention-policy.md) |
| g | Where possible, a general description of the technical and organisational security measures referred to in Article 32(1) | A paragraph, not an audit |

**Items (f) and (g) are qualified "where possible".** (a) to (e) are not. If you are triaging, complete the unqualified ones first.

**The lawful basis is not in the Article 30 list.** Add it anyway. Article 5(2) accountability makes you demonstrate it somewhere, and next to the purpose is the only place it can be checked.

---

## 2. Processor record: only four items

Article 30(2). Much shorter, and the difference is the point.

| # | Item |
|---|---|
| a | Name and contact details of the processor, each controller on whose behalf it acts, the representative and the DPO |
| b | The categories of processing carried out on behalf of each controller |
| c | Transfers to a third country, with identification and, where applicable, documented safeguards |
| d | Where possible, a general description of the technical and organisational security measures |

**No purposes. No categories of data subjects. No categories of personal data. No erasure limits.** The processor does not decide the purpose, so it is not asked to record one. It records **"the categories of processing carried out on behalf of each controller"**, which is a different thing: hosting, analytics, support access.

Teams that keep one merged record end up asserting purposes for customer data they do not control. That is a factual error with legal consequences.

---

## 3. Shape of an entry

One row per purpose, not per system. A single database usually appears in several rows.

| Field | Example |
|---|---|
| Activity | Customer support ticketing |
| Role | Controller |
| Purpose | Responding to and resolving customer enquiries |
| Lawful basis | Contract, Art. 6(1)(b) |
| Data subjects | Customers, prospective customers |
| Personal data | Name, email, account ID, message content |
| Special categories | None. If users volunteer health data in tickets, say so and say what you do about it |
| Systems | Zendesk, support-api, the ticket archive in S3 |
| Recipients | Zendesk (processor), the on-call engineer |
| Transfers | US. SCCs plus supplementary measures |
| Retention | 24 months after ticket closure |
| Security measures | TLS in transit, encryption at rest, SSO, role-based access |
| Owner | Head of Support |
| Last reviewed | 2026-03-02 |

The "special categories" row is worth keeping even when the answer is none. Free-text fields collect data you never intended to hold, and writing "none" forces someone to check.

---

## 4. Format and access

Article 30(3): the record shall be **"in writing, including in electronic form"**. A versioned Markdown table, a spreadsheet, and a purpose-built tool all satisfy this.

Article 30(4): you make it available to the supervisory authority on request. Practically, this means it must be exportable by someone who is not the person who built it.

**Choose the format by who maintains it.** If Legal and Support own most entries, a wiki or spreadsheet wins. Docs-as-code only works when engineers are the ones who know the answers, which is rarely true for the whole record.

---

## 5. The exemption that does not apply to you

Article 30(5) exempts organisations with fewer than 250 employees, **unless** any of the following is true. The conditions are joined by "or":

- the processing is likely to result in a risk to the rights and freedoms of data subjects; **or**
- the processing **is not occasional**; **or**
- the processing includes special categories of data under Article 9, or criminal conviction data under Article 10.

**"Not occasional" defeats the exemption for essentially every operating business.** Paying staff is not occasional. Running a customer database is not occasional. The exemption was written for genuinely sporadic processing, and a company with a product does not qualify.

Do not tell anyone the record is optional because the headcount is under 250.

---

## 6. Keeping it true

A record that describes last year's architecture is worse than none, because it produces confident wrong answers during an incident.

- **Attach an owner to every row.** The person who would know if it changed.
- **Review on a trigger, not a calendar.** A new processor, a new data field, a new country, a new purpose. Add the check to whatever gate already exists for those changes.
- **Reconcile against reality once a year.** Compare the record against the actual list of production data stores and third-party contracts. Every discrepancy is either a missing row or a system nobody owns.
- **Feed the [DPIA](data-protection-impact-assessment.md) from here.** The systematic description required by Article 35(7)(a) is this record for one activity, expanded.

---

## Common failures in this document

- **One merged record for controller and processor roles.** They require different fields.
- **One row per system instead of per purpose.** Hides purposes and makes the lawful basis unstatable.
- **Assuming the under-250 exemption.** "Not occasional" removes it.
- **Vague purposes.** "Business operations" tells a regulator nothing and tells you less.
- **Transfers listed without a mechanism.** The country is not the answer; the safeguard is.
- **No owner per row.** Nothing gets updated when the system changes.
- **Invented internal name.** Nobody outside the company recognises it.

---

## Related documents

- [`data-protection-impact-assessment.md`](data-protection-impact-assessment.md). Built on the description held here
- [`data-retention-policy.md`](data-retention-policy.md). Where the item (f) time limits are decided
- [`incident-response-plan.md`](incident-response-plan.md). The first consumer of this record during a breach
- [`../foundations/architecture-overview.md`](../foundations/architecture-overview.md). The system view this record is reconciled against
- [`security-review-checklist.md`](security-review-checklist.md). Where the item (g) measures are verified rather than asserted
