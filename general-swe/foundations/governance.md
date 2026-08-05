# Governance of {project}

*Also called: project governance, charter, constitution.*

*Italic text is guidance. Delete it as you fill each section in.*

*This document answers one question: when people disagree, what happens? Write it before you need it. Every mechanism below is copied from a project that runs at scale, but none of them is evidence-backed — see the notes at the end.*

*Fill in every number. A governance document that says "a majority of maintainers" without saying majority of whom, within what window, is not a governance document.*

| | |
|---|---|
| **Adopted** | YYYY-MM-DD |
| **Applies to** | *Which repositories and which organisation.* |
| **Supersedes** | *The previous version, or "nothing".* |

---

## Roles and rights

*Define each role by what it can do, not by how much it is admired. Electron's definitions are three words each and lose nothing: a maintainer "plays an active role in governance", a collaborator "is active in the community, but not in governance", a participant is either.*

| Role | Can do | Cannot do |
|---|---|---|
| *Contributor* | *Open issues and pull requests* | *Merge* |
| *Maintainer* | *Merge, triage, release* | *Change this document alone* |
| *{Steering body}* | *Set direction, resolve escalations, admit and remove maintainers* | *Act outside the powers listed here* |

*Name the steering body something your project will actually say out loud — steering council, TSC, core team, lead maintainers. Say how many seats it has. Python fixes it at five.*

*If your project is large enough to split, say how. Kubernetes delegates to SIGs and requires each one to publish a charter covering scope, responsibilities, areas of authority, how leaders are selected, how decisions are made, and how conflicts are resolved. Those six questions are a good audit of this document too.*

## Decision-making

*State which model you use and what happens when it fails. Four are in live use at scale, and they are genuinely different.*

- ***Consensus seeking.*** *The default at Node.js. Discussion continues until nobody objects strongly. Cheap when it works, and it needs a documented escape hatch or it stalls forever.*
- ***Consensus approval with veto.*** *The Apache Software Foundation's model for code changes: three `+1` votes and no `-1`. A `-1` is a veto that "cannot be overruled nor overridden by anyone" and stands until withdrawn.*
- ***Majority vote.*** *Homebrew resolves a vote the moment an option secures a simple majority, or automatically after 7 days with the leading option winning.*
- ***Council vote.*** *Python's steering council passes decisions on a strict majority of non-abstaining members, and every member must vote or explicitly abstain.*

*If you adopt a veto, adopt the condition that makes it survivable. The ASF requires that a veto carry "a technical justification showing why the change is bad (opens a security exposure, negatively affects performance, etc.)" and states plainly that "a veto without a justification is invalid and has no weight". Note also that the ASF permits vetoes on code changes but not on releases — "Releases may not be vetoed."*

**Lazy consensus.** *Silence gives assent, after a stated waiting period. The ASF's canonical form:*

> "The patch below fixes bug #8271847; if no-one objects within three days, I'll assume lazy consensus and commit it."

*Set a minimum voting window and say why. The ASF uses at least 72 hours "to provide an opportunity for all concerned persons to participate, regardless of their geographic location." Also state that only explicit votes count — the ASF warns "there is no implicit +1 from the release manager, or from anyone".*

## Appointment and removal

*The two hardest conversations in a project. Write the rules while nobody is angry.*

**Becoming a maintainer.** *Who may nominate, who votes, what threshold, how long the vote stays open, and whether the nominee is asked first.*

> *Node.js:* an existing collaborator nominates, the nomination stays open 72 hours, and it passes if no collaborator opposes. Node insists the nominee is asked beforehand, so a nomination they did not want does not appear in public.
> *Python:* two-thirds positive in a vote open one week, not vetoed by the steering council.
> *Homebrew:* simple majority of lead maintainers responding within 7 days, minimum quorum of 3; if quorum is missed the window extends by 7 days.

**Stepping back.** *Set an inactivity rule so nobody has to start the conversation. Node's is the cleanest found: a collaborator is automatically made emeritus if more than 12 months have passed since they authored or approved a commit that landed, and emeriti may ask to be restored. Python asks after two years and acts only if the person does not respond, keeping inactive members listed alongside active ones so credit survives.*

*Automatic and time-based costs nothing to operate. A judgement call costs someone a difficult message.*

**Removal for cause.** *A higher bar than everything else. Python requires a two-thirds majority to eject a core team member and spells out the arithmetic: "a 3:2 vote is insufficient; 4:1 in favor is the minimum required". Two protections are worth copying — the power "cannot be delegated", and it "cannot be used while a vote of no confidence is in process", so a body facing removal cannot eject the people removing it.*

**Removing the leadership.** *If your steering body can remove people, say how it can itself be removed. Python's vote of no confidence is triggered by one core team member calling for it publicly, seconded within one week, then a two-week vote succeeding at two-thirds. Homebrew removes its project leader on a two-thirds supermajority of lead maintainers.*

## Escalation and appeals

*What happens to a decision nobody accepts. This is the section homegrown governance documents skip, and the only one that matters on the worst day.*

*Give it a route, a name, and a deadline:*

> *Node.js:* any community member can ask the TSC to review something; if consensus-seeking fails, a collaborator applies the `tsc-agenda` label and it goes on the meeting agenda. The chair and the TSC "cannot veto or remove items".
> *Minimum Viable Governance:* appeal by opening an issue; maintainers respond in writing within a reasonable time; unresolved appeals escalate to the steering committee.
> *Homebrew:* a vote resolves automatically after 7 days with the leading option winning — a deadlock cannot outlast a week.

