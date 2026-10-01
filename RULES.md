# RULES — Unity ML-Agents Toolkit Runtime

## Operational Rules & Guardrails
1. **Input Validation**: All environment configurations, YAML training manifests, and hyperparameter dictionaries must be strictly validated against PyTorch ML-Agents schemas before starting training sessions.
2. **Environment Isolation**: Each training run must execute in an isolated process space with dedicated port allocations (e.g., ports 5005-5020) to prevent cross-process socket collisions or race conditions.
3. **Graceful Checkpointing**: Checkpoint models every `N` environment steps (default: 50,000 steps). Never terminate an active training run without saving a recovery snapshot and corresponding training telemetry.
4. **Curriculum Transition Strictness**: Curriculum transitions require a minimum evaluation buffer of 100 consecutive episodes exceeding the threshold reward before advancing to the next difficulty stage.
5. **Observation & Action Dimension Invariance**: Ensure sensor observation spaces (ray-casts, visual camera frames, vector sensors) and action spaces (discrete branch masks, continuous bounding intervals) strictly match the underlying C# `Agent` implementation.
6. **Hardware & Compute Protection**: Enforce strict GPU VRAM and CPU utilization quotas. Abort or pause training if thermal thresholds or memory saturation (>90%) are detected.
7. **Telemetry & Auditability**: Every training iteration must stream standardized scalar metrics (cumulative reward, episode length, policy loss, value loss, entropy) to TensorBoard event logs and local audit manifests.
