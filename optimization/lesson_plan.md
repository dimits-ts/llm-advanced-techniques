# Creating and Deploying Production-Ready Agentic Systems

## Module Information

### Goal
To transition participants from merely *using* Large Language Models to *architecting* resilient, scalable, and efficient LLM-powered production systems. The focus is on systemic design and trade-off analysis, rather than specific, proprietary coding implementations.

### Reusable Learning Objectives (RLOs)

*   **RLO 1 (Design):** Critically evaluate and design complex, end-to-end LLM applications using agentic, multi-agent architectures.
*   **RLO 2 (Implement):** Integrate specialized LLM capabilities (Tool Calling, Persona, ReACT) to build functional, real-world solutions.
*   **RLO 3 (Optimize):** Analyze and apply real-life engineering trade-offs (Cost, Latency, Quality) and employ necessary optimization strategies (Quantization) for production deployment.
*   **RLO 4 (Govern):** Critically assess the architectural limitations, ethical risks, and methodological constraints inherent in LLM-based systems.


## LLMs as system components (2 Hours)

**Focus:** Building *smart* applications. How do we give LLMs expertise and autonomy through structure and role?

**Case Study Focus:** Designing a collaborative system for complex task completion. Example used: Paper peer review (subject to change).

| Topic | Concepts Covered | Impact | Deliverable |
| :--- | :--- | :--- | :--- |
| **The LLM as a System Component** | The fundamental limitations of base LLMs (hallucination, lack of domain scope, narrow thought). Deciding when overcoming these limitations using multi-agent systems may be preferable compared to prompting or finetuning. | Identifying when an LLM needs external structure. Designing the boundaries of the LLM's action-space versus the surrounding execution environment. | Drafting and justifying the high-level strategy used to tackle the Case Study. |
| **Tool-Based Reasoning (ReACT)** | The ReACT framework: *Integrating Thought $\rightarrow$ Action $\rightarrow$ Observation*. | How LLM agents already use tools such as coding, CoT prompting, self-critique to tackle complex tasks. | Use an agent to dynamically receive non-standardized documents, and produce input that will be fed to the system. |
| **LLMs in Code Development** | Architectural patterns for integrating LLMs into the Software Development Lifecycle. Moving beyond simple generation to advanced roles (e.g., code review, test case generation, architecture planning). | How LLMs can not only generate code, but also help with project structure and architectural decisions. | Synthetic test-suite, documentation and code-review using LLMs. |

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


### 00:30 - 01:15: Tool-Based Reasoning (ReACT)

Deep dive into the ReACT loop
1. Thought -> Action -> Observation. Focus on the internal mechanism: how the LLM decides what tool to use and how to structure the tool call (structured output). Analyze the role of the execution environment ( "sandbox").
1. Layers of agent autonomy in the ReACT framework (see AthNLP Lab 6)
1. Introduce tool-calling and demonstrate how it is connected with CoT during agent execution
1. Live Demo: Solving math tasks using a simple tool (e.g., a Python script or API call) and tracing the ReACT loop. Participants should analyze a sample ReACT trace log and identify the 'Thought' step and the 'Action' taken.

