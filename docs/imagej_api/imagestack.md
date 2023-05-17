# `ij.ImageStack`

This section covers the `ImageStack` class. This class represents an expandable array of images

## Creating a stack from individual `ImagePlus` images

The `ImageStack` class can be used to create a stack from individual images. In the example below I will create a new `ImageStack` from a set three 2D images. When stacking images together, the individual images must all have the same shape. The image stack can then be used with the `ImagePlus` constructor to create a new `ImagePlus` object.

_Note:_ This example is written in Python (Jython for Fiji)

```python
from ij import IJ, ImagePlus, ImageStack

# open some images
imp1 = IJ.openImage("test_1.tif")
imp2 = IJ.openImage("test_2.tif")
imp3 = IJ.openImage("test_3.tif")

# create an empty image stack and add the images
stack = ImageStack()
stack.addSlice(imp1.getProcessor())
stack.addSlice(imp2.getProcessor())
stack.addSlice(imp3.getProcessor())

# convert the stack into a new ImagePlus
imp_stack = ImagePlus("test_stack", stack)
```