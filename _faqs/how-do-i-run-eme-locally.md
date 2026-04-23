---
title: How do I run EME locally?
date: 2026-04-23 12:00:00
enabled: true
category: "EME"
---
An [`tidy3d.EMESimulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMESimulation.html){: target="_blank" rel="noopener"} can be run end-to-end on a local machine by pairing it with the local mode solver. `EMESimulation.mode_simulations` yields one [`tidy3d.ModeSimulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeSimulation.html){: target="_blank" rel="noopener"} per EME cell, and `EMESimulation.propagate` turns the mode results into the device S-matrix.

### Prerequisites

`EMESimulation.mode_simulations` is available without any extra license and returns one `ModeSimulation` per EME cell. Turning those mode results into an S-matrix — via `EMESimulation.propagate`, `EMESimulation.compute_overlaps`, `EMESimulation.propagate_from_overlaps`, or the per-element staged helpers — requires the optional `tidy3d-extras` package with the `local_eme` feature. Install with `pip install "tidy3d[extras]"`; see the [extras plugin page](https://docs.flexcompute.com/projects/tidy3d/en/latest/extras/index.html){: target="_blank" rel="noopener"} for details.

### One-shot

```python
mode_data = [ms.run_local() for ms in sim.mode_simulations]
smatrix = sim.propagate(mode_data)
```

### Cloud-parallel mode solves

Pass the per-cell `ModeSimulation` objects to [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.run.run.html){: target="_blank" rel="noopener"} as a dict keyed by cell index. `web.run` preserves dict keys as task names in the returned mapping, so the results can be read back in canonical EME cell order and fed to `propagate`:

```python
from tidy3d import web

mode_sims = {f"cell_{i}": ms for i, ms in enumerate(sim.mode_simulations)}
results = web.run(mode_sims, task_name="eme_local_modes")
mode_data = [results[f"cell_{i}"] for i in range(len(mode_sims))]
smatrix = sim.propagate(mode_data)
```

### Reusing overlaps across sweep variants

Overlap integrals dominate the cost of propagation and are sweep-invariant under [`tidy3d.EMELengthSweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMELengthSweep.html){: target="_blank" rel="noopener"}, [`tidy3d.EMEModeSweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSweep.html){: target="_blank" rel="noopener"}, and [`tidy3d.EMEPeriodicitySweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEPeriodicitySweep.html){: target="_blank" rel="noopener"}. For iterative design on the same modal basis, compute them once with `EMESimulation.compute_overlaps` and replay them through `EMESimulation.propagate_from_overlaps`:

```python
import tidy3d as td

cell_overlaps, interface_overlaps = sim.compute_overlaps(mode_data)

# Reuse the overlaps across sweep configurations without re-solving modes.
smatrix = sim.propagate_from_overlaps(cell_overlaps, interface_overlaps)

swept = sim.updated_copy(sweep_spec=td.EMELengthSweep(scale_factors=[0.5, 1.0, 2.0]))
smatrix_swept = swept.propagate_from_overlaps(cell_overlaps, interface_overlaps)
```

### Full staged pipeline

For finer control — for example, to checkpoint intermediates to HDF5 or run individual stages out-of-order — each pipeline element is exposed as its own method. The stage artifacts they return (`EMEStageCellModes`, `EMEStageCellOverlap`, `EMEStageInterfaceOverlap`, `EMEStageCellSMatrix`, `EMEStageInterfaceSMatrix`) are all HDF5-serializable, so any subset of the pipeline can be cached to disk and replayed later:

```python
# Stage 1: per-cell mode data → validated, filtered cell-mode artifacts.
mode_data = [ms.run_local() for ms in sim.mode_simulations]
cell_modes = [sim.stage_cell_modes(md, cell_index=i) for i, md in enumerate(mode_data)]

# Stage 2: overlap integrals (per cell and per interface).
cell_overlaps = [sim.compute_cell_overlap(cm) for cm in cell_modes]
iface_overlaps = [
    sim.compute_interface_overlap(cell_modes[li], cell_modes[ri])
    for li, ri in sim.cell_index_pairs
]

# Stage 3: per-element S-matrices, then stacked device S-matrix.
cell_sms = [sim.compute_cell_smatrix(co) for co in cell_overlaps]
iface_sms = [
    sim.compute_interface_smatrix(cell_overlaps[li], cell_overlaps[ri], io)
    for (li, ri), io in zip(sim.cell_index_pairs, iface_overlaps)
]
smatrix = sim.compute_smatrix(cell_overlaps, cell_sms, iface_sms)
```

### Limitations

The local path only produces the device S-matrix. `EMESimulation.monitors` (such as `EMEFieldMonitor`, `EMEModeSolverMonitor`, `EMECoefficientMonitor`) are dropped with a warning; run the simulation through the remote backend if you need monitor data.

The local path also does not support `EMEFreqSweep` — list target frequencies in `EMESimulation.freqs` and control reuse with `EMEModeSpec.interp_spec` instead. Anisotropic media in bent cells with `bend_medium_frame="global"` are also unsupported locally; use `bend_medium_frame="co_rotating"` or the remote backend.
