# Which Types of Charge Boundary Conditions are Available?

| Date       | Category    |
|------------|-------------|
| 2025-06-24 19:15:49 | Charge |


There are three boundary conditions available for Charge simulations:

1) Voltage boundary ([VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html)), which sets a constant potential and is commonly used to model applied bias.



```python

import tidy3d as td
voltage\_source = td.DCVoltageSource(voltage=1)
voltage\_bc = td.VoltageBC(source=voltage\_source)

```



Note that the `voltage` argument can be a string, in which case all voltages will be simulated.

2) Current boundary ([CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html)), which sets a constant current and is commonly used to model a fixed current source.



```python

import tidy3d as td
current\_source = td.DCCurrentSource(current=1)
current\_bc = td.CurrentBC(source=current\_source)

```



The `current` argument must be a `float`.

3) Insulating boundary ([InsulatingBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.InsulatingBC.html)), which models an insulating boundary that blocks charge flow.



```python

import tidy3d as td
bc = td.InsulatingBC()

```



This boundary condition is typically used to simulate surfaces or interfaces that do not allow charge to pass through.

```
