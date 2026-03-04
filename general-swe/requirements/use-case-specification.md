# Use Case Specification

> One goal, one actor, and every way the interaction can go.
>
> **What it is good at.** Alternate paths. A user story says what someone wants; a use case says what happens when the card is declined, the session expires, the address fails validation, and the third attempt locks the account. Those branches are where the work actually lives, and they are the reason this form still earns its place.
>
> **The structure follows Alistair Cockburn**, *Writing Effective Use Cases* (Addison-Wesley, 2000). The field names below are his, and using his names rather than approximations matters, because a reader who knows the form will otherwise mis-read yours.
>
> **When not to use this.** Simple create-read-update-delete work. A use case for "the admin can edit a category name" is three paragraphs where one line would do. Write these for the flows with real branching: payment, authentication, onboarding, anything regulated, anything where getting the failure path wrong costs money.
>
> **Where it lives.** Wiki if business analysts and stakeholders maintain it. Docs-as-code if developers do and it changes with the code. Choose by author, not by preference.
>
> **Delete this block before publishing.**

---

## Casual form

Most use cases should be this. A paragraph, and you are done.

> **Reset a forgotten password.** The user requests a reset from the sign-in page and supplies their registered email address. The system sends a single-use link valid for 30 minutes. The user follows it, sets a new password meeting the policy, and is signed in. If the address is not registered, the system responds identically and sends nothing. If the link has expired or been used, the system says so and offers to send another.

**Write the casual form first, always.** If it captures everything, stop. Promote to the fully dressed form only when the branching genuinely exceeds what a paragraph can hold. Most teams do the opposite, produce twenty fully dressed use cases, and discover nobody reads them.

---

## Fully dressed form

Cockburn's template. Use the field names as given.

### Use case name

A short verb phrase naming the actor's goal. "Reset a forgotten password", not "Password reset functionality".

If you cannot name it as a goal someone has, it is probably not a use case. It might be a feature, a screen, or a subfunction.

### Context of use

A longer statement of the goal, if the name alone is not enough. Optional, and frequently is.

### Scope

What system is being treated as the black box under design. The whole enterprise, one system, one component.

Stating scope prevents the commonest confusion in use case writing: mixing steps the user takes with steps happening inside your system. If the scope is "the customer portal", then what the portal does internally is not a step.

### Level

One of three, in Cockburn's terms:

| Level | Means | Example |
|---|---|---|
| **Summary** | Spans multiple user goals, often over time | Manage an account through its lifetime |
| **User-goal** | One goal, one sitting, one person. The default | Reset a forgotten password |
| **Subfunction** | A step needed by other use cases, not a goal in itself | Validate password strength |

Cockburn explains the distinction with a sea-level metaphor: the sky extends far above and the sea far below, but there is only one level where they meet, and that level corresponds to user goals. Summary use cases are clouds or kites; subfunctions are fish or clams.

**Almost everything you write should be user-goal level.** The test is whether the actor would leave satisfied after doing just this. If they would still have to do something else to be finished, you are above the level. If nobody would ever set out to do only this, you are below it.

### Primary actor

The role that wants the goal achieved. A role name, not a person and not a job title if the job title includes people who would never do this.

### Stakeholders and interests

Everyone with a stake in the outcome, and what each needs from it. Underused, and it is where the non-obvious requirements come from.

> - **User:** wants access restored quickly, without contacting support.
> - **Security team:** needs the flow not to reveal whether an address is registered.
> - **Support:** needs a record of the attempt when a user calls anyway.
> - **Compliance:** needs every credential change written to an immutable audit log.

Two of those four produce requirements that no amount of thinking about the user would surface. That is the point of the section.

### Precondition

What is already true before this begins, and what the system does not need to check because something else guaranteed it.

Write only what is genuinely guaranteed. A precondition the system does not actually enforce is a defect waiting to happen.

### Minimal guarantees

What is true on **every** exit, including failures. Usually about logging, state consistency, and not leaving things half-done.

> The attempt is recorded in the audit log. No password is changed unless the flow completes.

This field is skipped more than any other and is one of the two most useful. It forces you to say what must hold when things go wrong, which is exactly the case nobody plans for.

### Success guarantees

What is true when the goal is achieved.

> The user's password is changed, all existing sessions are invalidated, and the user is signed in on the current device.

The session invalidation clause is the kind of requirement this field exists to surface. It follows from the goal but is not part of it, and it will be missed if nobody asks what "success" means precisely.

### Trigger

What starts the use case. A user action, a scheduled time, an external event.

### Main success scenario

The path where everything works. Numbered steps, three to nine of them.

Each step: the actor does something, or the system does something. Present tense, active voice, one thing per step.

> 1. The user selects "Forgot password" on the sign-in page.
> 2. The system requests an email address.
> 3. The user supplies an address.
> 4. The system generates a single-use token valid for 30 minutes and emails a link containing it.
> 5. The system confirms that a link has been sent, without stating whether the address was registered.
> 6. The user follows the link.
> 7. The system validates the token and requests a new password.
> 8. The user supplies a password meeting the policy.
> 9. The system stores it, invalidates existing sessions, records the change in the audit log, and signs the user in.

