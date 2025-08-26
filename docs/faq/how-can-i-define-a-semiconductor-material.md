# How Can I Define a Semiconductor Material?

| Date       | Category    |
|------------|-------------|
| 2025-08-26 10:03:06 | Charge |


A semiconductor material is specified using the [`MultiPhysicsMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.components.material.multi_physics.MultiPhysicsMedium.html), by setting its `charge` property to a [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html). The required parameters for the [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html) are:

### Density of States and Band Gap Energy

- `N_c` (PositiveFloat) – Effective density of states in the conduction band.  
  *Units: cm⁻³*

- `N_v` (PositiveFloat) – Effective density of states in the valence band.  
  *Units: cm⁻³*

- `E_g` (PositiveFloat) – Band gap energy.  
  *Units: eV*



### Electron-hole Recombination Mechanisms

Recombination mechanisms can include:

- [`Shockley-Read-Hall`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ShockleyReedHallRecombination.html)  
- [`Radiative Recombination`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.RadiativeRecombination.html)  
- [`Auger Recombination`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.AugerRecombination.html)

- `R` (List) – Array containing the recombination models to be applied to the material.

---

### Optional Arguments

- `delta_E_g` – [Slotboom model for band-gap narrowing](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SlotboomBandGapNarrowing.html)

- `N_a` – Number of acceptor charges (holes).
  *Units: cm⁻³*

- `N_d` – Number of donor charges (electrons).  
  *Units: cm⁻³*

The free carrier densities can be either a `float` number or a [doping box](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/index.html#doping) object.


For a practical example, please refer to [this example notebook](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver).
