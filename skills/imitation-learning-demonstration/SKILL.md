---
name: "imitation-learning-demonstration"
description: "Trains behavior cloning and generative adversarial imitation learning policies from human demonstrations."
---

# Imitation Learning & Demonstration

## Overview
This skill integrates human and heuristic demonstrations to accelerate reinforcement learning or bootstrap behaviors when reward design is challenging:
- **Behavioral Cloning (BC)**: Supervised learning on expert demonstration trajectories to initialize policies.
- **Generative Adversarial Imitation Learning (GAIL)**: Trains a discriminator network to distinguish between expert and agent trajectories, providing an intrinsic reward signal.

## Operational Workflow
1. **Demonstration Ingestion**: Read recorded Unity `.demo` files containing observation and action sequences.
2. **Data Filtering**: Remove failed or suboptimal episodes, ensuring only high-quality trajectories inform the training set.
3. **Pre-training Initialization**: Apply BC loss to pre-train policy networks before live environment interaction.
4. **Adversarial Training**: Concurrently optimize the GAIL discriminator alongside the PPO/SAC policy network.
5. **Reward Blending**: Balance GAIL intrinsic imitation rewards with extrinsic environment rewards.
