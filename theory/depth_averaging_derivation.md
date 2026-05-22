# Depth-Averaged Asymptotic Analysis

*Part of [multiphysics-simulation](../README.md)*

This document derives the 2D depth-averaged governing equations used across all four publications. The approach follows Lin, Storey & Santiago (*J. Fluid Mech.* 608, 43–70, 2008) and is extended here to coupled thermal, species transport, and induced-charge problems.

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

Non-dimensionalization scales: $[x,y] = H$, $[z] = d$, $[\phi] = E_0 H$, $[u,v] = U_{ev} = \varepsilon E_0^2 d^2 / \eta H$, $[w] = U_{ev} \cdot d/H$, $[p] = \eta U_{ev} H / d^2$.

---

## 1. Electric Field

### 1a. Conducting fluid

*Used in: Joule heating ([Electrophoresis 2017](../models/joule_heating_entry_flow/README.md)), Ferrofluid instability ([Microfluid. Nanofluid. 2015](../models/ferrofluid_instability_2015/README.md), [Sci. Rep. 2017](../models/ferrofluid_instability_2017/README.md)), ICEO ([Phys. Fluids 2017](../models/induced_charge_ICEO/README.md))*

The 3D governing equation for electric potential in a conducting fluid (conductivity σ):

$$\nabla \cdot (\sigma \mathbf{E}) = 0, \quad \mathbf{E} = -\nabla\phi$$

**Boundary condition at top/bottom walls** (electrically insulating):

$$\sigma \frac{\partial \phi}{\partial z} = 0 \quad \text{at } z = \pm 1$$

**O(δ⁰) balance:** The insulating BC forces $\partial\phi_0/\partial z = 0$, so $\phi_0 = \phi_0(x,y)$ — potential is uniform across the depth. This carries through all orders.

**O(δ²) balance** after depth-averaging:

$$\boxed{\nabla_H \cdot (\bar{\sigma} \nabla_H \bar{\phi}) = 0}$$

The depth-averaged equation preserves its 3D form exactly. Wall geometry enters only through fluid property averages.

### 1b. ICEO — simultaneous fluid + dielectric wall solution

*Used in: ICEO ([Phys. Fluids 2017](../models/induced_charge_ICEO/README.md))*

PDMS has negligible conductivity ($\sigma_w \approx 0$), so both fluid and wall satisfy Laplace's equation:

$$\nabla^2 \phi_f = 0 \quad \text{(fluid)}, \qquad \nabla^2 \phi_w = 0 \quad \text{(PDMS wall)}$$

The asymptotic expansion proceeds identically. At O(δ⁰), $\partial\phi_0/\partial z = 0$, so $\phi_0 = \phi_0(x,y)$. Continuing through O(δ²) and depth-averaging:

$$\boxed{\nabla_H^2 \bar{\phi}_f = 0, \qquad \nabla_H^2 \bar{\phi}_w = 0}$$

Both depth-averaged equations retain the Laplacian form. Fluid–wall coupling is handled through interface boundary conditions, not through the governing equations:

$$\bar{\phi}_w - \bar{\phi}_f = -\frac{\lambda}{\gamma^2}\frac{\varepsilon_w}{\varepsilon_f}\nabla_H \bar{\phi}_w \cdot \mathbf{n} + \zeta_w$$

$$\nabla_H \bar{\phi}_f \cdot \mathbf{n} = \frac{\varepsilon_w}{\varepsilon_f}\frac{\gamma^2 - 1}{\gamma^2}\nabla_H \bar{\phi}_w \cdot \mathbf{n}$$

where $\zeta_w = \zeta_i + \zeta_{eq}$ is the total wall zeta potential (induced + equilibrium), λ is the Debye length, and $\gamma^2 = 1 + j\omega\lambda^2/D$. The induced zeta potential scales as $\zeta_i \propto \lambda\varepsilon_w/\varepsilon_f \cdot E$ — larger for more polarizable walls and sharper corners.

---

## 2. Temperature Field

*Used in: Joule heating ([Electrophoresis 2017](../models/joule_heating_entry_flow/README.md))*

The 3D steady-state energy equation with Joule heating:

$$0 = \nabla \cdot (k\nabla T) + \sigma \langle E^2 \rangle$$

**Boundary conditions** at top and bottom surfaces encode heat dissipation through the substrate stack:

$$\frac{\partial T}{\partial z} = -\frac{d}{kR_{us}}(T - T_\infty) \quad \text{at } z = +1 \quad \text{(top: PDMS slab + natural convection)}$$

$$\frac{\partial T}{\partial z} = +\frac{d}{kR_{ls}}(T - T_\infty) \quad \text{at } z = -1 \quad \text{(bottom: PDMS film + glass slide)}$$

Thermal resistances:

