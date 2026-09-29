# Source audit: wyf3/llm_related

Audit date: 2026-09-29 (Asia/Shanghai)  
Audited branch: main  
Audited commit: a492338499a9381f1714ecda8c802684e0556d3e  
Local source: D:\MyLab\llm_related (clean working tree at audit)  
Remote main check: same SHA. Public repository: https://github.com/wyf3/llm_related

The inventory contains 27 top-level directories and 6 files (33 components). Each entry below is pinned to this commit. File links provide implementation evidence; linked papers are conceptual targets, not proof of implementation fidelity.

Classification vocabulary: FROM_SCRATCH means the core algorithm/model is implemented without pretrained model or framework code; MINIMAL_REIMPLEMENTATION means the central mechanism is handwritten while normal libraries/wrappers remain; ADAPTATION means existing models/trainers are modified; DEMO means integration or prototype rather than a controlled reproduction; VENDORED_UPSTREAM means a copied framework dominates; UNKNOWN means evidence is insufficient.

## all_to_tool_call

Source: [all_to_tool_call](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/all_to_tool_call)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Agent / Tool Use / Harness
Source type: DEMO

### What it actually implements
FastAPI proxy examples for direct and indirect tool calling over OpenAI-compatible APIs.

### Important files
- [all_to_tool_call/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/all_to_tool_call/README.md)
- [all_to_tool_call/all_to_tool_call.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/all_to_tool_call/all_to_tool_call.py)
- [all_to_tool_call/test.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/all_to_tool_call/test.ipynb)

### External dependencies / upstream
FastAPI, OpenAI-compatible API endpoint and credentials/configuration.

### Corresponding paper / mechanism
API tool calling / protocol integration; no standalone algorithm paper.

### What is pedagogically useful
Shows request schemas and direct-vs-indirect routing.

### What is implementation-specific noise
Server, provider and endpoint glue dominate.

### Is it genuinely from scratch?
No; service demo.

### Proposed action
READ_ONLY

### Destination
Archive; generic tool execution already belongs to Health-Copilot.

## code-r1

Source: [code-r1](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/code-r1)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training / Retrieval / Systems
Source type: VENDORED_UPSTREAM

### What it actually implements
A large vendored verl snapshot with Search-R1 retrieval/generation pieces and local recipe/reward edits. Package reports 0.4.1.dev. Outer repository history shows a later change to my_reward/code.py; that file validates think/code/observation/answer tag order and computes answer/code rewards with an LLM-judge call. Exact embedded upstream SHA is UNVERIFIED.

