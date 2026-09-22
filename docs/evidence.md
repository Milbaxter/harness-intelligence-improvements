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

## Comparisons not promoted to established improvements

- [Henry Pan, July 18, 2026](https://www.henrypan.com/blog/2026-07-18-harness-training/): 16/38 → 23/38 on a training subset. Useful development evidence, insufficient for a generalization claim.
- [Metis](https://github.com/Wholiver/metis#benchmark--comparison): a bundled comparison cannot establish that memory or additional agents individually help. Not included as a mechanism-level lesson.
- [AHE, April 28, 2026](https://shichun-liu.github.io/blog/2026/04/agentic-harness-eng-en/): benchmark optimization and relaxed one-hour timeouts require separate transfer and budget analysis before inclusion as a general improvement.

## Memory evidence

See [recent memory improvements](memory-improvements.md) for 2026 comparisons with specified baselines. High conversational-memory scores from different vendors are not treated as matched improvement evidence.
