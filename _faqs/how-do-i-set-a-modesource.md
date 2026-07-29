---
title: How Do I Set a Modesource?
date: 2026-04-28 18:52:01
enabled: true
category: "Sources"
---
The [tidy3d.ModeSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/mode/_autosummary/tidy3d.ModeSource.html#tidy3d.ModeSource){: .color-primary-hover} injects a current source in the simulation to excite a modal profile in a finite extent plane. It is commonly used to excite specific waveguide modes in photonic integrated circuits. To illustrate how to set up a [tidy3d.ModeSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/mode/_autosummary/tidy3d.ModeSource.html#tidy3d.ModeSource){: .color-primary-hover}, let's consider the case of injecting the first-order transverse electric (TE) mode in a silicon-on-insulator (SOI) waveguide operating at 1.55 $\mu$m.

<div markdown class="code-snippet">
{% highlight python %}
# Source bandwidth.
pulse = tidy3d.GaussianPulse(freq0=1.934e14, fwidth=6.245e12)

# Mode specification.
mode_spec = tidy3d.ModeSpec(
    target_neff=3.47,
    num_modes=2,
    sort_spec=tidy3d.ModeSortSpec(
        filter_key="TE_fraction",
        filter_reference=0.5,
    ),
)

# Source definition.
source = tidy3d.ModeSource(
    center=(0, 0, -2),
    size=(0, 2, 1.5),
    source_time=pulse,
    direction="+",
    mode_spec=mode_spec,
    mode_index=1,
    name="mode_source",
)
{% endhighlight %}
{% include copy-button.html %}</div>

You should use the `center` and `size` parameters to define a source plane surrounding the waveguide, then adjust the `source_time` dependence using [tidy3d.GaussianPulse](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GaussianPulse.html){: .color-primary-hover}. The `direction="+"` parameter specifies propagation in the positive waveguide axis. The [tidy3d.ModeSpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeSpec.html#tidy3d.ModeSpec){: .color-primary-hover} object includes all the specifications of a mode solver, which calculates the optical modes given the material distribution within the source plane. The modes calculated by the mode solver are sorted by decreasing effective index by default. Here, `sort_spec` uses [tidy3d.ModeSortSpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/mode/_autosummary/tidy3d.ModeSortSpec.html#tidy3d.ModeSortSpec){: .color-primary-hover} to place TE-like modes first by filtering on `TE_fraction >= 0.5`; within each group, modes use the default ordering by decreasing effective index. Finally, to inject the first-order TE mode in the waveguide, we set `mode_index=1`.

This [example](https://www.flexcompute.com/tidy3d/examples/notebooks/ModalSourcesMonitors/){: .color-primary-hover} illustrates setting up a [tidy3d.ModeSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/mode/_autosummary/tidy3d.ModeSource.html#tidy3d.ModeSource){: .color-primary-hover} source.
