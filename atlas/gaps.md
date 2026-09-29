# Gap analysis

The audit is pinned to a492338499a9381f1714ecda8c802684e0556d3e. “Missing” means the repository does not provide a focused, evidence-backed reproduction of the mechanism; a demo or a folder name is not treated as coverage.

| Gap / topic | Source coverage | Why it matters | Existing project coverage | Feasible minimal reproduction | Priority |
|---|---|---|---|---|---|
| Training data quality and deduplication | No reproducible data-quality study identified | Duplicate rate and filtering can change effective token budget and validation conclusions | None documented | Yes: exact/MinHash dedup, controlled small corpus/model sweep | P2 REP-032 |
| Scaling laws | No controlled scaling experiment | Helps interpret model/data/compute allocation | None documented | Yes, but small runs demonstrate trend noisily; label as toy | P2 REP-032 |
| FlashAttention / IO-aware attention | No faithful tiled kernel identified; standard attention only | Attention memory traffic is a central systems constraint | None | Yes: online softmax reference, numerical equivalence, intermediate-memory accounting | P1 REP-028 |
| Long-context positional methods and retrieval | Sparse DSA-like indexer exists; no broad long-context evaluation | Context length affects quality, memory and retrieval behavior | Health-Copilot covers application retrieval | Feasible later: length/generalization sweep and one mechanism | Deferred |
| Serving, continuous batching, paged KV and prefix cache | GQA/KV basics in decoder; no serving scheduler | Throughput, fragmentation and prefix sharing matter in deployment | Health-Copilot may host application serving, not kernel-level mechanism | Yes: allocator/request simulator first | P2 REP-029 |
| Quantization | No focused quantization study | Memory/quality tradeoff affects deployment feasibility | None | Yes: tiny linear layer and groupwise 4-bit error comparison | P2 REP-030 |
| Speculative decoding | No candidate implementation identified | Connects draft-model quality to target-call savings | None | Yes: categorical exactness proof and call count | P2 REP-031 |
| Test-time scaling and budget control | s1 is a pretrained fine-tune/demo; no verified budget-forcing reproduction | Separates more inference compute from more training | TraceSearch-R1 handles agentic search rollouts, not general budget curves | Yes: stub controller then optional small model | P1 REP-027 |
| Verifier / process reward models | RL examples have scalar reward functions; no isolated PRM/verifier calibration study | Reward validity is a major failure mode in reasoning training | TraceSearch-R1 covers reward/verifier engineering in its domain | Yes: tiny step labels and calibration/error analysis; overlap-aware | Deferred; consider only with distinct question |
| Evaluation discipline | No shared, versioned evaluation protocol across modules | Prevents improvements from prompt/data leakage or metric drift | Health-Copilot has project evaluation scope | Yes, as a per-reproduction controlled metric, not a new eval framework | Cross-cutting |
| Mechanistic interpretability | No focused module identified | Causal tests explain internal computation beyond behavior metrics | None | Yes: activation patching on a small known task | P2 REP-035 |
| Sparse autoencoders | No focused module identified | Learn sparse feature bases and study reconstruction/sparsity tradeoff | None | Yes, synthetic activations provide known ground truth | P2 REP-036 |
| Safety / prompt injection | No focused security experiment identified | Tool-using systems need explicit trust boundaries and adversarial tests | Health-Copilot covers agent/runtime scope | Feasible as a contained sandbox/eval, but no new Atlas candidate until distinct mechanism is chosen | Deferred |
| Tensor/pipeline/expert parallel, ZeRO | No local minimal implementation identified; vendor trees include framework code | Distributed layouts determine scale and communication cost | TraceSearch-R1 may depend on distributed execution | Small formulas/simulator feasible; genuine systems proof requires multiple devices | Deferred; Tier D only with hardware and a concrete question |
| Process-level document extraction / OCR | PDF and table demos exist | Useful domain engineering, but not LLM mechanism evidence | Potential Health-Copilot document needs | Feasible as application work, not Atlas reproduction | ARCHIVE |
| Domain-specific / AI for Science | Medical corpus demo only | Domain data can change objective and evaluation assumptions | Health-Copilot has medical use case | No standalone candidate from current audit | Deferred |

## Interpretation

Highest-value absent material is systems knowledge (tiled attention, KV allocation, quantization, speculative decoding), data/scaling methodology, and causal interpretability. The first systems item gets P1 because it is a bounded foundational mechanism; other items remain P2. The repository’s most visible weakness is that impressive labels sometimes wrap pretrained models or trainer adaptations; the Atlas therefore separates mechanism studies from source-folder names.

Search-Agent verification, reward design and tool environments are already serious TraceSearch-R1 territory. General retrieval, reranking, memory and agent harness work are already Health-Copilot territory. New Atlas candidates must isolate a different mechanism rather than recreate those stacks.


## Existing project boundaries

Exact implementation/test evidence for CS336-A1, CS336-A5, TraceSearch-R1 and Health-Copilot is in the [existing-repository audit](existing-repository-audit.md). Generic retrieval, memory, agents, harness/runtime and retrieval evaluation stay with Health-Copilot; agentic RL, rollouts, verifier/reward integration and trajectory provenance stay with TraceSearch-R1.
