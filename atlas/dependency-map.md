# Dependency map

This graph encodes useful implementation order, not scientific importance. Each node has one implementation home; cross-domain links are noted in atlas/directions.md.

## Core learning paths

~~~mermaid
flowchart TD
  TOK[REP-001 BPE tokenizer] --> LM[REP-002 tiny decoder LM]
  LM --> CACHE[REP-003 GQA and KV cache]
  LM --> MOE[REP-004 MoE routing]
  LM --> SFT[REP-013 assistant-only SFT mask]
  LM --> MLA[REP-015 MLA]
  LM --> GDN[REP-016 GatedDeltaNet]
  LM --> DSA[REP-017 DSA indexer]
  LM --> MTP[REP-018 MTP heads]
  GDN --> QNEXT[REP-019 Qwen3-Next hybrid]
  MLA --> QNEXT
  MTP --> QNEXT
  LM --> ATT[REP-020 Attention Residuals]
  LM --> MHC[REP-021 mHC]
  LM --> ENG[REP-022 Engram]
  LM --> VLM[REP-026 vision-language connector]
  SIG[REP-025 SigLIP objective] --> VLM

  PG[REP-005 policy gradient and baseline] --> PPO[REP-006 PPO and GAE]
  PPO --> RR[REP-007 RLOO / ReMax]
  RR --> GRPO[REP-008 GRPO]
  GRPO --> DAPO[REP-009 DAPO components]
  GRPO --> GDPO[REP-033 GDPO normalization]
  DPO[REP-014 DPO] -. preference objective .-> PPO
  GRPO --> TFG[REP-034 training-free memory comparison]

  KL[REP-010 KL geometry] --> KD[REP-011 same-token logit KD]
  KD --> ON[REP-012 on-policy KD]
  KD --> ULD[REP-023 ULD]
  KL --> ULD
  KD --> EMB[REP-024 embedding ranking KD]

  CACHE --> PAGED[REP-029 paged KV simulator]
  CACHE --> FLASH[REP-028 tiled attention]
  CACHE --> SPEC[REP-031 speculative decoding]
  LM --> QUANT[REP-030 weight quantization]
  LM --> DATA[REP-032 data dedup / small scaling]
  LM --> PATCH[REP-035 activation patching]
  PATCH --> SAE[REP-036 SAE]
  BUDGET[REP-027 s1 budget controller]
~~~

## Weekend entry points

These can start with no prerequisite training run:

- **REP-001** — tokenizer on a hand-written corpus.
- **REP-005** — categorical bandit policy and baseline.
- **REP-010** — two categorical distributions and KL gradients.
- **REP-028** — dense vs tiled attention on a tiny tensor.
- **REP-029** — request/block allocator simulation.
- **REP-030** — quantize a fixed small matrix.
- **REP-031** — draft/target categorical sampler.
- **REP-032** — deduplicate a small text sample.
- **REP-035** — activation patching on a toy transformer with a known behavior.
- **REP-036** — SAE over generated activations with known factors.

Model-based paths begin after REP-002. Policy-gradient order begins at REP-005; PPO is a helpful bridge before comparing RLOO/ReMax and implementing GRPO. KD order begins with probability-space KL, before token alignment and on-policy states. These dependencies are pedagogical; a reproduction should record what was skipped.
