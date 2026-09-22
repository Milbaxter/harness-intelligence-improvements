# Harness Intelligence Improvements

High-level lessons for making AI agents more capable by improving the software around the model.

Created: 2026-09-22. This repository synthesizes published experiments and the accompanying discussion. It is a research notebook, not a benchmark implementation or a claim of independently reproduced results.

## Central idea

A harness determines what a model sees, what it can do, how it receives feedback, and when it continues or stops. Improving those mechanisms can increase the capability of the complete agent without changing model weights.

The strongest recurring lesson is to repair a demonstrated bottleneck: missing feedback, unreliable actions, poor access to evidence, repeated failure, or badly allocated time. Adding more prompts, tools, agents, or memory is useful only when it addresses such a bottleneck.

## Lessons at a glance

| Principle | Change to make | Why it can increase capability |
|---|---|---|
| Ground reasoning in feedback | Execute tests and inspect results against the original requirements | Supplies new evidence and exposes incorrect beliefs |
| Make actions reliable | Match tool interfaces to the model; validate and recover from malformed actions | Converts an intended solution into an actual change |
| Manage access to evidence | Keep concise working context with retrievable full artifacts | Makes important information available without overwhelming attention |
| Recover from failed strategies | Detect repetition, timeouts, and reasoning without action | Redirects effort toward a different approach |
| Allocate compute deliberately | Reserve time for implementation and verification; tune reasoning effort | Spends the available budget on productive steps |
| Preserve progress | Keep edits, decisions, test evidence, and unresolved work across interruptions | Prevents the agent from losing or undoing successful work |
| Use specialization selectively | Give a reviewer or worker a bounded objective and relevant context | Can expose different errors or divide independent work |
| Learn from trajectories | Find recurring failures, change one mechanism, measure regressions | Turns harness development into a cumulative empirical process |

These are design hypotheses supported to different degrees. The evidence does not establish one universally optimal harness.

## Contents

- [Lessons](docs/lessons.md): the mechanisms, practical implications, and failure modes.
- [Evidence](docs/evidence.md): source-backed results and what they do—and do not—establish.
- [Experiment framework](docs/experiment-framework.md): how to evaluate a proposed improvement.

## Working definition of improvement

Prefer **more independently verified task success under a stated resource budget**. Also record latency, cost, regressions, and human intervention. More activity, longer reasoning, more tool calls, and larger teams of agents are not success measures by themselves.

Useful distinction:

- **Recovering existing capability:** the model already knows what to do, but the interface or runtime prevents execution.
- **Enabling additional reasoning:** execution feedback, retrieval, or another perspective supplies information that lets the system solve something it otherwise could not.

Both matter to users. Neither, by itself, demonstrates that the underlying model has become more intelligent.
