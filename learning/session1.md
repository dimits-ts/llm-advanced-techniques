# Lesson Plan: Prompting vs Fine-Tuning with LoRA and QLoRA

## Reusable Learning Objective (RLO)

By the end of this session, participants will understand how LoRA and QLoRA enable efficient fine-tuning of large language models and will be able to follow a complete fine-tuning workflow conceptually and in practice.

The focus is on building intuition for when prompting is sufficient, when fine-tuning is necessary, and how parameter-efficient fine-tuning works in modern LLM systems.



## Narrative

The session is structured around a single practical problem:

**Biomedical information extraction from unstructured text into a structured schema**

Participants will observe how the same task behaves under:

* Prompting only
* Fine-tuning with LoRA
* Efficient training with QLoRA

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

Intuition:
Instead of updating a large weight matrix W, LoRA approximates updates using:

W + ΔW, where ΔW = A × B (low-rank decomposition)

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



### Mini-project


1. Load biomedical dataset (structured extraction format)
1. Attach LoRA adapters using PEFT
1. Compare outputs:
   * Base model with prompting
   * Fine-tuned LoRA model

Discussion:

* What changed in behavior?
* Why does structure become more reliable after fine-tuning?

Final takeaway:

* Prompting is flexible but inconsistent
* LoRA enables targeted behavioral changes
* QLoRA makes this approach accessible in practice



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
