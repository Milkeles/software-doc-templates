# Web Development

Documents for teams shipping to browsers and to other people's clients.

These sit on top of [`general-swe/`](../general-swe/), not instead of it. A web team still writes architecture decision records, runbooks and postmortems. This area covers what is specific to the web: an interface other people build against, a rendering environment you do not control, and a set of legal obligations that apply to the front end and to almost nothing else in software.

---

## Groups

| Group | Use it when |
|---|---|
| [`foundations/`](foundations/) | Always. The API you publish, the front end's structure, which browsers you support, how changes reach users. |
| [`accessibility/`](accessibility/) | You have public users, sell to the public sector, or trade in the EU or UK. For most teams this is not optional and has not been since June 2025. |
| [`performance/`](performance/) | Speed affects your users or your revenue, and you want a number rather than an opinion. |

There is no methodology split here. Scrum and Kanban do not change what an API contract has to say.

---

## What makes web documentation different

Three constraints do not apply anywhere else in this repository, and every document in this area exists because of one of them.

**Your interface is a contract with people you cannot call.** A backend service can change an internal function signature and fix the callers. A public API cannot. Once someone integrates, the shape of your responses is frozen until you run a deprecation, and the deprecation is a document with dates in it. This is the same problem plan-driven teams solve with a baseline, arriving at teams who have never heard the word.

**You do not control the runtime.** Server code runs where you put it. Web code runs on a device you did not choose, over a network you cannot measure, in a browser version you did not pick. Almost everything in `performance/` and `browser-support-policy.md` exists to turn that uncertainty into a written decision instead of an assumption nobody stated.

**Some of it is law.** The European Accessibility Act has applied to consumer-facing services since 28 June 2025. EU public sector bodies have owed a published accessibility statement since 2019, in a format a Commission Implementing Decision specifies. US state and local government bodies face WCAG 2.1 AA deadlines in 2027 and 2028. This is the only area in the repository where skipping a document can produce a legal finding rather than an inconvenience.

---

## Where these documents live

The split runs cleaner here than anywhere else, because two of these documents are addressed to the public.

| Document | Home | Why |
|---|---|---|
| API design guide | Docs-as-code | Reviewed alongside the API it governs. A guide the API can drift from is not a guide |
| Frontend architecture | Docs-as-code | Describes the code, rots fastest when separated from it |
| Brand and visual guidelines | Wherever designers, agencies and partners can reach it, usually a public or shared page | Most of its readers never open a code editor |
| Design system guide | Published with the component library | Its readers are the people importing the components |
| Browser support policy | Docs-as-code, next to the browserslist config | The policy and the machine-readable version must not disagree |
| Rollout plan | Wherever the change is tracked, one per rollout | Short-lived. It is done when the flag is removed |
| Accessibility conformance report | Wherever procurement can reach it, usually a public page | Written for buyers, not for the team |
| Accessibility statement | A public URL on the site itself | Required to be published, and required to be linked from the site |
| Accessibility test plan | Docs-as-code | It is a test plan |
| Performance budget | Docs-as-code, next to the CI config that enforces it | An unenforced budget is a wish |
| Performance review | Wiki, one per period | A dated record, kept for comparison |

The rule underneath: **a document read by people outside your company lives where they can find it without asking you.** Everything else follows the usual test of whether it changes with the code.

---

## What to write first

1. **Browser support policy.** One page, and it settles arguments that otherwise recur monthly.
2. **API design guide**, if anyone consumes your API. Before the second version, not after.
3. **Accessibility statement**, if you are in scope. There is a deadline attached and it has passed.
4. **Performance budget**, once you have measured your current numbers. Not before.
5. The rest as the need appears.
