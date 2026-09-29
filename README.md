# LLM Reproduction Atlas

A lightweight index for small, controlled reproductions of LLM algorithms and architecture mechanisms. This repository is a planning Atlas, not an implementation monorepo. It records what to study, where an idea came from, the smallest experiment that would demonstrate understanding, and which project should own it.

## Purpose and boundaries

The audited source is [wyf3/llm_related](https://github.com/wyf3/llm_related), pinned locally at a492338499a9381f1714ecda8c802684e0556d3e. Its useful pattern is repeated small experiments; its directory structure and implementation choices are not adopted as this Atlas architecture. See the [source audit](atlas/source-audit-wyf3.md) and [pinned reference inventory](references/wyf3-llm-related.md).

Phase A contains documentation only. No model or dataset assets are stored here. A reproduction is complete when it demonstrates a mechanism through a correct formula, shape/gradient checks, an invariant or equivalence, a loss trend, a qualitative behavior, or a measured tradeoff. Full-paper benchmark parity is not required for a mechanism study.

## Domain map

The [taxonomy and directions](atlas/directions.md) map 14 areas: training data and scaling; model architecture; pretraining/SFT; post-training/alignment; reasoning and test-time scaling; distillation; retrieval/long context/memory; agents/tool use/harness; multimodal; training and inference systems; evaluation; interpretability; safety/security; and domain-specific AI. A mechanism can appear in several domains but has one implementation home.

## Proposed satellite repositories

- **LLM-From-Scratch** — tokenizer, tiny decoder pretraining/SFT, attention/KV cache, MoE fundamentals.
- **Modern-LLM-Architecture-Lab** — isolated MLA, GatedDeltaNet, DSA, MTP, AttnRes, mHC and Engram mechanisms.
- **PostTraining-From-Scratch** — small policy-gradient/PPO/RLOO/ReMax/GRPO/DAPO/DPO experiments; no rollout platform.
- **Distillation-Lab** — KL geometry, token logit KD, on-policy KD, ULD and embedding ranking transfer.
- **Multimodal-From-Scratch** — isolated SigLIP loss and small vision-language connector experiments.
- **LLM-Systems-Lab** — deferred queue for attention kernels, paged KV, quantization and speculative decoding.
- **Interpretability-Lab** — deferred queue for causal tracing and sparse autoencoders.

Boundaries and cross-links live in [directions.md](atlas/directions.md). Generic RAG/agent toy repositories are excluded: Health-Copilot already covers retrieval, reranking, memory, evaluation and tool execution. TraceSearch-R1 already covers search-agent RL, GRPO-style training, rollouts, rewards, verifiers and tool environments. The post-training satellite remains a minimal algorithm lab.

## First P0 queue

1. REP-001 byte-level BPE tokenizer
2. REP-002 tiny decoder-only Transformer
3. REP-003 GQA and incremental KV cache
4. REP-004 sparse top-k MoE routing
5. REP-005 policy gradient and baseline
6. REP-006 PPO clipping and GAE
7. REP-007 RLOO/ReMax baseline comparison
8. REP-008 GRPO group-relative advantages
9. REP-009 selected DAPO components
10. REP-010 KL direction and support coverage
11. REP-011 same-tokenizer token logit KD
12. REP-012 on-policy token distillation

The dependencies and weekend-sized entry points are in [dependency-map.md](atlas/dependency-map.md). All 43 matrix candidates are seeded with 12 P0, 16 P1, 8 P2 and 7 ARCHIVE items.

## Source limits and evidence

The source audit records actual files and the commit. Names ending in “from_scratch” are treated as claims to verify: several modules load pretrained encoders, use TRL/HF training loops, or implement only selected architecture components. Exact vendored verl snapshot SHAs, the specific provenance of dpsk_v4_attention.py, and the gptpdf revision behind pdf2markdown remain UNVERIFIED.

Use the templates for a future reproduction plan, experiment record and satellite README. Phase A stops here; architecture review precedes Phase B.
