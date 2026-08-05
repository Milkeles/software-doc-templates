# Interface: {Provider} to {Consumer}

*Also called: ICD (interface control document).*

*Italic text is guidance. Delete it as you fill each section in.*

| | |
|---|---|
| **Interface ID** | *Stable identifier. It will be cited elsewhere.* |
| **Version** | |
| **Status** | *Draft / agreed / in service / deprecated* |
| **Provider owner** | *Named person, provider side.* |
| **Consumer owner** | *Named person, consumer side.* |
| **Agreed on** | YYYY-MM-DD |

---

## Scope
*An OpenAPI document, a Protobuf definition or a JSON Schema expresses shape: paths, fields, types, required-ness. It is machine-readable, testable, and generated into clients. Nothing in this document should duplicate it.*

*What no schema expresses, and what breaks integrations in practice:*

- *who owns each side, and who to call at 2am*
- *what the error responses mean and what the caller should do about each*
- *whether a retry is safe*
- *ordering and delivery guarantees*
- *rate limits and what happens at the limit*
- *how much notice you get before it changes*
- *what happens to the data afterwards*

**Those seven are this document.** *If you find yourself listing fields, stop and link the schema instead.*

---

## 1. Parties and responsibilities

| | Provider | Consumer |
|---|---|---|
| **System** | | |
| **Owning team** | | |
| **Named owner** | | |
| **Support channel** | | |
| **Escalation** | *Who, and after how long* | |

*Both columns get filled. A document with an empty consumer column is a provider's API reference wearing a different title.*

**Who may change this document.** *Name the approvers on both sides. If a change control board exists for interfaces, state its scope of authority and its procedure.*

---

## 2. The interface

| | |
|---|---|
| **Nature** | *Synchronous API / message stream / file transfer / shared database / hardware* |
| **Transport and protocol** | *HTTPS, gRPC, AMQP, SFTP* |
| **Schema** | *Link. This document does not restate it* |
| **Schema version and location** | *Where the authoritative copy lives, and how it is versioned* |
| **Authentication** | *Mechanism and credential rotation, or link the relevant policy* |
| **Environments** | *Endpoint per environment, and which are production-like* |

```
   PROVIDER                 INTERFACE                 CONSUMER
   payments-svc  ---------> POST /refunds  --------->  ops-console
                            schema: refunds-v2.yaml
                            owner: joint
                            change notice: 90 days
```

*Draw the interface as its own box, not as an arrow. It is the third configuration item, and the diagram should show that it is owned rather than emitted.*

---

## 3. Behaviour the schema cannot express

*The section that earns the document.*

### Errors

| Condition | Response | What the consumer should do |
|---|---|---|
| *Refund amount exceeds original charge* | *422, code `AMOUNT_EXCEEDS_CHARGE`* | *Do not retry. Surface to the operator* |
| *Downstream provider unavailable* | *503, `Retry-After` header* | *Retry, honouring the header* |
| *Duplicate idempotency key* | *200 with the original result* | *Treat as success* |

*Every error a consumer can receive needs a row and an instruction. "500 Internal Server Error" with no guidance means every consumer invents its own retry policy, and one of them will invent a retry storm.*

### Guarantees

| | |
|---|---|
| **Idempotency** | *Which operations are safe to repeat, and the mechanism* |
| **Ordering** | *Guaranteed, per-key, or none* |
| **Delivery** | *At most once / at least once / exactly once, and be honest* |
| **Consistency** | *When a write becomes visible to a subsequent read* |
| **Timeouts** | *Provider's own timeout, and the one the consumer should set* |

### Limits and expected load

| | |
|---|---|
| **Rate limit** | *Requests per period, per what* |
| **Behaviour at the limit** | *429, queue, or drop. Say which* |
| **Expected volume** | *What the consumer has told the provider to plan for* |
| **Payload size** | |

*The expected volume row is a commitment in both directions. It is what lets the provider capacity-plan, and what lets them push back when actual traffic is ten times the agreed figure.*

### Availability

| | |
|---|---|
| **Target** | *State it as a number the consumer can design against* |
| **Maintenance windows** | *Or "none, changes are deployed continuously"* |
| **Planned downtime notice** | |
| **What the consumer does when it is down** | *Degrade, queue, or fail. Agreed in advance* |

