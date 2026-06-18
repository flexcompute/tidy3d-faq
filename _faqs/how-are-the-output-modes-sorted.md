---
title: How are the Output Modes Sorted?
date: 2026-04-28 18:51:48
enabled: true
category: "Mode Solver"
---
After running the Tidy3D <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolver.html#tidy3d.plugins.mode.ModeSolver">mode solver</a>, the modes are returned in a <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolverData.html#tidy3d.plugins.mode.ModeSolverData">ModeSolverData</a> object. The solver finds the <code>num_modes</code> modes closest to <code>target_neff</code>. If no custom sorting is specified, the returned modes are ordered by decreasing effective index.

To reproduce the old <code>filter_pol="te"</code> behavior, use a <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeSortSpec.html#tidy3d.ModeSortSpec"><code>tidy3d.ModeSortSpec</code></a> that puts modes with <code>TE_fraction >= 0.5</code> first:

<code>tidy3d.ModeSortSpec(filter_key="TE_fraction", filter_reference=0.5)</code>

To explicitly reproduce the old <code>filter_pol="tm"</code> behavior, use the same pattern with <code>TM_fraction</code>:

<code>tidy3d.ModeSortSpec(filter_key="TM_fraction", filter_reference=0.5)</code>

The example below uses the TE-like sorting. Modes with <code>TE_fraction >= 0.5</code> are returned first, and modes within each group use the default ordering by decreasing <code>n_eff</code>.

<div markdown class="code-snippet">
{% highlight python %}
import numpy as np
import tidy3d
from tidy3d.plugins.mode import ModeSolver
from tidy3d.plugins.mode.web import run as run_mode_solver

# Define the waveguide.
waveguide = tidy3d.Structure(
    geometry=tidy3d.Box(size=(tidy3d.inf, 0.5, 0.22)),
    medium=tidy3d.Medium(permittivity=3.47**2),
)

# Build a simulation object including the waveguide.
sim = tidy3d.Simulation(
    size=(10, 2.5, 1.5),
    grid_spec=tidy3d.GridSpec.auto(min_steps_per_wvl=20, wavelength=1.55),
    structures=[waveguide],
    run_time=1e-12,
    boundary_spec=tidy3d.BoundarySpec.all_sides(boundary=tidy3d.PML()),
)

# Plane where we want to solve the modes.
plane = tidy3d.Box(center=(0, 0, 0), size=(0, 2.5, 1.5))

# Equivalent to the old filter_pol="te" behavior.
mode_sort_spec = tidy3d.ModeSortSpec(
    filter_key="TE_fraction",
    filter_reference=0.5,
)

mode_spec = tidy3d.ModeSpec(
    num_modes=4,
    target_neff=3.47,
    sort_spec=mode_sort_spec,
)

# Build the mode solver.
freq0 = tidy3d.C_0 / 1.55
mode_solver = ModeSolver(
    simulation=sim,
    plane=plane,
    mode_spec=mode_spec,
    freqs=[freq0],
)

# Run the server-side mode solver.
mode_data = run_mode_solver(mode_solver)

# Get the mode polarization fraction.
print("TE polarization fraction:")
print(np.asarray(mode_data.pol_fraction["te"]).squeeze())
{% endhighlight %}
{% include copy-button.html %}</div>

Other sorting strategies are also possible. For example, modes can be sorted by <code>TM_fraction</code>, <code>mode_area</code>, <code>k_eff</code>, <code>wg_TE_fraction</code>, or <code>wg_TM_fraction</code>, depending on which modal property should define the ordering.
