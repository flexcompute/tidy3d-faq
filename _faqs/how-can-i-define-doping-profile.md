---
title: How Can I Define Doping Profile?
date: 2025-08-26 10:06:59
enabled: true
category: "Charge"
---
Doping is defined as a box with a specific doping profile and is added to a [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover}{: .color-primary-hover} object.  
Positive doping corresponds to the `N_d` (number of donors) parameter of the [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover}{: .color-primary-hover}, while negative doping corresponds to the `N_a` (number of acceptors).

The doping profile can be:

- **Uniform**, implemented using the [`ConstantDoping`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConstantDoping.html){: .color-primary-hover}{: .color-primary-hover} object:

<div markdown class="code-snippet">
{% highlight python %}
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
{% endhighlight %}
{% include copy-button.html %}</div>

- **Gaussian**, implemented using the [`GaussianDoping`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GaussianDoping.html){: .color-primary-hover}{: .color-primary-hover} object:

<div markdown class="code-snippet">
{% highlight python %}
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
{% endhighlight %}
{% include copy-button.html %}</div>

- **Arbitrary (user-defined)**, implemented by directly providing a [`SpatialDataArray`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SpatialDataArray.html){: .color-primary-hover}{: .color-primary-hover} to the `N_d` or `N_a` arguments of the [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover}{: .color-primary-hover}.  
This approach allows defining essentially any spatial doping profile (for example, Pearson-like implantation profiles derived from fab parameters).

<div markdown class="code-snippet">
{% highlight python %}
import tidy3d as td
import numpy as np

# Define geometry
geometry = td.Cylinder(radius=1, length=1)

# Pearson-like doping profile
def pearson_doping(z, P, R, T, S, offset=0):
    z = z - offset
    return P * (1 + ((z - R) / T)**2)**(S / 2 + 0.75) + offset

# Create coordinates
NUM_PTS = 300
rmin, rmax = geometry.bounds
x = np.linspace(rmin[0], rmax[0], NUM_PTS)
y = np.linspace(rmin[1], rmax[1], NUM_PTS)
z = np.linspace(rmin[2], rmax[2], NUM_PTS)
X, Y, Z = np.meshgrid(x, y, z)

# Mask geometry
mask = geometry.inside(X, Y, Z)

# Doping profile along z
doping_profile = pearson_doping(
    z, P=7.77e18, R=0.10384, T=0.07878, S=1.71, offset=z.min()
)

# Create SpatialDataArray
doping_values = td.SpatialDataArray(
    mask * np.tile(doping_profile, (len(x), len(y), 1)),
    coords={"x": x, "y": y, "z": z}
)
{% endhighlight %}
{% include copy-button.html %}</div>

The unit for the free carrier concentration is 1/$\text{cm}^3$.

It is important to note that doping boxes are additive; i.e., if two donor doping regions overlap, the total concentration will be the sum of the overlapping contributions.

