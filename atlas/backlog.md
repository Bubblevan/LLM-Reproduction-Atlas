# Backlog

The REP registry contains REP-001 through REP-036: 34 active work items and 2 covered navigation items. Every active item starts at BACKLOG. Formal-project implementation status never establishes REP coverage.

## REP-001 — Byte-level BPE tokenizer

Status: BACKLOG  
Priority: P0  
Study Track: Foundations<br>
Implementation Home: [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420)<br>
Coverage: SCAFFOLDED<br>
Action: COMPLETE_EXISTING<br>
Existing implementation evidence: [tests/adapters.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/tests/adapters.py): get_tokenizer and run_train_bpe remain NotImplementedError adapters; tokenizer tests specify behavior, but student-facing implementation is scaffolded. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: BPE  
Source inspiration: [train_llm_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch)

### Question

How do merge operations define a stable, reversible vocabulary?

### Minimal implementation

Complete the existing CS336-A1 tokenizer adapters for deterministic byte-level BPE training and encode/decode; expose vocabulary and lengths.

### Minimal experiment

Round-trip mixed text; compare token counts before/after merges.

### Completion gate

CS336-A1 tokenizer tests pass; mixed UTF-8 round trips hold; merges are deterministic and repeated substrings compress.

### Stretch goals

Unicode edges and pre-tokenization.

### Do NOT do

Do not use a production tokenizer library for the core algorithm or a large corpus.

## REP-002 — Tiny decoder-only Transformer

Status: BACKLOG  
Priority: P0  
Study Track: Foundations<br>
Implementation Home: [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420)<br>
Coverage: PARTIAL_EXISTING<br>
Action: COMPLETE_EXISTING<br>
Existing implementation evidence: Implemented components in [cs336_basics/layers.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/cs336_basics/layers.py), [cs336_basics/attention.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/cs336_basics/attention.py), [cs336_basics/nn_utils.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/cs336_basics/nn_utils.py); tests [tests/test_model.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/tests/test_model.py), [tests/test_nn_utils.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/tests/test_nn_utils.py). TransformerBlock/TransformerLM/training adapters remain unfinished; no end-to-end tiny LM trainer found. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-001 is useful for the full language path; a tokenizer stub is acceptable.  
Reference: GPT-style causal LM  
Source inspiration: [train_llm_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch)

### Question

Which components are needed for next-token learning on a tiny corpus?

### Minimal implementation

Complete the existing CS336-A1 TransformerBlock/TransformerLM in place. Finish batch sampling, AdamW, cosine schedule/warmup, gradient clipping and checkpoint serialization around the implemented Linear, Embedding, RMSNorm, SwiGLU, attention, RoPE, MHA and cross-entropy components.

### Minimal experiment

Overfit tiny text; record loss and sample continuations.

### Completion gate

Required CS336-A1 component and integration tests pass; masks and shapes are correct; gradients are finite; checkpoint round-trip works; a tiny end-to-end LM run shows falling loss and generation from trained weights.

### Stretch goals

Compare positions or MHA/GQA.

### Do NOT do

Do not reproduce large checkpoints or trainer ecosystems.


This gate completes the CS336-A1 assignment stack in place; it does not create another tiny Transformer implementation.
## REP-003 — GQA and incremental KV cache

Status: BACKLOG  
Priority: P0  
Study Track: Foundations / Systems<br>
Implementation Home: [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420) / extensions/gqa_kv_cache (planned; not created)<br>
Coverage: PARTIAL_EXISTING<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: MHA/attention in [cs336_basics/attention.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/cs336_basics/attention.py) and [tests/test_model.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/tests/test_model.py); no GQA head sharing or incremental KV cache found in the five repositories. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2305.13245)  
Source inspiration: [train_llm_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch)

### Question

How does KV head sharing reduce cache size while preserving attention?

### Minimal implementation

Implement full/incremental attention and per-layer KV cache.

### Minimal experiment

Compare cached logits to full-prefix logits; count bytes.

### Completion gate

Logits agree within tolerance; cache grows by one token and scales with KV heads.

### Stretch goals

Measure decode latency.

### Do NOT do

Do not build a serving server or fused kernel.

## REP-004 — Sparse top-k MoE routing

