---
name: "gym-pettingzoo-environment-adapter"
description: "Wraps Unity simulation instances into standard OpenAI Gym and PettingZoo multi-agent environments."
---

# Gym & PettingZoo Environment Adapter

## Overview
This skill provides bidirectional adapter layers connecting Unity ML-Agents simulation runtimes with standard Python reinforcement learning frameworks, including Gymnasium, OpenAI Gym, and PettingZoo (AEC and Parallel APIs).

## Operational Workflow
1. **API Selection**: Choose single-agent `Gymnasium` adapter or multi-agent `PettingZoo` wrapper based on agent architecture.
2. **Space Mapping**: Translate Unity observation specs (visual, vector) and action branches into standard `gym.spaces` (Box, Discrete, MultiDiscrete).
3. **Step Execution**: Coordinate synchronous `step(action)` and `reset()` calls across the communication channel.
4. **Multi-Agent Coordination**: Handle agent addition, elimination, and variable team step sequences seamlessly.
5. **Benchmark Compatibility**: Enable evaluation with standard RL benchmarking suites (CleanRL, Stable-Baselines3, Ray RLLib).