*Say where conduct complaints go instead, because they do not belong in this path. Homebrew decides them "by simple majority excluding the accuser and the accused".*

## Conflicts of interest

*Say what happens when one employer accumulates seats. Python caps it at two of five, and enforces it mechanically: if three of the top five vote-getters share an employer, the lowest-ranked is disqualified and the sixth candidate moves up, repeating until the council is valid. If circumstances change mid-term, members resign to fix it.*

*Also state that members with a conflict on a specific decision must abstain.*

*A project with a single corporate sponsor should say so plainly here rather than pretend otherwise.*

## Emergency powers

*Who can act first and explain later, and what makes that legitimate rather than a coup: a short list of triggers, and mandatory review afterwards.*

> *Homebrew:* any lead maintainer may immediately revoke access for malicious commits, compromised credentials, or abuse of access, and must notify the others. Restoration or permanent removal then needs a majority vote. When the project leader uses emergency powers, they "must submit the matter, decision and rationale… for review and confirmation by a majority vote of Lead Maintainers, within 7 days."

*Name who holds admin rights on the repositories and infrastructure, and keep that list to the minimum that can still act at 3am.*

## Trademarks and assets

*Who owns the name, the logo, the domain, the package registry entries, and any money. Developer-written governance documents almost always omit this, and it is the part with legal consequences.*

*Minimum Viable Governance handles it in three sentences, including the clause people forget: "If a Maintainer resigns or is removed, any rights the Maintainer may have in the Marks revert to the Organization."*

*State whether project discussions are confidential. MVG's answer is a flat no — information disclosed in project activity "is not confidential, regardless of any markings or statements to the contrary."*

## Amendments

*How this document changes, and by whom. Set the threshold higher than an ordinary decision, or the document protects nothing.*

*Two-thirds is the common choice: MVG requires "affirmative vote of 2/3 of all Maintainers", and PEP 13 requires two-thirds of votes cast in a vote open two weeks. Homebrew uses a majority of all maintainers, not just leads. Nobody publishes an argument for which is right — pick one and record the date of each amendment.*

*Exempt the housekeeping. PEP 13 needs no vote to update the current membership list.*

---

## Notes on using this template

*Delete this section too.*

**None of this is evidence-based, and you should say so if asked.** Every mechanism above comes from a normative document — PEP 13, the ASF voting rules, the Node.js governance file, Homebrew's charter, GitHub's Minimum Viable Governance. Those are authoritative for the projects that adopted them and nothing more. No study was found showing that one governance model produces better outcomes, higher contributor retention, or longer project life than another. Treat this as a menu of mechanisms that large projects rely on, not as best practice.

**Most projects do not need this document yet.** Minimum Viable Governance names the trigger better than anything else found: a corporate home becomes necessary "typically when your organization begins holding money". Before that, a maintainers list and a contributing guide usually carry the load. Writing elaborate governance for a three-person project is a way of avoiding the work.

**Start from Minimum Viable Governance, not from a large project's file.** GitHub's MVG project template is six sections and fits on a page: roles, decisions, how we work, no confidentiality, trademarks, amendments. It is CC-BY licensed and still labelled beta. Copying Kubernetes' or Python's governance into a small project imports machinery you cannot staff — Python's document exists to run a five-person elected council with employer caps and no-confidence votes.

**Consensus does not mean unanimity, and you should define it.** MVG's wording is the clearest: "While explicit agreement of all Maintainers is preferred, it is not required for consensus. Rather, the Maintainers will determine consensus based on their good faith consideration of a number of factors, including the dominant view of the Contributors and nature of support and objections." Without a definition, "we work by consensus" means whatever the loudest person says it means.

**The BDFL model's failure mode is succession, not operation.** It ran Python from inception until Guido van Rossum stepped down in July 2018. Replacing it took a formal process of its own — PEP 8000 and 8001 defined the process, PEP 8002 surveyed other projects, the 801x series were competing proposals, and PEP 8016 won a core-developer vote and became PEP 13. Roughly six months. If one person currently decides everything in your project, this document's real job is to answer what happens when they stop.

**Powers should come with instructions to use them rarely.** PEP 13 grants its council broad authority and then tells it not to use it: "The council should look for ways to use these powers as little as possible. Instead of voting, it's better to seek consensus." Its mandate describes the council as a "court of final appeal for decisions where all other methods have failed". Node.js says the same thing operationally — the agenda "is not to review or approve all patches", and the preference is "to minimize the need for TSC meetings to make decisions that can otherwise be made by collaborators on GitHub."

**Where this lives:** in the repository root as `GOVERNANCE.md`, versioned with the code, changed only by pull request. GitHub surfaces it in the community profile alongside the licence and code of conduct. Keep it in git rather than a wiki, because the amendment history is the point — a governance rule with no record of when it changed and who agreed is worth less than no rule. If your project sits under a foundation, note which decisions the foundation must approve; Node.js records that all changes to its TSC charter need approval from the OpenJS Foundation Cross-Project Council.

---

## Related documents

- [`contributing-guide.md`](contributing-guide.md). The day-to-day rules this document sits above
- [`code-review-guidelines.md`](code-review-guidelines.md). Where merge rights are exercised in practice
- [`rfc.md`](rfc.md). The process for decisions too large to settle in an issue
- [`architecture-decision-record.md`](architecture-decision-record.md). Where technical decisions are recorded once made
- [`incident-postmortem.md`](incident-postmortem.md). The other document that only matters on the worst day
