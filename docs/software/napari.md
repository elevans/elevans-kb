# napari

## Change image dimension scales

To adjust the scale of an image (in any dimension) open the `napari` terminal and assign a new scale list of dimensions to `viewer.layers["image"].scale` or `viewer.layers[0].scale` (where `0` is the index of the desired image if more than one image is open).

```python
viewer.layers[0].scale = [2, 1, 1] # 3D data with dimensions (pln, row, col)
```

In this example, increasing the first dimension's (`pln`) scale will result in a thicker 3D projection.