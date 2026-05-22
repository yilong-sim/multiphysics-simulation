# Depth-Averaged Asymptotic Analysis

This document walks through the derivation of the 2D depth-averaged governing equations used across all four publications. The approach follows Lin, Storey & Santiago (*J. Fluid Mech.* 608, 43–70, 2008) and is extended here to coupled thermal, species transport, and induced-charge problems.

---

## Problem Setup

Consider a shallow microchannel with:
- Lateral dimensions characterized by length scale **H** (x-y plane)
- Depth characterized by **d** (z-direction, half-depth)
- Smallness parameter: **δ = d/H ≪ 1**

The depth-averaged value of any field variable f is defined as:

$$\bar{f} = \frac{1}{2} \int_{-1}^{1} f \, dz$$

where z has been non-dimensionalized by d. Variables are expanded asymptotically:

$$f = f_0 + \delta f_1 + \delta^2 f_2 + \cdots$$

Non-dimensionalization scales: [x,y] = H, [z] = d, [φ] = E₀H, [u,v] = U_ev = εE₀²d²/ηH, [w] = U_ev·d/H, [p] = ηU_ev H/d².

---

## 1. Electric Field

### 1a. Conducting fluid (Papers 5, 6, 7, 8)

The 3D governing equation for electric potential in a conducting fluid (conductivity σ):

$$\nabla \cdot (\sigma \mathbf{E}) = 0, \quad \mathbf{E} = -\nabla\phi$$

**Boundary condition at top/bottom walls** (electrically insulating):

$$\sigma \frac{\partial \phi}{\partial z} = 0 \quad \text{at } z = \pm 1$$

**O(δ⁰) balance:** The insulating BC forces ∂φ₀/∂z = 0, so φ₀ = φ₀(x,y) — potential is uniform across the depth. This carries through all orders.

**O(δ²) balance** after depth-averaging:

$$\boxed{\nabla_H \cdot (\bar{\sigma} \nabla_H \bar{\phi}) = 0}$$

The depth-averaged electric equation preserves its 3D form exactly. Wall geometry enters only through fluid property averages.

### 1b. ICEO — simultaneous fluid + dielectric wall solution (Paper 7)

For induced charge electroosmosis, PDMS has negligible conductivity (σ_w ≈ 0), so both fluid and wall satisfy Laplace's equation:

$$\nabla^2 \phi_f = 0 \quad \text{(fluid)}, \qquad \nabla^2 \phi_w = 0 \quad \text{(PDMS wall)}$$

**Boundary condition at top/bottom** (insulating):

$$\frac{\partial \phi}{\partial z} = 0 \quad \text{at } z = \pm 1$$

The asymptotic expansion proceeds identically through each order. At O(δ⁰), ∂φ₀/∂z = 0, so φ₀ = φ₀(x,y). Continuing through O(δ²) and depth-averaging:

$$\boxed{\nabla_H^2 \bar{\phi}_f = 0, \qquad \nabla_H^2 \bar{\phi}_w = 0}$$

Both depth-averaged equations retain the Laplacian form. The coupling between fluid and wall is handled through boundary conditions at their interface, not through the governing equations themselves:

$$\bar{\phi}_w - \bar{\phi}_f = -\frac{\lambda}{\gamma^2}\frac{\varepsilon_w}{\varepsilon_f}\nabla_H \bar{\phi}_w \cdot \mathbf{n} + \zeta_w$$

$$\nabla_H \bar{\phi}_f \cdot \mathbf{n} = \frac{\varepsilon_w}{\varepsilon_f}\frac{\gamma^2 - 1}{\gamma^2}\nabla_H \bar{\phi}_w \cdot \mathbf{n}$$

where ζ_w = ζ_i + ζ_eq is the total wall zeta potential (induced + equilibrium), λ is the Debye length, and γ² = 1 + jωλ²/D. The induced zeta potential scales as ζ_i ∝ λε_w/ε_f · E — larger for more polarizable walls and sharper corners.

---

## 2. Temperature Field (Paper 5)

The 3D steady-state energy equation with Joule heating source:

$$0 = \nabla \cdot (k\nabla T) + \sigma \langle E^2 \rangle$$

**Boundary conditions** at top and bottom surfaces encode heat dissipation through the substrate stack:

$$\frac{\partial T}{\partial z} = -\frac{d}{kR_{us}}(T - T_\infty) \quad \text{at } z = +1 \text{ (top, upper substrate)}$$

$$\frac{\partial T}{\partial z} = +\frac{d}{kR_{ls}}(T - T_\infty) \quad \text{at } z = -1 \text{ (bottom, lower substrate)}$$

Thermal resistances of the two substrate stacks:

$$R_{us} = t_{us,\text{PDMS}}/k_\text{PDMS} + 1/h \quad \text{(PDMS slab + natural convection)}$$
$$R_{ls} = t_{ls,\text{PDMS}}/k_\text{PDMS} + t_\text{glass}/k_\text{glass} \quad \text{(PDMS film + glass slide)}$$

The isothermal condition at the bottom (microscope stage) and natural convection at the top enter as Robin boundary conditions. This is the key physical improvement over naive 2D models, which required an unrealistically large convective coefficient h → ∞ because depth-wise heat dissipation was not modeled.

Performing the asymptotic depth-averaging through O(δ²):

$$\boxed{0 = k\nabla_H^2 \bar{T} + \sigma E_{DC}^2(1 + r^2) - \frac{\bar{T} - T_\infty}{d_{ch}}\left(\frac{1}{R_{us}} + \frac{1}{R_{ls}}\right)}$$

where r = V_AC,RMS / V_DC is the AC-to-DC voltage ratio. The third term — absent in regular 2D models — dissipates Joule heat through the substrate stack per unit channel depth.

---

## 3. Flow Field

### 3a. Stokes flow with body force (Papers 5, 6, 7, 8)

The 3D Stokes equations:

$$\nabla \cdot \mathbf{u} = 0$$
$$0 = -\nabla p + \nabla \cdot (\eta \nabla \mathbf{u}) + \mathbf{f}_e$$

**Boundary condition at top/bottom walls** (Helmholtz-Smoluchowski electroosmotic slip):

$$\mathbf{u} = -\frac{\varepsilon \zeta_w}{\eta} \mathbf{E}_H \quad \text{at } z = \pm 1$$

Valid when EDL thickness (10–100 nm) ≪ channel depth (25–100 µm).

**O(δ⁰) balance:** The horizontal momentum equation integrates to a parabolic z-profile:

$$\mathbf{u}_0 = \left(\frac{\nabla_H p_0 - \mathbf{D}}{\eta}\right)\left(\frac{z^2}{2} - \frac{1}{2}\right) + \mathbf{u}_{eo,0}$$

where **D** is the body force term. The depth-average of this parabolic profile is:

$$\bar{\mathbf{u}}_0 = -\frac{1}{3}\left(\frac{\nabla_H p_0 - \mathbf{D}}{\eta}\right) + \mathbf{u}_{eo,0} \equiv \bar{\mathbf{U}}_0 + \mathbf{u}_{eo,0}$$

Collecting through O(δ²):

$$\boxed{0 = -\nabla_H \bar{p} + \nabla_H \cdot (\eta \nabla_H \bar{\mathbf{u}}) + \mathbf{f}_e - \frac{3\eta}{d^2}(\bar{\mathbf{u}} - \bar{\mathbf{u}}_{slip})}$$

**The last term is the central result of depth-averaging.** It did not exist in the original 3D equations — it emerges from depth-averaging the parabolic Couette-Poiseuille profile between the top/bottom walls.

Physically it has two contributions:
1. **Wall drag:** −3η·ū/d² — viscous resistance from the top/bottom no-slip surfaces
2. **EO slip correction:** +3η·ū_slip/d² — electroosmotic flow driven by the top/bottom wall zeta potential

In problems with dissimilar top and bottom walls (Paper 8, PDMS top vs glass bottom):