Status: BACKLOG  
Priority: P0  
Study Track: Foundations / Modern Architecture<br>
Implementation Home: [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420) / extensions/moe (planned; not created)<br>
Coverage: NONE<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: No MoE router/expert implementation or targeted test found in the five repositories. Planned extension path is outside official A1 content. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2101.03961)  
Source inspiration: [train_moe_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_moe_from_scratch)

### Question

How do top-k routing and balance loss affect expert use?

### Minimal implementation

Implement top-k gate, expert MLPs, weighted combine and balance statistic.

### Minimal experiment

Route balanced/skewed synthetic tokens; inspect counts and gradients.

### Completion gate

Selection/output match equations; balance responds to skew.

### Stretch goals

Tiny MoE LM vs equal-size dense model.

### Do NOT do

Do not add distributed expert parallelism.

## REP-005 — Policy gradient with a baseline

Status: BACKLOG  
Priority: P0  
Study Track: Post-training<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf) / extensions/policy_gradient_bandit (planned; not created)<br>
Coverage: PARTIAL_EXISTING<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: Related policy-gradient primitives in [cs336_alignment/reasoning/grpo_loss.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/cs336_alignment/reasoning/grpo_loss.py), tested by [tests/test_grpo.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/tests/test_grpo.py); no Atlas two-action-bandit variance experiment. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/1707.06347)  
Source inspiration: [ppo_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/ppo_from_scratch)

### Question

What changes with a baseline, and what must remain invariant?

### Minimal implementation

Categorical policy, score-function gradient, return, constant/learned baseline.

### Minimal experiment

Two-action bandit; compare gradient mean and variance across samples.

### Completion gate

Expected gradient targets same objective; variance comparison is seeded and reported.

### Stretch goals

Reward-to-go or entropy bonus.

### Do NOT do

Do not add language models or rollout services.

## REP-006 — PPO clipping and GAE

Status: BACKLOG  
Priority: P0  
Study Track: Post-training<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf) / extensions/ppo_gae (planned; not created)<br>
Coverage: PARTIAL_EXISTING<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: GRPO-style clipping in [cs336_alignment/reasoning/grpo_loss.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/cs336_alignment/reasoning/grpo_loss.py)/[tests/test_grpo.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/tests/test_grpo.py); no critic/value loss, GAE or bootstrap estimator found. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-005; REP-006 is a helpful bridge before estimator variants and group-relative objectives.  
Reference: [reference 1](https://arxiv.org/abs/1707.06347)  
Source inspiration: [ppo_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/ppo_from_scratch)

### Question

How do PPO clipping and GAE bound policy updates?

### Minimal implementation

Implement ratio, clipped surrogate, value loss and reverse-time GAE.

### Minimal experiment

Compare clipped/unclipped updates and GAE with discounted returns.

### Completion gate

Boundary equations match; finite gradients; lambda=1/value=0 matches MC returns.

### Stretch goals

Sweep clip range/lambda.

### Do NOT do

Do not build distributed RLHF infrastructure.

## REP-007 — RLOO and ReMax baselines

Status: BACKLOG  
Priority: P0  
Study Track: Post-training<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf) / extensions/rloo_remax (planned; not created)<br>
Coverage: NONE<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: No explicit RLOO/ReMax estimator or targeted test found in CS336-A5 or the eligible learning/reproduction repository CS336-A5. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-005; REP-006 is a helpful bridge before estimator variants and group-relative objectives.  
Reference: [reference 1](https://arxiv.org/abs/2402.14740), [reference 2](https://arxiv.org/abs/2310.10505)  
Source inspiration: [rloo](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rloo), [remax](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/remax)

### Question

How do leave-one-out and greedy baselines affect estimator variance?

### Minimal implementation

Compute RLOO and ReMax advantages from shared sample/reward tensors.

### Minimal experiment

Hold samples fixed; compare formula and empirical gradient variance.

### Completion gate

Manual formulas check; fixed-seed variance result is reproducible.

### Stretch goals

Add learned value baseline as reference.

### Do NOT do

Do not compare end-to-end model scores or inherit TRL loops.

## REP-009 — DAPO selected components

Status: BACKLOG  
Priority: P0  
Study Track: Post-training<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf) / extensions/dapo (planned; not created)<br>
Coverage: PARTIAL_EXISTING<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: Related GRPO/Dr.GRPO primitives in [cs336_alignment/reasoning/grpo_advantage.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/cs336_alignment/reasoning/grpo_advantage.py), [cs336_alignment/reasoning/grpo_loss.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/cs336_alignment/reasoning/grpo_loss.py), [tests/test_grpo.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/tests/test_grpo.py); no Clip-Higher, dynamic sampling/zero-variance filter or complete DAPO-specific overlong handling. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-005; REP-006 is a helpful bridge before estimator variants and group-relative objectives.  
Reference: [reference 1](https://arxiv.org/abs/2503.14476)  
Source inspiration: [dapo_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/dapo_from_scratch)

### Question

Which DAPO components change GRPO on identical samples?

### Minimal implementation

Switchable asymmetric clipping, group filtering and token aggregation.

### Minimal experiment

Ablate one switch at a time on fixed grouped sequences.

### Completion gate

Each option has equation-level example; disabled switches recover GRPO.

### Stretch goals

Study overlong sequence handling.

### Do NOT do

Do not claim complete DAPO or build large rollout systems.

## REP-010 — KL direction and support coverage

Status: BACKLOG  
Priority: P0  
Study Track: Distillation<br>
Implementation Home: Planned: Distillation-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2306.08543)  
Source inspiration: [knowledge_distillation_llm](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm)

