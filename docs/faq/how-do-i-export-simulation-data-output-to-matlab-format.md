# How do I export Simulation data output to MATLAB format?

| Date       | Category    |
|------------|-------------|
| 2025-02-05 13:47:06 | Data Visualization and Postprocessing |


You can use the [SimulationData.to_mat_file]( https://docs.flexcompute.com/projects/tidy3d/en/stable/api/_autosummary/tidy3d.components.data.sim_data.SimulationData.html#tidy3d.components.data.sim_data.SimulationData.to_mat_file) function to export simulation data in MATLAB format. For example:



```python

# Run the simulation and get the data.
sim_data = tidy3d.web.run(simulation, task_name="task", path="data/data.hdf5", verbose=True)

# Export to MATLAB format.
sim_data.to_mat_file('/path/to/file/data.mat') 

```

You can find detailed information about simulation data visualization and postprocessing in this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/VizData/">tutorial</a>.
