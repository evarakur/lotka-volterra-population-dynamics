# Lotka–Volterra Predator–Prey Dynamics

A Python-based computational biology project investigating nonlinear predator–prey interactions through numerical simulation, parameter sensitivity analysis, and numerical error assessment. The project implements forward Euler and explicit midpoint integration, evaluates a conserved quantity of the classical Lotka–Volterra system, and extends the model to include resource-limited prey growth.

## Project Overview

The Lotka–Volterra equations describe the interaction of a prey population, which grows in the absence of predators, and a predator population, which depends on prey for reproduction. This notebook explores population oscillations, phase-space trajectories, equilibrium values, the effect of model parameters, and the numerical behavior of different integration methods.

## Mathematical Model

The classical model is defined by

$$
\frac{dx}{dt}=\alpha x-\beta xy
$$

$$
\frac{dy}{dt}=\delta xy-\gamma y
$$

where $x$ and $y$ are prey and predator populations, respectively; $\alpha$ is the intrinsic prey growth rate; $\beta$ is the predation coefficient; $\gamma$ is the predator mortality rate; and $\delta$ is the predator growth coefficient associated with prey consumption.

The nonzero equilibrium is

$$
x^*=\frac{\gamma}{\delta},\qquad y^*=\frac{\alpha}{\beta}.
$$

The baseline parameter values are $\alpha=0.4$, $\beta=0.02$, $\gamma=0.5$, and $\delta=0.01$, giving an equilibrium of **50 prey and 20 predators**. The initial simulated populations are 60 prey and 25 predators.

## Methods and Analyses

1. **Model implementation and validation:** Implemented `lv_step()` and `run_lv()` using forward Euler integration; validated a single numerical step against expected population values.
2. **Population dynamics and phase-space analysis:** Visualized oscillatory predator–prey trajectories over time and in the prey–predator phase plane.
3. **Parameter sensitivity:** Varied $\alpha$, $\beta$, $\gamma$, and $\delta$ independently to examine their effects on equilibrium values and simulated trajectories.
4. **Numerical drift:** Evaluated how Euler time-step size affects phase-space trajectories and preservation of the classical model's conserved quantity.
5. **Integrator comparison:** Implemented the explicit midpoint method and compared its numerical drift with forward Euler integration.
6. **Logistic growth extension:** Introduced a prey carrying capacity and investigated long-term behavior for $K=500$, $K=200$, and $K=100$.

## Numerical Accuracy

For positive population values, the classical Lotka–Volterra system has the conserved quantity

$$
V(x,y)=\delta x-\gamma\ln(x)+\beta y-\alpha\ln(y).
$$

The notebook measures numerical drift as $\Delta V=V(x_{\mathrm{final}},y_{\mathrm{final}})-V(x_0,y_0)$. In the 200-time-unit comparison at **`dt = 0.1`**, the recorded results were:

| Integration method | Time step | Conserved-quantity drift |
|---|---:|---:|
| Forward Euler | 0.1 | 0.957131 |
| Explicit midpoint | 0.1 | 0.0000349 |

The midpoint method preserved the conserved quantity substantially better under these test conditions. Neither numerical method is exactly conservative, and the magnitude of drift depends on the simulation settings.

## Logistic Prey Growth

To represent finite environmental resources, prey growth is modified to include carrying capacity $K$:

$$
\frac{dx}{dt}=\alpha x\left(1-\frac{x}{K}\right)-\beta xy,
\qquad
\frac{dy}{dt}=\delta xy-\gamma y.
$$

The notebook uses midpoint integration to simulate this extension for 400 time units. Its recorded final population values were:

| Prey carrying capacity ($K$) | Final prey population | Final predator population |
|---|---:|---:|
| 500 | 50.00 | 18.00 |
| 200 | 50.00 | 15.00 |
| 100 | 50.00 | 10.00 |

Under these parameter settings, the simulated populations approach stable coexistence values, rather than exhibiting the sustained closed orbits of the ideal classical system.

## Tools and Techniques

- **Python** for numerical modeling and analysis
- **NumPy** for numerical arrays and population calculations
- **Matplotlib** for time-series and phase-space visualizations
- **Forward Euler and explicit midpoint methods** for numerical integration
- **Sensitivity and convergence analysis** for evaluating model behavior and numerical accuracy

## Run the Notebook

1. Open [`Lotka_Volterra_Population_Dynamics_Model.ipynb`](Lotka_Volterra_Population_Dynamics_Model.ipynb) in Jupyter Notebook or Google Colab.
2. Ensure Python, NumPy, and Matplotlib are available.
3. Run the cells sequentially to reproduce the simulations, printed results, and figures.

Install the Python dependencies locally with:

```bash
pip install numpy matplotlib notebook
```

## Limitations

The classical model assumes simplified interactions, fixed rate parameters, and no environmental constraints on prey growth. The logistic extension introduces density-dependent prey growth but does not capture spatial structure, stochasticity, age structure, or changing environmental conditions. Numerical trajectories are also affected by the choice of integration method and time step.

## Project Context

Developed from a biological dynamical systems coursework exercise and organized as a standalone computational modeling portfolio project. Before public redistribution, ensure that any retained instructor-provided material is permitted to be shared.
