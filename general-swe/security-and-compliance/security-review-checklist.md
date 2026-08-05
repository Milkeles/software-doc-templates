# Security Review Checklist

> A named security step in review, with a short list attached.
>
> **Also called:** Secure Code Review Checklist.
>
> **Read this before you trust the checklist.** Braz, Aeberhard, Çalikli and Bacchelli ran a randomised experiment with 150 participants, 62% of them professionals, for ICSE 2022. Reviewers told to focus on security were **eight times more likely** to find the planted vulnerability than reviewers given no instruction. Reviewers given a checklist did no better than reviewers given the instruction alone: "a security checklist does not significantly improve the outcome", including the checklist tailored to the vulnerability.
>
> **So what is this document for?** The instruction, not the list. The measured effect comes from asking someone to look at security as a distinct task. Keep the list because it distributes knowledge and settles arguments, but do not believe the ticking is what works. A long list is worse than a short one, because it converts an attention task into a clerical one.
>
> **The ceiling is real.** Edmundson and colleagues had 30 developers review code containing seven known vulnerabilities: "none of the subjects found all confirmed vulnerabilities", none found more than five, and more experience did not mean more accuracy. Review is one control among several, not the control.
>
> **Where it lives.** Docs-as-code, next to [code review guidelines](../foundations/code-review-guidelines.md), and short enough to sit in a pull request template.
>
> **Delete this block before publishing.**

---

## 1. When a change gets a security review

Reviewing everything to the same depth means reviewing nothing carefully. Define the trigger.

**Always, regardless of size:**

- Authentication, authorisation or session handling
- Cryptography, key handling or secrets
- Anything that parses untrusted input
- File upload, file path handling, deserialization
- A new external dependency, or a new outbound call
- Changes to what personal data is collected or where it goes
- Infrastructure, permissions or network policy

**On judgement:** everything else. Say who makes that call.

Tie the trigger to something mechanical where you can. Path-based code owners on the auth directory work better than a rule people are meant to remember.

---

## 2. The list

Short on purpose. Each line is a question a reviewer asks, not a box that proves something.

**Access control**

- Is authorisation checked on the server, for this specific object, on every path that reaches it?
- Can changing an identifier in the request reach another tenant's data?
- Does a new endpoint inherit the default deny, or was it added outside it?

**Input and output**

- Is every query parameterised, including the one built with string concatenation for a dynamic ORDER BY?
- Is output encoded for the context it lands in, not just escaped generically?
- Are file paths, redirects and outbound URLs validated against an allowlist rather than a blocklist?

**Secrets and configuration**

- Any credential, token or key in the diff, including in tests and fixtures?
- Does a new configuration default fail closed?
- Is a debug flag, verbose error, or stack trace reachable in production?

**Dependencies and supply chain**

- Is the new dependency maintained, and is it the package you think it is?
- Is the version pinned and the lockfile updated?
- Does the build pull anything unpinned at run time?

**Data**

- Does this change what personal data is collected, stored or sent anywhere new? If yes, the [ROPA](record-of-processing-activities.md) needs a row and possibly a [DPIA](data-protection-impact-assessment.md).
- Is anything sensitive being logged?
- Is the retention rule for this data implemented, or only written down?

**Errors and failure**

- What happens on timeout, partial write, or a malformed response from a dependency?
- Does the error message tell an attacker something the user did not need?

The last group is there because OWASP's 2025 list added **A10 Mishandling of Exceptional Conditions** as a category in its own right. It is the failure mode reviewers skip because the happy path passed.

---

## 3. What to check the list against

Use a public catalogue rather than inventing coverage. Three, with different jobs.

| Source | Current version | What it is for |
|---|---|---|
| **OWASP Top 10** | 2025, released January 2026 | Awareness of what is common now |
| **OWASP ASVS** | 5.0.0, released 30 May 2025 | Verification requirements, roughly 350 of them across 17 chapters |
| **NIST SSDF, SP 800-218** | v1.1, February 2022 | Practices across the whole lifecycle, not just review |

**The Top 10 is not a checklist, and using it as one is a category error.** OWASP says so directly. The 2025 edition drew on over 2.8 million applications and 589 CWEs, of which 248 landed in the ten categories. It tells you where the mass is; it does not tell you what to verify.