$$R_{us} = t_{us,\text{PDMS}}/k_\text{PDMS} + 1/h, \qquad R_{ls} = t_{ls,\text{PDMS}}/k_\text{PDMS} + t_\text{glass}/k_\text{glass}$$

The isothermal microscope stage at the bottom and natural convection at the top enter as Robin boundary conditions. This replaces the unrealistic $h \to \infty$ assumption required by prior naive 2D models, where depth-wise heat dissipation was not modeled.

Performing the asymptotic depth-averaging through O(δ²):

$$\boxed{0 = k\nabla_H^2 \bar{T} + \sigma E_{DC}^2(1 + r^2) - \frac{\bar{T} - T_\infty}{d_{ch}}\left(\frac{1}{R_{us}} + \frac{1}{R_{ls}}\right)}$$

where $r = V_{AC,RMS} / V_{DC}$ is the AC-to-DC voltage ratio. The third term — absent in regular 2D models — dissipates Joule heat through the substrate stack per unit channel depth.

---

## 3. Flow Field

*Used in: all four publications*

### 3a. Stokes flow with body force

The 3D Stokes equations:

$$\nabla \cdot \mathbf{u} = 0$$

$$0 = -\nabla p + \nabla \cdot (\eta \nabla \mathbf{u}) + \mathbf{f}_e$$

**Boundary condition at top/bottom walls** (Helmholtz–Smoluchowski electroosmotic slip):

$$\mathbf{u} = -\frac{\varepsilon \zeta_w}{\eta} \mathbf{E}_H \quad \text{at } z = \pm 1$$

Valid when EDL thickness (10–100 nm) ≪ channel depth (25–100 µm).

**O(δ⁰) balance:** The horizontal momentum equation integrates to a parabolic z-profile:

$$\mathbf{u}_0 = \left(\frac{\nabla_H p_0 - \mathbf{D}}{\eta}\right)\left(\frac{z^2}{2} - \frac{1}{2}\right) + \mathbf{u}_{eo,0}$$

where **D** collects the body force terms. Depth-averaging this parabolic profile:

$$\bar{\mathbf{u}}_0 = -\frac{1}{3}\left(\frac{\nabla_H p_0 - \mathbf{D}}{\eta}\right) + \mathbf{u}_{eo,0} \equiv \bar{\mathbf{U}}_0 + \mathbf{u}_{eo,0}$$

Collecting through O(δ²):

$$\boxed{0 = -\nabla_H \bar{p} + \nabla_H \cdot (\eta \nabla_H \bar{\mathbf{u}}) + \mathbf{f}_e - \frac{3\eta}{d^2}(\bar{\mathbf{u}} - \bar{\mathbf{u}}_{slip})}$$

**The last term is the central result of depth-averaging.** It does not exist in the original 3D equations — it emerges from depth-averaging the parabolic Couette–Poiseuille profile between the top/bottom walls. It has two physical contributions:

1. **Wall drag:** $-3\eta\bar{\mathbf{u}}/d^2$ — viscous resistance from top/bottom no-slip surfaces
2. **EO slip correction:** $+3\eta\bar{\mathbf{u}}_{slip}/d^2$ — electroosmotic flow driven by top/bottom wall zeta potentials

For problems with dissimilar top and bottom walls (Sci. Rep. 2017, PDMS top vs glass bottom):