### Question

Why does forward KL cover modes while reverse KL can concentrate?

### Minimal implementation

Categorical KL variants with stable log-softmax/autograd.

### Minimal experiment

Vary separated modes; plot probability mass and gradients.

### Completion gate

Identical distributions yield zero; finite differences match gradients.

### Stretch goals

Temperature and Jensen-Shannon comparison.

### Do NOT do

Do not involve text models before probability-space behavior is clear.

## REP-011 — Same-tokenizer token logit KD

Status: BACKLOG  
Priority: P0  
Study Track: Distillation<br>
Implementation Home: Planned: Distillation-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-010, then REP-011 for token-level distributions.  
Reference: [reference 1](https://arxiv.org/abs/2306.08543)  
Source inspiration: [knowledge_distillation_llm](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm)

### Question

How should token KD combine teacher probabilities and causal masks?

### Minimal implementation

Tiny shared-vocab teacher/student; temperature KL and label masks.

### Minimal experiment

Test matching logits, pads and one student update.

### Completion gate

Matching logits give zero loss; pads ignored; teacher stays frozen.

### Stretch goals

KL plus hard-label CE.

### Do NOT do

Do not download large checkpoints.

## REP-012 — On-policy token distillation

Status: BACKLOG  
Priority: P0  
Study Track: Distillation<br>
Implementation Home: Planned: Distillation-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-010, then REP-011 for token-level distributions.  
Reference: [reference 1](https://arxiv.org/abs/2306.08543)  
Source inspiration: [knowledge_distillation_llm](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm)

### Question

How does distilling on student prefixes differ from teacher forcing?

### Minimal implementation

Generate short student prefixes; query frozen teacher logits on those states.

### Minimal experiment

Compare state distribution/KL on a tiny grammar task.

### Completion gate

Prefix source explicit, teacher frozen, shifts and masks correct.

### Stretch goals

Mix teacher and student prefixes.

### Do NOT do

Do not use paid APIs or production rollout code.

## REP-014 — Direct Preference Optimization

Status: BACKLOG  
Priority: P1  
Study Track: Post-training<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf)<br>
Coverage: SCAFFOLDED<br>
Action: COMPLETE_EXISTING<br>
Existing implementation evidence: [cs336_alignment/assistant/dpo.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/cs336_alignment/assistant/dpo.py) and run_dpo.py are docstring-only; DPO adapter in [tests/adapters.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/tests/adapters.py) raises NotImplementedError; expected behavior in [tests/test_dpo.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/tests/test_dpo.py).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2305.18290)  
Source inspiration: [knowledge_distillation_llm](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm)

### Question

How does DPO move chosen/rejected odds relative to reference?

### Minimal implementation

Pairwise log-sigmoid objective over policy/reference log probabilities.

### Minimal experiment

