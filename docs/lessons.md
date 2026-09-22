# High-level lessons

The explanations below are a synthesis, not individually proven causal claims. See [evidence](evidence.md) for attribution and experimental limits.

## 1. Turn reasoning into a feedback loop

The productive cycle is **observe → propose → act → verify → revise**.

Rereading a solution often repeats the assumptions that produced it. Running a test, checking an artifact, or comparing behavior with the request introduces evidence from outside that reasoning process.

Practical changes:

- Define completion in terms of observable behavior.
- Check the result against the original requirements, not just the implementation.
- Before stopping, require relevant verification and an account of unresolved failures.
- Use informative failures to guide the next attempt.

Boundary: tests can be incomplete or wrong. Passing an agent-written test is weaker evidence when that test merely restates the agent's mistaken implementation. The final evaluator must remain independent of the agent.

## 2. Reduce the gap between intent and execution

An agent can understand a problem yet fail to express a valid action. Exact-text replacements, escaping, ambiguous tool schemas, and brittle patches can turn a reasoning success into an execution failure.

Practical changes:

- Use unambiguous references to files and locations.
- Reject stale edits with actionable error messages.
- Prefer structured tool results over prose that must be reinterpreted.
- Recover from malformed arguments and truncated responses where recovery is safe.
- Verify that edits were written to disk and that shell exit statuses reflect the command that matters.

Boundary: the best interface varies by model. A format that helps one model can hurt another. Measure whole-task success, not only tool-call validity.

## 3. Treat context as access to evidence

The goal is neither maximum context nor minimum context. It is reliable access to the information needed for the next decision.

Practical changes:

- Keep the objective, constraints, decisions, and unresolved questions explicit.
- Clip or summarize bulky outputs while preserving the full artifact for retrieval.
- Avoid repeatedly replaying large content that is already stored elsewhere.
- Distinguish observed facts from proposed explanations.
- Preserve provenance so the model can revisit the source of a claim.

Boundary: compression can remove the decisive clue. Retrieval must be usable, and summaries must not silently turn uncertainty into fact.

## 4. Interrupt unproductive repetition

Persistence is useful only while new evidence or progress accumulates. Repeated edits, identical timeouts, and long reasoning without action can signal a stalled strategy.

Practical changes:

- Detect repeated failure patterns rather than imposing a single arbitrary step limit.
- Surface the evidence that the current approach is failing.
- Ask for a revised hypothesis or a discriminating experiment.
- Preserve useful partial work before switching strategy.

Boundary: repetition is sometimes legitimate exploration. Intervene on evidence, and measure whether the intervention fixes more tasks than it disrupts.

## 5. Budget for the complete task

Reasoning consumes resources that might otherwise support implementation, testing, or a second approach. The agent needs enough budget to finish the whole cycle.

Practical changes:

- Give the agent accurate remaining-time or resource information.
- Reserve a final portion of the budget for verification and delivery.
- Test different reasoning allocations across task phases.
- Stop repeatedly waiting on an operation that cannot finish within the remaining budget.

Boundary: lower reasoning effort may reduce solution quality. Higher effort may improve it. Compare allocations under the same overall budget, with all delegated work included.

## 6. Preserve progress as explicit state

Long tasks fail when the agent forgets a decision, loses an edit, or interprets cleanup as permission to discard the solution.

Practical changes:

- Track what changed and which checks passed.
- Keep checkpoints before risky transitions.
- Carry unresolved work and its evidence into resumed sessions.
- Protect useful edits from accidental cleanup or reset operations.

Boundary: persistent memory can preserve stale or incorrect beliefs. Store scope, provenance, and validity conditions; allow correction and expiry.

## 7. Add other agents only for a defined purpose

A reviewer may catch a mistake because it has a different objective, evidence, or context. Multiple agents do not automatically supply independent reasoning.

Practical changes:

- Give workers bounded tasks with clear outputs.
- Give reviewers requirements and verification evidence, not only the author's rationale.
- Isolate changes where independent workers could conflict.
- Define how disagreements will be resolved using evidence.

Boundary: delegation introduces coordination cost, duplicated work, and correlated errors. The evidence reviewed here is weaker for attributing gains to multi-agent structure alone than for specific tool and feedback changes.

## 8. Optimize from failures, then test transfer

Treat each harness change as a falsifiable hypothesis about a recurring failure.

1. Collect trajectories and classify failures.
2. Choose a frequent or expensive failure that the harness can plausibly address.
3. Make a bounded change with a predicted effect.
4. Compare baseline and candidate on matched tasks.
5. Inspect newly solved tasks and regressions.
6. Freeze the change and test unseen tasks or another model.

Boundary: repeatedly optimizing against a benchmark makes that benchmark part of development. Gains there are not sufficient evidence of general capability. Record optimization expenditure separately from the cost of running the resulting agent.

## Overall interpretation

The harness can increase effective capability by making evidence more useful, actions more reliable, progress more durable, and recovery more directed. Judge each mechanism by what failure it repairs and whether that repair transfers beyond the cases that motivated it.
