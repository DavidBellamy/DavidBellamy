![Python](https://img.shields.io/badge/Python-Expert-3776AB?style=flat&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-Distributed-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![CUDA](https://img.shields.io/badge/CUDA-NCCL_/_PTX-76B900?style=flat&logo=nvidia&logoColor=white)
![SGLang](https://img.shields.io/badge/Inference-SGLang-blue?style=flat)
![vLLM](https://img.shields.io/badge/Inference-vLLM-blue?style=flat)
![RDMA](https://img.shields.io/badge/Networking-RDMA_/_mooncake-326CE5?style=flat)
![Kubernetes](https://img.shields.io/badge/Infra-Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Tools-Docker-2496ED?style=flat&logo=docker&logoColor=white)

### Hi, I'm David Bellamy.

I am a **Infrastructure Engineer for agentic training** and a Harvard PhD Statistician.

I am currently at Institute of Foundation Models (ifm.ai) building the reinforcement learning infrastructure for agentic training of a frontier-scale model that the team pretrained and midtrained in-house.

My work spans the **entire agentic RL training stack**: per-rollout sandbox runtimes, the agent layer, the Rust inference gateway, the inference engines, and the trainer. Recurring themes include cross-image NCCL weight transport between trainer and rollout engines, disaggregated prefill/decode reliability on multi-rail HGX fabrics, tokenizer-consistent training-on-rollouts (TITO), and per-rollout container orchestration at scale.

---

### Selected recent contributions (since March 2026)

I work across the full agentic-RL stack: sandbox runtime → agent layer → Rust gateway → inference engine ↔ trainer. Recent contributions span every layer.

**Inference-engine internals (vLLM / SGLang)**

| PR | Stack | Summary |
| :--- | :--- | :--- |
| [vllm#38669](https://github.com/vllm-project/vllm/pull/38669) | CUDA / PTX | Fix Marlin MoE repack PTX incompatibility on H100/H200 under CUDA 12.8. |
| [sglang#23003](https://github.com/sgl-project/sglang/pull/23003) | RDMA / PD | Per-GPU JSON mapping for `--disaggregation-ib-device`, enabling rail-aligned PD on HGX H100/H200. |
| [LLM360/sglang#12](https://github.com/LLM360/sglang/pull/12) | PyNCCL | Opt-in PyNCCL transport for the weight-update side group; trainer and rollout containers can ship different `libnccl` versions. Key for facilitating weight updates between trainer engines and inference engines. |
| [LLM360/sglang#14](https://github.com/LLM360/sglang/pull/14) | InfiniBand verbs | Serialize `ibv_reg_mr` to defend mooncake against an `nvidia-peermem` race that segfaults under concurrent GPU memory registration in SR-IOV VF environments. |

**Cross-stack gateway (Rust)**

| PR | Summary |
| :--- | :--- |
| [smg#1130](https://github.com/lightseekorg/smg/pull/1130) **(merged)** | `#[serde(flatten)]` catch-all on `ChatCompletionRequest` so engine-specific JSON fields (SGLang's `return_routed_experts` etc.) survive gateway deserialization. Fixes [upstream sglang issue #22740](https://github.com/sgl-project/sglang/issues/22740). |
| [smg#1239](https://github.com/lightseekorg/smg/pull/1239) | Mirrors flatten to six chat response structs so `routed_experts` and `completion_token_ids` round-trip end-to-end. |
| [smg#1238](https://github.com/lightseekorg/smg/pull/1238) | Strip `content-length` in `preserve_response_headers`. Catches a latent defensive bug in body-modification paths. |

**Distributed training reliability (Python trainer)**

| PR | Summary |
| :--- | :--- |
| [LLM360/miles#11](https://github.com/LLM360/miles/pull/11) **(merged)** | MoE routing-replay correctness: per-row complement padding avoids within-row expert-id duplicates. |
| [miles#1003](https://github.com/radixark/miles/pull/1003) | Per-rank `all_to_all_single` diagnostics for expert-parallel routing-replay split-size divergence. |
| [miles#888](https://github.com/radixark/miles/pull/888) | Restart-tolerant session proxy: router restarts (Ray failover, node loss) become transparent to active agents instead of cascading 404s. |

**Agentic RL system design (TITO)**

TITO (token-in / token-out) keeps exact inference-engine token IDs end-to-end, eliminating tokenizer-drift bugs in training-on-rollouts. The plumbing spans all four open-source layers of the stack:

- [harbor#1454](https://github.com/harbor-framework/harbor/pull/1454): agent-layer infrastructure (+379 lines).
- [LLM360/sglang#13](https://github.com/LLM360/sglang/pull/13) / [#15](https://github.com/LLM360/sglang/pull/15): engine surfaces completion token IDs and tokenizer SHA256 on `/get_model_info`.
- [smg#1239](https://github.com/lightseekorg/smg/pull/1239): gateway preserves engine-specific response fields.
- [miles#1024](https://github.com/radixark/miles/pull/1024): trainer-side TITO tokenizer supports agent-inserted assistant turns (e.g. terminus-2 / SWE-agent self-reflection).

**Per-rollout sandbox runtime (closed-source)**

Designed and operate the per-rollout sandbox layer: a Kubernetes cluster that spins up an isolated container for each agent rollout and persists tool/filesystem state across the rollout's lifetime. Scaled to **12,000 concurrent sandbox pods**, which surfaced (and required solving) cluster-wide network bandwidth saturation and host-level file-descriptor exhaustion.

---

### Earlier work

| Project | Description |
| :--- | :--- |
| [grpo-gsm8k](https://github.com/DavidBellamy/grpo-gsm8k) | Bare-metal GRPO on GSM8k. Decoupled training (Torch) and inference (vLLM). 83.2% Pass@1, matching SFT baselines while recovering reasoning capabilities. ([W&B report](https://api.wandb.ai/links/davidbellamy/acloshqg)) |
| [Labrador](https://github.com/DavidBellamy/labrador) | ML4H 2024 Best Paper. Empirical limits of masked LM pretraining on tabular EHR data. |
| [suttonbarto](https://github.com/DavidBellamy/suttonbarto) | Sutton & Barto exercises with rigorous derivations. |

---

<div align="left">
  <a href="https://scholar.google.com/citations?user=ZialG8UAAAAJ&hl=en">
    <img src="https://img.shields.io/badge/Google_Scholar-David_R._Bellamy-4285F4?style=for-the-badge&logo=google-scholar&logoColor=white" alt="Google Scholar"/>
  </a>
</div>
