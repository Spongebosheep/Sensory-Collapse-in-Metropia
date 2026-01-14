# Metropia Commuter Dynamics — The PurrStone Models (Phase 1–3)

This repository contains the Wolfram Mathematica notebooks used to generate all simulations, stability analyses, and figures for the *Modelling & Simulation* coursework report.

The project models a commuting system in the fictional city of **Metropia**. Crowd pressure produces stress; the consumer device **PurrStone** suppresses perceived stress. Across three phases, the model evolves from a minimal continuous-time baseline to a hybrid discrete–continuous system where *masked pain* shifts behaviour from physical feedback to volatile social signals.

---

## Repository contents

- `M&S Phase1.nb` — **Phase 1: Naive baseline** (crowding → stress, no behavioural feedback)
- `M&S Phase2.nb` — **Phase 2: Adoption without feedback** (add device adoption as a bounded state)
- `M&S Phase3.nb` — **Phase 3: Sensory decoupling + social waves** (logistic-map driver + forced ODE, chaos & tail risk)

> **Variable mapping (for readers):**
> - Phase 1 uses `crowd(t)` and `stress(t)`.
> - Phase 2–3 use nondimensional states `(x(t), y(t), z(t))` where, in report terms:
>   - `x ≈ crowding`, `y ≈ stress`, `z ≈ adoption` (device usage fraction).

---

## Requirements

- **Wolfram Mathematica 14.3+** (the notebooks were created with Wolfram 14.3).
- No external packages are required.

---

## Quick start (recommended workflow)

1. Open a notebook in Mathematica.
2. Run **Evaluation → Evaluate Notebook**.
3. If you only need specific figures, evaluate the notebook section-by-section instead of running the full notebook.

---

## What each notebook produces

### Phase 1 — Naive baseline (continuous-time ODE)
Core outputs:
- Analytical solution via `DSolve` (baseline reference).
- Numerical solution via `NDSolveValue`.
- Fixed point + Jacobian eigenvalues (local stability).
- Phase portrait / vector field plots.
- Numerical verification: **Euler vs RK4** error–step-size scaling (observed order-of-accuracy).

Typical runtime: **fast** (seconds).

---

### Phase 2 — Adoption without feedback (extended ODE + nondimensionalisation)
Core outputs:
- Nondimensional scaling table and derived parameters.
- Three-state system simulation with and without device coupling (`gamma = 0` vs `gamma > 0`).
- Equilibrium computation and stability (Jacobian eigenvalues).
- Additional equilibrium analysis in reduced subspace where applicable.

Typical runtime: **fast to moderate** (seconds to a couple of minutes depending on plots).

---

### Phase 3 — Hybrid model (logistic driver + forced ODE)
Core outputs:
- Logistic map analysis:
  - Bifurcation diagram.
  - Lyapunov exponent sweep (positive λ indicates chaos).
- Hybrid coupling:
  - Discrete orbit `x_n` converted to a piecewise-constant forcing `u(t)` (updated every `Tstep`).
  - Forced continuous-time ODE solved with `NDSolveValue`.
- System behaviour under chaotic forcing:
  - Time series, phase projections, and **stroboscopic sampling**.
  - Ensemble simulations (sensitivity to initial conditions).
  - Driven-system bifurcation-style plots / parameter sweeps (where enabled).

Typical runtime: **moderate to heavy**  
(Phase 3 includes parameter sweeps and large plots; reduce resolution parameters if needed.)

---

## Reproducibility notes

- Phase 3 uses `SeedRandom[...]` to make ensemble-style results reproducible.
- If you modify sweep resolution (e.g., `rStep`, `nIter`, `nTransient`, number of samples), expect small numerical/visual differences.
- For discontinuous forcing, solver robustness can depend on step-size control; Phase 3 includes solver settings (`AccuracyGoal`, `PrecisionGoal`, optional `MaxStepSize`) intended to stabilise results.

---

## Performance tips (if Phase 3 is slow)

- Reduce sweep resolution first:
  - Fewer `r` samples in Lyapunov/bifurcation plots.
  - Smaller `nIter` / `nTransient` for logistic calculations.
- Reduce ODE horizon (`tMax`) or increase `Tstep` (coarser forcing updates).
- Disable or defer high-resolution plots until the model behaviour is confirmed.

---

## Mapping to the report

- **Report Phase 1** ↔ `M&S Phase1.nb`
- **Report Phase 2** ↔ `M&S Phase2.nb`
- **Report Phase 3** ↔ `M&S Phase3.nb`

All figures in the report are generated directly from these notebooks (either as inline graphics or by re-running the relevant plotting cells).

---

## License / usage

This repository is provided for educational coursework purposes. If reusing any part of the model or figures, please cite the report and clearly attribute the original author.
