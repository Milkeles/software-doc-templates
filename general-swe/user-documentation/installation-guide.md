# Installation Guide

> Getting the software onto the reader's machine and proving it is there.
>
> **Also called:** Setup Guide, or Install Guide.
>
> **Why this one first.** Ask practitioners which documentation gap hurts most and missing installation instructions comes out top, ahead of the user manual and ahead of developer guides. It is also the gap with the shortest path to a lost user: someone who cannot install the thing never reaches anything else you wrote. If you are going to maintain one document properly, maintain this one.
>
> **The stake is higher than the content suggests.** This is the first thing anyone reads. A reader who cannot install does not go on to read anything else, and does not tell you why they left.
>
> **Where it lives.** Docs-as-code, and the short version in the [service README](../foundations/service-readme.md). The two must not disagree, so keep the README to the single happy path and link here for everything else.
>
> **Delete this block before publishing.**

---

## 1. Requirements

What the machine needs before anything is installed. Be exact.

| State | Instead of |
|---|---|
| Node.js 22.x or 24.x | Node.js (recent) |
| PostgreSQL 15 or later | A database |
| 4 GB RAM, 2 GB disk | Adequate resources |
| macOS 14+, Ubuntu 22.04+, Windows 11 | Any modern OS |

**Say which versions you test.** "Should work on earlier versions" is a promise you have not verified and will be held to.

Name what is *not* supported and why, if a reader could reasonably expect it. One line prevents a support thread.

---

## 2. Installation methods
If there is more than one way in, lead with a table so the reader picks once.

| Method | Use when |
|---|---|
| Package manager | You want the usual thing. Start here |
| Container image | You want isolation, or you are deploying |
| From source | You are contributing, or you need an unreleased change |

**Recommend one.** A guide that presents four equal options makes the reader research your project before installing it. Mark the default and let the rest follow.

---

## 3. Install

Steps per method, each self-contained. Do not make a reader following the container path read the package-manager path first.

Copyable commands, one per block, no shell prompts inside the copyable text if your site adds a copy button.

> ```
> brew install acme-cli
> ```

**Never pipe an unexamined script into a shell without saying so.** If you distribute `curl … | sh`, publish the script at a stable URL, say what it does, and offer a manual path. Readers in regulated environments cannot run it, and readers who care about supply chain will not.

Give the checksum or signature verification step where you publish binaries.

---

## 4. Verify

The step that is missing from most installation guides and that turns a hopeful reader into a confident one.

> ```
> acme --version
> ```
> ```
> acme 3.2.1
> ```
>
> Then run `acme doctor`. Every check should report `ok`.

**Show the expected output.** Without it, the reader has run a command and learned nothing.

If installation has server-side or configuration steps, verify those too. Reaching a version string proves the binary exists, not that it works.

---

## 5. First configuration

The minimum needed to make the install useful. Credentials, a config file, an environment variable.

Keep this to the minimum and link the reference for the rest. An installation guide that documents every setting has become a reference page and stopped being installable.

**Never put a real secret in an example.** Use an obvious placeholder and say where the real value comes from.

---

## 6. Common installation problems

Three to six, each as symptom, cause, fix. Only failures that happen *during installation*; general symptoms go in the [troubleshooting guide](troubleshooting-guide.md).

> **`command not found: acme` after a successful install**
> The install directory is not on your `PATH`. Add `~/.local/bin` to `PATH` and restart your shell.

These entries are written from real support traffic, not imagination. Review them after each release and delete the ones that no longer occur.

---

## 7. Upgrading

How to move between versions, whether config or data migrates, and where the breaking changes are listed.

Link the [changelog](../foundations/changelog.md) rather than restating it. Say explicitly whether upgrading is reversible.

---

## 8. Uninstalling

Rarely written, and its absence is noticed. Say what is removed, what is left behind, and where the leftover data lives.

A reader who cannot cleanly remove your software is a reader who hesitates to try it. Say it plainly:

> `brew uninstall acme-cli` removes the binary. Configuration in `~/.config/acme` and cached data in `~/.cache/acme` are left in place. Delete both to remove all traces.

---

## Testing this document

Same discipline as the [tutorial](tutorial.md), and the same decay rate.

- Run every method on a clean machine per supported platform before each release.
- Automate what you can in CI. A container build that follows the documented steps is a live test of them.
- Watch a new joiner install from the document once. Their first blocker is your top defect.

---

## Common failures in this document

- **Vague versions.** "Recent Node" is not a requirement anyone can check.
- **No verification step.** The reader cannot tell whether it worked.
- **Assumes the author's machine.** The tool the writer forgot they installed years ago blocks everyone else.
- **Every option presented equally.** The reader must make a research decision before starting.
- **No uninstall.** Raises the cost of trying the software.
- **Diverges from the README.** Two happy paths, one of them wrong.
- **Not re-run since the last release.** Rots faster than any other document here.

---

## Related documents

- [`../foundations/service-readme.md`](../foundations/service-readme.md). Carries the short happy path and links here
- [`troubleshooting-guide.md`](troubleshooting-guide.md). Symptoms after installation succeeds
- [`tutorial.md`](tutorial.md). What the reader does next
- [`../foundations/changelog.md`](../foundations/changelog.md). Breaking changes for upgrades
- [`../foundations/onboarding-guide.md`](../foundations/onboarding-guide.md). The internal equivalent, for engineers joining the team
