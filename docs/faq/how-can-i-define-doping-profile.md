# How Can I Define Doping Profile?

| Date       | Category    |
|------------|-------------|
| 2025-08-26 10:03:06 | Charge |


Doping is defined as a box with a specific doping profile and is added to a [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html) object.  
Positive doping corresponds to the `N_d` (number of donors) parameter of the [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html), while negative doping corresponds to the `N_a` (number of acceptors).

The doping profile can be:

- Uniform, implemented using the [`ConstantDoping`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConstantDoping.html) object:



```python
import tidy3d as td

box_coords = [
    [-1, -1, -1],
    [1, 1, 1]
]

constant_box1 = td.ConstantDoping(
    center=(0, 0, 0),
    size=(2, 2, 2),
    concentration=1e18
)

constant_box2 = td.ConstantDoping.from_bounds(
    rmin=box_coords[0],
    rmax=box_coords[1],
    concentration=1e18
)
```



- Gaussian, implemented using the [`GaussianDoping`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GaussianDoping.html) object:



```python
import tidy3d as td

box_coords = [
    [-1, -1, -1],
    [1, 1, 1]
]

gaussian_box1 = td.GaussianDoping(
    center=(0, 0, 0),
    size=(2, 2, 2),
    ref_con=1e15,
    concentration=1e18,
    width=0.1,
    source="xmin"
)

gaussian_box2 = td.GaussianDoping.from_bounds(
    rmin=box_coords[0],
    rmax=box_coords[1],
    ref_con=1e15,
    concentration=1e18,
    width=0.1,
    source="xmin"
)
```



The unit for the free carrier concentration is 1/$\text{cm}^3$.

It is important to note that doping boxes are additive; i.e., if two donor doping boxes overlap, the total concentration will be the sum of these two overlapping doping boxes.
