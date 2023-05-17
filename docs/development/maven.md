# maven

## Build specific Java `.jar` files and save them to a directory

This maven command removes all copies of the original ImageJ and replaces it the specified version of the ImageJ package. This command is great for testing different version of ImageJ with a local version of Fiji/PyImageJ without having to manually download individual of ImageJ's `.jar` file for testing.

```bash
$ rm /path/to/fiji/jars/ij-*.jar; mvn dependency:copy -DoutputDirectory=/path/to/fiji/jars/ -Dartifact=net.imagej:ij:1.54b
```