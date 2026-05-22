# Induced Charge Effects on Electrokinetic Entry Flow

**Publication:** Prabhakaran R.A., Zhou Y. et al., *Physics of Fluids* 29, 062001 (2017)  
DOI: [10.1063/1.4984741](https://doi.org/10.1063/1.4984741)

---

## Problem

In low-ionic-concentration electroosmotic flow, Joule heating is negligible. The dominant non-classical effect at the reservoir-microchannel junction is **induced charge electroosmosis (ICEO)**: electric field leaking into the dielectric PDMS corners polarizes the corner surfaces, generating an induced zeta potential that drives counter-rotating fluid vortices. Combined with positive DEP, these vortices trap and concentrate particles at the corners.

Prior 2D models of ICEO in microchannel geometries differed from experiments by up to an order of magnitude — the largest discrepancy in the ICEO literature. This work identifies the cause and fixes it.

---

## Why regular 2D models fail: three-way comparison

![Particle trapping comparison — experiment vs depth-averaged vs regular 2D](../../assets/figures/iceo_particle_comparison.png)

Left column: experiment (10 V DC + 200 V AC). Center: depth-averaged model prediction. Right: regular 2D model prediction.

The depth-averaged model correctly captures the vortex location near the channel entrance corners. The regular 2D model predicts circulations in the wrong location, wrong size, and wrong orientation — because it ignores the top/bottom wall damping on ICEO entirely. This comparison is the clearest single-image argument for why the depth-averaged approach matters.

---

## Physics of Induced Charge

Three-step mechanism:

1. **Field leakage:** Electric field lines penetrate the dielectric PDMS corners (ε_w = 4, not zero)
2. **Charge induction:** The leaked field polarizes the corner surface, producing an induced zeta potential:
$$\zeta_i = -\frac{\lambda}{\gamma^2}\frac{\varepsilon_w}{\varepsilon_f}\nabla_H \bar{\phi}_w \cdot \mathbf{n}$$
3. **ICEO flow:** Induced charge interacts with the tangential electric field to drive slip. Since both ζ_i and **E** scale linearly with applied voltage, ICEO scales as **E²** — quadratic, active under both DC and AC.

---

## Coupled Physics

**Electric field — simultaneous solution in fluid and PDMS wall:**
$$\nabla_H^2 \bar{\phi}_f = 0, \qquad \nabla_H^2 \bar{\phi}_w = 0$$

**Robin-type boundary condition at fluid-wall interface:**
$$\bar{\phi}_w - \bar{\phi}_f = \zeta_i + \zeta_w, \qquad \nabla_H \bar{\phi}_f \cdot \mathbf{n} = \frac{\varepsilon_w}{\varepsilon_f}\frac{\gamma^2-1}{\gamma^2}\nabla_H \bar{\phi}_w \cdot \mathbf{n}$$

**Depth-averaged Stokes flow with wall correction:**
$$0 = -\nabla_H \bar{p} + \eta \nabla_H^2 \bar{\mathbf{u}} - \frac{3\eta}{d^2}(\bar{\mathbf{u}} - \bar{\mathbf{u}}_{slip})$$

**Slip velocity (equilibrium + induced components):**

$$\bar{u}_{slip} \cdot t = -\frac{\varepsilon_0\varepsilon_f}{\eta}
\left(\zeta_{i,DC}\nabla_H\bar{\phi}_{f,DC} + \zeta_w\nabla_H\bar{\phi}_{f,DC} + \zeta_{i,AC}\nabla_H\bar{\phi}_{f,AC}\right) \cdot t$$

The key extension over prior ICEO models: solving Laplace's equation in both fluid and wall simultaneously, coupled through the Robin BC. The wall subdomain was not included in any previous 2D ICEO model — it was simply assumed insulating with no field leakage.

---

## Parameters

| Symbol | Value | Description |
|---|---|---|
| ε_f | 80 | Relative permittivity of water |
| ε_w | 4 | Relative permittivity of PDMS |
| d | 12.5 µm | Half-depth (25 µm channel) |
| ζ_w | −100 mV | Equilibrium wall zeta potential |
| ζ_p | −80 mV | Particle zeta potential |
| f_CM | +0.65 | Clausius-Mossotti factor (positive DEP) |
| σ_f | 6 µS/cm | Fluid conductivity (0.01 mM phosphate buffer) |

---

## Parametric Results

**Induced zeta potential ζ_i scales:**
- **Linearly** with AC voltage (ζ_i ∝ E)
- **Linearly** with wall permittivity ε_w (more polarizable wall → more induced charge)
- **Exponentially** with decreasing corner radius — steepest below 10 µm radius

Corner radius has by far the strongest effect: reducing radius from 40 µm to 2 µm increases maximum vorticity by more than 24× (60 s⁻¹ → 1450 s⁻¹). Sharp corners are the dominant geometric parameter for ICEO strength.
