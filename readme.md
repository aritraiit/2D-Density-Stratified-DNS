# 2D Stratified Fluid Turbulence Solver (Pseudo-Spectral Method)

This repository implements a fully dealiased, high-performance pseudo-spectral numerical solver designed to simulate two-dimensional, stably stratified, viscous fluid flow under the Boussinesq approximation. The flow is simulated in a square, doubly periodic domain $\mathbb{T}^2 = [0, 2\pi) \times [0, 2\pi)$.

---

## 🛠️ Code Overview & Background

This simulation platform was developed by **Aritra Roy**, former *S.N. Bhatt Memorial Excellence Fellow (2024)* at the [International Centre for Theoretical Sciences (ICTS-TIFR), Bangalore](https://www.icts.res.in/news/results-icts-s-n-bhatt-memorial-excellence-fellowship-program-2024).

---

## 📚 Governing Equations

The mathematical framework and non-dimensional coupling configuration implemented in this simulation are based on the setups detailed by **Okino & Hanazaki (2020)** in their study on direct numerical simulations of stratified fluid media:

> 📄 **Reference:** Okino, S., & Hanazaki, H. (2020). Direct numerical simulation of turbulence in a salt-stratified fluid. *Journal of Fluid Mechanics*, 891, A19. [doi:10.1017/jfm.2020.146](https://doi.org/10.1017/jfm.2020.146)

The solver integrates the coupled system for the vertical vorticity component $\omega = \partial_x v - \partial_y u$ and the active scalar density fluctuation field $\rho$:

$$\frac{\partial \omega}{\partial t} + \mathbf{u} \cdot \nabla \omega = \frac{1}{Re_0} \nabla^2 \omega - \frac{1}{Fr_0^2} \frac{\partial \rho}{\partial x}$$

$$\frac{\partial \rho}{\partial t} + \mathbf{u} \cdot \nabla \rho = \frac{1}{Re_0 Sc} \nabla^2 \rho + v$$

### Parameter & Variable Definitions:
* $\mathbf{u} = (u, v)$: The incompressible 2D velocity field satisfying the zero-divergence condition $\nabla \cdot \mathbf{u} = 0$.
* $\omega$: The vertical component of vorticity.
* $\rho$: The active scalar density fluctuation field.
* $Re_0$: The initial **Reynolds number**, governing momentum diffusion and viscous dissipation.
* $Fr_0$: The **Froude number**, scaling the structural strength of the baroclinic torque and buoyancy forces.
* $Sc$: The **Schmidt number**, tracking the ratio of momentum diffusivity (viscosity) to mass/scalar diffusivity.
* $-\frac{1}{Fr_0^2}\frac{\partial \rho}{\partial x}$: Represents the **buoyancy generation term** (Baroclinic Torque) feeding into the vorticity field.
* $v$: Represents the structural advection across the background linear density stratification profile.

---

## 🚀 Numerical Implementation Features

* **Pseudo-Spectral Discretization:** Spatial derivatives are evaluated with spectral accuracy in Fourier space, yielding highly accurate spatial distributions.
* **Dealiasing:** Features a fully dealiased nonlinear advection evaluation via the standard Orszag $2/3$-rule or padding technique to prevent spectral blocking.
* **Incompressibility Enforcement:** Velocity field projections are performed directly in Fourier space via the stream function formulation ($\|\mathbf{u}\| = \|\nabla \times \psi\|$) to enforce $\nabla \cdot \mathbf{u} = 0$ up to machine precision.

---

## 📊 Simulation Visualization

Below is a visualization showcasing the evolved flow fields, highlighting the complex interplay between small-scale turbulent structures, internal gravity waves, and density stratification:

![2D Stratified Fluid Turbulence Visualization]("D:\github documents\stratified2d_dns\contourmap.png")

