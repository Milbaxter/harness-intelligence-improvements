# Evidence and limitations

Sources reviewed during the discussion on 2026-09-22. Results below are author-reported; we did not reproduce the experiments. The studies use different tasks, models, budgets, and dates and must not be combined into a universal ranking. Linked pages may change.

## Deep Agents: improving the complete execution loop

- Source: [LangChain, Improving Deep Agents with harness engineering](https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering), February 17, 2026.
- Code: [langchain-ai/deepagents](https://github.com/langchain-ai/deepagents).
- Reported result: Terminal-Bench 2.0 score increased from **52.8% to 66.5%**, keeping GPT-5.2-Codex fixed.
- Changes included verification before completion, environment context, deadline awareness, repeated-edit detection, and reasoning-budget allocation.
- Supports: substantial system-level gains are possible without changing model weights.
- Does not establish: that verification alone caused the entire gain, that inference spending was identical, or that the improvements generalize to every workload. The team iterated using benchmark feedback.

## Oh My Pi: changing the action interface

- Source: [Can Bölük, The Harness Problem](https://stencil.so/blog/the-harness-problem), February 12, 2026.
- Code: [can1357/oh-my-pi](https://github.com/can1357/oh-my-pi), a Pi fork.
- Experiment: 180 tasks involving synthetic mutations to React source files, three runs per task, across multiple models and editing formats.
- Reported example: Grok Code Fast 1 increased from **6.7% to 68.3%** when moving from patch editing to hashline editing.
- Mechanism: short content hashes identify lines so the model can specify changes without copying exact old text.
- Supports: mechanical action failures can conceal substantial model capability.
- Limits: this is an editing benchmark, not an end-to-end software engineering ranking. Some models regress; the published results include a regression for DeepSeek V3.2. Exact-file restoration is also narrower than arbitrary valid bug fixes.

## Henry Pan: optimizing recovery and preserving work

- Source: [Training Agent Harnesses Like Model Weights](https://www.henrypan.com/blog/2026-07-18-harness-training/), July 18, 2026.
- Code: [workofart/harness-training](https://github.com/workofart/harness-training).
- Reported result: after a determinism-hardening reset, **16/38 to 23/38** solved on a Terminal-Bench training subset, using a fixed Qwen3.6-35B-A3B FP4 model.
- Changes included recovering from reasoning that exhausted the output limit, repairing tool arguments, and ensuring edits were submitted. Related SWE-bench experiments protected edits from cleanup commands and corrected shell pipelines that masked test failures.
- Supports: runtime reliability and failure recovery can materially affect completion.
- Limits: these are training-set improvements. Broader Terminal-Bench evaluation overlaps the training set. The author also reports cross-model and cross-task investigations, but those should be examined separately from training gains.

## Metis: orchestration as a candidate mechanism

- Source and code: [Wholiver/metis](https://github.com/Wholiver/metis#benchmark--comparison).
- Reported comparison: **73/89 (82.02%)** for Metis versus **60/89 (67.42%)** for OpenCode on Terminal-Bench 2.1 with DeepSeek V4 Flash.
- The authors claim the same tasks, budget, and environment. Metis includes recursive agent roles, persistent memory, and verification gates.
- Supports: a concrete open-source candidate for testing whether a different execution structure helps.
- Limits: this is the project's own comparison. We did not independently reproduce it or establish the contribution of individual components. It does not prove that more agents or memory alone improves performance.

## AHE: automatic optimization and transfer

- Source: [Shichun Liu, Agentic Harness Engineering](https://shichun-liu.github.io/blog/2026/04/agentic-harness-eng-en/), April 28, 2026.
- Reported result: **69.7% to 77.0%** on Terminal-Bench 2.0 with GPT-5.4, after automatic harness evolution.
- The report describes tool, middleware, memory, and prompt changes, plus evaluations with other models and SWE-bench Verified.
- Supports: harness search can discover useful changes and transfer is an important separate evaluation.
- Limits: evaluation timeouts were relaxed to one hour per task, and optimization used the benchmark itself. These scores should not be directly ranked against standard-timeout submissions. Transfer claims remain author-reported.

## What is established versus inferred

**Observed in the cited reports:** changing harness components can change task success substantially with fixed model weights; effects differ across models; execution and verification failures are measurable sources of lost performance.

**Our synthesis:** feedback quality, action reliability, evidence access, progress preservation, and recovery are useful categories for designing improvements.

**Still open:** which combination wins on a particular user's work; how much improvement survives held-out evaluation; how gains change under equal total cost; whether a complex architecture justifies its coordination overhead.
