# Creating and Deploying Production-Ready Agentic Systems

## Module Information

### Goal
To transition participants from merely *using* Large Language Models to *architecting* resilient, scalable, and efficient LLM-powered production systems. The focus is on systemic design and trade-off analysis, rather than specific, proprietary coding implementations.

### Reusable Learning Objectives (RLOs)

*   **RLO 1 (Design):** Critically evaluate and design complex, end-to-end LLM applications using agentic, multi-agent architectures.
*   **RLO 2 (Implement):** Integrate specialized LLM capabilities (Tool Calling, Persona, ReACT) to build functional, real-world solutions.
*   **RLO 3 (Optimize):** Analyze and apply real-life engineering trade-offs (Cost, Latency, Quality) and employ necessary optimization strategies (Quantization) for production deployment.
*   **RLO 4 (Govern):** Critically assess the architectural limitations, ethical risks, and methodological constraints inherent in LLM-based systems.

***
## LLMs as system components (2 Hours)
**Focus:** Building *smart* applications. How do we give LLMs expertise and autonomy through structure and role?

**Case Study Focus:** Designing a collaborative system for complex task completion. Example used: Paper peer review (subject to change).

| Topic | Concepts Covered | Impact | Deliverable |
| :--- | :--- | :--- | :--- |
| **The LLM as a System Component** | The fundamental limitations of base LLMs (hallucination, lack of domain scope, narrow thought). Deciding when overcoming these limitations using multi-agent systems may be preferable compared to prompting or finetuning. | Identifying when an LLM needs external structure. Designing the boundaries of the LLM's action-space versus the surrounding execution environment. | Drafting and justifying the high-level strategy used to tackle the Case Study. |
| **Tool-Based Reasoning (ReACT)** | The ReACT framework: *Integrating Thought $\rightarrow$ Action $\rightarrow$ Observation*. | How LLM agents already use tools such as coding, CoT prompting, self-critique to tackle complex tasks. | Use an agent to dynamically receive non-standardized documents, and produce input that will be fed to the system. |
| **Persona Prompting** | Defining the AI's role, expertise, constraints, and tone (The "System Prompt"). Techniques for maintaining role consistency and ensuring the LLM acts as a true domain expert. | Prompt Engineering for *identity*. Controlling output quality and style through constraints and meta-prompts. | Demo focused on implementing agent configurations (personas, prompts).|
| **Agent-to-Agent Interaction** | The concept of multiple specialized agents collaborating (e.g., summarizer agent, stakeholder agents, decision-maker agent). Using LLM-only synthetic discussions as an example of internal validation. | Orchestration patterns (defining conversational/task flow templates). Managing state between collaborating components. | Workflow Diagram |

**Mini-Project Milestone**: High-level documentation of the proposed system. |


## Autonomous LLM agents: Costs, safety, scalability (2 Hours)
**Focus:** Building *functional* applications. How do we make LLMs act on the real world and correct their own mistakes? Making applications *efficient, affordable, and safe* in a production environment.

| Topic | Concepts Covered | Impact | Deliverable |
| :--- | :--- | :--- | :--- |
| **Cost & Latency Trade-offs** | The financial and performance realities of LLM deployment. Benchmarking large vs. small models vs. local inference. Strategic model selection based on task complexity vs. budget. | **Economics/DevOps:** Analyzing the total cost of ownership (TCO) for an LLM system. Designing application logic to minimize redundant API calls and excessive token generation. | Cost analysis |
| **Inference Optimization** | Conceptual understanding of model optimization techniques: **Quantization** (reducing precision for memory/speed) and its impact on model accuracy. | **Deployment:** Understanding the operational side of model serving (e.g., choosing optimized inference engines). | Optimization Strategy Plan |
| **LLMs in Code Development** | Architectural patterns for integrating LLMs into the Software Development Lifecycle. Moving beyond simple generation to advanced roles (e.g., code review, test case generation, architecture planning). | How LLMs can not only generate code, but also help with project structure and architectural decisions. | Synthetic test-suite, documentation and code-review using LLMs. |


**Mini-Project Milestone**: Create a prototype of the end-to-end system using LLMs as coding and design assistants.



## Session 3: Final recap and student presentations

| Topic | Concepts Covered | Impact | Deliverable |
| :--- | :--- | :--- | :--- |
| **Full Architecture Review** | Synthesizing all concepts: How the Agent, the Tools, the Reflection Loops, and the Optimization Strategy combine into a single, robust production pipeline. | **Synthesis:** Building a comprehensive end-to-end architectural diagram that accounts for all system components. | Final System Diagram |
| **Final Evaluation & Governance** | Defining sophisticated metrics beyond text similarity (e.g., Task Success Rate, Mean Time to Completion, Cost Per Query). Conducting a final review of ethical constraints and deployment decisions. | Establishing rigorous, measurable quality metrics.| System Evaluation Document | 

**Mini-Project Milestone**: Final Presentations Participants deliver their final architectural design, detailing their chosen agent flow, how they addressed a core architectural trade-off, and what ethical guardrails they implemented.