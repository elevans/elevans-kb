# Java application profiling

# Use JDK Flight Recorder to profile a Java application

You can use the built-in JDK profiling tool, Flight Recorder, to produce a dump file that can be used with
JDK Misson Control for further analysis.

```bash
$ fiji-linux-x64 -XX:StartFlightRecording=filename=/home/edward/Downloads/java_app_dump.jfr,dumponexit=true
```
