# Dependency map

This graph orders mechanisms and learning prerequisites, not repositories. Each node resolves to its actual Implementation Home in the matrix. A Study Track does not imply a dedicated repository.

~~~mermaid
flowchart TD
  TOK[REP-001 tokenizer: CS336-A1] --> LM[REP-002 tiny LM: CS336-A1]
  LM --> CACHE[REP-003 GQA/KV cache: CS336-A1 extension]
  LM --> MOE[REP-004 MoE: CS336-A1 extension]
  LM --> SFT[REP-013 response mask: CS336-A5, covered]
  LM --> MLA[REP-015 MLA: architecture candidate]
  LM --> GDN[REP-016 GatedDeltaNet: architecture candidate]
  LM --> DSA[REP-017 DSA indexer: architecture candidate]
  LM --> MTP[REP-018 MTP heads: architecture candidate]
  GDN --> QNEXT[REP-019 Qwen3-Next hybrid]
  MLA --> QNEXT
  MTP --> QNEXT
  LM --> ATT[REP-020 Attention Residuals]
  LM --> MHC[REP-021 mHC]
  LM --> ENG[REP-022 Engram]
  LM --> VLM[REP-026 vision-language connector]
  SIG[REP-025 SigLIP objective] --> VLM
  PG[REP-005 bandit baseline: CS336-A5 extension] --> PPO[REP-006 PPO and GAE: CS336-A5 extension]
  PPO --> RR[REP-007 RLOO/ReMax: CS336-A5 extension]
  RR --> GRPO[REP-008 GRPO: CS336-A5, covered]
  GRPO --> DAPO[REP-009 DAPO: CS336-A5 extension]
  GRPO --> GDPO[REP-033 GDPO: CS336-A5 extension]
  DPO[REP-014 DPO: CS336-A5 scaffold] -. preference objective .-> PPO
  GRPO --> TFG[REP-034 memory method: Health-Copilot read-only boundary]
  KL[REP-010 KL geometry: Distillation candidate] --> KD[REP-011 same-token logit KD]
  KD --> ON[REP-012 on-policy KD]
  KD --> ULD[REP-023 ULD]
  KL --> ULD
  KD --> EMB[REP-024 embedding ranking KD]
  CACHE --> PAGED[REP-029 paged KV: deferred Systems]
  CACHE --> FLASH[REP-028 tiled attention: deferred Systems]
  CACHE --> SPEC[REP-031 speculative decoding: deferred Systems]
  LM --> QUANT[REP-030 quantization: deferred Systems]
  LM --> DATA[REP-032 dedup/scaling: CS336-A1 extension]
  LM --> PATCH[REP-035 activation patching: deferred Interpretability]
  PATCH --> SAE[REP-036 SAE: deferred Interpretability]
  BUDGET[REP-027 s1 controller: CS336-A5 extension candidate]
  TRACE[TraceSearch-R1: search-agent RL and provenance]
  HEALTH[Health-Copilot: retrieval, memory, agents and evaluation]
~~~

## Weekend entry points

- REP-001 — complete tokenizer adapters in CS336-A1 on a hand-written corpus.
- REP-005 — categorical bandit policy/baseline in CS336-A5.
- REP-010 — categorical distributions and KL gradients in Distillation-Lab.
- REP-028 — dense vs tiled attention on a tiny tensor; deferred Systems candidate.
- REP-029 — request/block allocator simulation; deferred Systems candidate.
- REP-030 — quantize a fixed small matrix; deferred Systems candidate.
- REP-031 — draft/target categorical sampler; deferred Systems candidate.
- REP-032 — deduplicate a small sample under a CS336-A1 extension path.
- REP-035 — activation patching on a toy transformer; deferred Interpretability.
- REP-036 — SAE over generated activations with known factors; deferred Interpretability.

Model paths begin after REP-002 in CS336-A1. PPO/GAE is distinct from GRPO clipping; GRPO is already covered by CS336-A5 and is not duplicated. KD begins with probability-space KL before token alignment and on-policy states. Record skipped prerequisites in each future reproduction.
