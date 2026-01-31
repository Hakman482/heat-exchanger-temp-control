# Project Overview

This project models and controls a heat exchanger temperature process in MATLAB/Simulink (R2025b). The goal is to achieve good **setpoint tracking** while also rejecting **load disturbances** that enter the process through a separate disturbance path.

## What was built
Four progressively more capable architectures were implemented and compared:

1. **Open-loop process + disturbance model**  
   Establishes baseline dynamics and shows how disturbances directly shift the output when no control is applied.

2. **PI Feedback control (with ITAE performance index)**  
   Classic closed-loop temperature control using a PI controller, including comparison of tuned vs untuned controller settings.

3. **Feedforward (disturbance compensation)**  
   Disturbance is measured/available and used to generate a compensating control action. Sensitivity to feedforward delay mismatch is also studied.

4. **Combined Feedforward + Feedback**  
   Industry-style architecture: feedforward removes predictable disturbance impact; feedback corrects model mismatch, unmeasured disturbances, and residual error.

## Why this matters in industry
Heat exchanger temperature loops are typically slow, include **transport delay (dead time)**, and face frequent disturbances (e.g., inlet temperature/flow changes). Pure feedback can correct disturbances, but usually **after** the output has already deviated. Feedforward can act earlier, but depends on model accuracy and delay matching. The combined architecture is practical because it delivers:
- Faster disturbance rejection (feedforward action)
- Robustness to modelling errors and unmeasured effects (feedback correction)
- Improved overall performance without overly aggressive PI tuning
