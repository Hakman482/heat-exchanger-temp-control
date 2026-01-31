# heat-exchanger-temp-control

# Heat Exchanger Temperature Control (Simulink)
Model-based temperature control design for a heat exchanger using:
- Open-loop FOPDT + dead time modelling
- PI feedback control (tuned vs untuned comparison)
- Feedforward disturbance compensation (delay sensitivity study)
- Combined Feedforward + Feedback architecture (industry-style solution)

> Built and simulated in MATLAB/Simulink R2025b.

---

## 1) System Model
The process is modelled as first-order plus dead time (FOPDT) for both the plant and disturbance path.

- Plant (temperature path):  Gp(s) = 1 / (21.3 s + 1) with delay
- Disturbance path:          Gd(s) = 1 / (25 s + 1) with delay

![Open-loop model](docs/media/sim_open_loop.png)

---

## 2) Control Architectures Implemented
### A) PI Feedback Control
PI controller tuned to improve setpoint tracking and reduce steady-state error.
Includes ITAE performance index computation for objective comparison.

![Feedback PI model](docs/media/sim_feedback_PI.png)

### B) Feedforward Disturbance Compensation
Feedforward designed to cancel measured disturbance influence through model inversion/ratio and delay alignment.

![Feedforward model](docs/media/sim_feedforward.png)

### C) Combined Feedforward + Feedback
Feedforward handles predictable disturbance effects; feedback corrects model mismatch and unmeasured disturbances.

![Combined control model](docs/media/sim_combined.png)

---

## 3) Key Results (Plots)
### Open-loop response
![Open-loop response](docs/media/plot_open_loop.png)

### Tuned vs Untuned PI
![Tuned vs Untuned PI](docs/media/plot_tuned_vs_untuned.png)

### Feedforward delay sensitivity (20.3s vs 25.3s)
![FF delay sweep](docs/media/plot_ff_delay_sweep.png)

### Combined control response
![Combined response](docs/media/plot_combined.png)

### Comparison: plant vs feedback vs feedforward vs combined
![All comparison](docs/media/plot_all_comparison.png)

---

## 4) How to Run
1. Open the Simulink models in `/sim`
2. Run simulations and view scopes/plots
3. (Optional) Export plots to `/docs/media` for documentation

**Requirements**
- MATLAB R2025b
- Simulink
- Control System Toolbox (recommended)

---

## 5) Documentation
- Model details: docs/model.md  
- Control design notes: docs/control_design.md  
- Results and discussion: docs/results.md  
- Full report PDF: report/IPC_assignment_Hakeem.pdf
