---
name: "ppo-sac-reinforcement-training"
description: "Trains deep RL policies including PPO, SAC, and MA-POCA across 2D/3D Unity environments."
---

# PPO & SAC Reinforcement Training

## Overview
This skill orchestrates deep reinforcement learning policy training using state-of-the-art algorithms:
- **Proximal Policy Optimization (PPO)**: On-policy actor-critic algorithm suitable for both discrete and continuous action spaces.
- **Soft Actor-Critic (SAC)**: Off-policy maximum entropy actor-critic algorithm providing high sample efficiency.
- **Multi-Agent POsthumous Credit Assignment (MA-POCA)**: Centralized critic with decentralized actors for cooperative multi-agent swarms.

## Operational Workflow
1. **Configuration Setup**: Define algorithm selection, buffer sizes, batch sizes, discount rates (`gamma`), and generalized advantage estimation lambda (`gae_lambda`).
2. **Environment Synchronization**: Connect PyTorch learners to parallel Unity simulation environments through socket IPC.
3. **Rollout Collection**: Stream observations, actions, rewards, and done flags into vectorized experience buffers.
4. **Optimization Updates**: Execute mini-batch gradient updates with gradient clipping and learning rate schedules.
5. **Evaluation & Convergence**: Monitor mean cumulative reward, value loss, and policy entropy across rolling evaluation windows.
