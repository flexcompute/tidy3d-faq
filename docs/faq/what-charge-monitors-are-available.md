# What Charge Monitors are Available?

| Date       | Category    |
|------------|-------------|
| 2025-06-30 21:10:35 | Charge |


Currently, there are three monitors available:

- [SteadyPotentialMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SteadyPotentialMonitor.html):

    - This monitor records the electric potential ($\Phi$).
 


```python
import tidy3d as td
voltage_monitor_z0 = td.SteadyPotentialMonitor(
center=(0, 0.14, 0), size=(0.6, 0.3, 0), name="voltage_z0", unstructured=True,
)```



- [SteadyFreeCarrierMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SteadyFreeCarrierMonitor.html):

    - This monitor records the steady-state free carrier concentrations ($J_n$ for electrons and $J_p$ for holes).



```python
import tidy3d as td
voltage_monitor_z0 = td.SteadyFreeCarrierMonitor(
center=(0, 0.14, 0), size=(0.6, 0.3, 0), name="voltage_z0", unstructured=True,
)```



- [SteadyCapacitanceMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SteadyCapacitanceMonitor.html):

    - This monitor records the small-signal capacitance within the area or volume defined by the monitor.



```python
import tidy3d as td
capacitance_global_mnt = td.SteadyCapacitanceMonitor(
center=(0, 0.14, 0), size=(td.inf, td.inf, 0), name="capacitance_global_mnt",
)```



For an application example of Charge monitors, please refer to [this](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver/) example.

Note that currents are naturally computed for DC isothermal simulations without the need for a monitor. They can be accessed via the `charge_data.device_characteristics.steady_dc_current_voltage` object, as illustrated in [this](https://www.flexcompute.com/tidy3d/examples/notebooks/ThermoOpticDopedModulator) example.
