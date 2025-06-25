# How Can I Define the Simulation Grid?

| Date       | Category    |
|------------|-------------|
| 2025-06-24 19:15:49 | Charge |


There are two classes available for defining the grid specification:

- [UniformUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.UniformUnstructuredGrid.html):

    - This class implements a simple uniform unstructured grid, with the grid size defined by the `dl` argument. For an application example, see [this](https://www.flexcompute.com/tidy3d/examples/notebooks/MachZehnderModulator/) example.

    

```python
    heat_grid = UniformUnstructuredGrid(dl=0.1)
    ```



- [DistanceUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DistanceUnstructuredGrid.html):

    - This class specifies the mesh size based on the distance from material interfaces. The finer grid near interfaces is defined by the `dl_interface` argument, while the coarser bulk grid size is set using `dl_bulk`. The distances over which `dl_interface` and `dl_bulk` are enforced can be controlled with the `distance_interface` and `distance_bulk` arguments, respectively. For an application example, see [this](https://www.flexcompute.com/tidy3d/examples/notebooks/ThermallyTunedRingResonator/) example notebook.

    

```python
    heat_grid = DistanceUnstructuredGrid(
        dl_interface=0.1,
        dl_bulk=1,
        distance_interface=0.3,
        distance_bulk=2,
    )
    ```


