# Lessons bounded by benchmark evidence

Only the comparisons documented in this repository support the statements below. None is a universal prescription.

1. **Editing interfaces can change success substantially.** Hashline improved Grok Code Fast 1 on the cited editing benchmark; other models can regress. Test an interface with the intended model. [Evidence](evidence.md#oh-my-pi-changing-the-action-interface)
2. **Complete harness changes can improve a fixed model.** Deep Agents reports a Terminal-Bench gain from a bundle of verification, context, recovery and budget changes. The result cannot assign the entire gain to one component. [Evidence](evidence.md#deep-agents-improving-the-complete-execution-loop)
3. **Retrievable trajectory notes can improve memory QA.** LongMemEval-V2 reports gains on both tiers when notes supplement observations. [Memory evidence](memory-improvements.md)
4. **Original evidence still matters alongside summaries.** Removing raw observations from AgentRunbook-R reduces accuracy in its ablation. [Memory evidence](memory-improvements.md)
5. **Controller design can improve memory accuracy and latency together relative to a specified baseline.** AgentRunbook-C V2 beats vanilla Codex on the recorded comparison; its gain cannot be attributed solely to learned strategy notes. [Memory evidence](memory-improvements.md)

Preserving progress, adding reviewers, forgetting stale beliefs and other plausible interventions remain hypotheses unless a future addition supplies a qualifying experiment. Use the [experiment framework](experiment-framework.md) to test them.
