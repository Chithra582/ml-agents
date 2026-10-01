---
name: "curriculum-learning-orchestration"
description: "Sequences environment task complexity and reward thresholds through automated curricula."
---

# Curriculum Learning Orchestration

## Overview
Curriculum learning breaks complex reinforcement learning tasks into progressively difficult stages (lessons). By mastering simpler environments first, agents learn complex navigation, manipulation, and decision behaviors efficiently.

## Operational Workflow
1. **Curriculum Definition**: Construct YAML curriculum configs defining environment parameter variations (e.g., arena size, obstacle speed, target distance).
2. **Metric Monitoring**: Track rolling episode reward averages and completion rates for the active lesson.
3. **Threshold Evaluation**: Validate whether performance meets or exceeds lesson graduation criteria over the required minimum episode window.
4. **Stage Advancement**: Update environment parameters smoothly to transition agents to the next curriculum tier without inducing policy shock.
5. **Telemetry Recording**: Log all lesson transitions and parameter changes to TensorBoard and audit logs.
