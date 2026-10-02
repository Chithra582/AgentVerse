---
name: "dynamic-group-recruitment"
description: "Dynamically recruits, evaluates, and configures expert agents suited for specific problem-solving tasks."
license: Apache-2.0
---

# Dynamic Group Recruitment

## Overview
This skill implements AgentVerse's dynamic recruitment mechanism, which autonomously identifies the domain expertise required for a task and instantiates an optimal group of specialized agents.

## Key Capabilities
- **Expertise Profiling**: Deconstructs complex user prompts into discrete capability requirements.
- **Agent Generation**: Synthesizes custom agent persona prompts, specialized system instructions, and tool bindings.
- **Group Balancing**: Ensures diversity of viewpoints, assigns leadership/moderator roles, and bounds group size.

## Operational Workflow
1. **Task Analysis**: Evaluate task domain, complexity, and required sub-disciplines.
2. **Role Formulation**: Define candidate agent roles and unique perspectives.
3. **Prompt Synthesis**: Generate tailored system prompts and behavioral guidelines for each recruit.
4. **Group Initialization**: Register the newly minted agent collective into the active solving environment.