Train a tiny categorical policy on synthetic preference pairs.

### Completion gate

Chosen margin rises; reference detached; sign matches derivation.

### Stretch goals

Sweep beta and label noise.

### Do NOT do

Do not add reward model or preference UI.

## REP-015 — Multi-head Latent Attention

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2405.04434)  
Source inspiration: [deepseek_learn/MLA.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/MLA.py)

### Question

Are naive and absorbed MLA algebraically equivalent?

### Minimal implementation

Latent KV compression plus two attention formulations.

### Minimal experiment

Compare outputs and cache size across tiny configurations.

### Completion gate

Outputs agree within tolerance; selected configs store fewer cache values.

### Stretch goals

Benchmark cache bandwidth.

### Do NOT do

Do not claim DeepSeek-V2 training reproduction.

## REP-016 — Gated DeltaNet recurrence

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2505.09388)  
Source inspiration: [train_qwen3_next_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch)

### Question

What update does a gated delta rule perform, and when is chunking equivalent?

### Minimal implementation

Implement recurrent delta update and chunked scan.

### Minimal experiment

Compare sequential/chunked states across chunk boundaries.

### Completion gate

Paths match tolerance; state shapes documented.

### Stretch goals

Profile recurrent vs quadratic memory.

### Do NOT do

Do not build all of Qwen3-Next.

## REP-017 — DeepSeek Sparse Attention indexer

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: DeepSeek-V3.2 report  
Source inspiration: [deepseek_learn/dsa/model.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/dsa/model.py)

### Question

Can a learned top-k indexer retain useful full-attention mass?

### Minimal implementation

Tiny full-attention teacher, indexer, top-k gather and sparse attention.

### Minimal experiment

Measure teacher mass retained and output error as k changes.

### Completion gate

Selection is causal/stable; mass rises with k; warmup gradients reach indexer.

### Stretch goals

Teacher-score KL warmup.

### Do NOT do

Do not claim production fidelity.

## REP-018 — Multi-token prediction heads

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2412.19437)  
Source inspiration: [deepseek_learn/MTP_train](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/MTP_train)

### Question

How do future-token heads align targets and send auxiliary gradients?

### Minimal implementation

Attach small shifted prediction heads to a causal backbone.

### Minimal experiment

Check shifts on deterministic tokens; compare head-wise CE.

### Completion gate

Offsets correct and each head receives finite gradients.

### Stretch goals

Convergence with/without heads.

### Do NOT do

Do not rebuild DeepSeek-V3 training stack.

## REP-019 — Qwen3-Next hybrid block schedule

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: Qwen3-Next technical report  
Source inspiration: [train_qwen3_next_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch)

### Question

How does block composition change compute and behavior?

### Minimal implementation

Configurable attention/GatedDeltaNet/MoE tiny stack.

### Minimal experiment

Causality/shape checks and tiny next-token task; ablate schedules.

### Completion gate

Config matches block order, masks/state reset correctly, loss can decrease.

### Stretch goals

Compare equal-depth schedules.

### Do NOT do

Do not claim full Qwen3-Next fidelity.

## REP-020 — Attention Residuals

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2603.15031)  
Source inspiration: [kimi_attnres/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/kimi_attnres/train.py)

### Question

How does learned mixing over layer states differ from residual addition?

### Minimal implementation

Softmax-weight earlier hidden states in a tiny stack.

### Minimal experiment

Compare norms and gradient contributions to ordinary residual baseline.

### Completion gate

Weights normalize and gradients finite; toy loss responds.

### Stretch goals

History windows and initialization.

### Do NOT do

Do not bundle MoE or claim full Kimi architecture.

## REP-021 — Manifold-constrained Hyper-Connections

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2512.24880)  
Source inspiration: [deepseek_learn/mHC.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/mHC.ipynb)

### Question

Does Sinkhorn make residual mixing approximately doubly stochastic?

### Minimal implementation

Learned mixing logits with iterative row/column normalization.

### Minimal experiment

Check marginal sums, activation norms and iteration convergence.

### Completion gate

Marginals meet documented tolerance.

### Stretch goals

Compare unconstrained deep residual stack.

### Do NOT do

Do not treat notebook as proof of full paper results.

