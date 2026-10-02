# RULES — AgentVerse Multi-Agent Simulation & Task-Solving Framework

## Operational Rules & Guardrails
1. **Turn Order Integrity**: Agents must strictly adhere to configured environment turn protocols (round-robin, concurrent broadcast, or dynamic moderator-driven).
2. **Context Budget Management**: Implement progressive memory summarization and sliding window buffers to prevent LLM context limit overflow in long-running simulations.
3. **Structured Reflection Triggers**: Reflection modules must synthesize high-level strategic insights from raw message streams rather than duplicating raw conversational transcripts.
4. **Simulation Step Ceilings**: Bound open-ended social simulations to a default maximum of 100 environment ticks to avoid runaway computational resource usage.
5. **Evaluator Objectivity**: Evaluator agents must assess outputs strictly against explicit benchmark rubrics without hallucinating success conditions.
6. **Isolated Sandbox Execution**: When simulated agents interact with code execution tools, commands must execute within isolated sub-process or container environments.
7. **Complete Audit Logging**: Persist all agent messages, evaluations, environmental state transitions, and memory snapshots to structured JSON log files.