$$\bar{\mathbf{u}}_{slip} = \frac{\varepsilon(\zeta' + \zeta'')}{2\mu}\mathbf{E}$$

where ζ' and ζ'' are the top and bottom wall zeta potentials respectively.

### 3b. ICEO slip boundary condition

*Used in: ICEO ([Phys. Fluids 2017](../models/induced_charge_ICEO/README.md))*

The slip velocity on channel sidewalls includes both equilibrium and induced zeta potential components:

$$\bar{\mathbf{u}}_{slip} \cdot \mathbf{t} = -\frac{\varepsilon_0\varepsilon_f}{\eta}\left(\zeta_{i,DC}\nabla_H\bar{\phi}_{f,DC} + \zeta_w\nabla_H\bar{\phi}_{f,DC} + \zeta_{i,AC}\nabla_H\bar{\phi}_{f,AC}\right) \cdot \mathbf{t}$$

Since ICEO scales as $\zeta_i \cdot E \propto E^2$, the induced-charge-driven flow is quadratic in electric field — it operates under both DC and AC fields and produces counter-rotating vortices at polarizable corners.

---

## 4. Species Transport

*Used in: Ferrofluid instability ([Sci. Rep. 2017](../models/ferrofluid_instability_2017/README.md))*

The 3D convection-diffusion equation for ferrofluid nanoparticle concentration c:

$$\frac{\partial c}{\partial t} + \mathbf{v} \cdot \nabla c = D\nabla^2 c$$

**Boundary conditions** at top/bottom (non-penetrating):

$$\frac{\partial c}{\partial z} = 0 \quad \text{at } z = \pm 1$$

**O(δ⁰) balance:** $\partial^2 c_0/\partial z^2 = 0$ with the non-penetrating BC gives $c_0 = c_0(x,y,t)$ — concentration is uniform across the depth at leading order.

**O(δ¹) balance:** depth-averaging gives $\partial c_0/\partial t + \bar{\mathbf{u}}_0 \cdot \nabla_H c_0 = 0$.

Integrating the z-equation yields the first-order concentration variation:

$$\frac{\partial c_1}{\partial z} = Pe_d \left(\bar{\mathbf{U}}_0 \cdot \nabla_H c_0\right)\left(\frac{1}{2}z - \frac{1}{2}z^3\right)$$

where $\bar{\mathbf{U}}_0$ is the Poiseuille-like (non-uniform) part of the depth velocity profile.

**O(δ²) balance** after depth-averaging and collecting through O(δ):

$$\boxed{\frac{\partial c}{\partial t} + \mathbf{u} \cdot \nabla c = D\nabla^2 c + \frac{2d^2}{105D}\nabla \cdot \left[\mathbf{U}(\mathbf{U} \cdot \nabla c) + (\nabla \cdot \mathbf{U})(\mathbf{U} \cdot \nabla c)\right]}$$

where $\mathbf{U} = \mathbf{u} - \varepsilon(\zeta' + \zeta'')/2\mu \cdot \mathbf{E}$ is the velocity departure from the mean electroosmotic slip.

**Physical interpretation:** The correction term is a Taylor dispersion effect. The non-uniform depth velocity profile **U** stretches concentration gradients in the depth direction; when depth-averaged, this appears as enhanced apparent diffusivity in the horizontal plane, proportional to $U^2/D$. The coefficient 2/105 comes from integrating the resulting z⁴ and z⁶ polynomial profiles. Without this term, instability onset is incorrectly predicted even when the flow field is accurately represented.

---

## 5. Summary

| Equation | Publication | Depth-averaged form |
|---|---|---|
| Electric field (conducting fluid) | All four | $\nabla \cdot (\bar{\sigma}\nabla\bar{\phi}) = 0$ |
| Electric field (ICEO, fluid + wall) | Phys. Fluids 2017 | $\nabla^2\bar{\phi}_f = 0$, $\nabla^2\bar{\phi}_w = 0$ |
| Temperature | Electrophoresis 2017 | $k\nabla^2\bar{T} + Q_J = (\bar{T}-T_\infty)(R_{us}^{-1}+R_{ls}^{-1})/d_{ch}$ |
| Momentum | All four | $0 = -\nabla_H \bar{p} + \eta\nabla_H^2 \bar{u} + f_e - 3\eta(\bar{u}-\bar{u}_{slip})/d^2$ |
| Continuity | All four | $\nabla \cdot \bar{\mathbf{u}} = 0$ |
| Concentration | Sci. Rep. 2017 | $\partial_t c + \mathbf{u}\cdot\nabla c = D\nabla^2 c + (2d^2/105D)\nabla\cdot[\mathbf{U}(\mathbf{U}\cdot\nabla c)]$ |

The wall correction term $-3\eta(\bar{\mathbf{u}} - \bar{\mathbf{u}}_{slip})/d^2$ is the single most consequential term absent from regular 2D models. Its omission causes:

- 2–3× under-prediction of electrokinetic instability threshold electric fields
- Wrong vortex size, location, and orientation in ICEO predictions
- Unphysical temperature fields requiring unrealistic convective heat transfer coefficients

---

## 6. Validity Range

The model is accurate when $\delta = d/H \ll 1$. For electrokinetic instability specifically:

| Channel depth-to-width ratio | Recommended model |
|---|---|
| d/W < 0.3 | Depth-averaged (6–15% error on threshold) |
| 0.3 < d/W < 0.5 | Transitional; depth-averaged preferred |
| d/W > 0.5 | Regular 2D acceptable (wall effects weaken) |

Asymptotic consistency allows adding or dropping terms of O(δ²) without loss of accuracy at the retained order.

---

## References

1. Lin H., Storey B.D., Santiago J.G. "A depth-averaged electrokinetic flow model for shallow microchannels." *J. Fluid Mech.* 608, 43–70 (2008).
2. Hoburg J.F., Melcher J.R. *J. Fluid Mech.* 73, 333–351 (1976).
3. Chen C.-H., Lin H., Lele S.K., Santiago J.G. *J. Fluid Mech.* 524, 263–303 (2005).
4. Storey B.D., Tilley B.S., Lin H., Santiago J.G. *Phys. Fluids* 17, 018103 (2005).
