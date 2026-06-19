# {service-name}

*Italic text is guidance. Delete it as you fill each section in.*

*One sentence: what this service does and for whom. Written so someone who has never heard of it understands within seconds.*

> **Example.** Authorises card payments for the retail checkout and records them in the ledger.

| | |
|---|---|
| **Owner** | *Team name, plus the chat channel to ask in.* |
| **On-call** | *Link to the rota or escalation policy.* |
| **Tier** | *How much it matters: tier 1 pages, tier 3 waits until Monday.* |
| **Status** | Active \| Maintenance only \| Deprecated, replaced by X |

*This is the highest-traffic document your team owns and the cheapest to maintain. It exists to stop interruptions. Every question it answers is a question nobody asks you.*

---

## Run it locally

*The shortest path from a fresh clone to something working. Commands, in order, copy-pasteable.*

*Test this yourself on a clean machine at least once. Every service README contains a setup step that only works because of something already installed on the author's laptop.*

```bash
# prerequisites: what must already be installed, with versions
# then:
```

*State how long it should take and what "it worked" looks like: an address to open, a log line to expect, a command that returns something.*

---

## Test it

*How to run the tests, and how to run only the fast ones. If the full suite takes twenty minutes, say so here rather than letting a new joiner discover it.*

```bash
```

---

## Configuration

*Every environment variable or setting: name, what it does, whether it is required, and the default. Secrets are named here but never valued; say where they come from.*

| Variable | Required | Default | What it does |
|---|---|---|---|
| | | | |

---

## Architecture in brief

*Five to ten lines, or a small diagram. What it calls, what calls it, what it stores and where.*

*Resist writing more. Link the [architecture overview](architecture-overview.md) for depth. A README that grows an architecture chapter stops being scannable, which was its only advantage.*

**Dependencies.** *What must be up for this to work, and what happens to this service when each one is not.*

| Depends on | Purpose | If it is down |
|---|---|---|
| | | |

---

## Deploy it

*How code reaches production: the pipeline, what gates it, how long it takes, who can trigger it.*

*Then how to roll back, with the command. This is the single most looked-up line in any README, and it is looked up under pressure. Put it here in full, not behind a link.*

---

## Operate it

*Links, not content. The content belongs in the documents linked.*

- **Dashboards:** *link*
- **Alerts and runbooks:** *link to [runbook](runbook.md)*
- **Logs:** *where, and the query that filters to this service*
- **SLOs:** *link*

**Common failures.** *Two or three lines. The things that actually go wrong, each pointing at the runbook section that handles it.*

---

## API

*Link to the contract: OpenAPI file, protobuf definitions, schema. If it is generated, say where from and how to regenerate it.*

*Do not paste endpoint documentation here. It will be wrong within a month, and the generated version will be right.*

---

## Contributing

*Branch naming, commit conventions, how a change gets reviewed, anything unusual about this repository. Link the [code review guidelines](code-review-guidelines.md) rather than restating them.*

---

## Notes on using this template

*Delete this section too.*

**Order it by how often something is needed.** Setup and rollback are read weekly; the architecture summary is read once. The template above is already in that order.

**Under two screens.** A README's advantage over every other document is that people read it. Length destroys that. When a section outgrows the page, move it into its own document and leave a link.

**Check it on every onboarding.** The setup steps are the part that breaks silently, and a new joiner is the only person who will notice. Make fixing the README the first pull request they merge.

**Where this lives:** the repository root, as `README.md`. There is no defensible alternative.

---

## Related documents

- [`architecture-overview.md`](architecture-overview.md). Depth on the system shape this file only summarises in five to ten lines
- [`runbook.md`](runbook.md). What "operate it" links to when an alert actually fires
- [`code-review-guidelines.md`](code-review-guidelines.md). What "contributing" points to instead of restating the review bar
- [`onboarding-guide.md`](onboarding-guide.md). Where a new joiner is sent to run this file's setup steps for the first time