The 2025 list, since most published summaries still show 2021:

```
A01  Broken Access Control                     (SSRF folded in here)
A02  Security Misconfiguration
A03  Software Supply Chain Failures            (new framing, wider than
                                                vulnerable components)
A04  Cryptographic Failures
A05  Injection
A06  Insecure Design
A07  Authentication Failures
A08  Software or Data Integrity Failures
A09  Security Logging and Alerting Failures
A10  Mishandling of Exceptional Conditions     (new)
```

Eight categories are data-derived and two come from the practitioner survey.

---

## 4. ASVS, and what changed in 5.0

If you need verification requirements rather than awareness, ASVS is the catalogue. Two things about version 5.0 change how you use it.

**Levels are no longer risk tiers.** They are priority-based: the standard defines them by "comparing risk reduction with the effort to implement". Level 1 is roughly the top 20% by that trade-off and exists to "decrease the barrier to entry"; Level 2 adds another 50%, so reaching it means about 70% cumulative; Level 3 is the remaining 30%. Verbatim: "Rather than the ASVS prescriptively stating what level an application should be at, an organization should analyze its risks and decide."

**Do not port a 4.x mapping.** Of the 286 requirements in 4.0.3, **only 11 remain unchanged**, and 109 of them, 38%, are no longer separate requirements at all.

**Version 5.0 added documentation requirements**, which is the part worth noticing here. Certain security decisions must be written down so that the implementation can be checked against them, and ASVS is explicit that "verifying that the documentation is in place and that the actual implementation are two separate activities". A standard now treats writing the decision down as a verifiable security control. That is the argument for this whole group of documents, made by someone other than us.

---

## 5. Beyond review

Review is a weak control used alone. The measured detection rates say so. Put the cheap automation in front of it so reviewers spend attention on what tools cannot see.

- Dependency scanning and a lockfile check in CI.
- Secret scanning on push, not only on merge.
- Static analysis tuned to near-zero false positives, because a noisy tool trains people to ignore it.
- A dated, owned process for acting on findings. NIST SSDF calls this practice group **Respond to Vulnerabilities (RV)**, alongside Prepare the Organization (PO), Protect the Software (PS) and Produce Well-Secured Software (PW).

For build integrity specifically, SLSA is the reference. The current approved specification is **v1.2**, which adds a Source Track alongside the Build Track; the Build Track covers Levels 1 to 3. Levels apply **per artifact**, not per organisation, so "we are SLSA Level 3" is not a statement the framework supports.

For programme-level maturity rather than per-change verification, OWASP SAMM v2.0 (January 2020, still current) organises 15 practices across five business functions. CIS Controls v8.1 (June 2024) covers 18 controls and 153 safeguards. Both answer "is our security programme adequate", which is a different question from "is this change safe".

---

## 6. Length cap
Every checklist grows. Each incident adds a line, and nobody removes one.

Cap it. Twenty items, hard limit. Adding an item means removing an item or automating one.

The best outcome for any line is that it stops being a line and becomes a test, a lint rule, or a type. That is the only way a list gets shorter, and the evidence says the length was never where the value was.

---

## Common failures in this document

- **Treated as the control.** No reviewer in the Edmundson study found more than five of seven vulnerabilities.
- **Believing the list is what works.** The randomised evidence attributes the effect to the instruction.
- **Too long.** Turns attention into clerical work and gets skimmed.
- **Top 10 used as a verification checklist.** OWASP says it is awareness.
- **ASVS levels read as risk tiers.** In 5.0 they are priority-based.
- **A 4.0.3 mapping carried forward.** Only 11 of 286 requirements are unchanged.
- **Findings with no owner.** SSDF makes response a practice group of its own.

---

## Related documents

- [`../foundations/code-review-guidelines.md`](../foundations/code-review-guidelines.md). The review process this attaches to
- [`../foundations/threat-model.md`](../foundations/threat-model.md). What you decided to defend against, which sets what to look for
- [`incident-response-plan.md`](incident-response-plan.md). What happens when review missed something
- [`data-protection-impact-assessment.md`](data-protection-impact-assessment.md). Where privacy risk gets assessed rather than reviewed
- [`../foundations/test-strategy.md`](../foundations/test-strategy.md). Where a checklist item goes to become a test