### Important files
- [code-r1/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/code-r1/README.md)
- [code-r1/search_r1/](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/code-r1/search_r1/)
- [code-r1/verl/](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/code-r1/verl/)
- [code-r1/examples/data_preprocess/preprocess_search_r1_dataset.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/code-r1/examples/data_preprocess/preprocess_search_r1_dataset.py)`n- [code-r1/my_reward/code.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/code-r1/my_reward/code.py)

### External dependencies / upstream
verl, PyTorch, Transformers, Ray/Accelerate, retrieval service and model/data assets. README names volcengine/verl.

### Corresponding paper / mechanism
Search-R1: https://arxiv.org/abs/2503.09516 ; upstream https://github.com/PeterGriffinJin/Search-R1

### What is pedagogically useful
Read local reward, prompt/data adapter and retrieval loop; compare specific deltas to upstream.

### What is implementation-specific noise
Vendored trainer dominates the tree; running its recipes needs substantial systems/model setup.

### Is it genuinely from scratch?
No; copied framework plus adaptation.

### Proposed action
READ_ONLY

### Destination
Archive full reproduction; TraceSearch-R1 overlaps.

## dapo_from_scratch

Source: [dapo_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/dapo_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training / Reasoning
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
GRPO-shaped loop with asymmetric clipping, zero-variance group filtering and DAPO-like aggregation; not every DAPO component is present.

### Important files
- [dapo_from_scratch/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/dapo_from_scratch/train.py)
- [dapo_from_scratch/reward_func.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/dapo_from_scratch/reward_func.py)
- [dapo_from_scratch/test.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/dapo_from_scratch/test.py)

### External dependencies / upstream
PyTorch, HF model/data and accelerator configuration.

### Corresponding paper / mechanism
DAPO: https://arxiv.org/abs/2503.14476 ; https://dapo-sia.github.io/

### What is pedagogically useful
Extract clipping, group filtering and aggregation as independent equations.

### What is implementation-specific noise
Training and rollout scaffold can obscure component attribution.

### Is it genuinely from scratch?
Partly: handwritten update mechanics, partial recipe.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-009.

## deep_research

Source: [deep_research](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deep_research)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Agent / Tool Use / Harness
Source type: DEMO

### What it actually implements
SearXNG/MCP search prototype with query generation, relevance filtering and context extraction; not a robust end-to-end research loop.

### Important files
- [deep_research/prompts.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deep_research/prompts.py)
- [deep_research/client.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deep_research/client.py)
- [deep_research/search_mcp.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deep_research/search_mcp.py)
- [deep_research/searxng/docker-compose.yaml](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deep_research/searxng/docker-compose.yaml)

### External dependencies / upstream
SearXNG/MCP, LLM endpoint, credentials and local services.

### Corresponding paper / mechanism
Search agent scaffold; no isolated paper mechanism verified.

### What is pedagogically useful
Useful to inspect integration boundaries and failure handling.

### What is implementation-specific noise
External service setup/orchestration is most of the work.

### Is it genuinely from scratch?
No; demo.

### Proposed action
ARCHIVE

### Destination
Health-Copilot owns generic agent runtime; archive scaffold.

## deepseek_learn

Source: [deepseek_learn](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Model Architecture / Distillation / Post-training
Source type: ADAPTATION

### What it actually implements
Collection: MLA naïve/absorbed attention; MTP heads attached to pretrained HF causal LM; DSA indexer warmup from full-attention scores then sparse top-k; toy mHC and Engram notebooks; undocumented chunk-compressor/indexer attention; TRL GRPOTrainer R1-style run with Qwen2.5-0.5B/GSM8K Chinese.

### Important files
- [deepseek_learn/MLA.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/MLA.py)
- [deepseek_learn/MTP_train/MTP.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/MTP_train/MTP.py)
- [deepseek_learn/dsa/model.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/dsa/model.py)
- [deepseek_learn/dsa/warmup_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/dsa/warmup_train.py)
- [deepseek_learn/dsa/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/dsa/train.py)
- [deepseek_learn/mHC.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/mHC.ipynb)
- [deepseek_learn/engram.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/engram.ipynb)
- [deepseek_learn/dpsk_v4_attention.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/dpsk_v4_attention.py)
- [deepseek_learn/deepseek_r1_train/deepseek_r1_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/deepseek_learn/deepseek_r1_train/deepseek_r1_train.py)

### External dependencies / upstream
PyTorch, Transformers Qwen2 internals, TRL GRPOTrainer, pretrained model/data; README links dataset for DSA.

### Corresponding paper / mechanism
MLA https://arxiv.org/abs/2405.04434 ; MTP https://arxiv.org/abs/2412.19437 ; DSA https://github.com/deepseek-ai/DeepSeek-V3.2-Exp/blob/main/DeepSeek_V3_2.pdf ; mHC https://arxiv.org/abs/2512.24880 ; Engram https://arxiv.org/abs/2601.07372

### What is pedagogically useful
Mechanism-sized MLA/DSA/MTP studies; compare code with papers and mark omissions.

### What is implementation-specific noise
Mixed prototypes, pretrained model glue, and no single reproducible package contract.

### Is it genuinely from scratch?
No single label: core mechanisms are adaptations; mHC/Engram are toy prototypes; R1 run uses TRL.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Modern-LLM-Architecture-Lab for isolated mechanisms.

## gdpo

Source: [gdpo](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gdpo)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training / Multi-objective RL
Source type: ADAPTATION

### What it actually implements
Launch script selects GDPO estimator/reward manager in vendored verl 0.4.1.dev; core algorithm normalizes reward dimensions separately. Tree is not an original minimal trainer.

### Important files
- [gdpo/train_gdpo.sh](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gdpo/train_gdpo.sh)
- [gdpo/verl/verl/trainer/ppo/core_algos.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gdpo/verl/verl/trainer/ppo/core_algos.py)
- [gdpo/verl/verl/workers/reward_manager/](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gdpo/verl/verl/workers/reward_manager/)

### External dependencies / upstream
Vendored verl/PyTorch/Ray and model/data recipes; exact embedded source SHA UNVERIFIED.

### Corresponding paper / mechanism
GDPO https://arxiv.org/abs/2601.05242 ; verl https://github.com/volcengine/verl

### What is pedagogically useful
Isolate per-dimension normalization in a tiny fixed-batch equation test.

### What is implementation-specific noise
Vendor framework setup is unnecessary for learning normalization.

### Is it genuinely from scratch?
No; algorithm adaptation plus vendored upstream.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-033.

## grpo_from_scratch

Source: [grpo_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/grpo_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training / Reasoning
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
Handwritten grouped completions, scalar rewards, group-relative normalized advantages and clipped policy objective.

### Important files
- [grpo_from_scratch/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/grpo_from_scratch/train.py)
- [grpo_from_scratch/reward_func.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/grpo_from_scratch/reward_func.py)
- [grpo_from_scratch/test.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/grpo_from_scratch/test.py)

### External dependencies / upstream
PyTorch, HF model/data, accelerator optional for provided training recipe.

### Corresponding paper / mechanism
DeepSeekMath GRPO https://arxiv.org/abs/2402.03300

### What is pedagogically useful
Rebuild update from tiny logits and inspect group normalization.

### What is implementation-specific noise
Model loading, data and rollout batching are supporting scaffolding.

### Is it genuinely from scratch?
Partly; central objective mechanics handwritten.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-008.

## kimi_attnres

Source: [kimi_attnres](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/kimi_attnres)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Model Architecture
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
Custom model uses input-conditioned softmax weights over previous sublayer states, plus ordinary attention and MoE; it omits parts of block AttnRes design.

### Important files
- [kimi_attnres/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/kimi_attnres/train.py)
- [kimi_attnres/test.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/kimi_attnres/test.py)
- [kimi_attnres/sft_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/kimi_attnres/sft_train.py)

### External dependencies / upstream
PyTorch/HF tokenizer and training/data stack.

### Corresponding paper / mechanism
Attention Residuals https://arxiv.org/abs/2603.15031

### What is pedagogically useful
Implement the residual aggregation primitive alone and compare gradient/normalization paths.

### What is implementation-specific noise
MoE, attention, data and full training confound the residual mechanism.

### Is it genuinely from scratch?
Partial minimal mechanism sketch, not faithful full paper implementation.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Modern-LLM-Architecture-Lab, REP-020.

## knowledge_distillation_embedding

Source: [knowledge_distillation_embedding](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Distillation / Retrieval
Source type: ADAPTATION

### What it actually implements
Teacher/student query-positive-negative scores are distilled with listwise KL; teacher embeddings can be local or OpenAI API; Qwen3 student uses last-token pooling; evaluation reports MAP/MRR/NDCG.

### Important files
- [knowledge_distillation_embedding/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding/README.md)
- [knowledge_distillation_embedding/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding/train.py)
- [knowledge_distillation_embedding/dataset.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding/dataset.py)
- [knowledge_distillation_embedding/evaluation.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding/evaluation.py)
- [knowledge_distillation_embedding/get_distillation_data_local.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding/get_distillation_data_local.py)
- [knowledge_distillation_embedding/get_distillation_data_openai.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_embedding/get_distillation_data_openai.py)

### External dependencies / upstream
Transformers, PyTorch, PEFT/LoRA option, Qwen3 Embedding model, optional API and data.

### Corresponding paper / mechanism
Qwen3 Embedding report https://github.com/QwenLM/Qwen3-Embedding/blob/main/qwen3_embedding_technical_report.pdf

### What is pedagogically useful
Recreate score-distribution transfer with tiny embeddings before loading checkpoints.

### What is implementation-specific noise
Pooling config and pretrained model/data determine results.

### Is it genuinely from scratch?
No; adaptation of pretrained teacher/student models.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Distillation-Lab, REP-024.

## knowledge_distillation_llm

Source: [knowledge_distillation_llm](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Distillation
Source type: ADAPTATION

### What it actually implements
Forward, reverse and skewed KL variants; same-tokenizer logits; on-policy token-distillation scripts/examples.

### Important files
- [knowledge_distillation_llm/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm/README.md)
- [knowledge_distillation_llm/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm/train.py)
- [knowledge_distillation_llm/utils.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm/utils.py)
- [knowledge_distillation_llm/on_policy_distillation_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm/on_policy_distillation_train.py)
- [knowledge_distillation_llm/on_policy_distillation_train_rl.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm/on_policy_distillation_train_rl.py)

### External dependencies / upstream
PyTorch, Transformers/TRL, teacher/student checkpoints and dataset.

### Corresponding paper / mechanism
MiniLLM https://arxiv.org/abs/2306.08543 ; KD objective references in README.

### What is pedagogically useful
Start with categorical KL, then shared-vocabulary and on-policy states.

### What is implementation-specific noise
Framework loops and model downloads can hide objective differences.

### Is it genuinely from scratch?
No; pretrained model/trainer adaptation.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Distillation-Lab, REP-010–012.

## knowledge_distillation_llm_cross_tokenizer

Source: [knowledge_distillation_llm_cross_tokenizer](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm_cross_tokenizer)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Distillation
Source type: ADAPTATION

### What it actually implements
Universal Logit Distillation aligns teacher/student token distributions with matched-token KL and handling for unmatched probability mass. README example pairs Qwen2.5-0.5B student and GLM-4-9B teacher.

### Important files
- [knowledge_distillation_llm_cross_tokenizer/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm_cross_tokenizer/README.md)
- [knowledge_distillation_llm_cross_tokenizer/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm_cross_tokenizer/train.py)
- [knowledge_distillation_llm_cross_tokenizer/utils.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm_cross_tokenizer/utils.py)
- [knowledge_distillation_llm_cross_tokenizer/dataset.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/knowledge_distillation_llm_cross_tokenizer/dataset.py)

### External dependencies / upstream
README pins Transformers 4.45.2 and PyTorch 2.6; two tokenizers/checkpoints.

### Corresponding paper / mechanism
ULD https://arxiv.org/abs/2402.12030

### What is pedagogically useful
Test alignment and mass accounting with toy tokenizers first.

### What is implementation-specific noise
Large pretrained teacher is costly and unnecessary for learning alignment.

### Is it genuinely from scratch?
No; pretrained model adaptation.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Distillation-Lab, REP-023.

## langgraph_agent

Source: [langgraph_agent](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/langgraph_agent)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Agent / Tool Use / Harness
Source type: DEMO

### What it actually implements
Planner→execute→report LangGraph example with MemorySaver and file/shell tools; execute path is explicitly simplified.

### Important files
- [langgraph_agent/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/langgraph_agent/README.md)
- [langgraph_agent/state.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/langgraph_agent/state.py)
- [langgraph_agent/nodes.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/langgraph_agent/nodes.py)
- [langgraph_agent/graph.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/langgraph_agent/graph.py)
- [langgraph_agent/tools.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/langgraph_agent/tools.py)

### External dependencies / upstream
LangGraph, model endpoint and local tools.

### Corresponding paper / mechanism
LangGraph docs; generic graph agent pattern.

### What is pedagogically useful
Read state transitions/tool boundary as reference.

### What is implementation-specific noise
Framework wiring and demo behavior are not a standalone mechanism.

### Is it genuinely from scratch?
No; orchestration demo.

### Proposed action
ARCHIVE

### Destination
Health-Copilot; archive generic scaffold.

## llm_agent_zero

Source: [llm_agent_zero](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Agent / Tool Use / Post-training
Source type: ADAPTATION

### What it actually implements
Curriculum and executor roles with custom rewards/data generation/scripts; each role contains a full verl 0.4.1.dev copy. Exact vendor SHA UNVERIFIED.

### Important files
- [llm_agent_zero/curriculum/curriculum_reward.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/curriculum/curriculum_reward.py)
- [llm_agent_zero/curriculum/generate_curriculum_train_data.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/curriculum/generate_curriculum_train_data.py)
- [llm_agent_zero/curriculum/run.sh](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/curriculum/run.sh)
- [llm_agent_zero/executor/executor_reward.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/executor/executor_reward.py)
- [llm_agent_zero/executor/filter_questions.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/executor/filter_questions.py)
- [llm_agent_zero/executor/run.sh](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/executor/run.sh)
- [llm_agent_zero/curriculum/verl/](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/curriculum/verl/)
- [llm_agent_zero/executor/verl/](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/llm_agent_zero/executor/verl/)

### External dependencies / upstream
verl, Transformers, PyTorch, Ray/multi-GPU, checkpoint/data pipeline.

### Corresponding paper / mechanism
Agent0 https://arxiv.org/abs/2511.16043 ; https://github.com/aiming-lab/Agent0

### What is pedagogically useful
Inspect curriculum/executor changes and rewards; consider a toy only for a distinct question.

### What is implementation-specific noise
Duplicated vendored frameworks and large-scale recipe dominate.

### Is it genuinely from scratch?
No; system adaptation with vendored upstream.

### Proposed action
READ_ONLY

### Destination
TraceSearch-R1 overlap; no separate repository.

## pdf2markdown

Source: [pdf2markdown](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/pdf2markdown)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Multimodal / Document AI
Source type: ADAPTATION

### What it actually implements
PDF-to-Markdown pipeline around RapidLayout and pretrained Qwen2-VL. README says it is secondarily based on gptpdf; exact revision UNVERIFIED.

### Important files
- [pdf2markdown/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/pdf2markdown/README.md)
- [pdf2markdown/pdf2markdown.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/pdf2markdown/pdf2markdown.py)

### External dependencies / upstream
RapidLayout, Transformers/Qwen2-VL, local checkpoint, OCR/layout dependencies.

### Corresponding paper / mechanism
gptpdf https://github.com/CosmosShadow/gptpdf ; exact local provenance UNVERIFIED.

### What is pedagogically useful
Useful only as document-pipeline reference.

### What is implementation-specific noise
Pretrained VLM and document tooling dominate; no isolated LLM algorithm.

### Is it genuinely from scratch?
No; application adaptation.

### Proposed action
ARCHIVE

### Destination
No satellite.

## ppo_from_scratch

Source: [ppo_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/ppo_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
Handwritten actor-critic PPO with rollout buffer, reward model, KL reward, GAE and clipped policy/value losses.

### Important files
- [ppo_from_scratch/ppo_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/ppo_from_scratch/ppo_train.py)

### External dependencies / upstream
PyTorch, Transformers actor/reward models, data and accelerator.

### Corresponding paper / mechanism
PPO https://arxiv.org/abs/1707.06347

### What is pedagogically useful
Strip to a categorical policy and scalar trajectories to study equations.

### What is implementation-specific noise
RLHF reward/data orchestration is much larger than objective.

### Is it genuinely from scratch?
Partly; update mechanics handwritten, language-model stack upstream.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-005–006.

## rag_demo

Source: [rag_demo](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rag_demo)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Retrieval / Long Context / Memory
Source type: DEMO

### What it actually implements
Chinese BM25 plus FAISS dense retrieval, RRF fusion and local Qwen prompting over a small medical corpus.

### Important files
- [rag_demo/rag.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rag_demo/rag.ipynb)
- [rag_demo/medical_data.txt](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rag_demo/medical_data.txt)

### External dependencies / upstream
BM25/FAISS, embedding model, local Qwen path.

### Corresponding paper / mechanism
Hybrid RAG/RRF demo.

### What is pedagogically useful
Notebook is a reference for retrieval components.

### What is implementation-specific noise
Small corpus and pipeline wiring are not a distinct reproduction.

### Is it genuinely from scratch?
No; demo.

### Proposed action
ARCHIVE

### Destination
Health-Copilot covers retrieval/evaluation.

## reinforce++

Source: [reinforce++](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/reinforce++)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training
Source type: ADAPTATION

### What it actually implements
Subclass of TRL RLOOTrainer with custom advantage normalization and token KL handling toward REINFORCE++ recipe.

### Important files
- [reinforce++/train_reinforce++.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/reinforce++/train_reinforce++.py)
- [reinforce++/data_process.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/reinforce++/data_process.ipynb)

### External dependencies / upstream
TRL, Transformers, Accelerate and model/data setup.

### Corresponding paper / mechanism
REINFORCE++ https://arxiv.org/abs/2501.03262

### What is pedagogically useful
Compare estimator equations in the shared policy-gradient lab.

### What is implementation-specific noise
Inherited trainer semantics and recipe details complicate attribution.

### Is it genuinely from scratch?
No; framework subclass/adaptation.

### Proposed action
READ_ONLY

### Destination
Reference only unless isolated estimator question emerges.

## remax

Source: [remax](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/remax)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training
Source type: ADAPTATION

### What it actually implements
HF/TRL rollout helpers with greedy-response baseline and ReMax-style policy objective.

### Important files
- [remax/train_remax.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/remax/train_remax.py)
- [remax/data_process.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/remax/data_process.ipynb)

### External dependencies / upstream
TRL/Transformers, Accelerate and model/data recipe.

### Corresponding paper / mechanism
ReMax https://arxiv.org/abs/2310.10505

### What is pedagogically useful
Isolate greedy baseline/objective in synthetic policy space.

### What is implementation-specific noise
Rollout helpers and training recipe are framework glue.

### Is it genuinely from scratch?
No; framework adaptation.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-007.

## rloo

Source: [rloo](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rloo)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Post-training
Source type: ADAPTATION

### What it actually implements
TRL RLOOTrainer subclass/custom training loop using leave-one-out baseline.

### Important files
- [rloo/train_rloo.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rloo/train_rloo.py)
- [rloo/data_process.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/rloo/data_process.ipynb)

### External dependencies / upstream
TRL, Transformers, Accelerate, dataset/model.

### Corresponding paper / mechanism
RLOO https://arxiv.org/abs/2402.14740

### What is pedagogically useful
Compare against ReMax with shared samples.

### What is implementation-specific noise
Trainer inherits substantial behavior outside the custom file.

### Is it genuinely from scratch?
No; trainer adaptation.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-007.

## s1_from_scratch

Source: [s1_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/s1_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Reasoning / Test-Time Compute
Source type: ADAPTATION

### What it actually implements
Fine-tunes pretrained Qwen2.5-0.5B with HF Trainer/LoRA; generation uses VLLM model but does not implement full s1 budget forcing.

### Important files
- [s1_from_scratch/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/s1_from_scratch/README.md)
- [s1_from_scratch/s1_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/s1_from_scratch/s1_train.py)
- [s1_from_scratch/generate.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/s1_from_scratch/generate.py)

### External dependencies / upstream
Transformers, PEFT, VLLM, pretrained Qwen checkpoint/data.

### Corresponding paper / mechanism
s1 https://arxiv.org/abs/2501.19393

### What is pedagogically useful
Implement budget controller separately with a stub/small model.

### What is implementation-specific noise
Fine-tuning and serving dependencies are not the inference-time mechanism.

### Is it genuinely from scratch?
No; pretrained fine-tuning, incomplete s1 recipe.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-027.

## table_extract

Source: [table_extract](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/table_extract)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Multimodal / Document AI
Source type: DEMO

### What it actually implements
Notebook joins ModelScope table structure recognition and PaddleOCR geometry into formatted table output.

### Important files
- [table_extract/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/table_extract/README.md)
- [table_extract/table2txt.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/table_extract/table2txt.ipynb)

### External dependencies / upstream
ModelScope, PaddleOCR and pretrained document models.

### Corresponding paper / mechanism
Document table extraction pipeline.

### What is pedagogically useful
Could be useful as document-processing reference.

### What is implementation-specific noise
OCR/layout integration, not LLM reproduction.

### Is it genuinely from scratch?
No; demo.

### Proposed action
ARCHIVE

### Destination
No satellite.

## train_llm_from_scratch

Source: [train_llm_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Pretraining / Model Architecture
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
Custom decoder includes RMSNorm, RoPE, GQA repeat_kv, attention, MLP, HF PreTrainedModel wrapper, CE and generation. Tokenizer notebook uses byte BPE; SFT/DPO scripts are beyond README; README points to MiniMind data.

### Important files
- [train_llm_from_scratch/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch/README.md)
- [train_llm_from_scratch/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch/train.py)
- [train_llm_from_scratch/train_tokenizer.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch/train_tokenizer.ipynb)
- [train_llm_from_scratch/sft_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch/sft_train.py)
- [train_llm_from_scratch/dpo_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch/dpo_train.py)
- [train_llm_from_scratch/dataset.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_llm_from_scratch/dataset.py)

### External dependencies / upstream
PyTorch and Transformers wrapper; tokenizer/data scripts; MiniMind data reference.

### Corresponding paper / mechanism
GPT-style causal LM; GQA https://arxiv.org/abs/2305.13245 ; DPO https://arxiv.org/abs/2305.18290

### What is pedagogically useful
Handwritten model core and small tokenizer/training path.

### What is implementation-specific noise
HF integration, data acquisition and training utilities remain dependencies.

### Is it genuinely from scratch?
Partly; useful handwritten core, not zero-dependency.

### Proposed action
REPRODUCE

### Destination
LLM-From-Scratch, REP-001–003 and REP-013.

## train_moe_from_scratch

Source: [train_moe_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_moe_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Model Architecture / Pretraining
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
Reuses the small decoder foundation and adds top-k router, expert MLPs and balance loss; includes pretraining/SFT scripts.

### Important files
- [train_moe_from_scratch/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_moe_from_scratch/README.md)
- [train_moe_from_scratch/moe_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_moe_from_scratch/moe_train.py)
- [train_moe_from_scratch/moe_sft_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_moe_from_scratch/moe_sft_train.py)
- [train_moe_from_scratch/dataset.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_moe_from_scratch/dataset.py)

### External dependencies / upstream
PyTorch, Transformers wrapper, model/data config.

### Corresponding paper / mechanism
Switch/MoE https://arxiv.org/abs/2101.03961

### What is pedagogically useful
Study sparse dispatch and balance loss on tiny backbone.

### What is implementation-specific noise
Duplicated decoder files/data are secondary.

### Is it genuinely from scratch?
Partly; MoE mechanism handwritten on framework scaffold.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
LLM-From-Scratch, REP-004.

## train_multimodal_from_scratch

Source: [train_multimodal_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Multimodal
Source type: ADAPTATION

### What it actually implements
Loads pretrained SigLIP and Qwen2.5-0.5B; trains two-layer projector/image packing with CE; includes pretraining/SFT, multi-image variants and Gradio demo.

### Important files
- [train_multimodal_from_scratch/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch/README.md)
- [train_multimodal_from_scratch/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch/train.py)
- [train_multimodal_from_scratch/sft_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch/sft_train.py)
- [train_multimodal_from_scratch/sft_train_multi_images.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch/sft_train_multi_images.py)
- [train_multimodal_from_scratch/trainer.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_multimodal_from_scratch/trainer.ipynb)

### External dependencies / upstream
Transformers; pretrained vision/language checkpoints; LLaVA/Chinese-LLaVA datasets; Gradio.

### Corresponding paper / mechanism
LLaVA https://arxiv.org/abs/2304.08485

### What is pedagogically useful
Study connector and visual token placement with frozen stubs.

### What is implementation-specific noise
Pretrained towers/data and demo make the folder name misleading.

### Is it genuinely from scratch?
No; connector adaptation between pretrained models.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Multimodal-From-Scratch, REP-026.

## train_qwen3_next_from_scratch

Source: [train_qwen3_next_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Model Architecture / Pretraining
Source type: MINIMAL_REIMPLEMENTATION

### What it actually implements
Handwritten full-attention and GatedDeltaNet paths with MoE/configured decoder; no MTP head found. Partial Qwen3-Next reimplementation.

### Important files
- [train_qwen3_next_from_scratch/README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch/README.md)
- [train_qwen3_next_from_scratch/pretrain.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch/pretrain.py)
- [train_qwen3_next_from_scratch/sft_train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch/sft_train.py)
- [train_qwen3_next_from_scratch/moe_test.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch/moe_test.py)
- [train_qwen3_next_from_scratch/test_moe.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_qwen3_next_from_scratch/test_moe.ipynb)

### External dependencies / upstream
PyTorch, Transformers compatibility, tokenizer assets and training data.

### Corresponding paper / mechanism
Qwen3-Next https://qwen.ai/blog?from=res&id=4074cca80393150c248e508aa62983f9cb7d27cd

### What is pedagogically useful
Check recurrence and hybrid schedule at tiny scale.

### What is implementation-specific noise
Not the complete architecture/training recipe; checkpoint compatibility is limited.

### Is it genuinely from scratch?
Partial handwritten blocks, incomplete architecture coverage.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Modern-LLM-Architecture-Lab, REP-016 and REP-019.

## train_siglip_from_scratch

Source: [train_siglip_from_scratch](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_siglip_from_scratch)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Multimodal
Source type: ADAPTATION

### What it actually implements
Loads pretrained image/text AutoModels; custom SigLIP pairwise sigmoid loss with learned scale/bias and MUGE data.

### Important files
- [train_siglip_from_scratch/model.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_siglip_from_scratch/model.py)
- [train_siglip_from_scratch/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_siglip_from_scratch/train.py)
- [train_siglip_from_scratch/dataset.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_siglip_from_scratch/dataset.py)
- [train_siglip_from_scratch/data_process.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/train_siglip_from_scratch/data_process.ipynb)

### External dependencies / upstream
Transformers pretrained image/text encoders and MUGE data.

### Corresponding paper / mechanism
SigLIP https://arxiv.org/abs/2303.15343

### What is pedagogically useful
Recreate the loss on synthetic embeddings, optionally compare contrastive baseline.

### What is implementation-specific noise
Pretrained towers dominate compute and obscure loss learning.

### Is it genuinely from scratch?
No; only loss is custom; encoders pretrained.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
Multimodal-From-Scratch, REP-025.

## training-free_grpo

Source: [training-free_grpo](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/training-free_grpo)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Reasoning / Test-Time Compute / Memory
Source type: ADAPTATION

### What it actually implements
OpenAI-compatible API loop generates and merges experiences and updates prompts/token priors without gradient updates. Distinct from parameter-training GRPO.

### Important files
- [training-free_grpo/train.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/training-free_grpo/train.py)
- [training-free_grpo/prompts.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/training-free_grpo/prompts.py)
- [training-free_grpo/compress.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/training-free_grpo/compress.py)

### External dependencies / upstream
OpenAI-compatible endpoint/credentials if run as written; can simulate offline.

### Corresponding paper / mechanism
Training-Free GRPO https://arxiv.org/abs/2510.08191

### What is pedagogically useful
Reproduce memory aggregation offline on deterministic toy rollouts.

### What is implementation-specific noise
API cost/prompt management are not needed to study core update.

### Is it genuinely from scratch?
No; API-driven adaptation, no weight gradients.

### Proposed action
REIMPLEMENT_DIFFERENTLY

### Destination
PostTraining-From-Scratch, REP-034 as a simulated P2 study.

## Root files

### .gitignore

Source: [.gitignore](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/.gitignore)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Repository metadata
Source type: UNKNOWN

### What it actually implements
Ignore rules only; no reproduction topic.

### Important files
- [.gitignore](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/.gitignore)

### External dependencies / upstream
Git conventions.

### Corresponding paper / mechanism
None.

### What is pedagogically useful
No reproduction value.

### What is implementation-specific noise
Housekeeping.

### Is it genuinely from scratch?
No; metadata.

### Proposed action
ARCHIVE

### Destination
Atlas metadata only.

### README.md

Source: [README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/README.md)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Repository metadata
Source type: UNKNOWN

### What it actually implements
Short overview; it does not document all source components.

### Important files
- [README.md](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/README.md)

### External dependencies / upstream
No substantial requirements recorded.

### Corresponding paper / mechanism
Repository intent only.

### What is pedagogically useful
Starting point for author intent.

### What is implementation-specific noise
Inventory is incomplete.

### Is it genuinely from scratch?
No; metadata.

### Proposed action
READ_ONLY

### Destination
references/wyf3-llm-related.md.

### all_embd_to_openai.py

Source: [all_embd_to_openai.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/all_embd_to_openai.py)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Inference / Integration
Source type: DEMO

### What it actually implements
FastAPI OpenAI-compatible embeddings endpoint backed by OpenVINO BGE CPU inference and token handling.

### Important files
- [all_embd_to_openai.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/all_embd_to_openai.py)

### External dependencies / upstream
FastAPI, OpenVINO, local BGE model assets.

### Corresponding paper / mechanism
Embedding API compatibility; no novel model method.

### What is pedagogically useful
Useful CPU inference/API adapter example.

### What is implementation-specific noise
Wrapper and local model setup dominate.

### Is it genuinely from scratch?
No; integration shim.

### Proposed action
ARCHIVE

### Destination
No satellite.

### date_modify.ipynb

Source: [date_modify.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/date_modify.ipynb)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Domain-specific utility
Source type: DEMO

### What it actually implements
Date/time extraction experiments using jionlp and LLM endpoint calls.

### Important files
- [date_modify.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/date_modify.ipynb)

### External dependencies / upstream
jionlp and optional LLM endpoint/configuration.

### Corresponding paper / mechanism
Date extraction/normalization utility.

### What is pedagogically useful
Small language-aware parsing examples.

### What is implementation-specific noise
Notebook endpoint experiments; narrow scope.

### Is it genuinely from scratch?
No; utility notebook.

### Proposed action
ARCHIVE

### Destination
No satellite.

### gradio_mcp_client.py

Source: [gradio_mcp_client.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gradio_mcp_client.py)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Agent / Tool Use / Harness
Source type: DEMO

### What it actually implements
Gradio MCP SSE client with dynamic tools and OpenAI chat completions.

### Important files
- [gradio_mcp_client.py](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/gradio_mcp_client.py)

### External dependencies / upstream
Gradio, MCP SSE transport and compatible chat API.

### Corresponding paper / mechanism
MCP protocol integration.

### What is pedagogically useful
Dynamic tool schema exchange.

### What is implementation-specific noise
UI/provider/server wiring dominates.

### Is it genuinely from scratch?
No; integration demo.

### Proposed action
ARCHIVE

### Destination
Health-Copilot only if a concrete need arises.

### table_rag.ipynb

Source: [table_rag.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/table_rag.ipynb)
Commit: a492338499a9381f1714ecda8c802684e0556d3e
Category: Retrieval / Document AI
Source type: DEMO

### What it actually implements
DOCX tables become header-row chunks, then local BGE/FAISS/Qwen retrieval; includes Mammoth HTML splitting.

### Important files
- [table_rag.ipynb](https://github.com/wyf3/llm_related/tree/a492338499a9381f1714ecda8c802684e0556d3e/table_rag.ipynb)

### External dependencies / upstream
Mammoth, FAISS, local BGE and Qwen.

### Corresponding paper / mechanism
Table-aware chunking and RAG demo.

### What is pedagogically useful
Table row boundaries are a useful applied design note.

### What is implementation-specific noise
Pipeline duplicates serious retrieval scope.

### Is it genuinely from scratch?
No; demo.

### Proposed action
ARCHIVE

### Destination
Health-Copilot.

## Cross-cutting evidence notes

- “from_scratch” names do not guarantee wholly scratch implementations: SigLIP and VLM modules load pretrained encoders; s1 fine-tunes pretrained Qwen; Qwen3-Next covers selected blocks only.
- Vendored verl trees in code-r1, gdpo and llm_agent_zero lack nested Git history in this clone. Package version 0.4.1.dev does not identify the exact embedded commit; provenance is UNVERIFIED.
- deepseek_learn/dpsk_v4_attention.py lacks an attributable paper/revision pointer in local context; exact claimed DeepSeek V4 correspondence is UNVERIFIED.
- pdf2markdown README names gptpdf as a starting point, but exact imported revision is UNVERIFIED.
- mHC.ipynb and engram.ipynb are prototypes without a training recipe; paper-level fidelity is UNVERIFIED.
