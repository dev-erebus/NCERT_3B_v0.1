# NCERT_3B_v0.1

3B-parameter reasoning model fine-tuned via Group Relative Policy Optimization (GRPO) on structured NCERT Class 6–12 STEM curricula (Physics, Chemistry, Mathematics, and Biology), quantized to GGUF (`2.02 GB`) for offline execution on constrained mobile and consumer hardware.

* **Model Weights & GGUF Artefact:** [huggingface.co/Erebus007/NCERT_3B_v0.1](https://huggingface.co/Erebus007/NCERT_3B_v0.1)[cite: 2]
* **Base Architecture:** `Llama-3.2-3B` (`llama` family, `3B` parameters)[cite: 2]
* **Fine-Tuning Objective:** Unsloth QLoRA + Group Relative Policy Optimization (GRPO)
* **Artefact Footprint:** `2.02 GB` (`NCERT_3B_v0.1.gguf`)

---

## Model & Quantization Specification

| Parameter / Component | Verified Specification |
| :--- | :--- |
| **Repository Identifier** | `Erebus007/NCERT_3B_v0.1` (Verified commit `63fce13`)[cite: 1, 2] |
| **Base Architecture** | `Llama-3.2-3B` (`llama` architecture, 3B parameters)[cite: 2] |
| **Training Corpus** | 10,000 structured NCERT knowledge cards (Classes 6–12: Physics, Chemistry, Mathematics, Biology)[cite: 3] |
| **Alignment / RL Method** | Group Relative Policy Optimization (GRPO) via Unsloth QLoRA[cite: 3] |
| **Output Protocol** | Structured `<reasoning>...</reasoning>` derivation block followed by `<answer>...</answer>` |
| **Training Hardware** | AMD Instinct MI300X (ROCm backend) |
| **Serialized Artefact** | `NCERT_3B_v0.1.gguf` (`2.02 GB` single-file GGUF)[cite: 1] |
| **Deployment Envelope** | 100% offline inference; validated for 3 GB–6 GB RAM Android and consumer hardware[cite: 3] |

---

## Training Methodology & Grounding Invariants

Standard supervised fine-tuning on textbook question-answer pairs optimises surface token likelihood without verifying intermediate derivations. `NCERT_3B_v0.1` applies **Group Relative Policy Optimization (GRPO)** across 10,000 verified NCERT curriculum cards[cite: 3] under explicit structural and factual invariants:

| Invariant / Stage | Mechanism | Failure Mode Prevented |
| :--- | :--- | :--- |
| **Structural Reasoning Gate** | Enforces `<reasoning>...</reasoning>` generation prior to emitting `<answer>...</answer>`. | Prevents direct heuristic guessing on multi-step Physics and Mathematics derivations. |
| **Curriculum Grounding Reward** | Scores intermediate derivation steps and final numerical/symbolic outputs against verified NCERT Class 6–12 solutions[cite: 3]. | Suppresses ungrounded parametric drift outside CBSE/NCERT curriculum boundaries. |
| **Offline GGUF Serialisation** | Compresses FP16 weights (~6.1 GB) into a `2.02 GB` GGUF binary (`NCERT_3B_v0.1.gguf`)[cite: 1]. | Eliminates network latency and fits within constrained mobile userspace memory limits. |

---

## Local Execution (`llama.cpp`)

Download `NCERT_3B_v0.1.gguf` (`2.02 GB`) from [Hugging Face](https://huggingface.co/Erebus007/NCERT_3B_v0.1)[cite: 1, 2] and run offline inference via `llama-cli` or `llama-server`:

```bash
# CLI interactive / single-prompt inference
./llama-cli \
  -m NCERT_3B_v0.1.gguf \
  -c 2048 \
  --temp 0.2 \
  -p "Derive the expression for the electric field on the axial line of an electric dipole."
