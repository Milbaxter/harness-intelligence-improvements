# Evaluating an intelligence improvement

## Define the claim first

Use a specific hypothesis:

> The agent often stops without executing relevant tests. A completion check that asks for verification against the requirements will improve independently graded success within the same total budget.

Avoid claims such as “more memory makes it smarter” without naming the failure being addressed.

## Hold the comparison together

Record and control, where practical:

- Model identifier, provider, inference settings, and test dates.
- Harness commit, prompts, tools, extensions, and task instructions.
- Starting repository state, environment, permissions, and network access.
- Total time, token, and dollar budgets, including all subagents and reviewers.
- Task set, evaluator version, repetitions, and retry policy.

If an intervention changes one of these, label it explicitly. Report infrastructure errors and replacements rather than silently selecting the best rerun.

## Measure outcomes and mechanisms

| Measure | Question |
|---|---|
| Independently verified success | Did the system actually finish the requested work? |
| Newly solved tasks and regressions | Which tasks improved, and which got worse? |
| Cost per successful task | How much do successes and failures together cost? |
| Latency distribution | Does the change improve typical runs while creating very slow failures? |
| Human intervention | How often must a person rescue or clarify execution? |
| Mechanism-specific failure rate | Did the targeted failure actually become less frequent? |

Useful diagnostic counts include rejected edits, repeated identical failures, tests executed before completion, lost edits, context-retrieval misses, and time spent without progress. These explain outcomes; they do not replace them.

## Separate development from evaluation

- Use a development set to discover changes.
- Freeze the candidate before running a held-out set.
- Repeat runs where stochastic variation could change the conclusion.
- Report uncertainty and paired task outcomes, not just one aggregate percentage.
- Test transfer to a different repository, task type, or model before claiming generality.
- Keep task-specific solutions and hidden graders inaccessible to the acting agent.

## Prefer the simplest supported intervention

Start with the failure, then choose a mechanism:

| Observed failure | Candidate intervention |
|---|---|
| Correct intent, invalid edit | Better edit interface and actionable validation |
| Stops after writing untested code | Completion verification check |
| Repeats the same failed command | Failure-history signal and strategy-change prompt |
| Loses critical evidence after compaction | Structured progress record with retrievable sources |
| Runs out of time before finishing | Phase-aware budget information and verification reserve |
| Deletes or forgets a working fix | Checkpoints and explicit progress preservation |
| Cannot coordinate independent work | Bounded delegation with verified outputs |

## Experiment record template

```text
Name:
Date:
Target failure and baseline evidence:
Hypothesis:
Baseline harness commit:
Candidate harness commit:
Model/provider/settings:
Tasks and development/held-out split:
Independent evaluator:
Budgets and accounting:
Repetitions and retry policy:
Success rate and uncertainty:
Newly solved tasks:
Regressions:
Cost and latency:
Human intervention:
Did the targeted mechanism improve?:
Transfer results:
Decision: retain / revise / reject / insufficient evidence
Known limitations:
Artifact and trajectory locations:
```

A promising result is a reason to run the next controlled test. It is not automatically a reason to add the feature to every agent.
