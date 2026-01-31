# Results & Discussion

This section summarizes the behavior of each architecture using the simulation plots.

---

## 1) Open-loop response (baseline)
In open-loop, both the plant input and the disturbance propagate to the output with no correction.

Key observation:
- With unit steps on both channels and unity DC gains, the output approaches **~2** in steady state (≈ 1 from plant path + 1 from disturbance path).

![Open-loop response](media/plot_open_loop.png)

**Interpretation**
This baseline demonstrates why control is necessary: the disturbance has a direct additive impact on output, and the plant is relatively slow (thermal inertia + dead time).

---

## 2) PI feedback: tuned vs untuned
The tuned PI improves the transient response compared to the untuned case.

![Tuned vs untuned PI](media/plot_tuned_vs_untuned.png)

**Qualitative comparison**
- **Untuned PI**: larger overshoot and more oscillatory transient before settling.
- **Tuned PI**: reduced overshoot and smoother settling, while still converging to the setpoint (≈ 1) due to integral action.

**Practical takeaway**
PI tuning is a tradeoff: pushing faster response can increase overshoot/oscillation, especially with dead time in the loop. Using ITAE helps bias tuning toward good settling behavior.

---

## 3) Feedforward disturbance cancellation (delay sensitivity)
Feedforward is evaluated under disturbance-only conditions (i.e., output should ideally remain near 0 if cancellation is perfect).

![FF delay sweep](media/plot_ff_delay_sweep.png)

**Observed behavior**
- When the feedforward delay matches better, the residual output deviation (“bump”) is smaller.
- A larger mismatch produces a noticeably higher transient peak before returning toward zero.

**Practical takeaway**
Feedforward works best when:
- the disturbance is measurable
- the disturbance model is accurate
- dead-time alignment is correct

Even small delay errors can degrade cancellation significantly.

---

## 4) Combined control response
The combined architecture achieves fast tracking with small overshoot and good settling.

![Combined response](media/plot_combined.png)

**Observed behavior**
- Small overshoot above the setpoint
- Smooth convergence to steady state (~1)
- Minimal residual error

**Practical takeaway**
The combined controller achieves good performance without overly aggressive PI tuning because the feedforward path reduces the disturbance burden on feedback.

---

## 5) Overall comparison (all strategies)
This plot compares: plant process (open-loop), feedback, feedforward (disturbance-only), and combined.

![All comparison](media/plot_all_comparison.png)

**Interpretation**
- **Plant (open-loop)**: slow rise, ends near 2 because both plant input and disturbance contribute.
- **Feedback**: corrects toward the setpoint, but shows a larger transient peak (feedback reacts after deviation is detected).
- **Feedforward (disturbance-only)**: stays near 0 when cancellation is effective; sensitive to delay mismatch.
- **Combined**: tracks setpoint with small overshoot and settles smoothly—best overall balance.

---

## Engineering conclusions (PPT-style)
- The process is well-approximated by FOPDT + dead time (thermal inertia + transport delay).
- PI feedback eliminates steady-state error but can overshoot under dead-time effects if untuned.
- Feedforward can suppress disturbances early, but requires accurate model + delay matching.
- The combined FF+FB architecture delivers the most practical performance: early disturbance compensation + robust correction.