### Data

| | |
|---|---|
| **Personal data** | *What crosses this interface, under whose lawful basis* |
| **Retention** | *How long each side keeps it* |
| **Deletion** | *How a deletion request propagates across the interface* |

*Skip this section only if no personal data crosses. If it does, this is where two teams discover they each assumed the other was the controller.*

---

## 4. Change control

*The clause consumers actually depend on.*

| Change type | Example | Notice | Approval |
|---|---|---|---|
| *Additive, backward compatible* | *New optional field* | *None* | *Provider* |
| *Behavioural, compatible* | *Error message wording* | *Release notes* | *Provider* |
| *Breaking* | *Field removed, type changed, semantics changed* | *90 days, new version* | *Both parties* |
| *Emergency security fix* | | *As soon as possible* | *Provider, notified after* |

**Define "breaking" explicitly.** *Providers and consumers disagree about this constantly. Writing down that removing a field is breaking, and that adding an optional one is not, resolves it once.*

**Versioning.** *How versions are expressed, how many are supported at once, and for how long. Link the [deprecation plan](deprecation-plan.md) for the retirement process.*

*The pattern to avoid, named by Robinson and Fowler: big-bang versioning, where "schema changes ripple through providers and consumers, disrupting uptime, retarding evolution and reducing revenue generating opportunities."*

---

## 5. Verification

*How each side proves it still honours the agreement, without a release meeting.*

**Where you can enumerate your consumers**, *use consumer-driven contract tests. Each consumer publishes what it actually depends on, and the provider's build fails when it breaks any of them. This replaces most of the coordination this document otherwise requires.*

*Note the stated limit: the pattern "is applicable in the context of either a single enterprise or a closed community of well-known services". If your consumers are the public, or anyone with an API key, you cannot collect their contracts, and a published interface document plus a real notice period is the mechanism you have. The two are complementary, and which one you need depends only on whether you can name your consumers.*

| | |
|---|---|
| **Contract tests** | *Where they run, whose build they break* |
| **Test environment** | *Endpoint, credentials process, data reset policy* |
| **Reference implementation** | *If one exists* |

---

## Notes on using this template

*Delete this section too.*

**Write one only when the interface crosses a boundary you cannot unilaterally change.** A different team with its own roadmap, a different company, a contract, a regulator, or a consumer you cannot enumerate. An interface between two services owned by the same team does not need one; the schema plus a shared on-call rota covers it.

IEEE Std 828-2012 puts the reason precisely: "Interfaces represent 'agreements' between different development efforts. Each party is constrained by the requirements of the interface. Thus, each interface represents at least three CIs: the interface specification itself, and components on either side of the interface." That third item is the point. The specification is a versioned thing in its own right, owned jointly, not a description belonging to whichever side wrote it. Treating it as the provider's documentation is how consumers discover breaking changes in production.

**One document per interface, not one per system.** A system with four consumers on different terms has four agreements. Merging them produces a document where no consumer can find their own commitments.

**Version this document with the schema.** They change together or the pair becomes untrustworthy. Put both in the same repository, and make the schema the thing that generates code, so drift is caught by the compiler rather than by a reader.

**The signature line is the point of an ICD.** In its aerospace and defence origins the document is agreed, dated, and changed only by both parties. That formality is often the only thing standing between a consumer and an unannounced breaking change. Keep it even when the parties are two teams in one company.

**If the interface is a shared database, say so plainly.** It is still an interface, it is the hardest kind to change, and it is the one least likely to have a document. The schema is the contract whether anyone agreed to it or not.

**Where this lives:** in a repository both parties can read, versioned alongside the schema, published to wherever consumers actually look. If the consumer is external, a wiki behind your SSO is the same as not having written it.

---

## Related documents

- [`architecture-overview.md`](architecture-overview.md). Where this interface sits in the system
- [`deprecation-plan.md`](deprecation-plan.md). Retiring a version of this interface
- [`changelog.md`](changelog.md). Where compatible changes are announced
- [`configuration-management-plan.md`](configuration-management-plan.md). Why the specification is a configuration item in its own right
- [`test-strategy.md`](test-strategy.md). Where contract testing sits among the other levels
- [`threat-model.md`](threat-model.md). A trust boundary usually runs exactly here
