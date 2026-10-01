# EXPLAINABILITY — Unity ML-Agents Toolkit Runtime

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* Unity ML-Agents Toolkit Runtime (`unity-ml-agents-toolkit`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Developer Tools / Game AI & Reinforcement Learning  

---

## 1. Overview & Operational Purpose
The **Unity ML-Agents Toolkit Runtime** provides an automated, production-grade reinforcement learning orchestration runtime connecting Unity simulation environments with PyTorch deep learning architectures. It enables automated policy training, curriculum progression, imitation learning from expert trajectories, and standardized ONNX model export for embedded in-game inference.

Its operational purpose is to streamline the lifecycle of game AI development, robotic simulation, and multi-agent coordination by automating hyperparameter scheduling, multi-instance environment communication, and policy validation.

---

## 2. How the Agent Decides (Decision-Making Logic)
Unity ML-Agents Toolkit Runtime operates across a deterministic, multi-stage decision pipeline:

```
[Stage 1: Observation Intake] ──> [Stage 2: Policy Evaluation] ──> [Stage 3: Action Sampling]
                                                                          │
                                                                          ▼
[Stage 6: Checkpoint Export] <── [Stage 5: Gradient Update] <── [Stage 4: Reward Attribution]
```

### 2.1 Observation Intake & Normalization
- **Decision:** Validate sensor observations (vector, raycast, visual) against expected dimension schemas and apply running mean/variance normalization.
- **Rules:** Reject malformed observation vectors, pad missing modality buffers with null masks, and normalize visual tensors to `[0.0, 1.0]`.

### 2.2 Policy Evaluation & Action Selection
- **Decision:** Execute forward pass through actor network to sample continuous action vectors or discrete action branches.
- **Rules:** Apply action masks to disallow invalid game actions, enforce action clipping within specified ranges, and add exploratory Gaussian noise during training phases.

### 2.3 Reward Attribution & Advantage Estimation
- **Decision:** Compute temporal difference targets and Generalized Advantage Estimation (GAE) across distributed trajectory rollouts.
- **Rules:** Weight extrinsic simulation rewards against intrinsic curiosity (ICM) or imitation (GAIL) signals according to configuration coefficients.

### 2.4 Curriculum Promotion & Checkpointing
- **Decision:** Assess rolling average performance against curriculum milestone criteria and trigger lesson transitions.
- **Rules:** Require a minimum threshold pass rate over 100 consecutive episodes before incrementing lesson level; trigger ONNX export upon convergence.

---

## 3. Data & Privacy
| Data Category | Retention Policy | Third-Party Sharing | Storage Mechanism |
|---|---|---|---|
| Environment State Observations | Ephemeral (Session Buffer) | None | In-Memory PyTorch Tensors |
| Trajectory Demonstration Recordings | Configurable Project Retention | None | Local `.demo` Binary Files |
| Model Checkpoints & ONNX Graphs | Permanent (Until Deleted by User) | None | Local Storage (`/models/`) |
| Training Telemetry & Scalar Logs | Project Lifecycle (TensorBoard) | None | Local Event Files (`/summaries/`) |

Unity ML-Agents Toolkit Runtime complies with operational security and privacy standards:
- **No Cloud Data Exfiltration:** All training sessions, observation buffers, and neural network weights remain strictly within local environment boundaries without unauthenticated external network transmission.
- **Epistemic Isolation:** Simulation environments and policy rollouts run in isolated local subprocesses, isolated from host OS credentials, private user data, and external systems.
- **Sanitized Model Payloads:** Exported ONNX graphs contain only mathematical tensor operators, weights, and biases, free of embedded code, metadata identifiers, or environment binaries.
- **Data Minimization:** Only state variables and sensory inputs explicitly declared in the Unity C# `Agent` interface are captured during training rollouts.

---

## 4. Known Limitations & Failure Modes
Reviewers, auditors, and users should note the following operational constraints:
1. Environment Desynchronization
   - *Limitation:* Multi-instance Unity simulation processes may desynchronize if physics steps or rendering framerates fluctuate under high host CPU load.
   - *Mitigation:* The agent enforces fixed physics timesteps (`FixedUpdate`) and sets communication timeouts with automatic environment restart fallbacks.
2. Sparse Reward Policy Stagnation
   - *Limitation:* Agents in environments with delayed or sparse reward structures may experience zero gradient signals and fail to explore effectively.
   - *Mitigation:* The agent configures Intrinsic Curiosity Modules (ICM) and Generative Adversarial Imitation Learning (GAIL) to provide dense exploratory incentives.
3. Overfitting to Simulation Quirks
   - *Limitation:* Policies can overfit to specific physics engine artifacts or deterministic obstacle placements, resulting in brittle real-world or production behavior.
   - *Mitigation:* The agent orchestrates domain randomization across friction, mass, visual lighting, and spawn positions during training rollouts.
4. GPU Memory Exhaustion
   - *Limitation:* Large batch sizes paired with high-resolution visual camera observations across multiple parallel instances can exhaust GPU VRAM.
   - *Mitigation:* The agent dynamically scales down rollout buffer lengths and micro-batch sizes when VRAM utilization crosses 85%.

---

## 5. Verification, Safety & Human Oversight
Unity ML-Agents Toolkit Runtime integrates multi-layer safety rails to ensure full human accountability and system integrity:
- **Real-Time Human Approval Gate:** Production model deployment, destructive checkpoint deletion, and distributed cluster dispatch require affirmative human confirmation.
- **Emergency Session Interrupt:** Training runs can be immediately paused, snapshotted, or aborted via standard SIGINT/SIGTERM handlers without corrupting saved weights.
- **Step Quota Guardrails:** Strict maximum step boundaries (`max_steps`) prevent runaway training sessions, infinite simulation loops, and excessive compute expenditure.
- **Structured Audit Logging:** Every training launch, hyperparameter modification, curriculum advancement, and model export is recorded in immutable, timestamped JSON/YAML manifests.
