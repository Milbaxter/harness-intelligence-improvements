# Harness Intelligence Improvements

Recent, benchmark-backed improvements to AI agent harnesses and memory systems.

Reviewed: **2026-09-22**. “Recent” means results first published or materially updated in **2026**. This is a research notebook, not a benchmark implementation. Results are author-reported and have not been independently reproduced here.

## Inclusion rule

An improvement needs a primary source, a named benchmark and metric, a numerical baseline/candidate comparison, and enough model/setup information to interpret it. Claims stay within the measured setting. A bundled system comparison supports the bundle; only a controlled ablation supports attribution to an individual component. Benchmark evidence is not proof of universal capability.

Exclude unsupported design advice, standalone high scores, cross-vendor rankings with unmatched configurations, and training-set gains presented as generalization. Unknown cost, variance, or evaluation controls must be stated.

## Supported comparisons

| Improvement | Benchmark | Reported baseline → candidate | Scope |
|---|---|---|---|
| Hashline editing interface | 180 React mutation tasks | 6.7% → 68.3% | Grok Code Fast 1; model-dependent, narrower than software engineering |
| Deep Agents harness changes | Terminal-Bench 2.0 | 52.8% → 66.5% | Fixed GPT-5.2-Codex; bundled changes |
| Add trajectory notes to retrieval | LongMemEval-V2 Small / Medium | 42.8% → 51.0% / 38.1% → 45.9% | Same reader and retrieval family |
| Structured AgentRunbook-R retrieval | LongMemEval-V2 Small / Medium | 51.0% → 58.6% / 45.9% → 57.0% | More retrieval computation; not equal-cost evidence |
| AgentRunbook-C V2 controller bundle | LongMemEval-V2 Small | 69.90% → 75.61% | Same GPT-5.4-mini, xhigh; no isolated online-memory attribution |

These rows are separate experiments, not a leaderboard. Memory QA accuracy does not establish improved downstream task completion.

## Contents

- [Harness evidence](docs/evidence.md): sources, measured comparisons, and excluded claims.
- [Recent memory improvements](docs/memory-improvements.md): benchmark settings, latency, ablations, and limits.
- [Supported lessons](docs/lessons.md): narrow implications of these experiments.
- [Experiment framework](docs/experiment-framework.md): methodology for evaluating future additions; not itself a list of proven interventions.

## License

[MIT](LICENSE). The license covers this repository's original material. Referenced research, datasets, and third-party code retain their own licenses.
