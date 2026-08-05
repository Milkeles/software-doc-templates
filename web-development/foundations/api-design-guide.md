# API Design Guide

> The rules your API follows, written once, so that every endpoint does not become an argument.
>
> **Also called:** API style guide, or API design standards.
>
> **This is not your API reference.** OpenAPI generates the reference. This document contains the decisions OpenAPI cannot express: what your status codes mean, whether a retry is safe, how you version, what happens when you deprecate. A consumer can read your OpenAPI file and still not know whether it is safe to retry a failed `POST`.
>
> **Where it lives.** Docs-as-code, reviewed alongside the API it governs. A guide the API can drift from is not a guide.
>
> **Write it before the second version, not after.** The first version is a design. The second is a migration, and by then the rules are set by whatever the first version happened to do.
>
> **Delete this block before publishing.**

---

## 1. Scope and audience

Who this applies to and who reads it.

State whether the rules bind internal services, public consumers, or both, and what happens to APIs written before the guide existed. "All new endpoints from 2026-03-01; existing endpoints migrate at their next major version" is a usable answer. Silence means the guide applies to nothing.

---

## 2. Resources and naming

The section that saves the most argument per line written.

Fix and state:

- **Nouns or verbs**, and the exception list. Most guides settle on plural nouns for collections with a small set of named actions where a resource does not fit.
- **Case.** `snake_case`, `camelCase`, or `kebab-case`, in paths, in query parameters, and in JSON bodies. These can differ; say if they do.
- **Collection and item paths.** `/orders`, `/orders/{orderId}`.
- **Nesting depth limit.** Two levels is a common ceiling. Deeper hierarchies encode relationships that change.
- **Identifiers.** Opaque strings or integers, and whether consumers may parse them. If they are opaque, say so explicitly, because consumers will parse them otherwise and you will not be able to change the format.

One line example is worth more than a paragraph:

> `GET /v1/customers/{customerId}/orders?status=pending&page_size=50`

**Write down the exceptions you already have.** A guide that describes an idealised API nobody has is ignored. A guide that says "these six endpoints predate this document and are frozen" is used.

---

## 3. HTTP semantics

Cite the RFCs rather than restating them. The HTTP specification was reissued in June 2022 and the old numbers are obsolete:

| RFC | Covers | Obsoletes |
|---|---|---|
| **RFC 9110** | HTTP Semantics: methods, status codes, headers | 7231, 7232, 7233, 7235, and others |
| **RFC 9111** | HTTP Caching | 7234 |
| **RFC 9112** | HTTP/1.1 | parts of 7230 |
| **RFC 9113** | HTTP/2 | 7540 |
| **RFC 9114** | HTTP/3 | |

Citing RFC 7231 in 2026 tells a reader the guide has not been revisited in four years.

Document only where you make a choice the RFC leaves open:

**Which status codes you use, and what each means in your API.** Not the RFC definition, your usage. "409 means the resource is in a state that forbids this transition. 422 means the body parsed but failed validation." Consumers write branching logic against these.

**Safe, idempotent, cacheable.** RFC 9110 defines these properties per method. State which of your operations deviate, and how a consumer makes a non-idempotent operation safe to retry. If you support an idempotency key header, this is where it is specified: the header name, the key format, how long keys are retained, and what happens on a replay with a different body.

**Which methods you do not accept.** `PATCH` is the usual question. If you support it, say which patch format: JSON Merge Patch (RFC 7396) or JSON Patch (RFC 6902). They behave differently and the difference matters for null handling.

---

## 4. Versioning

**There is no settled answer here, and any guide claiming otherwise is quoting one house style.** State which you follow and why, because your consumers will have integrated against others.

The three published positions disagree directly:

| Source | Rule |
|---|---|
| **Google AIP-185** | Major version in the URI path: `/v1/`. Never `v1.0`; minor versions do not appear |
| **Azure REST API Guidelines** | Required `api-version` **query parameter** with a date value, `2026-03-01`. Omitting it returns HTTP 400 `MissingApiVersionParameter` |
| **Zalando RESTful API Guidelines** | Rule 113 SHOULD avoid versioning entirely. Rule 115 **MUST NOT use URI versioning**. Rule 114 MUST use media type versioning where versioning is unavoidable |

Zalando's Rule 115 forbids precisely what Google AIP-185 mandates. No RFC settles it. Pick one, write down which, and give the reason in one sentence so the next person does not reopen it.

**A note on citing Microsoft.** The `microsoft/api-guidelines` `Guidelines.md` is deprecated; the repository now directs readers to the Azure REST API Guidelines and the Microsoft Graph REST API Guidelines. Citing "the Microsoft REST API Guidelines" without saying which is now wrong.

Whatever you choose, specify:

- **What counts as breaking.** Removing a field, narrowing a type, adding a required request field, changing an error code, tightening validation. Publish the list. Most disputes are about whether a change was breaking, not about how to version.
- **What consumers must tolerate.** Usually: unknown response fields must be ignored, and enum values may be added. Say it, because if you do not, adding a field is a breaking change in practice.
- **How many versions you run at once**, and for how long.

---

## 5. Errors

### Format

**RFC 9457 Problem Details for HTTP APIs** (July 2023, obsoleting RFC 7807) is the standards-track option. Content type `application/problem+json`.

Its members are `type`, `status`, `title`, `detail`, `instance`. **None of them are strictly required**, and `type` defaults to `about:blank` when absent. Many guides state they are mandatory; they are not. If you want them mandatory in your API, that is your rule to state, not the RFC's.

Here too the published guides disagree. Zalando Rule 176 mandates `application/problem+json`. Azure mandates a proprietary `ErrorResponse` body with an `x-ms-error-code` header. If you are building on a platform, its convention may already be decided for you.

### Content

