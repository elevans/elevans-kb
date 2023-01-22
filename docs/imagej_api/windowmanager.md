# `ij.WindowManager`

This section covers the `WindowManager`. The WindowManager has limited function in headless mode.

## **HACK:** `ij.py.show()` triggers a `java.awt.HeadlessException`

When running macros with `ij.py.run_macro()` an active image needs to be set. This can be done by converting the desired image to an `ImagePlus` (_e.g._ `imp = ij.py.to_imageplus(img)`) and then set active by calling `ij.py.show()`. This will register the image with the `WindowManager` for the macro. This works even in headless mode.

There is a bug however that triggers a `java.awt.HeadlessException` if there is not at least one registred `ImagePlus` with the `WindowManager`. To workaround this bug, you can crate a dummy image of 1 pixel and register it with the `WindowManager`.

```python
if ij.WindowManager.getIDList() is None:
    ij.py.run_macro('newImage("dummy", "8-bit", 1, 1, 1);')
```