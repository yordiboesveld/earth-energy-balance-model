# Earth Energy Balance Model

This project investigates equilibrium solutions of a nonlinear Earth energy balance model (EBM) using a pseudo-arclength numerical continuation and stability analysis methods. The model describes the balance between absorbed solar radiation, emitted thermal radiation, and diffusive heat redistribution across the Earth. This project was developed as part of the Applications in PDE course at TU Delft.

## Problem

Latitude $\theta$ is rewritten to a coordinate $x = \sin{\theta}$ (dimensionless), such that $x \in [-1,1]$ from pole to pole. The temperature distribution $T(t,x)$ satisfies

$$
R_A - R_E + R_D = C_T \frac{\partial T}{\partial t},
$$

where:
- $R_A$ represents absorbed solar radiation,
- $R_E$ represents emitted thermal radiation,
- $R_D$ models diffusive heat transport.

The absorbed radiation is given by

$$
R_A = Q(x)(1-\alpha(T(x))) + \mu,
$$

where $Q(x)$ is the solar radiation, $\mu$ is a greenhouse forcing parameter and $\alpha(T)$ is a temperature-dependent albedo function describing transitions between ice-covered and ice-free regions. Here, the functions $Q(x)$ and $\alpha(T)$ are defined as

$$
Q(x) = Q_0 (1-0.241(3x^2-1)),
$$

$$
\alpha(T) = \alpha_1 - \frac{1}{2}(\alpha_2 - \alpha_1)(1+\tanh(M(T-T_{*}))).
$$

Thermal radiation is modeled by

$$
R_E = \varepsilon_0 \sigma_0 T^4,
$$

while diffusive heat transport is modeled as

$$
R_D =
\frac{\partial}{\partial x}
\left(D(1-x^2)\frac{\partial T}{\partial x}
\right).
$$

We focus on equilibrium solutions of the EBM. Therefore, we consider steady-state solutions satisfying

$$
\frac{\partial T}{\partial t}=0.
$$

To discretize the spatial dimension, a truncated Legendre eigenfunction expansion is employed:

$$
T(\mathbf{a},x)
\approx
\sum_{n=0}^{N} a_n P_n(x),
$$

where $P_n(x)$ are Legendre polynomials and $\mathbf{a}$ contains the expansion coefficients. Applying a Galerkin projection results in a nonlinear algebraic system with $N+1$ unknown coefficients.

To study the equilibrium structure of the EBM, pseudo-arclength continuation is applied in the greenhouse forcing parameter $\mu$, ranging from $0$ to $100$. This allows the computation of equilibrium branches and bifurcation diagrams, including unstable solution branches.

The resulting bifurcation diagram is analyzed together with the extent of ice coverage on the planet.

## Implemented Methods

- Legendre eigenfunction expansion
- Galerkin projection
- Newton-Raphson method
- Jacobian construction
- Pseudo-arclength continuation
- Linear stability analysis

## Results

The notebook contains:
- Equilibrium temperature distributions
- Bifurcation diagrams
- Continuation of equilibrium branches
- Stability analysis of equilibrium states
- Ice coverage analysis

The experiments illustrate the existence of multiple climate equilibria, bifurcation behavior, and transitions between ice-covered and ice-free climate states.

## Running the Project

The project was developed and tested using Python 3.12. Install the required packages: pip install -r requirements.txt

Open the notebook:

jupyter notebook notebooks/earth-energy-balance-model.ipynb

Run all cells sequentially to reproduce the bifurcation diagram.
