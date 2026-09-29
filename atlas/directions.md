# Directions and repository boundaries

## Taxonomy

The taxonomy is a knowledge map. Cross-cutting items get one implementation home in the matrix; references from other domains are links, not duplicate implementations.

| Domain | Coverage in source / Atlas | Cross-cutting examples |
|---|---|---|
| Training Data & Scaling | weak source coverage; REP-032 queued | dedup affects scaling interpretation and evaluation |
| Model Architecture | decoder, MoE, MLA, GatedDeltaNet, DSA, MTP, AttnRes, mHC, Engram | attention intersects inference memory; Engram intersects memory |
| Pretraining / SFT | small causal LM and assistant-only masking candidates | data/tokenizer choices affect every downstream result |
| Post-training & Alignment | PPO, RLOO, ReMax, REINFORCE++, GRPO, DAPO, GDPO, DPO | GRPO also belongs to reasoning and verifier-based learning |
| Reasoning / Verification / Test-Time Scaling | GRPO, DAPO, s1 budget forcing, training-free GRPO | reward/verifier quality and inference budget are distinct axes |
| Distillation | forward/reverse KL, on-policy, ULD, embedding ranking | intersects compression and student deployment |
| Retrieval / Long Context / Memory | source has RAG demos; Atlas defers paged KV and isolates Engram | Health-Copilot owns application retrieval and memory |
| Agent / Tool Use / Harness | source demos, Search-R1/Agent0 adaptations | TraceSearch-R1 and Health-Copilot already have serious coverage |
| Multimodal | SigLIP loss and projector adaptation | visual tokens are an architecture and data interface |
| Efficiency / Training Systems / Inference Systems | weak source coverage; future systems queue | GQA/KV cache is in LLM-From-Scratch; larger serving systems deferred |
| Evaluation | source demos report task metrics, but no common robust eval harness | every experiment needs a small controlled metric |
| Interpretability | absent as a coherent source module; two P2 items | activation patching and SAE should use tiny known circuits/features first |
| Safety / Security | weak/absent isolated mechanism | prompt injection sandbox may be scoped inside Health-Copilot |
| Domain-specific / AI for Science | medical retrieval/document examples; no distinct research mechanism | date utility and OCR demos are archived |

### Cross-cutting placement rules

- GRPO has one implementation in PostTraining-From-Scratch; its reasoning/verifier relationship is documented in the experiment notes.
- GQA cache correctness lives with the foundational decoder; serving allocation and prefix reuse live in LLM-Systems-Lab.
- DSA and Engram live in the architecture lab even though they retrieve information; neither becomes a second RAG application.
- ULD and embedding ranking distillation live in Distillation-Lab, not a separate retrieval project.
- s1 budget forcing and training-free GRPO are inference-time reasoning studies. The latter never updates weights; its P2 study uses offline simulated memory.
- Evaluation work is attached to each reproduction’s minimal controlled experiment. A standalone evaluation framework is deferred unless a specific metric or benchmark question emerges.

## Satellite repository proposal

| Repository | Keep | Explicit boundary |
|---|---|---|
| LLM-From-Scratch | byte BPE, small decoder, SFT masking, GQA/KV cache, MoE, data dedup experiment | no production trainer, distributed runtime or copied framework |
| Modern-LLM-Architecture-Lab | one module per architecture mechanism, formula/shape/invariant check, optional microbenchmark | no broad model zoo and no claim of full paper reproduction from a toy block |
| PostTraining-From-Scratch | shared tiny categorical policy and explicit objective equations; PPO→RLOO/ReMax→GRPO→DAPO; optional DPO/GDPO | no agent/search environment, web UI, or production rollout service |
| Distillation-Lab | categorical KL through model/tokenizer/embedding transfer | no checkpoint hub or large-scale compression benchmark |
| Multimodal-From-Scratch | isolated pairwise objective and connector/packing path | no from-scratch vision tower or large pretraining pipeline in the initial scope |
| LLM-Systems-Lab | deferred kernel/cache/quantization/decoding studies | no serving product; Tier D only when the concept requires it |
| Interpretability-Lab | deferred causal interventions and SAE feature recovery | no general observability platform |

The first five form coherent study homes. The last two remain named future directions, not Phase A repositories. Do not create repositories until architecture review approves the boundaries.

## Compute and time conventions

| Tier | Target | Typical acceptable proof |
|---|---|---|
| A | laptop CPU, tiny synthetic tensors/corpus | equations, shapes, finite gradients, invariant or toy behavior |
| B | one 16GB GPU | tiny model/data runs; primary local target |
| C | one 40–48GB GPU | only where a pretrained encoder or larger activation materially teaches the concept |
| D | multi-GPU | avoid; justify per candidate, never inherit vendor recipe requirements blindly |

Expected time labels XS/S/M/L describe relative scope, not elapsed-time promises. Candidate experiments should avoid downloading checkpoints by default; use tiny initialized modules, synthetic inputs, or local assets only if already available.
