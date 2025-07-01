---
title: How Can I Define Doping Profile?
date: 2025-06-30 21:10:35
enabled: true
category: "Charge"
---
Doping is defined as a box with a specific doping profile and is added to a [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover} object.  
Positive doping corresponds to the `N_d` (number of donors) parameter of the [`SemiconductorMedium`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover}, while negative doping corresponds to the `N_a` (number of acceptors).

The doping profile can be:

- Uniform, implemented using the [`ConstantDoping`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConstantDoping.html){: .color-primary-hover} object:

<div markdown class="code-snippet">{% highlight python %}
import tidy3d as td
box\_coords = \[
\[-1, -1, -1],
\[1, 1, 1]
]
constant\_box1 = td.ConstantDoping(center=(0, 0, 0), size=(2, 2, 2), concentration=1e18)
constant\_box2 = td.ConstantDoping.from\_bounds(rmin=box\_coords\[0], rmax=box\_coords\[1], concentration=1e18){% endhighlight %}
{% include copy-button.html %}</div>

- Gaussian, implemented using the [`GaussianDoping`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GaussianDoping.html){: .color-primary-hover} object:

<div markdown class="code-snippet">{% highlight python %}
import tidy3d as td
box\_coords = \[
\[-1, -1, -1],
\[1, 1, 1]
]
gaussian\_box1 = td.GaussianDoping(
center=(0, 0, 0),
size=(2, 2, 2),
ref\_con=1e15,
concentration=1e18,
width=0.1,
source="xmin"
)
gaussian\_box2 = td.GaussianDoping.from\_bounds(
rmin=box\_coords\[0],
rmax=box\_coords\[1],
ref\_con=1e15,
concentration=1e18,
width=0.1,
source="xmin"
){% endhighlight %}
{% include copy-button.html %}</div>

The unit for the free carrier concentration is 1/$\text{cm}^3$.

It is important to note that doping boxes are additive; i.e., if two donor doping boxes overlap, the total concentration will be the sum of these two overlapping doping boxes.