## REP-022 — Engram conditional memory

Status: BACKLOG  
Priority: P1  
Study Track: Modern Architecture<br>
Implementation Home: Planned: Modern-LLM-Architecture-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2601.07372)  
Source inspiration: [deepseek_learn/engram.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/engram.ipynb)

### Question

When does hashed n-gram memory help and how do collisions matter?

### Minimal implementation

Deterministic hash slots, n-gram embeddings and gated lookup.

### Minimal experiment

Repeated-pattern task: report retrieval accuracy and collision rate.

### Completion gate

Hash deterministic; collision accounting correct; gate learns toy target.

### Stretch goals

Sweep table size/order.

### Do NOT do

Do not build vector DB or claim full Engram reproduction.

## REP-023 — Universal Logit Distillation

Status: BACKLOG  
Priority: P1  
Study Track: Distillation<br>
Implementation Home: Planned: Distillation-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: REP-010 and REP-011.  
Reference: [reference 1](https://arxiv.org/abs/2402.12030)  
Source inspiration: [knowledge_distillation_llm_cross_tokenizer](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm_cross_tokenizer)

### Question

How can distributions be compared across different token boundaries?

### Minimal implementation

Character/span alignment, matched-token term and unmatched-mass handling.

### Minimal experiment

Two toy vocabularies split equivalent strings differently.

### Completion gate

Aligned mass follows documented rule; gradients finite; same segmentation reduces to standard KD.

### Stretch goals

Tokenizer edge cases and batching.

### Do NOT do

Do not load multi-billion parameter models.

## REP-024 — Embedding ranking distillation

Status: BACKLOG  
Priority: P1  
Study Track: Distillation<br>
Implementation Home: Planned: Distillation-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: Qwen3 Embedding report  
Source inspiration: [knowledge_distillation_embedding](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding)

### Question

Can listwise distillation preserve a teacher's ranking?

### Minimal implementation

Fixed/tiny embeddings and KL over candidate similarity scores.

### Minimal experiment

Synthetic query-positive-negative set; report MAP/MRR.

### Completion gate

Scores align and ranking metric moves in expected direction.

### Stretch goals

Pointwise regression and temperature.

### Do NOT do

Do not claim Qwen benchmark results without its assets.

## REP-025 — SigLIP pairwise sigmoid loss

Status: BACKLOG  
Priority: P1  
Study Track: Multimodal<br>
Implementation Home: Planned: Multimodal-From-Scratch (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2303.15343)  
Source inspiration: [train_siglip_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_siglip_from_scratch)

### Question

How does SigLIP pairwise sigmoid differ from batch-softmax?

### Minimal implementation

Normalized pair logits, learned scale/bias and pair labels.

### Minimal experiment

Known matching pairs; compare gradients and batch-size behavior.

### Completion gate

Signs/labels correct; matching scores improve on synthetic features.

### Stretch goals

Objective cost as batch grows.

### Do NOT do

Do not train towers or fetch MUGE initially.

## REP-026 — Vision-language connector and feature packing

Status: BACKLOG  
Priority: P1  
Study Track: Multimodal<br>
Implementation Home: Planned: Multimodal-From-Scratch (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2304.08485)  
Source inspiration: [train_multimodal_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch)

### Question

How do projected image tokens enter a causal LM sequence?

### Minimal implementation

Small projector, placeholder replacement and labels/masks with stubs.

### Minimal experiment

Overfit synthetic image-feature to answer mapping; inspect positions.

### Completion gate

Image tokens in correct slots; connector gradients finite; loss falls.

### Stretch goals

Multi-image packing after single-image check.

### Do NOT do

Do not train pretrained encoders or build a demo.

## REP-027 — s1 budget forcing

Status: BACKLOG  
Priority: P1  
Study Track: Reasoning / Test-Time Scaling<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf) / extensions/s1_budget_forcing (planned; not created)<br>
Coverage: NONE<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: See dependency-map.md; use a stub where training would cause setup work.  
Reference: [reference 1](https://arxiv.org/abs/2501.19393)  
Source inspiration: [s1_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/s1_from_scratch)

### Question

How does fixed inference budget affect answer quality and token cost?

### Minimal implementation

Controller that continues/stops reasoning under explicit budget.

### Minimal experiment

Synthetic multistep task at several token budgets.

### Completion gate

Budget enforcement exact; fixed-seed quality/cost table.

### Stretch goals

Confidence-based continuation.

### Do NOT do

Do not fine-tune a large checkpoint or conflate search rollouts.

## REP-028 — FlashAttention tiling

Status: BACKLOG  
Priority: P1  
Study Track: Systems<br>
Implementation Home: Deferred: LLM-Systems-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2205.14135), [reference 2](https://arxiv.org/abs/2307.08691)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap), [no faithful source implementation](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/no faithful source implementation)

### Question

How can tiled online softmax compute exact attention with less memory?

### Minimal implementation

Tiled Q/K/V and numerically stable online max/sum/output.

### Minimal experiment

Compare output/gradients with dense reference; count intermediate tensors.

### Completion gate

Numerical agreement and smaller materialized score storage.

### Stretch goals

Benchmark tile sizes after correctness.

### Do NOT do

Do not write CUDA/Triton in first version.

## REP-029 — Paged KV cache and prefix reuse

Status: BACKLOG  
Priority: P2  
Study Track: Systems<br>
Implementation Home: Deferred: LLM-Systems-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2309.06180)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap), [only basic cache exists](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/only basic cache exists)

