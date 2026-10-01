# Computational Physics Labs

**Adrien Creténier**
Computational physics course (*Physique Numérique*), **ENS Paris-Saclay — academic year 2022–2023**

---

## Overview

This repository gathers five computational physics labs, each designed and supervised by a different member of the teaching staff of ENS Paris-Saclay. They cover quantum mechanics, atomic physics, thermal physics, nonlinear dynamics and condensed matter. In each lab, a physics problem is turned into a numerical one, solved in Python, and checked against analytical results or experimental data.

All notebooks were written individually.

> **Language note:** the lab subjects and the notebooks are written in **French**.

| Lab | Field | Main numerical methods |
|---|---|---|
| [Solving Schrödinger equation](./Solving%20Schrodinger%20equation) | Quantum mechanics | Finite differences, tridiagonal eigenvalue problem |
| [Energy levels of an alkali atom](./Energy%20levels%20of%20an%20alkali%20atom) | Atomic physics | Radial eigenvalue problem, Poisson solver, self-consistent iteration |
| [Heat diffusion](./Heat%20diffusion) | Thermal physics | 2D finite differences, sparse linear systems, Gauss–Seidel iteration |
| [Study of deterministic chaos](./Study%20of%20deterministic%20chaos) | Nonlinear dynamics | Iterated maps, bifurcation diagram, Lyapunov exponent, box counting |
| [X-ray diffraction from a crystalline surface](./X-ray%20diffraction%20from%20a%20crystalline%20surface) | Condensed matter | 1D and 2D fast Fourier transforms |

## The labs

### Solving the Schrödinger equation

The 1D stationary Schrödinger equation is discretised by finite differences, which turns it into an eigenvalue problem for a tridiagonal Hamiltonian matrix, solved with `scipy.linalg.eigh_tridiagonal`.

- **Validation:** infinite square well and harmonic oscillator, compared with the analytical energies and wavefunctions (Hermite polynomials). This includes a study of artefacts caused by the finite size of the computational box.
- **Double well:** symmetric and antisymmetric states, localisation, estimate of the tunnelling frequency, and an asymmetric well under an applied electric field.
- **Electron in a 1D crystal:** an effective periodic potential reveals the formation of energy bands.
- **Computational cost:** how diagonalisation time scales with matrix size, comparing tridiagonal, Hermitian and general solvers.

### Energy levels of an alkali atom

This lab computes the electronic energy levels of an atom with a single valence electron.

- **Hydrogen (validation):** the radial equation is solved numerically in atomic units, and the results are checked against the exact solution, including the degeneracy in $l$. The lab also includes energy-level diagrams, radial functions and 2D/3D plots of the 1s, 2s and 2p orbitals built with spherical harmonics.
- **Sodium:** the potential seen by the valence electron, created by the nucleus and the 10 other electrons, is found by a **self-consistent iterative method**:
  1. compute the orbitals in the current potential;
  2. compute the electronic charge density;
  3. solve the Poisson equation numerically;
  4. update the potential, with mixing to help convergence.

  The loop stops on a convergence criterion. The converged levels are compared with the experimental spectrum of sodium, and the excited states are identified. The method is then applied to predict the levels of lithium and potassium, and to estimate atomic sizes.

### Heat diffusion

This lab computes the steady-state temperature distribution in a 2D object, motivated by the example of a cylinder-head gasket in a piston engine.

- The heat equation with a source term is discretised by finite differences. This turns it into a large, sparse linear system $\mathbb{A}\mathbf{T} = \dot{\mathbf{Q}}$.
- The system is solved with the iterative **Gauss–Seidel** method and a convergence criterion. The heat flux is computed from the temperature gradient.
- The lab studies:
  - a homogeneous square with fixed boundary temperatures;
  - a point heat source, including how the result depends on grid resolution;
  - heterogeneous domains with one or two circular holes at imposed temperatures, which model the engine cylinders.

### Study of deterministic chaos

This lab studies the **logistic map** $x_{p+1} = r\,x_p(1 - x_p)$, a simple population model with chaotic behaviour.

- **Fixed points and stability:** analysis of the fixed points and their stability, with cobweb diagrams.
- **Route to chaos:** bifurcation diagram, period-doubling cascade, and zoom on periodic windows ("islands of stability") inside the chaotic regime.
- **Sensitivity to initial conditions:** extraction of the **Lyapunov exponent** from the exponential divergence of nearby trajectories.
- **Fractal dimension:** estimate of the dimension of the attractor by **box counting**.

### X-ray diffraction from a crystalline surface

The diffracted amplitude is the Fourier transform of the charge density. The lab uses this to compute diffraction patterns numerically.

- **1D atomic chain:** a chain of Gaussian atoms. The numerical FFT intensity is checked against the analytical formula.
- **2D lattices:** diffraction patterns of a square lattice, a centred square lattice and a lattice with a two-atom basis. They illustrate the reciprocal lattice, spot shapes, resolution and the role of the atomic form factor.
- **Comparison with experiment:** interpretation of a measured LEED (low-energy electron diffraction) pattern of a Si(001) surface.

## Repository structure

Each folder contains two files with the same name as the folder:

```
<Lab name>/
├── <Lab name>.pdf     # Lab subject written by the supervising teacher (in French)
└── <Lab name>.ipynb   # My notebook: code, figures and analysis (in French)
```

## Requirements

- Python 3 and Jupyter
- NumPy
- SciPy
- Matplotlib (including `mpl_toolkits`, which ships with Matplotlib, for 3D plots)

## License

The notebooks are released under the MIT License. The lab subjects (`.pdf` files) were written by the ENS Paris-Saclay teaching staff. They are included for context only and are not covered by this license.

## Acknowledgements

I thank the teachers of the Physics Department of ENS Paris-Saclay who designed and supervised these labs. The alkali-atom lab draws on the quantum mechanics courses of Jean-François Roch (ENS Paris-Saclay) and Manuel Joffre (École polytechnique).