Supporting Material:
* Code: [TA2026_AgenticApps from ion](https://eclass.aueb.gr/modules/document/index.php?course=INF312&openDir=/696120c1xPUf) and [AthNLP 2025 Lab 6](https://github.com/athnlp/athnlp-labs-2025/blob/main/labs/athnlp_lab_6.ipynb)
* Slides: [ion slides 52, 53](https://eclass.aueb.gr/modules/document/file.php/INF210/slides_2025_26/nlp_slides_part06_nlp_with_transformers.pdf)


### 01:15 - 02:00: LLMs in Code Development

* The difference between "Code Generation" (low complexity, quick output) and "Code Augmentation/Refinement" (high complexity, iterative feedback, systemic thinking).
    * Connect former with ReACT: calculator vs Claude in identifying bugs in a library
    * Connect latter with model capabilities (local model vs proprietary model)
    * When should we use either?
* In what other domains can we use LLMs?
    * Documentation: Docstrings and sphinx
    * Tests (Test-driven development?)
    * Code reviews: Potential, challenges, limitations

Supporting material:
* Code: [AthNLP 2025 Lab 5](https://github.com/athnlp/athnlp-labs-2025/blob/main/labs/AthensNLP_Summer_School_Lab5_prompting.ipynb)
* Slides: [ion slides 50-53](https://eclass.aueb.gr/modules/document/file.php/INF210/slides_2025_26/nlp_slides_part06_nlp_with_transformers.pdf)


## Autonomous LLM agents: Costs, safety, scalability (2 Hours)

**Focus:** Building *functional* applications. How do we make LLMs act on the real world and correct their own mistakes? Making applications *efficient, affordable, and safe* in a production environment.

| Topic | Concepts Covered | Impact | Deliverable |
| :--- | :--- | :--- | :--- |
| **Persona Prompting** | Defining the AI's role, expertise, constraints, and tone (The "System Prompt"). Techniques for maintaining role consistency and ensuring the LLM acts as a true domain expert. | Prompt Engineering for *identity*. Controlling output quality and style through constraints and meta-prompts. | Demo focused on implementing agent configurations (personas, prompts).|
| **Agent-to-Agent Interaction** | The concept of multiple specialized agents collaborating (e.g., summarizer agent, stakeholder agents, decision-maker agent). Using LLM-only synthetic discussions as an example of internal validation. | Orchestration patterns (defining conversational/task flow templates). Managing state between collaborating components. | Workflow Diagram |
| **Cost & Latency Trade-offs** | The financial and performance realities of LLM deployment. Benchmarking large vs. small models vs. local inference. Strategic model selection based on task complexity vs. budget. | **Economics/DevOps:** Analyzing the total cost of ownership (TCO) for an LLM system. Designing application logic to minimize redundant API calls and excessive token generation. | Cost analysis |
| **Inference Optimization** | Conceptual understanding of model optimization techniques: **Quantization** (reducing precision for memory/speed) and its impact on model accuracy. | **Deployment:** Understanding the operational side of model serving (e.g., choosing optimized inference engines). | Optimization Strategy Plan |



**Mini-Project Milestone**: Create a prototype of the end-to-end system using LLMs as coding and design assistants.


### 00:00 - 00:30 Persona Prompting

Advanced prompting pattern: Injecting sociodemographic information
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
* Code: [AthNLP 2026 Lab6](https://github.com/athnlp/athnlp-labs-2026/blob/main/labs/lab6.ipynb)


### 00:30 - 01:00 Agent-to-Agent Interaction
Serves as an introduction to the final project for the module.
* Introduce roles, instructions, context as building blocks
* Explain different ways of solving a problem (prompting, one agent, multiple agents, discussion)
* Introduce project

Supporting material:
* Code: [AthNLP 2026 Lab6](https://github.com/athnlp/athnlp-labs-2026/blob/main/labs/lab6.ipynb)


### 01:00 - 01:30 Cost & Latency Trade-offs


* Pros and cons of proprietary LLMs (connect with Katerina)
* Open-source cloud providers
* Locally hosted models: Opex vs Capex
* Cost comparison: frameworks, assumptions, project cost analysis
* Infosec: Legal and ethical issues, GDPR, EU AI Act, sensitive corporate information
* Development speed vs inference speed
* When should we use proprietary LLMs?


### 01:30 - 02:00: Quantization

* VRAM and speed constraints
* Quantization as a scalable solution
* The mathematics behind quantization
* Tradeoff: accuracy vs. cost
* Connection with QLora and parameter-aware pretraining


## Bringing everything together, evaluation and student presentations (2 hours)

| Topic | Concepts Covered | Impact | Deliverable |
| :--- | :--- | :--- | :--- |
| **System Evaluation**| System evaluation according to goals and claims. Common, reusable metrics. | Recognizing what can be tested and what can be achieved by multiagent systems. | System Evaluation Document |
| **Full Architecture Review** | How the Agent, the Tools, prompts, setup, and the Optimization Strategy combine into a single production pipeline. | Building a comprehensive end-to-end architectural diagram that accounts for all system components. | Final System Diagram |
| **Final Presentation** | Conducting a final review of the system implemented in the project. | Justifying decisions and implementation based on lessons from this module. | Final presentation and demo. | 

**Mini-Project Milestone**: Participants deliver their final architectural design, detailing their chosen agent flow, how they addressed trade-offs, and how they implemented it (e.g., used LLMs for test generation).


### 00:00 - 00:45: System Evaluation 

* Identifying the problem to be solved (which may be different from what originally planned).
* Identifying the claims of the system based on this problem.
* What inherent limitations (boundaries) are there based on model capability and architecture decisions?
* Common trap: Believability $\neq$ realism $\neq$ replicability
* How do we quantify whether we solved the claims?
* When is a claim sufficiently supported?
* What common metrics can we use?
* What happens in practise?


### 00:45 - 01:10: Full Architecture Review

Summarize the entire module and link it to previous modules.


### 01:10 - 02:00: Final Presentation

Students will briefly showcase their work, decisions, implementation, and maybe a small demo (requires teams of students to be viable time-wise).


Supporting material:
* Contents: [LLM-Based Social Simulations Require a Boundary](https://arxiv.org/abs/2506.19806), [Examining the Expanding Role of Synthetic Data Throughout the AI Development Pipeline](https://arxiv.org/abs/2501.18493)