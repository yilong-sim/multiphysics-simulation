# Joule Heating Effects on Electroosmotic Entry Flow

**Publication:** Prabhakaran R.A., Zhou Y. et al., *Electrophoresis* 38, 572–579 (2017)  
DOI: [10.1002/elps.201600296](https://doi.org/10.1002/elps.201600296)

---

## Problem

Prior studies of Joule heating in electrokinetic microfluidics were limited to the interior of microchannels. This work examines the **reservoir-microchannel junction** — a region of inherently large electric field gradients due to the size mismatch between millimeter-scale reservoirs and micrometer-scale channels.

Under DC-biased AC electric fields, Joule heating concentrates in the narrow constriction region. Temperature gradients alter fluid properties (conductivity σ, permittivity ε, viscosity η) locally, and the electric field acts on these gradients to produce an **electrothermal body force**. Above a threshold AC voltage, this force generates counter-rotating fluid vortices at the channel entrance.

---

## All six coupled fields at once

![Six-panel COMSOL output at 600 V AC](../../assets/figures/joule_heating_6panel.png)

Electric field (A), temperature (B), permittivity (C), conductivity (D), electrothermal body force (E), and fluid velocity magnitude (F) under 20 V DC-biased 600 V AC. The constriction amplifies E by ~4×, raising local temperature by ~20 K, which shifts σ by +50% and ε by −10%, producing the body force that drives the circulations in F.

This is what multiphysics coupling looks like concretely: six interdependent fields, none of which can be solved independently.

---

## Coupled Physics

Four fields solved simultaneously:

**Electric field** (DC component; AC ratio r enters as a parameter):
$$\nabla_H \cdot (\sigma \mathbf{E}_{DC}) = 0$$

**Temperature** (steady-state, with substrate thermal resistance BCs):
$$0 = k\nabla_H^2 T + \sigma E_{DC}^2(1 + r^2) - \frac{T - T_\infty}{d_{ch}}\left(\frac{1}{R_{us}} + \frac{1}{R_{ls}}\right)$$

**Flow** (Stokes with electrothermal body force and wall correction):

$$0 = -\nabla_H p + \nabla_H \cdot (\eta \nabla_H \mathbf{u}) + \mathbf{f}_e - \frac{3(\eta\mathbf{u} + \varepsilon\zeta_w \mathbf{E}_{DC})}{d_{ch}^2}$$

**Particle tracing** (fluid velocity + electrophoresis):

$$\mathbf{U}_P = \mathbf{u} + \frac{\varepsilon\zeta_p}{\eta}\mathbf{E}_{DC}$$

The thermal resistance terms R_us (upper substrate: PDMS slab + natural convection) and R_ls (lower substrate: PDMS film + glass slide) replace the unrealistic h → ∞ assumption of prior 2D models. See [theory/depth_averaging_derivation.md](../../theory/depth_averaging_derivation.md) for the derivation.

---

## Microfluidic Chip

PDMS-based chip fabricated by soft lithography:
- Main channel: 400 µm wide, 25 µm deep, 1 cm total length
- Constriction: 40 µm wide, 1 mm long at each end
- Reservoirs: 5 mm diameter; corner radius at junction: 30 µm
- Three-layer construction: 2 mm PDMS slab / 10 µm PDMS film / 1 mm glass slide
- Tracer particles: 520 nm fluorescent polystyrene in 5 mM phosphate buffer (σ = 0.1 S/m)

---

## Parameters

| Symbol | Value | Description |
|---|---|---|
| σ∞ | 0.1 S/m | Fluid conductivity at room temperature |
| α | 0.02 K⁻¹ | Temperature coefficient of conductivity |
| β | −0.0046 K⁻¹ | Temperature coefficient of permittivity |
| k | 0.61 W/(m·K) | Fluid thermal conductivity |
| k_PDMS | 0.15 W/(m·K) | PDMS thermal conductivity |
| k_glass | 1.38 W/(m·K) | Glass thermal conductivity |
| d_ch | 25 µm | Channel depth |
| h | 10 W/(m²·K) | Natural convection coefficient |
| ζ_w | −50 mV | Wall zeta potential |
| ζ_p | −80 mV | Particle zeta potential |

---

## Key Results

- Electrothermal circulations first appear at 500 V AC; grow with increasing AC voltage
- Temperature at the constriction center rises parabolically with AC voltage; reservoir temperature rises linearly at a much lower rate — this gradient drives the vortices
- Joule heat is rejected primarily downward through the glass slide, consistent with 3D modeling
- Computational cost: **10 min on a laptop** (120k elements) vs. **>4 hours on a 24-core cluster** for the equivalent 3D model
