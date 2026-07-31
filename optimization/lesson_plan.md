# Creating and Deploying Production-Ready Agentic Systems

## Module Information

### Goal

To transition participants from merely *using* Large Language Models to *architecting* resilient, scalable, and efficient LLM-powered production systems. The focus is on systemic design and trade-off analysis, rather than specific, proprietary coding implementations.

### Reusable Learning Objectives (RLOs)

*   **RLO 1 (Design):** Critically evaluate and design complex, end-to-end LLM applications using agentic, multi-agent architectures.
*   **RLO 2 (Implement):** Integrate specialized LLM capabilities (Tool Calling, Persona, ReACT) to build functional, real-world solutions.
*   **RLO 3 (Optimize):** Analyze and apply real-life engineering trade-offs (Cost, Latency, Quality) and employ necessary optimization strategies (Quantization) for production deployment.
*   **RLO 4 (Govern):** Critically assess the architectural limitations, ethical risks, and methodological constraints inherent in LLM-based systems.


## Autonomous LLM agents (2 Hours)

**Focus:** Building *smart* applications. How do we give LLMs expertise and autonomy through structure and role?

**Case Study Focus:** Designing a collaborative system for complex task completiReAon. Example used: Paper peer review (subject to change).

**Mini-Project Milestone**: High-level documentation of the proposed system.


### 00:00 - 00:30: The LLM as a System Component

Example: Mathematics
* LLMs very poor at calculating even basic problems
* Identify why these mistakes happen during prompting
* Explain how finetuning and RL won't work (number tokenization issues, LLMs as parrots, hallucinations)
* Explain how reasoning may not work (CoT failure modes)
* Conclusion: We need to provide external help to the LLM

Supporting Material:
* Code: [AthNLP 2025 Lab 5](https://github.com/athnlp/athnlp-labs-2025/blob/main/labs/AthensNLP_Summer_School_Lab5_prompting.ipynb)


### 00:30 - 01:00: Tool-Based Reasoning (ReAct)

Deep dive into the ReACT loop
1. Thought -> Action -> Observation. Focus on the internal mechanism: how the LLM decides what tool to use and how to structure the tool call (structured output). Analyze the role of the execution environment ( "sandbox").
1. Layers of agent autonomy in the ReACT framework (see AthNLP Lab 6)
1. Introduce tool-calling and demonstrate how it is connected with CoT during agent execution
1. Live Demo: Solving math tasks using a simple tool (e.g., a Python script or API call) and tracing the ReACT loop. Participants should analyze a sample ReACT trace log and identify the 'Thought' step and the 'Action' taken.
1. Live Demo: Claude use of tools

Supporting Material:
* Code: [TA2026_AgenticApps from ion](https://eclass.aueb.gr/modules/document/index.php?course=INF312&openDir=/696120c1xPUf) and [AthNLP 2025 Lab 6](https://github.com/athnlp/athnlp-labs-2025/blob/main/labs/athnlp_lab_6.ipynb)
* Slides: [ion slides 52, 53](https://eclass.aueb.gr/modules/document/file.php/INF210/slides_2025_26/nlp_slides_part06_nlp_with_transformers.pdf)


### 01:00 - 02:00 Agent-to-Agent Interaction

Serves as an introduction to the final project for the module.
* Introduce roles, instructions, context as building blocks
* Explain different ways of solving a problem (prompting, one agent, multiple agents, discussion)
* Explain dynamics of the system, and how to evaluate it (present ).
* Introduce project
* Advanced prompting pattern: Injecting sociodemographic information
    * What is the idea behind it?
        * LLMs should know from pretraining how certain groups behave
        * In reality, LLMs don't understand behaviors--they may occasionally accidentally replicate them.
        * Even then, they don't know how these groups behave, but rather which tokens are associated with them (connect with Katerina's lecture), resulting in stereotyping
        * Talk about general limitations
    * Is it useful? Yes.
        * Shifts output distribution (although maybe not in the direction we would want)
        * Enables varied outputs, which may lead to emergent properties due to interaction
        * Enables POV generation
    * Examples: Building discussions with and without personas.

Supporting material:
* Code: [AthNLP 2026 Lab6](https://github.com/athnlp/athnlp-labs-2026/blob/main/labs/lab6.ipynb), [AthNLP 2025 Lab 5](https://github.com/athnlp/athnlp-labs-2025/blob/main/labs/AthensNLP_Summer_School_Lab5_prompting.ipynb)
* Slides: [ion slides 50-53](https://eclass.aueb.gr/modules/document/file.php/INF210/slides_2025_26/nlp_slides_part06_nlp_with_transformers.pdf)


## Cost, scalability, evaluation (2 Hours)

### 00:00 - 00:30 Cost & Latency Trade-offs

* Pros and cons of proprietary LLMs (connect with Katerina)
* Open-source cloud providers
* Locally hosted models: Opex vs Capex
* Cost comparison: frameworks, assumptions, project cost analysis
* Development speed vs inference speed
* When should we use proprietary LLMs?


### Inference Optimization

#### 00:30 - 10:00 Quantization

* VRAM and speed constraints
* Quantization as a scalable solution
* The mathematics behind quantization
* Tradeoff: accuracy vs. cost
* Connection with QLora and parameter-aware pretraining

#### 01:00 - 01:30: KV-Caching

### 01:30 - 02:00: System Evaluation 

* Identifying the claims of the system based on this problem.
* What inherent limitations (boundaries) are there based on model capability and architecture decisions?
* Common trap: Believability $\neq$ realism $\neq$ replicability
* What common metrics can we use?
* HCI evaluation

**Mini-Project Milestone**: Create a prototype of the end-to-end system using LLMs as coding and design assistants.


## Bringing everything together, evaluation and student presentations (2 hours)


### 00:00 - 01:00 Legal, ethical and practical considerations
* Infosec sensitive information
* Legal issues: GDPR, EU AI Act
* Ethical issues


### 01:00 - 02:00: Final Presentation

Students will briefly showcase their work, decisions, implementation, and maybe a small demo (requires teams of students to be viable time-wise).

**Mini-Project Milestone**: Participants deliver their final architectural design, detailing their chosen agent flow, how they addressed trade-offs, and how they implemented it (e.g., used LLMs for test generation).

Supporting material:
* Contents: [LLM-Based Social Simulations Require a Boundary](https://arxiv.org/abs/2506.19806), [Examining the Expanding Role of Synthetic Data Throughout the AI Development Pipeline](https://arxiv.org/abs/2501.18493)
