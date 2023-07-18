# netplan

## Enable ethernet and wifi via netplan

Depending on your server configuration, your networking interfaces may be managed by `Cloud-init`. You can quickly determine this by checking the content of `/etc/netplan` and looking for a file called `50-cloud-init.yaml`. This file is generated automatically and is processed lexigraphically. Which means if you make a file that named `99-your-config.yaml` it will override the `Cloud-init` configuration.

Here's how you can enable ethernet on your server.

**Note:** These configs should be placed in `/etc/netplan/99-your-config.yaml`.

```
network:
  version: 2
  ethernets:
    ethX:
      dhcp4: true
```

Where `ethX` is your ethernet interface, likely `eth0`.

Here's how you can enable wifi on your server:

```
network:
  version: 2
  wifis:
    wlanY:
      access-ponits:
        "your SSID":
          password: "SSID password"
        dhcp4: true
        optional: true
```

Where `wlanY` is your wifi interface, likely `wlan0`.

And here is how you can enable ethernet and disable wifi:

```
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: true
  wifis:
    wlan0:
      dhcp4: false
      optional: true
      access-points: {}
```
