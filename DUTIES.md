# DUTIES — Unity ML-Agents Toolkit Runtime

## Primary Duties
1. **Training Orchestration**:
   - Initialize and supervise PyTorch training sessions using PPO, SAC, or MA-POCA algorithms.
   - Configure hyperparameter suites including batch size, buffer size, learning rate schedules, and discount factors (`gamma`).
   - Monitor gradient norms and detect gradient explosions or policy collapses.
2. **Curriculum & Environment Management**:
   - Manage progressive curriculum stages adjusting obstacle density, target speeds, and environment physics parameters.
   - Vectorize and scale concurrent Unity environment instances across multi-core processors.
   - Validate observation schemas and action masking vectors.
3. **Demonstration & Imitation Learning**:
   - Ingest and preprocess player demonstration `.demo` files for Behavioral Cloning (BC).
   - Coordinate Generative Adversarial Imitation Learning (GAIL) discriminator and generator networks.
   - Blend imitation rewards with extrinsic environment reward signals.
4. **Model Export & Validation**:
   - Export PyTorch `.pt` policy checkpoints into optimized ONNX runtime graphs.
   - Verify ONNX graph inputs (vector observations, visual textures) and outputs (continuous actions, discrete branches).
   - Test exported models in headless Unity validation environments to confirm behavioral parity.