### Question

How does block allocation reduce cache fragmentation and share prefixes?

### Minimal implementation

Fixed blocks, block tables, refcounts and request release.

### Minimal experiment

Replay varied lengths; compare allocated/useful slots and prefix duplication.

### Completion gate

No leaks; refcounts correct; fragmentation defined.

### Stretch goals

Arrival/departure continuous-batch simulation.

### Do NOT do

Do not build an inference server or reproduce vLLM.

## REP-030 — Weight-only GPTQ or AWQ

Status: BACKLOG  
Priority: P2  
Study Track: Systems<br>
Implementation Home: Deferred: LLM-Systems-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2210.17323), [reference 2](https://arxiv.org/abs/2306.00978)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap)

### Question

What quality cost accompanies groupwise low-bit quantization?

### Minimal implementation

Groupwise scales/zero points and dequantized tiny linear layer.

### Minimal experiment

Measure bytes/output error for 4-bit vs fp16.

### Completion gate

Values in range, byte count correct, error visible.

### Stretch goals

Simplified calibration after baseline.

### Do NOT do

Do not use large checkpoints or claim full GPTQ/AWQ.

## REP-031 — Speculative decoding

Status: BACKLOG  
Priority: P2  
Study Track: Systems<br>
Implementation Home: Deferred: LLM-Systems-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2211.17192)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap)

### Question

Why can speculative decoding preserve target sampling?

### Minimal implementation

Draft proposal, acceptance and residual replacement on categorical logits.

### Minimal experiment

Compare sampled frequencies with target-only and count target calls.

### Completion gate

Frequencies agree within statistical tolerance; rejection covered.

### Stretch goals

Vary draft agreement and proposal length.

### Do NOT do

Do not optimize GPU batching or build production decoder.

## REP-032 — Deduplication and tiny scaling study

