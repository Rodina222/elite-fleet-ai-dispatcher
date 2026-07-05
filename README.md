# AI-Powered Fleet Dispatch System
**Generative AI for Constrained Autonomous Fleet Operations**

*Supervised Fine-Tuning of Qwen2.5-7B-Instruct for multi-class operational decision-making under strict safety constraints.*
---

## Live Demo

Try the deployed application on Hugging Face Spaces:

🤗 https://huggingface.co/spaces/Rodina222/elite-fleet-dispatcher

The demo allows users to submit a mission brief and receive:

- Vehicle recommendation
- Step-by-step reasoning
- Safety-aware decision making

---

##  Key Metrics Achieved
* **Vehicle Selection Accuracy:** `25%` (baseline) → `81%`
* **Safety Adherence Rate:** `100%` (zero-tolerance constraint enforced)
* **Reasoning Quality (BERTScore F1):** `0.953` on held-out evaluation set
* **Task Type:** 5-class constrained decision classification

##  Project Overview
This project focuses on adapting a Large Language Model (LLM) for constrained operational decision-making in high-end fleet dispatch scenarios. 

The model receives structured mission briefs and must:
1. Select the optimal vehicle (from 5 dynamically generated options).
2. Respect hard safety constraints (e.g., maintenance flags, driver fatigue).
3. Generate a coherent, step-by-step reasoning trace.

Unlike generic chat fine-tuning, this project targets rule-bound, high-precision decision systems, where incorrect outputs may violate physical or operational safety requirements.

##  Model & Training Setup
* **Base Model:** `Qwen/Qwen2.5-7B-Instruct` (released by Alibaba Cloud, hosted on Hugging Face)
* **Training Method:** Supervised Fine-Tuning (SFT)
* **Parameter-Efficient Fine-Tuning:** LoRA (rank = 32, alpha = 64) via PEFT
* **Optimization Framework:** Unsloth
* **Experiment Tracking:** Weights & Biases (W&B)
* **Inference Tracing:** LangSmith
* **Deployment:** Gradio interface on Hugging Face Spaces

*This setup enables efficient domain adaptation without the computational overhead of full model retraining.*

##  Dataset Description
The custom dataset (`elite_fleet_advanced_reasoning.csv`) consists of **~2,000 supervised instruction samples** in a structured format:
* **Instruction:** System-level dispatch role prompt.
* **Input:** Detailed mission brief with operational constraints (mission type, client profile, telemetry).
* **Output:** Ground-truth vehicle decision + step-by-step reasoning trace.

###  Task Formulation & Data Split
* **Multi-class classification:** 5 vehicle options (`Option 1` – `Option 5`).
* **Balanced Distribution:** ~350–420 samples per option to prevent class collapse.
* **Data Split:** A stratified 90/10 train/validation split was utilized to preserve class balance, improving model generalization and reducing bias during fine-tuning.

##  Learning Objective
The model is trained to jointly optimize:
1. Correct vehicle classification.
2. Constraint compliance (strict adherence to hard safety rules).
3. High-fidelity reasoning trace generation.

##  Research Contribution
This work demonstrates that parameter-efficient fine-tuning (PEFT) of a 7B parameter LLM can achieve:
* **>80%** constrained decision accuracy
* **>95%** reasoning semantic fidelity
* **100%** enforcement of hard safety constraints

...all without full model retraining. It provides strong evidence that LLMs can be adapted beyond conversational and generative tasks into strictly structured, operational intelligence systems.

## Team Contributions

### [Raneem Hussein](https://github.com/Raneemhussien) — Dataset Preparation

Responsible for the complete data pipeline, including:

* Designing fleet dispatch scenarios.
* Preparing the supervised instruction dataset.
* Structuring the Instruction–Input–Output format.
* Balancing vehicle classes.
* Organizing and preprocessing the dataset for training.

### [Rodina Khallaf](https://github.com/Rodina222) — Model Development

Responsible for the complete machine learning pipeline, including:

* Selecting the base LLM.
* Designing the fine-tuning approach.
* Implementing the LoRA training pipeline.
* Training and validating the model.
* Hyperparameter configuration.
* Performance evaluation.
* Experiment tracking using Weights & Biases.
* Inference monitoring with LangSmith.
* Deploying the trained model to Hugging Face Spaces.

##  Limitations & Future Work
* **Data Distribution:** The dataset is semi-synthetic and may not perfectly capture real-world distribution shifts or edge-case anomalies.
* **Robustness:** Performance under adversarial or heavily out-of-distribution prompts requires further evaluation.
* **Future Work:** Implementing Reinforcement Learning from Human Feedback (RLHF) or constraint-aware decoding strategies could further enhance operational robustness.


