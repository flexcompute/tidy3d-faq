# How Can I Save and Load a Fitted Medium?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 12:38:02 | Mediums |


After fitting a medium, as described [here](https://docs.flexcompute.com/projects/tidy3d/en/stable/notebooks/Fitting.html), it is possible to save the fitted medium as an hdf5 file and save time when using it in another model. To save the file, just use the `.to_file` method:



```python
fitted_medium.to_file('medium_name.hdf5')
```



Now, the saved medium can be loaded with the [PoleResidue](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PoleResidue.html) `.from_file` method:



```python
loaded_medium = td.PoleResidue.from_file('medium_name.hdf5')
```



To use this medium via the web GUI, you have two options: 

(a): open the "Material Utilities", select the "Private Library", and click the "Upload Material" button; 

(b): in the workbench, create a new medium and choose the "Import Material" option in the "Add Medium" panel.