$$\bar{\mathbf{u}}_{slip} = \frac{\varepsilon(\zeta' + \zeta'')}{2\mu}\mathbf{E}$$

where ζ' and ζ'' are the top and bottom wall zeta potentials respectively.

### 3b. ICEO slip boundary condition (Paper 7)

For ICEO, the slip velocity on channel sidewalls includes both equilibrium and induced components:

$$\bar{\mathbf{u}}_{slip} \cdot \mathbf{t} = -\frac{\varepsilon_0\varepsilon_f}{\eta}\left(\zeta_{i,DC}\nabla_H\bar{\phi}_{f,DC} + \zeta_w\nabla_H\bar{\phi}_{f,DC} + \zeta_{i,AC}\nabla_H\bar{\phi}_{f,AC}\right) \cdot \mathbf{t}$$

Since ICEO scales as ζ_i · E ∝ E², the entire induced-charge-driven flow is quadratic in electric field — it operates under both DC and AC fields and produces counter-rotating vortices at polarizable corners.

---

## 4. Species Transport — Concentration Field (Paper 8)

The 3D convection-diffusion equation for ferrofluid nanoparticle concentration c:

$$\frac{\partial c}{\partial t} + \mathbf{v} \cdot \nabla c = D\nabla^2 c$$

**Boundary conditions** at top/bottom (non-penetrating):

$$\frac{\partial c}{\partial z} = 0 \quad \text{at } z = \pm 1$$

**O(δ⁰) balance:** ∂²c₀/∂z² = 0 with the non-penetrating BC gives c₀ = c₀(x,y,t) — concentration is uniform across the depth at leading order.

**O(δ¹) balance:** depth-averaging gives:

$$\frac{\partial c_0}{\partial t} + \bar{\mathbf{u}}_0 \cdot \nabla_H c_0 = 0$$

Integrating the z-equation yields the first-order concentration variation:

$$\frac{\partial c_1}{\partial z} = Pe_d \left(\bar{\mathbf{U}}_0 \cdot \nabla_H c_0\right)\left(\frac{1}{2}z - \frac{1}{2}z^3\right)$$

where **Ū₀** is the velocity departure from the electroosmotic slip (the Poiseuille-like part of the depth profile).

**O(δ²) balance:** depth-averaging gives:

$$\frac{\partial \bar{c}_1}{\partial t} + \bar{\mathbf{u}}_1 \cdot \nabla_H c_0 + \bar{\mathbf{u}}_0 \cdot \nabla_H \bar{c}_1 = \frac{1}{Pe_d}\nabla_H^2 c_0 + \frac{2}{105}Pe_d\left[(\bar{\mathbf{U}}_0 \cdot \nabla_H)(\bar{\mathbf{U}}_0 \cdot \nabla_H c_0) + (\nabla_H \cdot \bar{\mathbf{U}}_0)(\bar{\mathbf{U}}_0 \cdot \nabla_H c_0)\right]$$

Collecting through O(δ) and returning to dimensional form:

$$\boxed{\frac{\partial c}{\partial t} + \mathbf{u} \cdot \nabla c = D\nabla^2 c + \frac{2d^2}{105D}\nabla \cdot \left[\mathbf{U}(\mathbf{U} \cdot \nabla c) + (\nabla \cdot \mathbf{U})(\mathbf{U} \cdot \nabla c)\right]}$$

where **U** = **u** − ε(ζ' + ζ'')/2μ · **E** is the velocity departure from the mean electroosmotic slip (the non-uniform part of the depth profile).

**Physical interpretation:** The second term on the right is a Taylor dispersion correction. It arises because the non-uniform velocity profile across the channel depth — the parabolic Poiseuille component **U** — stretches concentration gradients in the depth direction. When depth-averaged, this transverse stretching appears as an enhanced apparent diffusivity in the horizontal plane, proportional to U²/D. The coefficient 2/105 comes from integrating the z⁴ and z⁶ polynomial profiles that result from the depth-averaging algebra.

This term is essential for accurately predicting the ferrofluid/water interface dynamics: without it, instability onset is incorrectly predicted even when the flow field is accurately captured.

---

## 5. Summary of Depth-Averaged Equations

| Equation | Papers | Depth-averaged form |
|---|---|---|
| Electric field (conducting) | 5, 6, 7, 8 | ∇·(σ̄∇φ̄) = 0 |
| Electric field (Laplace, ICEO) | 7 | ∇²φ̄_f = 0, ∇²φ̄_w = 0 |
| Temperature | 5 | k∇²T̄ + Q_Joule = (T̄ − T∞)(1/R_us + 1/R_ls)/d_ch |
| Momentum | 5, 6, 7, 8 | 0 = −∇p̄ + η∇²ū + f_e − 3η(ū − ū_slip)/d² |
| Continuity | all | ∇·ū = 0 |
| Concentration | 8 | ∂c/∂t + u·∇c = D∇²c + (2d²/105D)∇·[U(U·∇c)] |

The wall correction term **−3η(ū − ū_slip)/d²** appears in every momentum equation. It is the single most important term that regular 2D models omit, and its absence causes:
- 2–3× under-prediction of electrokinetic instability threshold electric fields
- Wrong vortex size, location, and orientation in ICEO
- Unphysical temperature fields requiring unrealistic heat transfer coefficients

---

## 6. Validity

The depth-averaged model is accurate when δ = d/H ≪ 1. In practice for electrokinetic instability:

| Channel depth-to-width ratio | Recommended model |
|---|---|
| d/W < 0.3 | Depth-averaged model |
| 0.3 < d/W < 0.5 | Transitional; depth-averaged preferred |
| d/W > 0.5 | Regular 2D acceptable (wall effects weaken) |

The asymptotic consistency allows adding or dropping terms of O(δ²) without loss of accuracy at the order retained.

---

## References

1. Lin H., Storey B.D., Santiago J.G. "A depth-averaged electrokinetic flow model for shallow microchannels." *J. Fluid Mech.* 608, 43–70 (2008).
2. Hoburg J.F., Melcher J.R. *J. Fluid Mech.* 73, 333–351 (1976).
3. Chen C.-H., Lin H., Lele S.K., Santiago J.G. *J. Fluid Mech.* 524, 263–303 (2005).
4. Storey B.D., Tilley B.S., Lin H., Santiago J.G. *Phys. Fluids* 17, 018103 (2005).
