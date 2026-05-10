# NCERT_3B_v0.1
A 3B parameter, GRPO fine-tuned reasoning model trained on the NCERT dataset (Classes 6-12). Aggressively 4-bit quantized (GGUF) via Unsloth to run 100% offline on low-end 3-6GB RAM edge devices. Built to bridge the digital divide in education.
# 🥊 NCERT_3B_v0.1 (The "Brawler")

An edge-optimized, GRPO fine-tuned reasoning engine built specifically to run 100% offline on budget smartphones. 

### 📖 The Story: Bridging the Divide
This project was born out of a 30-hour sleepless engineering sprint to solve a massive frustration: the digital divide in education. Elite reasoning AI is almost exclusively locked behind expensive cloud APIs or high-end hardware. As an AI engineer navigating the rigors of the Class 12 curriculum—from thermodynamics to matrix operations—I realized that true educational equity means taking elite AI out of the cloud and putting it directly into the pocket of the student. 

The goal wasn't just to build a tutor; it was to build a reasoning engine that could comfortably run on a standard 4GB-6GB RAM mobile phone without internet access.

### ⚙️ The Technical Grind
To make this a reality, I had to bridge massive cloud hardware with extreme edge constraints:
1. **The Muscle:** The training pipeline was executed on an **AMD MI300X** utilizing ROCm. 
2. **The Brain:** Instead of standard instruct-tuning, I utilized **GRPO (Group Relative Policy Optimization) Reinforcement Learning**. The model is heavily penalized if it doesn't think step-by-step. It is forced to generate explicit `<reasoning>` logic before outputting a final `<answer>`, ensuring factual accuracy for complex physics and math problems.
3. **The Diet:** The base Llama-3.2-3B model was aggressively quantized via **Unsloth** into a 4-bit GGUF format. 

**The Result:** A 6.1 GB model compressed into a **1.9 GB** footprint that executes natively on an Android device without hallucinating or crashing the OS memory limits. 

### 📂 Repository Contents
* `PROCESS_ARCHITECTURE.md`: A deep dive into the ROCm setup, GRPO reward functions, and memory management.
* `Training_Log.ipynb`: The raw Jupyter notebook proving the 30-hour fine-tuning process.
* `NCERT_Brawler.html`: An accessible export of the loss metrics and quantization logs.

**Built for the Edge. Built for the Students.**
