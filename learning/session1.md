# Lesson Plan: Prompting vs Fine-Tuning with LoRA and QLoRA

## Reusable Learning Objective (RLO)

By the end of this session, participants will understand:
1. How LoRA and QLoRA enable efficient fine-tuning of large language models and will be able to follow a complete fine-tuning workflow conceptually and in practice 
1. Differentiate between supervised fine-tuning (SFT) and preference-based alignment (DPO/GRPO)

The focus is on building intuition for when prompting is sufficient, when fine-tuning is necessary, and how parameter-efficient fine-tuning works in modern LLM systems and how alignment techniques are essential for injecting reliability and safety into production LLM systems.


## Narrative

The session is structured around a single practical problem:

**Biomedical information extraction from unstructured text into a structured schema**

Participants will observe how the same task behaves under:

* Prompting only
* Fine-tuning with LoRA
* Efficient training with QLoRA
* Further training with GRPO/DPO

The goal is to show how model behavior shifts from flexible but inconsistent outputs to structured and reliable predictions.


## Session Structure

### 0:00 – 0:10 — Introduction and Problem Framing

* Introduce the biomedical extraction task:

  * Extract entities such as disease, gene, drug, and outcome from abstracts
* Show why this is a realistic ML problem:

  * Structured outputs are required in real systems
  * Errors are costly in domain-specific settings
* Set expectations for the session:

  * We are not just improving prompts
  * We are changing how the model behaves

Central idea: Prompting is powerful but limited when consistency and structure matter.


### 0:10 – 0:30 — Prompting as the Baseline

* Demonstrate a few-shot prompt for biomedical extraction
* Show typical failure modes:

  * Missing fields
  * Hallucinated entities
  * Inconsistent formatting across samples
  * Sensitivity to prompt wording

Discussion:

* Why does prompting sometimes fail even with good examples?
* What assumptions are baked into pretrained models?

Transition:
Prompting alone is often not enough when outputs must be reliable and standardized.


### 0:30 – 0:50 — Why Fine-Tuning Exists

* Define fine-tuning as modifying model weights to adapt behavior
* Contrast with prompting:

  * Prompting: changes input behavior
  * Fine-tuning: changes model parameters

Explain limitations of full fine-tuning:

* High GPU memory requirements
* High training cost
* Separate full model per task
* Risk of catastrophic forgetting

Central idea:
Full fine-tuning is powerful but often impractical for most teams and use cases.


### 0:50 – 1:20 — LoRA: Parameter-Efficient Fine-Tuning

* Introduce LoRA as a way to avoid updating all model weights
* Core idea:

  * Freeze base model
  * Learn small low-rank adapter matrices

Explain why this works:

* Large models are overparameterized
* Many task adaptations lie in low-dimensional subspaces

Benefits:

* Far fewer trainable parameters
* Lower memory usage
* Faster training
* Modular task adapters

Central idea:
We are not retraining the model, we are steering it using small updates.

Supporting Material:
* Code: [TA2026_Transformers from ion](https://eclass.aueb.gr/modules/document/index.php?course=INF312&openDir=/696120c1xPUf)

### 1:20 – 1:45 — QLoRA: Making Fine-Tuning Practical

* Introduce QLoRA as LoRA + quantization
* Explain 4-bit quantization conceptually:

  * Model weights stored in lower precision
  * Reduces memory footprint significantly

Key components:

* Base model loaded in 4-bit precision
* LoRA adapters trained on top
* Gradient updates applied only to adapters

Why this matters:

* Enables fine-tuning of large models on limited hardware
* Makes experimentation accessible beyond large research labs

Key idea:
QLoRA turns fine-tuning from an expensive research operation into a practical engineering workflow.


### 1:45 – 2:00 — SFT vs RL

* Introduction to Alignment: Encouraging a model to behave according to desired human values (consistency, safety, format adherence).
  * SFT asks, "What is the correct output?" (A single labeled answer).Alignment asks, ""Of these two outputs, which one is better?"" (A comparative judgment).
    
* Biomedical Example: Given an input abstract, the model generates two outputs:
  * Choice A: Complete, valid JSON structure, but includes a minor semantic error (e.g., wrong gene symbol).
  * Choice B: Perfect JSON structure, but misses one critical entity (e.g., null for drug).
  * If we prioritize perfect format/structure, the preference data dictates that Choice A is worse because it violates the structural constraint, even if the semantics are closer.
  * Discuss how preference data can be gathered automatically (rule-based validators, automated checks for JSON syntax) or through human labeling.


### 2:00 – 2:15 — RLHF and PPO/GRPO

* Briefly introduce the classical RLHF pipeline (PPO/GRPO) for historical context and completeness.
   
  1. SFT: Train the baseline model
  1. Train a separate model (the RM) to assign a scalar score (a ""reward"") to every possible output.
  1. PPO Loop: The LLM generates an output. The RM scores it. The PPO algorithm uses this score to update the LLM's weights, pushing it toward higher scores.
  1. However, is computationally massive. It requires training and maintaining two models (the LLM and the RM), making it overkill for many standard consistency tasks.
* Connection with slide 41 from [ion slides](https://eclass.aueb.gr/modules/document/file.php/INF210/slides_2025_26/nlp_slides_part06_nlp_with_transformers.pdf)
   

### 2:15 - 2:35 — DPO: Direct Preference Optimization (20 min)

* DPO is the modern, efficient method for turning preference data into model updates.
  * Unlike RLHF, DPO eliminates the need for a complex, separate Reward Model (RM)—a major computational bottleneck of older RLHF techniques.
  * Instead of asking the model to maximize a reward score, DPO directly minimizes a "ranking loss." (some math here, enough for students to understand the underlying mechanism)
* Why DPO?
  * Extremely practical, making high-quality alignment accessible even with limited compute (tying back to the QLoRA efficiency theme).
* Connection with slides 42,43,44 from [ion slides](https://eclass.aueb.gr/modules/document/file.php/INF210/slides_2025_26/nlp_slides_part06_nlp_with_transformers.pdf)


### 2:35-2:45 — Pulling it all together
1. Prompting: Flexible idea of the task.
1. QLoRA (SFT): Competence/Accuracy -> The model learns what the answer looks like.
1. DPO (RL): Reliability/Consistency -> The model learns how to behave (e.g., perfectly structured).
1. Real-world production systems require both SFT (for knowledge) and Alignment (for safe, consistent, reliable output).


### Mini-project

1. Load biomedical dataset (structured extraction format)
1. Attach QLoRA adapters using PEFT
1. Optimize format with DPO
1. Compare outputs:
   * Base model with prompting
   * Fine-tuned QLoRA model
   * Fine-tuned DPO model


## Concepts

* Prompting modifies input behavior, not model parameters
* Fine-tuning modifies model behavior through weight updates
* LoRA reduces trainable parameters via low-rank decomposition
* QLoRA enables efficient fine-tuning via quantization
* Real-world ML systems prioritize reliability and consistency over flexibility alone


## Notes

* Reinforce one idea repeatedly: improving behavior does not require retraining everything
* Anchor explanations in the biomedical extraction example
* Avoid deep mathematical derivations; focus on intuition and system behavior
* Use comparisons frequently to show tradeoffs
* Keep attention on "why this matters in practice"


## Expected Outcomes

Participants leave with:

* A mental model of how LoRA and QLoRA work
* Understanding of when fine-tuning is appropriate
* Familiarity with a real Hugging Face PEFT workflow
* Ability to interpret fine-tuning results at a conceptual level
