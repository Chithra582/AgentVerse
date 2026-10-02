# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **AgentVerse Multi-Agent Simulation & Task-Solving Framework** (`agentverse`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** AgentVerse Multi-Agent Simulation & Task-Solving Framework (`agentverse`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Multi-Agent Simulation & Autonomous Problem Solving  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

AgentVerse is a versatile multi-agent framework designed to deploy and orchestrate large language model (LLM) agents across dual operating paradigms: autonomous social simulation and collaborative task solving. In social simulation mode, AgentVerse models emergent interactions among autonomous agents placed in structured environments (e.g., courtroom trials, classroom debates, game-theoretic dilemmas). In task-solving mode, AgentVerse implements a dynamic recruitment pipeline where specialized expert agents are autonomously assembled, guided through collaborative planning, distributed execution, and evaluated via iterative reflection loops.

### 1. Decision Architecture

The user prompt intake, environment initialization, dynamic recruitment, collaborative problem solving, and reflective synthesis pipeline operates across a deterministic, five-stage architecture:

```
User Task / Simulation Scenario (e.g., "Simulate a 5-agent judicial debate on data privacy")
    │
    ▼
[Stage 1: Scenario Intake & Environment Configuration]
    │  - Ingests scenario configuration and establishes environmental mechanics
    │  - Determines execution mode: emergent social simulation vs. collaborative task-solving
    │  - Configures observation visibility matrices, turn order policies, and communication topologies
    ▼
[Stage 2: Dynamic Agent Recruitment & Persona Synthesis]
    │  - Evaluates problem complexity and identifies required domain disciplines
    │  - Synthesizes tailored agent personas, system instructions, and tool assignments
    │  - Instantiates agent working memory buffers and long-term reflection stores
    ▼
[Stage 3: Collaborative Multi-Turn Execution & Environment Stepping]
    │  - Advances simulation ticks and dispatches dialogue turns to active agents
    │  - Coordinates structured debates, distributed execution, and inter-agent message passing
    │  - Manages environment state mutations and collects multi-agent observation streams
    ▼
[Stage 4: Evaluator Assessment & Reflective Feedback Loop]
    │  - Evaluator agents assess intermediate outputs against explicit benchmark criteria
    │  - Generates targeted critique prompts and triggers reflection cycles
    │  - If consensus or quality falls below thresholds, dispatches iterative revision turns
    ▼
[Stage 5: Consensus Synthesis & Trajectory Archival]
    │  - Aggregates verified agent contributions into a cohesive final solution
    │  - Compresses conversation histories and persists distilled episodic memories
    │  - Commits complete simulation traces to auditable structured storage
    ▼
Validated Task Solution / Auditable Multi-Agent Simulation Trajectory Record
```

### 2. Decision Logic & Routing Formulations

AgentVerse evaluates dynamic recruitment suitability, group consensus, and evaluation confidence using deterministic mathematical models:

1. **Agent Recruitment Suitability Score ($S_{\text{recruit}}$)**:
   $$S_{\text{recruit}}(a, T) = (w_r \cdot R_{\text{relevance}}) + (w_d \cdot D_{\text{diversity}}) + (w_c \cdot C_{\text{capacity}})$$
   where:
   - $R_{\text{relevance}} \in [0, 1]$ represents semantic alignment between candidate persona $a$ and task domain $T$.
   - $D_{\text{diversity}} \in [0, 1]$ measures persona cosine orthogonality relative to previously recruited agents.
   - $C_{\text{capacity}} \in \{0, 1\}$ indicates tool and reasoning capacity match.
   - Weights: $w_r = 0.45, w_d = 0.35, w_c = 0.20$ ($\sum w_i = 1.0$).

2. **Group Consensus Metric ($C_{\text{consensus}}$)**:
   $$C_{\text{consensus}} = \frac{2}{N(N-1)} \sum_{i=1}^{N} \sum_{j > i}^{N} \text{Sim}(\mathbf{e}_i, \mathbf{e}_j)$$
   where $\mathbf{e}_i, \mathbf{e}_j$ are normalized semantic embedding vectors of the conclusions emitted by agents $i$ and $j$. If $C_{\text{consensus}} < 0.75$, the moderator agent triggers an additional round of debate.

### 3. Thresholding & Refusal Decision Criteria

AgentVerse enforces strict operational boundaries to ensure simulation safety and resource control:
- **Refusal of Unconstrained Shell Execution**: Simulated agents attempting to execute arbitrary host commands without sandbox confinement are refused (`ERR_UNSANDBOXED_EXECUTION_FORBIDDEN`).
- **Turn Ceiling Enforcement**: Simulation scenarios enforce a maximum ceiling of 100 environment ticks to prevent runaway execution (`WARN_MAX_TICKS_REACHED`).
- **Context Window Overflow Safeguard**: Working memory buffers exceeding 80% of model context limits trigger automatic semantic summarization (`WARN_MEMORY_COMPRESSION_ACTIVATED`).
- **Refusal to Skip Evaluation Gate**: Task solutions cannot be marked finalized without passing the evaluator agent threshold (`ERR_EVALUATION_GATE_UNMET`).

