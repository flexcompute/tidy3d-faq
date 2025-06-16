---
title: What are the Units for Heat Simulation?
date: 2025-06-16 16:19:01
enabled: true
category: "Heat"
---
All units follow the SI system, except for length, which is defined in micrometers (µm). This is particularly important when specifying conductivity:

- `conductivity` (`PositiveFloat`) – [units = W/(µm·K)]
- `capacity` (`PositiveFloat`) – [units = J/(kg·K)]

However, it is straightforward to define a material using SI units with the [`SolidMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SolidMedium.html){: .color-primary-hover}`.from_si_units` method.
