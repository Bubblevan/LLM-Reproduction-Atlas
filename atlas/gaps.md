# Gap analysis

This file describes candidate learning questions; formal-project implementation state is not REP coverage. Project boundary definitions live in [directions](directions.md) and [the existing-repository audit](existing-repository-audit.md).

| Gap / topic | Learning/reproduction evidence | Why it matters | Feasible focused study | Priority |
|---|---|---|---|---|
| Training data quality and deduplication | No controlled study in CS336-A1/A5 | Duplicates affect effective token budget and validation conclusions | Exact/MinHash dedup with a small controlled corpus/model sweep | P2 REP-032 |
| Scaling laws | No controlled scaling experiment | Helps interpret model/data/compute allocation | Small run with explicit toy limitations | P2 REP-032 |
| FlashAttention / IO-aware attention | No faithful tiled kernel identified | Memory traffic constrains attention | Online-softmax reference, equivalence and memory accounting | P1 REP-028 |
| Long-context methods | No broad focused evaluation | Context length affects quality and retrieval | Length/generalization sweep with one mechanism | Deferred |
| Serving and paged KV | No serving scheduler in learning homes | Throughput, fragmentation and prefix sharing matter | Allocator/request simulator | P2 REP-029 |
| Quantization | No focused study | Memory/quality tradeoff affects deployment | Tiny layer and groupwise low-bit error comparison | P2 REP-030 |
| Speculative decoding | No candidate implementation | Connects draft quality to target-call savings | Exactness proof with categorical sampler | P2 REP-031 |
| Test-time scaling and budget control | No verified budget-forcing reproduction | Separates inference compute from training | Stub controller then optional small model | P1 REP-027 |
| Verifier/process reward models | No isolated calibration study | Reward validity matters in reasoning training | Tiny labels and calibration/error analysis | Deferred |
| Evaluation discipline | No shared versioned protocol | Prevents leakage and metric drift | Per-reproduction controlled metric | Cross-cutting |
| Mechanistic interpretability | No focused module | Causal tests explain computation | Activation patching on a small known task | P2 REP-035 |
| Sparse autoencoders | No focused module | Studies sparse feature/reconstruction tradeoff | Synthetic activations with known factors | P2 REP-036 |
| Safety / prompt injection | No focused isolated experiment | Tool systems need trust boundaries | Bounded adversarial sandbox/eval if distinct mechanism is selected | Deferred |
| Tensor/pipeline/expert parallel, ZeRO | No minimal learning implementation | Distributed layout determines communication | Small formulas/simulator; hardware proof later | Deferred |
| PDF/table extraction | Application integration, not an isolated LLM mechanism | Useful document engineering | Keep as source reference, not REP | Source-only |
| Domain-specific AI | No distinctive isolated mechanism | Domain data changes evaluation assumptions | No standalone candidate identified | Deferred |

The Atlas prioritizes bounded algorithm and architecture questions. Application integration and formal-project scope remain context; they cannot replace an independently completable REP experiment.