**Do not put conditionals in these steps.** No "if", no "unless". The moment you need one, it is an extension. Keeping the main scenario branch-free is what makes it readable, and readability is the entire advantage of this form over a flowchart.

**Do not describe the interface.** "The user supplies an address" survives a redesign. "The user types into the email field and clicks Submit" does not, and will be wrong within a year.

### Extensions

Every way each step can go differently. Number them against the step: 3a, 3b, 4a.

For each: the condition, then the steps that follow, then where it rejoins or how it ends.

> **3a. The address is not registered.**
>  3a1. The system waits the same interval as the success path and returns the same confirmation.
>  3a2. No email is sent. The attempt is recorded. Use case ends.
>
> **4a. The email provider is unavailable.**
>  4a1. The system queues the message for retry over 15 minutes.
>  4a2. If still undelivered, the system records a delivery failure for support. Use case ends.
>
> **7a. The token has expired.**
>  7a1. The system explains that the link has expired and offers to send another.
>  7a2. If accepted, resume at step 4.
>
> **7b. The token has already been used.**
>  7b1. As 7a1. The reuse is flagged in the audit log as a possible replay.
>
> **8a. The password fails the policy.**
>  8a1. The system states which rule failed and requests another. Resume at step 8.
>
> **8b. Three consecutive policy failures.**
>  8b1. The system invalidates the token and requires a fresh reset request. Use case ends.

**This section is the whole value of the document.** The main success scenario is what everyone already imagined. The extensions are what nobody thought about, and the discipline of walking each step and asking "what else could happen here" is the thinking the format exists to force.

Extensions become test cases almost directly. That is the practical reason to write them at this level of detail.

### Technology and data variations list

Where a step can happen through different technologies or with different data, and it matters.

> 3. Address may be supplied by typing or by autofill.
> 6. Link may be followed on a different device from the one that requested it.

Item 6 there is a real design question hiding in a variations list, and it is the sort of thing this field is for.

---

## Use cases and user stories

They are not competitors, and the framing that treats them as such causes teams to pick the wrong tool.

Mike Cohn draws the distinction in *User Stories Applied* (Addison-Wesley, 2004): a use case is a written agreement between customers and developers with a long shelf life, while a story is a placeholder for a conversation, scoped to fit an iteration. Cockburn's own later position is that the forms are complementary rather than opposed.

The practical rule that follows:

| Situation | Reach for |
|---|---|
| The conversation will happen, soon, with the person who knows | A user story |
| The conversation cannot happen: supplier, regulator, distributed team, or a year from now | A use case |
| Many alternate paths and failure modes | A use case, regardless |
| Backlog planning and sizing | Stories, sliced from the use case |

A common and effective combination: one use case establishes the full behaviour, and stories slice it for delivery. The use case is where the extensions live so they are not lost between sprints.

**A note on the widely quoted Cockburn line comparing a user story to a use case as a gazelle to a gazebo.** It circulates everywhere and cannot be traced to a dated publication. Do not cite it.

---

## On UML use case diagrams

The current specification is UML 2.5.1 (OMG, December 2017). Use case diagrams remain in it, with actors, use cases, `include`, `extend` and generalisation.

Know what the diagram is for: **it is an index, not a specification.** It shows which actors have which goals, on one page. It shows none of the behaviour, which is everything below "main success scenario" above.

A diagram is worth drawing when you have enough use cases that a list is hard to navigate. It is never a substitute for the text, and a project that produced diagrams and no text has documented its table of contents.

`include` and `extend` are the parts people misuse. If you are unsure which applies, you probably do not need either; two plain use cases and a cross-reference will be clearer to every reader.

---

## Common failures in this document

- **Fully dressed everywhere.** Twenty ceremonial documents, none read. Casual form first.
- **Interface described instead of intent.** Obsolete at the next redesign.
- **Conditionals in the main scenario.** Destroys the readability that justified the format.
- **No extensions.** Reduces the use case to a paragraph with headings, and discards its only real advantage.
- **Minimal guarantees omitted.** Nobody states what must hold on failure, so nothing does.
- **Written at the wrong level.** Subfunction use cases proliferate and hide the actual user goals.
- **Stakeholders and interests skipped.** The security, audit and support requirements go unfound until late.

---

## Related documents

- [`product-requirements-document.md`](product-requirements-document.md). Where use cases are referenced rather than embedded
- [`non-functional-requirements.md`](non-functional-requirements.md). Use cases carry behaviour; quality attributes need their own form
- [`../waterfall/software-requirements-specification.md`](../waterfall/software-requirements-specification.md). Use cases can be an SRS section, and ISO/IEC/IEEE 29148 places operational scenarios in stakeholder requirements
- [`../foundations/test-strategy.md`](../foundations/test-strategy.md). Extensions convert to test cases with very little translation
