# LLM Reproduction Atlas

A planning index for small, controlled LLM learning/reproduction experiments. It records what to study, the minimum experiment, and the eligible learning repository that owns it.

## REP invariant

> A REP represents a concrete, independently completable learning/reproduction experiment.

Coverage can be established by a dedicated reproduction repository, a coursework repository whose purpose is learning/reimplementation, or an explicitly isolated reproduction extension. A formal production/research project does not establish REP coverage merely because it contains a related component. For every REP, evidence must come from an eligible learning/reproduction home.

The registry has REP-001 through REP-036: 34 active work items and 2 COVERED_EXISTING navigation items. REP-037 through REP-043 are retired; their source information remains in the [source audit](atlas/source-audit-wyf3.md) and [reference inventory](references/wyf3-llm-related.md).

## Study Tracks

Conceptual learning paths. A Study Track does not imply a dedicated repository.

- Foundations: tokenization, decoder stack, optimization, training loop, data and scaling.
- Modern Architecture: MLA, GatedDeltaNet, DSA, MTP, hybrid blocks, Attention Residuals, mHC, Engram and MoE.
- Post-training: policy-gradient baselines, PPO/GAE, RLOO/ReMax, GRPO/DAPO, GDPO and DPO.
- Distillation: KL geometry, token-logit KD, on-policy KD, ULD and embedding transfer.
- Multimodal: SigLIP objective and vision-language connectors.
- Systems: attention IO, paged KV, quantization and speculative decoding.
- Interpretability: causal activation interventions and sparse autoencoders.
- Cross-cutting studies include reasoning, memory, retrieval, agents and evaluation.

See [directions](atlas/directions.md), the [matrix](atlas/matrix.md), and the [dependency map](atlas/dependency-map.md).

## Implementation Homes

### Existing learning/reproduction homes

- [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420): foundational coursework; finish its unfinished assignment adapters before adding isolated extensions.
- [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf): post-training coursework; complete its DPO scaffold and host distinct educational experiments.

### Potential future reproduction homes

- Modern-LLM-Architecture-Lab
- Distillation-Lab
- Multimodal-From-Scratch

### Deferred

- LLM-Systems-Lab
- Interpretability-Lab

## Formal Project Boundaries

Formal-project implementation status is not REP completion evidence.

### TraceSearch-R1

Bubblevan/TraceSearch-R1 is an active formal search-agent/RL project. It may inform Atlas scope and integration decisions, but it is not an Atlas reproduction repository, does not provide REP coverage, and is not a project Atlas must reproduce in full for completeness.

### Health-Copilot

Bubblevan/Health-Copilot is an active formal retrieval/memory/multi-agent/harness project. It may inform scope and integration decisions, but it is not an Atlas reproduction repository and does not provide REP coverage. The presence of a memory, retrieval or agent component does not mean a separately specified Atlas mechanism has been reproduced.

## Revised P0 queue

There are 11 active P0 items. REP-008 GRPO is covered by CS336-A5 and is navigation-only.

1. REP-001 — complete CS336-A1 BPE/tokenizer adapters.
2. REP-002 — complete CS336-A1 TransformerBlock/TransformerLM, optimizer, schedule, clipping, checkpoint and tiny end-to-end training.
3. REP-003 — extend CS336-A1 with GQA and incremental KV cache.
4. REP-004 — extend CS336-A1 with MoE, outside official assignment content.
5. REP-005 — add the two-action bandit variance experiment in CS336-A5.
6. REP-006 — add critic/value loss and GAE/bootstrapping in CS336-A5.
7. REP-007 — add RLOO/ReMax estimators in CS336-A5.
8. REP-009 — add isolated DAPO components in CS336-A5.
9. REP-010 — KL direction/support experiment.
10. REP-011 — same-tokenizer token-logit distillation.
11. REP-012 — on-policy token distillation.

REP-013 response-only masking is also covered by CS336-A5 and removed from active work. REP-034 is an independent P2 reproduction with no home assigned yet. See the [repository audit](atlas/existing-repository-audit.md) for eligible-project evidence and formal-project boundaries.
