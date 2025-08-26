---
title: Which Types of Charge Boundary Conditions are Available?
date: 2025-08-26 12:47:03
enabled: true
category: "Charge"
---
There are three boundary conditions available for Charge simulations:

1) Voltage boundary ([VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html){: .color-primary-hover}), which sets a constant potential and is commonly used to model applied bias.

<div markdown class="code-snippet">
{% highlight python %}
import tidy3d as td

voltage_source = td.DCVoltageSource(voltage=1)
voltage_bc = td.VoltageBC(source=voltage_source)
{% endhighlight %}
{% include copy-button.html %}</div>

Note that the `voltage` argument can be an list or array, in which case all voltages will be simulated.

2) Current boundary ([CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html){: .color-primary-hover}), which sets a constant current and is commonly used to model a fixed current source.

<div markdown class="code-snippet">
{% highlight python %}
import tidy3d as td

current_source = td.DCCurrentSource(current=1)
current_bc = td.CurrentBC(source=current_source)
{% endhighlight %}
{% include copy-button.html %}</div>

The `current` argument must be a `float`.

3) Insulating boundary ([InsulatingBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.InsulatingBC.html){: .color-primary-hover}), which models an insulating boundary that blocks charge flow.

<div markdown class="code-snippet">
{% highlight python %}
import tidy3d as td
bc = td.InsulatingBC()
{% endhighlight %}
{% include copy-button.html %}</div>

This boundary condition is typically used to simulate surfaces or interfaces that do not allow charge to pass through.
