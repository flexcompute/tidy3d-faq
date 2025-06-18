# How do I include fabrication constraints in adjoint topology optimization?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 23:00:02 | Inverse Design |


To ensure reliable fabrication of a device, it is crucial to avoid using feature sizes below a certain radius of curvature when performing inverse design. To achieve this in topology (density-based) optimization, you can use a conic density filter, which is popular in topology optimization problems, to enforce a minimum feature size specified by the <code>filter_radius</code> variable. Next, a hyperbolic tangent projection function can be applied to eliminate grayscale and obtain a binarized permittivity pattern. The code <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd3InverseDesign/">example</a> below demonstrates how to apply the conic filter and the tanh projection to the design parameters before obtaining the permittivity values.

```python
from tidy3d.plugins.autograd import make_filter_and_project, rescale

# radius of the circular filter (um) and the threshold strength
radius = 0.120
beta = 50

filter_project = make_filter_and_project(radius, lx / nx)


def get_eps(params, beta):
    """Get the permittivity values (1, eps_wg) array as a function of the parameters (0, 1)"""
    processed_params = filter_project(params, beta)
    eps = rescale(processed_params, 1, eps_wg)
    return eps


def make_input_structures(params, beta) -> List[td.Structure]:
    box = td.Box(center=(0, 0, 0), size=(lx, ly, lz))
    eps_data = get_eps(params, beta=beta).reshape((nx, ny, 1))
    custom_structure = td.Structure.from_permittivity_array(geometry=box, eps_data=eps_data)

    return [custom_structure]

```

 

 

 
