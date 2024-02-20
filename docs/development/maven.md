# maven

## Build and install a Java project to a directory

This maven command builds your target project and installs it in the given directory. Here is an example installing SciJava Ops into a pre-exisiting Fiji installation:.

```bash
$ mvn clean install -Dscijava.app.directory=/path/to/fiji.app
```

## Build specific Java `.jar` files and save them to a directory

This maven command removes all copies of the original ImageJ and replaces it the specified version of the ImageJ package. This command is great for testing different version of ImageJ with a local version of Fiji/PyImageJ without having to manually download individual of ImageJ's `.jar` file for testing.

```bash
$ rm /path/to/fiji/jars/ij-*.jar; mvn dependency:copy -DoutputDirectory=/path/to/fiji/jars/ -Dartifact=net.imagej:ij:1.54b
```

## Useful commands

Use `-rf :module-name` to "resume from" a particular module in the build pipeline. For example:

```bash
$ mvn clean install mvn clean install -Dscijava.app.directory=/path/to/fiji.app -rf:scijava-ops-image
```