Status: BACKLOG  
Priority: P2  
Study Track: Foundations / Training Data & Scaling<br>
Implementation Home: [Bubblevan/CS336-A1](https://github.com/Bubblevan/CS336-A1/tree/3d26a6334ab59f6e23e6e86aa6807db7ff39e420) / extensions/data_quality_scaling (planned; not created)<br>
Coverage: NONE<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: CS336-A1 data/batch scaffolding in [tests/adapters.py](https://github.com/Bubblevan/CS336-A1/blob/3d26a6334ab59f6e23e6e86aa6807db7ff39e420/tests/adapters.py); no controlled deduplication/scaling study found. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2203.15556)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap)

### Question

How do duplicates alter unique token budget and small-model loss?

### Minimal implementation

Exact/MinHash dedup and deterministic small train/validation split.

### Minimal experiment

Sweep duplicate fraction/unique-token exposure; plot validation loss.

### Completion gate

Counts auditable; split has no leakage; small-sample caveat stated.

### Stretch goals

Near-duplicate thresholds and token/model ratios.

### Do NOT do

Do not claim scaling law from a handful of toy runs.

## REP-033 — GDPO reward-dimension normalization

Status: BACKLOG  
Priority: P2  
Study Track: Post-training<br>
Implementation Home: [Bubblevan/CS336-A5](https://github.com/Bubblevan/CS336-A5/tree/26653042601b8dfde33e0ababa5cd4728e5756bf) / extensions/gdpo (planned; not created)<br>
Coverage: PARTIAL_EXISTING<br>
Action: EXTEND_EXISTING<br>
Existing implementation evidence: Reward/group primitives in [cs336_alignment/reasoning/grpo_advantage.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/cs336_alignment/reasoning/grpo_advantage.py)/[tests/test_grpo.py](https://github.com/Bubblevan/CS336-A5/blob/26653042601b8dfde33e0ababa5cd4728e5756bf/tests/test_grpo.py); no per-dimension GDPO normalization found. [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2601.05242)  
Source inspiration: [gdpo/train_gdpo.sh](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gdpo/train_gdpo.sh), [gdpo/verl/verl/trainer/ppo/core_algos.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gdpo/verl/verl/trainer/ppo/core_algos.py)

### Question

What changes when reward dimensions normalize separately?

### Minimal implementation

Per-dimension centered/scaled advantages on fixed grouped samples.

### Minimal experiment

Scale one reward channel 10x; compare scalarized/decoupled updates.

### Completion gate

Observed invariance/sensitivity matches stated equation.

### Stretch goals

Missing and zero-variance dimensions.

### Do NOT do

Do not vendor verl or run distributed trainer.

## REP-034 — Training-free GRPO semantic memory

Status: BACKLOG  
Priority: P2  
Study Track: Reasoning / Memory<br>
Implementation Home: UNASSIGNED<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No implementation/test for offline rollouts, experience aggregation and retrieval was found in eligible learning/reproduction repositories CS336-A1 or CS336-A5.<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2510.08191)  
Source inspiration: [training-free_grpo](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/training-free_grpo)

### Question

Can accumulated external experience help without parameter updates?

### Minimal implementation

Offline rollouts, successful-experience aggregation, memory retrieval and policy/decision feedback.

### Minimal experiment

Compare held-out behavior with empty memory versus retrieved memory using identical offline rollouts and a fixed evaluation set.

### Completion gate

No weights change; retrieved records traceable; result reproducible.

### Stretch goals

Duplicate/conflicting memory policies.

### Do NOT do

Do not call paid APIs or describe it as gradient-based GRPO.

## REP-035 — Activation patching and causal tracing

Status: BACKLOG  
Priority: P2  
Study Track: Interpretability<br>
Implementation Home: Deferred: Interpretability-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2202.05262)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap)

### Question

Does a hidden activation causally support a known output?

### Minimal implementation

Forward hooks and patch clean/corrupted activations in tiny model.

### Minimal experiment

Measure target-logit restoration by layer and token.

### Completion gate

Intervention explicit; control has expected null effect.

### Stretch goals

Path patching or local pretrained model.

### Do NOT do

Do not claim a full circuit from one intervention.

## REP-036 — Sparse autoencoder feature dictionary

Status: BACKLOG  
Priority: P2  
Study Track: Interpretability<br>
Implementation Home: Deferred: Interpretability-Lab (not created)<br>
Coverage: NONE<br>
Action: NEW_REPRODUCTION<br>
Existing implementation evidence: No directly relevant implementation and targeted test found in the eligible learning/reproduction repositories CS336-A1 and CS336-A5; see [audit details](existing-repository-audit.md#reproduction-level-crosswalk).<br>
Prerequisites: None; start from a small corpus or synthetic tensors.  
Reference: [reference 1](https://arxiv.org/abs/2309.08600)  
Source inspiration: [Gap](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/Gap)

### Question

Can an SAE recover known factors from mixed activations?

### Minimal implementation

Small encoder/decoder with reconstruction and sparsity penalty.

### Minimal experiment

Sweep sparsity; measure L0, reconstruction and feature recovery.

### Completion gate

Tradeoff recorded and feature matching checkable against synthetic ground truth.

### Stretch goals

Dead-feature resampling or local activations.

### Do NOT do

Do not make claims from synthetic activations alone.

