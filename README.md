# LLM Reproduction Atlas

A lightweight index for small, controlled reproductions of LLM algorithms and architecture mechanisms. This is a planning Atlas, not an implementation monorepo. It records what to study, the smallest experiment that demonstrates the mechanism, and the repository that owns any implementation.

## Purpose and boundaries

The audited source is [wyf3/llm_related](https://github.com/wyf3/llm_related), pinned at a492338499a9381f1714ecda8c802684e0556d3e. Its small-experiment pattern is useful; its directory structure and implementation choices are not adopted as this Atlas architecture. See the [source audit](atlas/source-audit-wyf3.md), [pinned reference inventory](references/wyf3-llm-related.md), and [existing-repository reconciliation](atlas/existing-repository-audit.md).

Phase A and A.1 are documentation and audit only. No model or dataset assets are stored here. A reproduction can establish a mechanism through formulas, shape/gradient checks, an invariant or equivalence, a loss trend, qualitative behavior, or a measured tradeoff. Full-paper benchmark parity is not required for a mechanism study.

## Study Tracks

These are conceptual learning paths. A Study Track does not imply a dedicated repository.

- Foundations: tokenizer, decoder stack, optimization, data quality and scaling.
- Modern Architecture: MLA, GatedDeltaNet, DSA, MTP, hybrid blocks, Attention Residuals, mHC and Engram.
- Post-training: policy-gradient baselines, PPO/GAE, RLOO/ReMax, GRPO/DAPO, GDPO and DPO.
- Distillation: KL geometry, token-logit KD, on-policy KD, ULD and embedding transfer.
- Multimodal: SigLIP objective and vision-language connector experiments.
- Systems: attention IO, paged KV, quantization and speculative decoding.
- Interpretability: causal activation interventions and sparse autoencoders.
- Cross-cutting tracks include test-time reasoning, retrieval, memory, agents and evaluation.

See [taxonomy and boundaries](atlas/directions.md) and the [matrix](atlas/matrix.md).

## Implementation Homes

Existing repositories own coherent implementation work:

- [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420): foundational assignment; finish unfinished adapters and end-to-end tiny LM path before adding extensions.
- [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf): post-training fundamentals; complete the DPO scaffold and extend for distinct textbook experiments.
- [Bubblevan/TraceSearch-R1](https://github.com/Bubblevan/TraceSearch-R1/tree/db2246ff0f418d799742c17ee4dde28a3a322ba0): advanced search-agent RL, grouped rollouts, environments, verifier/reward integration and trajectory provenance.
- [Bubblevan/Health-Copilot](https://github.com/Bubblevan/Health-Copilot/tree/9e023dbddc1f8025e3608bfae4c5390c1a7957ef): applied retrieval, memory, agent/runtime, multi-agent and retrieval evaluation.

Potential new repositories, only if a later architecture review approves them:

- Modern-LLM-Architecture-Lab
- Distillation-Lab
- Multimodal-From-Scratch

Deferred: LLM-Systems-Lab and Interpretability-Lab. No repository was created in Phase A.1. The former LLM-From-Scratch and PostTraining-From-Scratch proposals are removed.

## Revised P0 queue

There are 11 active P0 items. REP-008 GRPO is covered and is navigation-only.

1. REP-001 — complete CS336-A1 byte-level BPE/tokenizer adapters.
2. REP-002 — complete CS336-A1 TransformerBlock/TransformerLM, optimizer, schedule, clipping, checkpoint and tiny end-to-end training.
3. REP-003 — extend CS336-A1 with GQA and incremental KV cache.
4. REP-004 — extend CS336-A1 with MoE, outside official assignment content.
5. REP-005 — add two-action bandit variance experiment in CS336-A5.
6. REP-006 — add critic/value loss and GAE/bootstrapping in CS336-A5.
7. REP-007 — add RLOO/ReMax estimators in CS336-A5.
8. REP-009 — extend CS336-A5 with separately tested DAPO components.
9. REP-010 — KL direction/support experiment.
10. REP-011 — same-tokenizer token-logit distillation.
11. REP-012 — on-policy token distillation.

REP-013 response-only masking is also COVERED_EXISTING and removed from active work. REP-014 DPO remains SCAFFOLDED in CS336-A5 and should be completed there. See the [dependency map](atlas/dependency-map.md), [repository audit](atlas/existing-repository-audit.md), and [matrix](atlas/matrix.md). The source catalog still has 43 candidates; 34 are active after reconciliation.
