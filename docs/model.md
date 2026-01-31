# Process & Disturbance Model

## Modelling approach
The heat exchanger temperature process and the disturbance path were both modelled as **First-Order Plus Dead Time (FOPDT)** blocks in Simulink:

- a first-order lag: `K / (τs + 1)`
- a transport delay (dead time): `e^{-Ls}`

This structure is widely used for thermal processes because it captures:
- slow thermal inertia (first-order lag)
- transport/mixing delay between actuation/disturbance and measured output (dead time)

## Plant (temperature) path
From the Simulink plant block:

\[
G_p(s) = \frac{1}{21.3s + 1}\,e^{-L_p s}
\]

Where:
- \(τ_p = 21.3\) s (plant time constant)
- \(K_p = 1\) (DC gain)
- \(L_p\) = plant dead time (as configured in your `DelayT/DelayH` block)

## Disturbance path
From the Simulink disturbance model block:

\[
G_d(s) = \frac{1}{25s + 1}\,e^{-L_d s}
\]

Where:
- \(τ_d = 25\) s (disturbance time constant)
- \(K_d = 1\) (DC gain)
- \(L_d\) = disturbance dead time (as configured in your `DelayD` block)

## Open-loop output composition
In the open-loop model, a step input \(u(t)\) and step disturbance \(d(t)\) both propagate through their respective dynamics and are summed at the output:

\[
y(s) = G_p(s)\,u(s) + G_d(s)\,d(s)
\]

Because both paths have unity DC gain, unit steps on both channels lead to a steady-state output approximately equal to **2** (one unit from each path), which is consistent with the open-loop plot.

## Simulink implementation
See the open-loop block diagram:

![Open-loop model](media/sim_open_loop.png)
