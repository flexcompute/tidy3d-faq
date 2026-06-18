---
title: How Can I Define a Semiconductor Material?
date: 2025-08-26 10:06:59
enabled: true
category: "Charge"
---
A semiconductor material is specified using the [`MultiPhysicsMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.MultiPhysicsMedium.html){: .color-primary-hover}, by setting its `charge` property to a [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover}. The required parameters for the [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover} are:

### Density of States and Band Gap Energy

- `N_c` (PositiveFloat) – Effective density of states in the conduction band.  
  *Units: cm⁻³*

- `N_v` (PositiveFloat) – Effective density of states in the valence band.  
  *Units: cm⁻³*

- `E_g` (PositiveFloat) – Band gap energy.  
  *Units: eV*

---

### Mobility Models

Mobility can be dependent on both doping and temperature, based on the [Caughey-Thomas mobility model](None){: .color-primary-hover}, implemented with the class [`CaugheyThomasMobility`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CaugheyThomasMobility.html){: .color-primary-hover}, or constant (implemented with the class [`ConstantMobilityModel`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConstantMobilityModel.html){: .color-primary-hover}.


- `mobility_n` (Union[`CaugheyThomasMobility`, `ConstantMobilityModel`]) – Electron mobility model.

- `mobility_p` (Union[`CaugheyThomasMobility`, `ConstantMobilityModel`]) – Hole mobility model.

---

### Electron-hole Recombination Mechanisms

Recombination mechanisms can include:

- [`Shockley-Read-Hall`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ShockleyReedHallRecombination.html){: .color-primary-hover}  
- [`Radiative Recombination`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.RadiativeRecombination.html){: .color-primary-hover}  
- [`Auger Recombination`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.AugerRecombination.html){: .color-primary-hover}

- `R` (List) – Array containing the recombination models to be applied to the material.

---

### Optional Arguments

- `delta_E_g` – [Slotboom model for band-gap narrowing](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SlotboomBandGapNarrowing.html){: .color-primary-hover}

- `N_a` – Number of acceptor charges (holes).
  *Units: cm⁻³*

- `N_d` – Number of donor charges (electrons).  
  *Units: cm⁻³*

The free carrier densities can be either a `float` number or a [doping box](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/index.html#doping){: .color-primary-hover} object.


For a practical example, please refer to [this example notebook](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver){: .color-primary-hover}.
