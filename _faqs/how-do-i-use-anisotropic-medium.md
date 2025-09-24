---
title: How Do I Use Anisotropic Medium?
date: 2025-09-24 11:50:54
enabled: true
category: "Inverse Design"
---
Currently, classes of [AnisotropicMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.AnisotropicMedium.html){: .color-primary-hover} are not supported with the `autograd` plugin.  
However, it is possible to work with diagonally anisotropic materials by defining a [CustomMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CustomMedium.html#tidy3d.CustomMedium){: .color-primary-hover} that uses a diagonally anisotropic [PermittivityDataset](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PermittivityDataset.html){: .color-primary-hover}.

The following example shows how to create an anisotropic LN medium with the extraordinary axis aligned along the z-axis:


<div markdown class="code-snippet">
{% highlight python %}
# Define the coordinates for the medium
X = [-1e12, 1e12]
f = [td.C_0]
coords = dict(x=X, y=X, z=X, f=f)

# Define the datasets
n_e = 2.17
n_o = 2.23

eps_xx = td.ScalarFieldDataArray(np.ones((2, 2, 2, 1)) * n_e**2, coords=coords)
eps_yy = eps_xx
eps_zz = td.ScalarFieldDataArray(np.ones((2, 2, 2, 1)) * n_o**2, coords=coords)

# Define anisotropic permittivity dataset
permittivity = td.PermittivityDataset(
    eps_xx=eps_xx,
    eps_yy=eps_yy,
    eps_zz=eps_zz
)

# Define anisotropic custom medium
medium = td.CustomMedium(eps_dataset=permittivity)
{% endhighlight %}
{% include copy-button.html %}</div>
