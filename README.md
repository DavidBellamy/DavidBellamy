![Python](https://img.shields.io/badge/Python-Expert-3776AB?style=flat&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-Native_Internals-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![vLLM](https://img.shields.io/badge/Inference-vLLM-blue?style=flat)
![Kubernetes](https://img.shields.io/badge/Infra-Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Tools-Docker-2496ED?style=flat&logo=docker&logoColor=white)
![W&B](https://img.shields.io/badge/Ops-Weights_&_Biases-FFBE00?style=flat&logo=weightsandbiases&logoColor=black)

### Hi, I'm David Bellamy.

I am a **Post-Training & Reasoning Researcher** and a Harvard PhD Statistician.

I am currently on an engineering sabbatical, building **bare-metal reasoning stacks** to understand the numerics of Reinforcement Learning for LLMs. My focus is on scaling inference-time compute and designing non-parametric value aggregation methods.

---

### Featured Projects

| Project | Description | Stack |
| :--- | :--- | :--- |
| **[grpo-gsm8k](https://github.com/DavidBellamy/grpo-gsm8k)** | **DeepSeek-R1 Reproduction:** A bare-metal implementation of Group Relative Policy Optimization (GRPO) on GSM8k. Decoupled training loop (Torch) and inference (vLLM) on distributed GPUs. | `PyTorch` `vLLM` |
| **[suttonbarto](https://github.com/DavidBellamy/suttonbarto)** | **RL Theory:** Rigorous Python implementations and mathematical proofs for exercises in Sutton & Barto's *Reinforcement Learning*. | `Python` `LaTeX` `NumPy` |
| **[Labrador](https://github.com/DavidBellamy/labrador)** | **ML4H Best Paper:** Code for *Limits of Masked Language Modeling*, benchmarking Transformers vs. XGBoost on tabular EHR data. | `TensorFlow` |

---

### Research Highlights

* **DeepSeek-R1 Replication:** Achieved **83.2% Pass@1** on GSM8k using GRPO, matching SFT baselines while recovering reasoning capabilities. [Read the W&B Report](https://api.wandb.ai/links/davidbellamy/acloshqg).
* **Optimization:** Implemented length-aware batch packing for SFT, reducing padding overhead from 50% → 21%.
* **Best Paper Award (ML4H 2024):** Demonstrated empirical limits of transfer learning in medical tabular data.

---

<div align="left">
  <a href="https://scholar.google.com/citations?user=ZialG8UAAAAJ&hl=en">
    <img src="https://img.shields.io/badge/Google_Scholar-David_R._Bellamy-4285F4?style=for-the-badge&logo=google-scholar&logoColor=white" alt="Google Scholar"/>
  </a>
</div>
