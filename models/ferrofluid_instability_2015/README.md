# Electric Field-Induced Instabilities in Ferrofluid Microflows

**Publication:** Thanjavur Kumar D., Zhou Y. et al., *Microfluidics and Nanofluidics* 19, 43–52 (2015)  
DOI: [10.1007/s10404-015-1546-8](https://doi.org/10.1007/s10404-015-1546-8)

---

## Problem

This work demonstrates for the first time that a DC electric field can drive electroosmotic flow of ferrofluid while simultaneously producing strong **electrokinetic instabilities** at the ferrofluid/water interface. The mechanism is the electrical conductivity mismatch between the two fluids: ferrofluid is approximately 180× more conductive than DI water, inducing free charge at the interface that the electric field acts upon to generate a destabilizing body force.

At sufficient electric field strength, the interface transitions from stable diffusion → periodic instability waves → chaotic flow, all at Reynolds number ≈ 1.

---

## Instability progression (experimental)

![Experimental instability time series](../../assets/figures/ferrofluid_instability_sequence.png)

Time-series snapshots of 0.2× ferrofluid (dark)/water co-flow at four DC electric fields. Stable diffusion at 172.2 V/cm; intermittent waves at 175.0 V/cm; sustained periodic waves at 177.8 V/cm (threshold); chaotic flow at 555.6 V/cm. All my experimental work — microchannel fabrication, solution preparation, imaging, and threshold measurement.

---

## My Experimental Contribution

**Microchannel fabrication:** T-shaped PDMS channel by standard soft lithography. Side branches 8 mm × 100 µm; main branch 10 mm × 200 µm; depth 40 µm throughout.

**Ferrofluid preparation:** EMG 408 (Ferrotec, Fe₃O₄ nanoparticles, ~10 nm diameter) at three concentrations: 0.1×, 0.2×, 0.3× by volume fraction. Measured electrical conductivity by Accumet AP85 conductivity meter — linear with concentration, R² = 0.9975.

**Threshold measurement:** Electric field increased continuously from zero; threshold defined as the minimum field at which periodic waves are visually sustained at the T-junction.

---

## Governing Equations

**Electric field:**
$$\nabla \cdot (\sigma \nabla \phi) = 0$$

**Navier-Stokes with electric body force (Coulomb + dielectric):**
$$\rho\left(\frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u}\right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho_e \mathbf{E} - \frac{1}{2}E^2 \nabla \varepsilon$$

**Species transport (ferrofluid concentration):**
$$\frac{\partial c}{\partial t} + \mathbf{u} \cdot \nabla c = D\nabla^2 c$$

Fluid properties concentration-dependent:
$$\sigma = c\sigma_f + (1-c)\sigma_w, \qquad \mu = \mu_f \, e^{\ln(\mu_w/\mu_f)(1-c)}$$

---

## Key Results

| Ferrofluid concentration | Experimental threshold |
|---|---|
| 0.1× | 213.8 V/cm |
| 0.2× | 177.8 V/cm |
| 0.3× | 169.4 V/cm |

Threshold decreases with increasing ferrofluid concentration — higher σ_f increases the conductivity ratio and the destabilizing free charge density.

The regular 2D model predicts the decreasing trend correctly but under-predicts all thresholds by 2–3×. This systematic error, traced to the neglect of top/bottom wall stabilizing effects, motivated the depth-averaged model in the follow-on *Scientific Reports* paper.
