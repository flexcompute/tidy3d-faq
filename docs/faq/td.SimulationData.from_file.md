# Td.simulationdata.from_file?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 13:50:36 | Web API |


The `SimulationData.from_file` method allows you to load a [SimulationData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.components.data.sim_data.SimulationData.html) object directly from a locally saved file. It is a good alternative to the [`web.load`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.load.html) to avoid the time of downloading the simulation from the cloud.

The file can be saved with the `SimulationData.to_file` method. For more details, check [this](https://docs.flexcompute.com/projects/tidy3d/en/latest/faq/docs/faq/how-do-i-save-and-load-the-simulationdata-object.html) tutorial.

## Example


```python
python
# Load a Simulation from an HDF5 file
sim_data = SimulationData.from_file(fname="folder/sim.hdf5")
```


