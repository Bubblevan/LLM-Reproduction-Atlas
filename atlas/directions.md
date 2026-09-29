# Directions and repository boundaries

## REP invariant

> A REP represents a concrete, independently completable learning/reproduction experiment.

Coverage may come from a dedicated reproduction repository, learning/reimplementation coursework, or an explicitly isolated reproduction extension. Formal production/research project contents cannot establish REP coverage. Coverage status and evidence must be based on an eligible learning/reproduction home.

## Study Tracks

A Study Track is conceptual organization. A Study Track does not imply a dedicated repository.

| Study Track | Representative mechanisms |
|---|---|
| Foundations | Tokenization, decoder stack, optimization, training loop, data and scaling |
| Modern Architecture | MLA, GatedDeltaNet, DSA, MTP, hybrid blocks, Attention Residuals, mHC, Engram and MoE |
| Post-training | Policy gradient, PPO/GAE, RLOO/ReMax, GRPO/DAPO, GDPO and DPO |
| Distillation | KL geometry, token KD, on-policy KD, ULD and embedding transfer |
| Multimodal | SigLIP objective and vision-language connectors |
| Systems | Tiled attention, paged KV, quantization and speculative decoding |
| Interpretability | Activation patching and sparse autoencoders |
| Reasoning / Test-Time Scaling | Budget forcing, search and inference compute |
| Retrieval / Memory | Retrieval and memory mechanisms studied in isolation |
| Agents / Harness | Tool execution, orchestration and evaluation mechanisms studied in isolation |

## Implementation Homes

### Existing learning/reproduction homes

- **CS336-A1:** foundational coursework and its completion work. GQA/KV cache, MoE and data-quality studies belong under clearly separate extension paths, outside official assignment content.
- **CS336-A5:** post-training coursework, including the tested response-only mask and GRPO. Complete DPO in its scaffold; add distinct educational experiments only where the coursework lacks the mechanism.

### Potential future reproduction homes

| Candidate | Track | Scope |
|---|---|---|
| Modern-LLM-Architecture-Lab | Modern Architecture | Small isolated mechanisms with formula, shape and invariant evidence. |
| Distillation-Lab | Distillation | Small categorical/token/embedding transfer experiments. |
| Multimodal-From-Scratch | Multimodal | Isolated objectives and connector paths, not large-scale pretraining. |

### Deferred

| Candidate | Reason |
|---|---|
| LLM-Systems-Lab | Keep systems mechanisms queued until a coherent physical home is needed. |
| Interpretability-Lab | Keep the direction deferred until a coherent set of experiments is ready. |

## Formal Project Boundaries

Formal-project implementation status is not REP completion evidence. These projects can inform scope or integration context; they are not Atlas Implementation Homes and cannot produce any REP Coverage value.

### TraceSearch-R1

An active formal search-agent/RL project. Its search environments, grouped rollouts and provenance may inform boundaries. Atlas does not reproduce the formal project wholesale for completeness.

### Health-Copilot

An active formal retrieval/memory/multi-agent/harness project. Its components do not imply that an isolated Atlas memory, retrieval or agent mechanism is already reproduced.

## Coverage and action vocabulary

| Coverage | Meaning |
|---|---|
| NONE | No relevant implementation found in an eligible learning/reproduction home. |
| SCAFFOLDED | Placeholder or incomplete stub exists in an eligible home. |
| PARTIAL_EXISTING | Related primitives exist in an eligible home, but the REP experiment/mechanism is incomplete. |
| COVERED_EXISTING | Implementation and relevant test/experiment exist in an eligible home; not active work. |
| SUPERSEDED | Reserved for a learning/reproduction home replacing the objective; formal projects cannot cause this status. |
| ARCHIVED | Not used in the REP registry; keep non-candidates in source audit/reference material. |

| Action | Meaning |
|---|---|
| NEW_REPRODUCTION | Build a focused reproduction in a later approved home. |
| COMPLETE_EXISTING | Finish an eligible coursework/reproduction scaffold. |
| EXTEND_EXISTING | Add a distinct mechanism below an eligible home's extension boundary. |
| READ_ONLY | Read-only research on an eligible reproduction reference; does not by itself claim coverage. |
| NO_ACTION | Already covered by eligible learning/reproduction evidence. |

The [matrix](matrix.md) contains REP-001–REP-036. Retired source items remain discoverable in the [source audit](source-audit-wyf3.md) and [reference inventory](../references/wyf3-llm-related.md).
