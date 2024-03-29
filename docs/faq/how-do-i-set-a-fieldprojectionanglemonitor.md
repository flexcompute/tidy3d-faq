# How do I set a FieldProjectionAngleMonitor?

| Date       | Category    |
|------------|-------------|
| 2023-12-19 17:16:43 | Monitors |


A FieldProjectionAngleMonitor object samples electromagnetic near fields in the frequency domain and projects them at given observation angles. The `center` and `size` fields defines where the monitor will be placed in order to record near fields, typically very close to the structure of interest. The near fields are then projected to far-field locations defined by `phi`, `theta`, and `proj_distance`, relative to the `custom_origin`. If the distance between the near and far field locations is much larger than the size of the device, one can typically set `far_field_approx` to `True`, which will make use of the far-field approximation to speed up calculations. If the projection distance is comparable to the size of the device, we recommend setting `far_field_approx` to `False`, so that the approximations are not used, and the projection is accurate even just a few wavelengths away from the near field locations. For applications where the monitor is an open surface rather than a box that encloses the device, it is advisable to pick the size of the monitor such that the recorded near fields decay to negligible values near the edges of the monitor. You can define a FieldProjectionAngleMonitor object by



```python

monitor = FieldProjectionAngleMonitor(
    center=(1,2,3),
    size=(2,2,2),
    freqs=[250e12, 300e12],
    name='n2f_monitor',
    custom_origin=(1,2,3),
    phi=[0, np.pi/2],
    theta=np.linspace(-np.pi/2, np.pi/2, 100)
    )

```



For details, please refer to the [API reference](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionAngleMonitor.html).