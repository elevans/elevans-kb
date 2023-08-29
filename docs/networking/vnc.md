# VNC

## Create an SSH tunnel for VNC

You can do port forwarding to createa an SSH tunnel to a VNC session. First start your VNC session on your server by running `vncserver`. You can then check which port is being used by the server using the following command:

```bash
$ ps -ef | grep vnc 
```

Next on your local computer open a terminal and foward the local system port to the VNC display port via SSH:

```bash
$ ssh -L 5902:127.0.0.1:5902 -N -f -l username server
```

- **-L 5902:127.0.0.1:5902** Foward port `5902` to the ssh server port `5902` (_i.e._ the VNC display).
- **-N**: Do not execute a remote command (_i.e._ just foward the port).
- **-f**: Make the SSH port fowarding a background processes.
- **-l**: User name and server address.