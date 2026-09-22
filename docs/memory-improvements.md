# Recent memory improvements supported by benchmarks

Reviewed 2026-09-22. Author-reported results; not independently reproduced here. Improvements apply to the evaluated configurations, not to memory systems in general. Percentage-point differences are absolute.

## 1. Retrieval notes and structured retrieval — May 2026

Source: [LongMemEval-V2, Table 2](https://arxiv.org/html/2605.12493v1#S5.T2).
Code: [official repository](https://github.com/xiaowu0162/LongMemEval-V2).

| Method | Small accuracy | Medium accuracy | Small / Medium query latency |
|---|---:|---:|---:|
| Raw-slice RAG | 42.8% | 38.1% | 0.1s / 0.1s |
| Slices plus notes | 51.0% | 45.9% | 0.2s / 0.3s |
| AgentRunbook-R | 58.6% | 57.0% | 26.9s / 25.8s |

Fixed Qwen3.5-9B reader/controller and Qwen3-Embedding-8B embeddings. The benchmark has 451 questions; returned evidence is capped at 200K tokens. It measures answering questions about stored trajectories, not executing future tasks.

Adding notes improves accuracy by 8.2/7.8 points. Structured retrieval improves another 7.6/11.1 points, with substantially higher latency. Removing the raw-slice pool lowers AgentRunbook-R to 42.3%/33.5%: retaining original evidence matters in this configuration.

Limits: retrieval computation differs; latency excludes a full lifecycle cost comparison. These measurements do not prove equal-cost gains or isolated benefits of every memory representation.

## 2. Lightweight controller plus accumulated retrieval experience — August 2026

Source: [AgentRunbook-C V2 research update, final comparison table](https://xiaowu0162.github.io/longmemeval-v2/agentrunbook-c-v2/).
Code: [controller](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/memory_modules/agentrunbook_c_v2.py), [online learning](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/memory_modules/agentrunbook_online_learning.py).

LongMemEval-V2 Small; GPT-5.4-mini, xhigh reasoning:

| System | Accuracy | Average online query latency |
|---|---:|---:|
| Vanilla Codex | 69.90% | 177.20s |
| AgentRunbook-C V1 | 74.90% | 108.30s |
| AgentRunbook-C V2 | 75.61% | 130.54s |

V2 gains 5.71 points over vanilla and 0.71 over V1. It is faster than vanilla but slower than V1 at this setting. The bundle uses a simpler controller and consolidation of reusable retrieval experience into strategy notes without answer labels.

Limits: no isolated online-memory gain established here; no repeated-run uncertainty or consolidation-inclusive cost accounting in this table. The page's opening medium-effort figures differ from its final table; this entry uses only the explicitly labeled xhigh table values.

## Excluded from the improvement list

- Agent Zero's standalone scores and cross-paper rankings: unmatched model/system settings do not isolate an improvement.
- Generic recommendations about graphs, provenance, forgetting, or additional agents without a qualifying comparison.
- Claims that these QA gains demonstrate better real-world task execution. That requires a separate downstream evaluation.
