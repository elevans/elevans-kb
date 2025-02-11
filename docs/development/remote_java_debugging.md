# Remote Java debugging

## Setup remote Java debugging

### VS Code

In the working Java project, edit the `.vscode/launch.json` and add the following entry:

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "java",
            "name": "remote_debug",
            "request: "attach",
            "hostName": "localhost",
            "port": 8300,
        }
    ]
}
```

Click on **Run** and select **Start Debugging**.

## Connecting to Java application

### VS Code

Connect to a Java application by starting it with the following
flag (_note the port number_):

```bash
$ ./ImageJ2-linux64 -agentlib:jdwp=server=y,suspend=y,transport=dt_socket,address=localhost:8300
```

For more complicated tasks, like starting Fiji with a specific JDK version and custom JARs, pass the -agentlib flag to the JDK:

```bash
$ export FIJI_HOME=/home/edward/Documents/software/fiji_sjo; /home/edward/Documents/software/java/jdks/zulu11.70.15-ca-jdk11.0.22-linux_x64/bin/java -agentlib:jdwp=server=y,suspend=y,transport=dt_socket,address=localhost:8300 -cp "$FIJI_HOME/jars/*:$FIJI_HOME/jars/bio-formats/*:$FIJI_HOME/plugins/*" sc.fiji.Main
```

Once the application is running, it should wait for the debugger to begin listening. In VS code start the debuggr.