### 4. Fallback Decision Mechanism

Continuous multi-agent operational stability is maintained through multi-tier fault recovery:
- **Provider Cascade**: If foundation model endpoints encounter rate limits (HTTP 429) or timeouts, the LLM client cascades across secondary providers (OpenAI, Anthropic, Azure, Local vLLM).
- **Deadlock Resolution Protocol**: If multi-agent debate reaches an intractable deadlock after 3 debate rounds, the moderator agent executes a majority-vote arbitration fallback.
- **Graceful Agent Recovery**: If an individual simulated agent crashes or outputs unparseable JSON, the environment substitutes a deterministic default response and logs the anomaly.

### 5. Human-in-the-Loop Governance

Human operators retain full authority and operational oversight over AgentVerse:
- **Interactive Web UI & Visualization**: Operators can observe live multi-agent conversations, turn progressions, and state metrics in real-time.
- **Human-as-an-Agent Intervention**: Operators can join simulations as active participants, inject guidance, or pause agent execution at any tick.
- **Complete Trajectory Auditing**: Every agent utterance, evaluation score, and environmental state transition is logged in structured JSON for post-hoc analysis.

---

## The Data It Uses

AgentVerse operates under strict principles of data minimization, environment isolation, and privacy protection.

### 1. Ingested Input Data

The framework processes only operational data necessary to execute multi-agent simulations:
- **User Instructions**: Natural language task prompts, simulation scenario descriptions, and constraint parameters.
- **Scenario Presets**: Declarative YAML configurations defining agents, environmental rules, and tool bindings.
- **Agent Observation Streams**: In-simulation messages, sensor readings, and intermediate agent reasoning traces.

### 2. Configuration & Reference Data

- **Benchmark Datasets**: Standardized benchmark evaluation tasks (HumanEval, GSM8k, social simulation presets).
- **Prompt Templates**: System instruction templates for specialized roles, moderators, and evaluators.
- **Vector Index Stores**: Dense embedding indices used for episodic memory retrieval.

### 3. Base Model & Inference Lineage

- **Deterministic Orchestration Kernel**: Python simulation loop, environment state machine, and turn schedulers execute 100% deterministically.
- **Foundation LLMs**: High-capability frontier models (GPT-4o, Claude 3.5 Sonnet, LLaMA-3) deployed for agent role-playing and problem solving.
- **Zero Training on User Data**: User scenario specifications, simulated dialogues, and task outputs are never utilized for model fine-tuning or training.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against indirect prompt injection in simulated environments, agent collusion, and unauthorized tool invocation.
- **Local Sandbox Confinement**: Simulation logs, generated artifacts, and memory vector stores reside strictly on the local machine.
- **Automated Secret Scrubbing**: API tokens, authorization headers, and environment keys are redacted from logs and exports.
- **Zero Commercial Monetization**: Simulation runs, agent dialogue transcripts, and evaluation benchmarks are never commercialized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of AgentVerse is essential for effective deployment.

### 1. High Computational and Token Overhead
- **Limitation**: Running multi-agent simulations with dozens of interactive turns consumes significant LLM API tokens.
- **Mitigation**: AgentVerse incorporates selective memory retrieval, token budget ceilings, and lightweight local open-weight model support.

### 2. Social Simulation Sycophancy & Role Drift
- **Limitation**: In long-running social simulations, agents may exhibit role drift or align prematurely with peers (sycophancy).
- **Mitigation**: System prompts incorporate personality anchors and periodic reflection checks to reinforce character consistency.

### 3. Real-Time Hardware Interaction Constraints
- **Limitation**: AgentVerse operates within simulated software environments and cannot directly control physical robotic hardware without custom drivers.
- **Mitigation**: Users integrate hardware abstraction layers and ROS adapters for robotics deployments.

### 4. Complex Spatial Physics Simulation
- **Limitation**: While AgentVerse simulates discrete grid worlds and textual topologies, it does not provide continuous 3D physics engines.
- **Mitigation**: External physics engines (e.g., Unity, MuJoCo) can be integrated via the environment interface API.

### 5. Multi-Party Scalability Bottlenecks
- **Limitation**: Scalability in fully connected communication topologies degrades quadratically with agent count ($O(N^2)$).
- **Mitigation**: AgentVerse provides partitioned room topologies, moderator-mediated routing, and localized spatial observation horizons.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & routing formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested user instructions, scenario presets & observations | Section 1 | Verified |
| - Configuration, benchmark datasets & prompt templates | Section 2 | Verified |
| - Base model lineage & deterministic orchestration kernel | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - High computational and token overhead | Section 1 | Verified |
| - Social simulation sycophancy & role drift | Section 2 | Verified |
| - Real-time hardware interaction constraints | Section 3 | Verified |
| - Complex spatial physics simulation | Section 4 | Verified |
| - Multi-party scalability bottlenecks | Section 5 | Verified |