Whatever the format, document:

**A stable machine-readable code per error.** Consumers branch on it, so it is part of your contract and cannot change. HTTP status alone is too coarse: a single 400 covers a dozen distinct problems.

**Which errors are retryable and how.** State it in the guide and, where possible, in the response. A consumer who cannot tell a transient failure from a permanent one will either retry forever or give up on the first blip.

**Validation error shape.** Which field failed and why, in a structure a client can map to a form. This is the most-requested and least-specified part of most error designs.

**What never appears.** Stack traces, internal hostnames, SQL, upstream vendor errors passed through verbatim. This is a security rule, not a style rule.

---

## 6. Pagination, filtering, sorting

Pick one pagination style and use it everywhere. Two styles in one API doubles every consumer's work.

| Style | Good for | Cost |
|---|---|---|
| Cursor / token | Large or actively changing collections | Cannot jump to page N |
| Offset / limit | Small, stable collections; needs a total count | Items skip or repeat when the collection changes mid-traversal |

**Document the concurrent-write behaviour.** This is the thing that bites consumers and the thing almost no guide states. If a row is inserted while a client is paging, does it see a duplicate, miss an item, or neither? Say which.

Also specify: default and maximum page size, whether a total count is returned (and whether it is exact), how the client knows it has reached the end, and how filters combine when several are supplied.

---

## 7. Authentication and authorisation

The scheme belongs in OpenAPI. The policy belongs here.

- How a consumer obtains credentials, and how they are rotated.
- Token lifetime and refresh behaviour.
- Scope or permission model, and which scope each operation requires. Consumers cannot build a least-privilege integration without this.
- The difference between 401 and 403 in your API, stated explicitly. Guides that leave this implicit produce clients that retry authentication on authorisation failures.
- What is logged, and confirmation that credentials are not.

---

## 8. Rate limits

If you have limits, publish them. An undocumented limit is discovered in production by the consumer who least expected it.

- What is counted: requests, or a weighted cost per operation.
- The window, and whether it is fixed or sliding.
- Scope: per key, per user, per IP, per endpoint.
- Response on breach: 429, and the headers you return. Name them exactly.
- Whether `Retry-After` is sent, and whether consumers must honour it.
- Whether limits differ by plan, and how a consumer discovers their own.

---

## 9. Deprecation and sunset

The section with the strongest standards backing and the weakest adoption.

**RFC 9745** defines the `Deprecation` HTTP response header field (Proposed Standard, 2025). **RFC 8594** defines the complementary `Sunset` header. They are designed to be used together, and RFC 9745 is normative about the relationship:

> The timestamp given in the `Sunset` HTTP header field MUST NOT be earlier than the one given in the `Deprecation` header field.

Document:

- **Minimum notice period** between deprecation and removal, in months. This is a commitment; state it as one.
- **How consumers are told.** The headers, plus whatever out-of-band channel you use. Headers alone reach the client, not the person who has to act.
- **The `Link` relation** pointing at the deprecation documentation, which both RFCs support.
- **What you do about consumers who do not migrate.** The answer that keeps you honest is usually a staged brownout rather than a silent switch-off.

Machine-readable deprecation is worth the effort because it is the only mechanism that reaches an integration whose author has left the company.

This guide states the policy. Each individual removal gets its own [deprecation plan](../../general-swe/foundations/deprecation-plan.md) with real dates in it.

---

## 10. Changes to this guide

How rules get added or changed, and what happens to APIs built under the old rules.

The realistic policy: new rules apply to new endpoints, existing endpoints migrate at their next major version, and the guide records when each rule was added. Without this, the guide either freezes or invalidates the API it governs.

---

## Notes on using this template

*Delete this section before publishing.*

**Fill only the rows OpenAPI cannot already express.** OpenAPI 3.2.0 (published 19 September 2025) describes structure: paths, parameters, schemas, response shapes. It does not describe meaning or policy, and the gap it leaves is exactly this document:

| Not expressible in OpenAPI | Consequence if undocumented |
|---|---|
| Whether an operation is idempotent, and how retries are made safe | Consumers retry and duplicate charges |
| Rate limit semantics: what counts, what resets when, what happens at the limit | Consumers back off wrong, or not at all |
| Consistency guarantees, including read-after-write | Consumers write then immediately read and get stale data |
| What each error code actually means and whether the client should retry | Every failure becomes a support ticket |
| Pagination semantics under concurrent writes | Items skipped or duplicated across pages, silently |
| Naming and resource-modelling conventions | Every new endpoint is designed from scratch |
| Deprecation policy and support windows | Consumers discover removal by outage |
| Authentication and authorisation policy, as opposed to scheme | Integrators guess at scope requirements |

If your finished guide only restates what OpenAPI already says, delete it and keep the OpenAPI file.

---

## Common failures in this document

- **Restates OpenAPI.** Adds nothing and rots separately.
- **Describes an API you do not have.** Written as aspiration, ignored by everyone shipping.
- **Silent on retries and idempotency.** The most expensive omission, because the failure mode is duplicated writes.
- **Versioning declared without a reason.** Reopened at every design review.
- **"Breaking change" undefined.** Every version bump becomes a negotiation.
- **Cites obsolete RFCs.** 7231 for semantics, 7807 for problem details. Both superseded.
- **No deprecation policy.** Guarantees that removing anything is an incident.

---

## Related documents

- [`frontend-architecture.md`](frontend-architecture.md). If your own front end is a consumer, it is bound by this guide too
- [`rollout-plan.md`](rollout-plan.md). How an API change reaches production
- [`../../general-swe/foundations/architecture-decision-record.md`](../../general-swe/foundations/architecture-decision-record.md). Versioning and error-format choices are ADR material. Record the decision once, then let this guide state the rule without re-arguing it
