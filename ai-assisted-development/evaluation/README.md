# Evaluation

Two documents for answering a question none of the testing templates elsewhere in this repository are built to answer: is the model's output actually good enough, and is it staying that way?

## The documents

| Document | Answers |
|---|---|
| [`evaluation-plan.md`](evaluation-plan.md) | How do we measure whether this agent-assisted feature is good enough to ship, and by what method? |
| [`eval-run-log.md`](eval-run-log.md) | Run after run, is it actually staying good, or drifting? |

## When to use each

**Evaluation plan: once a feature's correctness or quality depends on a model's judgment, not just deterministic code.** A feature where the model only calls conventional, testable functions doesn't need this; the existing [test strategy](../../general-swe/foundations/test-strategy.md) covers it. A feature where the model decides what to say, what tool to call, or how to interpret ambiguous input needs a way to grade behavior that a pass/fail unit test can't capture.

**Eval run log: from the point the evaluation plan exists and evals actually start running.** A plan defines the method once; the log is where the results of running that method, again and again as the system changes, actually accumulate.

## Why we use them

This is a different kind of correctness than the rest of the repository's testing documents check for. A [test case specification](../../general-swe/foundations/test-case-specification.md) or a [master test plan](../../general-swe/waterfall/master-test-plan.md) verifies that deterministic code does what it's specified to do: the same input produces the same output, every time, or the test fails. A model does not have that property. The same prompt can produce a different response on different runs, and "correct" is frequently a matter of degree; an agent that gets 80% of the way to the right answer is meaningfully better than one that fails outright, in a way a binary pass/fail test doesn't represent. Evaluation, in the sense used here, is the discipline of measuring that kind of graded, sometimes-nondeterministic correctness on purpose, rather than discovering it's wrong from a user complaint.

Both OpenAI's and Anthropic's own published guidance on building and shipping agentic systems converge on the same practice, independently: evaluate early, evaluate continuously, and grade the eventual outcome with partial credit rather than a single pass/fail bar. Anthropic's guidance adds a discipline worth stating plainly here: the decision to use an agent at all, rather than a simpler workflow or a single well-tuned model call, should itself be justified by what the evaluation shows, not assumed before any measurement happens.

## Where these live

**Wherever the team already tracks its engineering methodology, reviewed on a set cadence, for the evaluation plan.** It defines a standing method, the same way a test strategy does, and belongs alongside it.

**Wherever the team already tracks recurring engineering work, for the eval run log.** It's an operational record that grows over time, the same shape as a [toil log](../../platform-engineering/reliability/toil-log.md): the value is in the trend, not any single entry, and it should be exactly as lightweight as the team's other running records.
