# Directions and repository boundaries

## Study Tracks

A Study Track is a conceptual learning path. A Study Track does not imply a dedicated repository. Every matrix item has one Implementation Home: an existing repository, a planned extension path, a later potential repository, or a deferred/archive reference.

| Study Track | Representative mechanisms | Current boundary |
|---|---|---|
| Foundations | Tokenization, decoder stack, optimization, training loop | CS336-A1; complete its official assignment adapters before extensions. |
| Modern Architecture | MLA, GatedDeltaNet, DSA, MTP, hybrid blocks, Attention Residuals, mHC, Engram, MoE | MoE extends CS336-A1; other topics may use Modern-LLM-Architecture-Lab. |
| Post-training | Policy gradient, PPO/GAE, RLOO/ReMax, GRPO/DAPO, GDPO and DPO | CS336-A5 owns fundamentals; complete DPO there and extend for distinct experiments. |
| Distillation | KL geometry, token KD, on-policy KD, ULD, embedding transfer | Potential Distillation-Lab. |
| Multimodal | SigLIP objective and vision-language connectors | Potential Multimodal-From-Scratch. |
| Systems | Tiled attention, paged KV, quantization and speculative decoding | LLM-Systems-Lab deferred; GQA/KV cache is a CS336-A1 extension. |
| Interpretability | Activation patching and sparse autoencoders | Interpretability-Lab deferred. |
| Reasoning / Test-Time Scaling | Budget forcing, search and inference compute | CS336-A5 for pedagogical objectives; TraceSearch-R1 for search-agent RL and real rollouts. |
| Retrieval / Memory | BM25/dense retrieval, fusion and provenance-aware memory | Health-Copilot owns applied retrieval and memory; no toy duplicate. |
| Agents / Harness | Tool execution, replay, multi-agent orchestration and evaluation | Health-Copilot and TraceSearch-R1 retain their established domains. |

## Existing Implementation Homes

- **CS336-A1:** official foundational assignment and completion work. GQA/KV cache, MoE and data-quality studies belong below clearly separate extensions/ paths, not in official assignment content.
- **CS336-A5:** post-training fundamentals, including tested response masks and GRPO. Add pedagogical PPO/GAE, RLOO/ReMax, DAPO or bandit studies only where the exact mechanism is absent. Complete DPO in its existing scaffold.
- **TraceSearch-R1:** search-agent RL, grouped rollouts, search environments, verifier/reward integration, trajectory provenance and project-level GRPO actor updates. This is an advanced reference, not a claim of exact full Search-R1 reproduction.
- **Health-Copilot:** generic retrieval, memory, multi-agent, harness/runtime and retrieval evaluation. Keep paper-specific memory methods read-only unless a distinct, non-toy need is identified.

## Potential new repositories

These are candidates for later review, not repositories created in Phase A.1.

| Candidate | Track | Scope |
|---|---|---|
| Modern-LLM-Architecture-Lab | Modern Architecture | Isolated mechanisms with formula, shape, invariant and optional microbenchmark evidence. |
| Distillation-Lab | Distillation | Small categorical/token/embedding transfer experiments without a checkpoint hub. |
| Multimodal-From-Scratch | Multimodal | Isolated objectives and connector paths; no large from-scratch vision tower. |

## Deferred repositories

| Candidate | Reason |
|---|---|
| LLM-Systems-Lab | Keep future systems studies queued by mechanism; no need to create the repository now. |
| Interpretability-Lab | Retain the direction until a coherent group of experiments is ready for review. |

The former **LLM-From-Scratch** and **PostTraining-From-Scratch** proposals are removed. Their distinct experiments belong in CS336-A1 or CS336-A5, with official assignment work separated from extensions.

## Coverage and action vocabulary

Coverage requires implementation plus an appropriate test or experiment, not a README claim or filename.

| Coverage | Meaning |
|---|---|
| NONE | No relevant implementation found. |
| SCAFFOLDED | Placeholder, test adapter or incomplete stub; mechanism not implemented. |
| PARTIAL_EXISTING | Relevant primitives exist, but the Atlas experiment or required mechanism is incomplete. |
| COVERED_EXISTING | Implementation and relevant test/experiment exist; not active backlog work. |
| SUPERSEDED | Existing advanced reference replaces this Atlas objective; no exact paper reproduction is implied. |
| ARCHIVED | Source/reference record only. |

| Action | Meaning |
|---|---|
| NEW_REPRODUCTION | Build a focused reproduction in a later approved home. |
| COMPLETE_EXISTING | Finish the scaffold or implementation in its current home. |
| EXTEND_EXISTING | Add a distinct mechanism below an existing repository's extension boundary. |
| READ_ONLY | Use the existing home as reference; no duplicate experiment is queued. |
| NO_ACTION | Already covered, archived or out of scope. |

See the [repository audit](existing-repository-audit.md) and [matrix](matrix.md) for exact ownership and code/test evidence.
