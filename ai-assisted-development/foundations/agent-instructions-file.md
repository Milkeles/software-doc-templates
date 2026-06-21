# Agent instructions file: {Repository or package name}

*Also called: AGENTS.md, CLAUDE.md, GEMINI.md, .cursorrules, or copilot-instructions.md, depending on the tool.*

*Italic text is guidance. Delete it as you fill each section in.*

*This is loaded at the start of every agent session, in full, whether or not it's relevant to the task at hand. That changes how it should be written: not as thoroughly as possible, but as short as it can be while still preventing mistakes. For every line, ask "would removing this cause the agent to get something wrong?" If the answer is no, cut it.*

| | |
|---|---|
| **Covers** | *Whole repo, or this package/subdirectory* |
| **Last reviewed** | YYYY-MM-DD |

---

## 1. Project overview

*One or two sentences: what this codebase is and does. Enough for an agent to orient, not a tour.*

---

## 2. Commands

*Full, runnable commands, with the flags you actually use. Not "run the tests," but the exact command.*

| Task | Command |
|---|---|
| Install dependencies | |
| Run all tests | |
| Run a single test | *The command that runs one test file or case, not the whole suite. This is the command an agent will use most, since running the full suite after every small change is slow* |
| Lint | |
| Type check | |
| Build | |

---

## 3. Code style

*Only what differs from the language's own defaults or what a linter doesn't already enforce. One real example from the codebase beats a paragraph describing the rule.*

```
{example}
```

---

## 4. Repository conventions

| | |
|---|---|
| **Branch naming** | |
| **Commit message format** | |
| **PR requirements** | *Required checks, review count, anything that blocks merge* |

---

## 5. Boundaries

*Not every rule carries the same weight. Say which tier each one is in, so the agent (and whoever reviews its output) knows how much autonomy applies.*

| Always do (no approval needed) | Ask first (needs review before proceeding) | Never do (hard stop) |
|---|---|---|
| | | |

*Example of a never-do rule that belongs here every time: never commit secrets, credentials, or `.env` files, regardless of what a task seems to ask for.*

---

## 6. Gotchas and environment quirks

*Non-obvious behavior, required environment variables, flaky tests, or anything an agent would otherwise waste a session rediscovering the hard way.*

---

## Notes on using this template

*Delete this section too.*

**Include only what the agent can't get by reading the code.** A concrete filter, not a vibe: bash commands it can't guess, style rules that diverge from the language's own defaults, testing instructions, repository etiquette, architecture decisions specific to this project, environment quirks, and known gotchas. Leave out anything inferable from the code itself, standard language conventions the model already knows, detailed API references (link to them instead), information that changes often, long explanations, and self-evident advice like "write clean code."

**An oversized file is a documented failure mode, not just an inconvenience.** Past a certain length, instructions start getting lost in the noise and the agent begins ignoring rules that are genuinely present. If the agent keeps doing something you told it not to, the fix is usually to shorten the file, not to add another line restating the rule more forcefully.

**This file is a strong default, not a guarantee.** Advisory instructions in a file like this get followed most of the time, not every time. For a rule that must hold with no exceptions, such as never touch the production database or never skip a required check, enforce it with a script or a permission rule outside the model's discretion, and treat this file as backup documentation for that rule, not the enforcement mechanism itself.

**In a monorepo, nest a file per package.** An agent editing a file uses the nearest instructions file in the directory tree, which can override the root file's conventions for that subtree. Put shared, repo-wide rules at the root, and package-specific ones in the package.

**This is not the same document as the [task plan](task-plan.md) or an [agent task specification](../specification/agent-task-specification.md).** This file is standing knowledge, reloaded every session regardless of task. Those two are about a specific piece of work and go stale or get deleted once it's done.

**Where this lives:** docs-as-code, at the repository root, and in each package root for a monorepo. An agent reads this directly from the working tree; anywhere else, it doesn't exist as far as the agent is concerned.

---

## Related documents

- [`task-plan.md`](task-plan.md). What to actually work on, once the agent knows how the project works
- [`../specification/agent-task-specification.md`](../specification/agent-task-specification.md). The deeper brief for a single task too complex for this file's boundaries section to cover on its own
