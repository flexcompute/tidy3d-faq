---
title: How do I create an active material?
date: 2023-12-05 19:31:06
enable: true
category: "Mediums"
---
<div><div>By default, Tidy3D will not allow medium specifications that give rise to active materials to avoid potential divergences. However, you can override this by setting the field <code>allow_gain=True</code> in any medium, e.g. <code>tidy3d.Medium(permittivity=2.0, conductivity=-1.0, allow_gain=True)</code>.</div></div>

<div> </div>
