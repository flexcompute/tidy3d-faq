# How do I include fabrication constraints in adjoint shape optimization?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 22:49:03 | Inverse Design |


To ensure reliable fabrication of a device, it is crucial to avoid using feature sizes below a certain radius of curvature when performing inverse design. To achieve this, you can use a penalty function that estimates the radius of curvature around each boundary vertex and applies a substantial penalty to the objective function if the value falls below the minimum radius. The code <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd5BoundaryGradients/">example</a> below demonstrates how to use the  <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/v2.7.0/api/_autosummary/tidy3d.plugins.autograd.invdes.make_curvature_penalty.html">tidy3d.plugins.autograd.invdes.make_curvature_penalty</a> function.

```python
from tidy3d.plugins.autograd import make_curvature_penalty

curvature_penalty = make_curvature_penalty(min_radius=0.15)

def penalty(params: np.ndarray) -> float:
    """Compute penalty for a set of parameters."""
    ys = get_ys(params)
    points = anp.array([xs, ys]).T
    return curvature_penalty(points)
```

 

 

 
