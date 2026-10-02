---
name: "multi-agent-environment-simulation"
description: "Configures and executes multi-agent social simulations with custom rules, roles, and environments."
license: Apache-2.0
---

# Multi-Agent Environment Simulation

## Overview
This skill executes emergent social simulations involving multiple autonomous LLM agents operating within customized environmental rules, spatial layouts, and communication topologies.

## Key Capabilities
- **Environment Rule Enforcement**: Controls agent perception visibility, action legality, and state transitions.
- **Turn Scheduling**: Supports round-robin, priority-based, and moderator-managed dialogue scheduling.
- **Scenario Customization**: Configures social dilemmas, bargaining games, and debate forums via declarative YAML presets.

## Operational Workflow
1. **Scenario Loading**: Load environment configuration, agent profiles, and initial state variables.
2. **Observation Generation**: Construct agent-specific perceptual inputs based on visibility and spatial proximity.
3. **Turn Dispatch**: Prompt active agents according to the schedule policy.
4. **Environment Mutation**: Process agent actions, update world state, and log interactions.
