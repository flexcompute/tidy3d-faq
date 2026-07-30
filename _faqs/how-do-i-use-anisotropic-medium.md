---
title: How Do I Use Anisotropic Medium?
date: 2025-09-24 11:50:54
enabled: true
category: "Inverse Design"
---
The [AnisotropicMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.AnisotropicMedium.html){: .color-primary-hover}{: .color-primary-hover} class is supported with the `autograd` plugin for diagonal anisotropy and can directly used in inverse design workflows.

The following example shows how to create an anisotropic LN medium with the extraordinary axis aligned along the z-axis:

<div markdown class="code-snippet">
{% highlight python %}
import tidy3d as td

# Define medium components
n_e = 2.17
n_o = 2.23

medium_xx = td.Medium(permittivity=n_o**2)
medium_yy = td.Medium(permittivity=n_o**2)
medium_zz = td.Medium(permittivity=n_e**2)

# Define anisotropic medium
medium = td.AnisotropicMedium(xx=medium_xx, yy=medium_yy, zz=medium_zz)
{% endhighlight %}
{% include copy-button.html %}</div>

Alternatively, you can use the built-in material library, which includes several anisotropic materials. For example, to load lithium niobate:

<div markdown class="code-snippet">
{% highlight python %}
LiNbO3 = td.material_library["LiNbO3"]["Zelmon1997"](2){: .color-primary-hover}
{% endhighlight %}
{% include copy-button.html %}</div>
