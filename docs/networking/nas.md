# Network-attached Storage (NAS)

## Connecting to a NAS

```bash
$ sudo apt update
$ sudo apt install nfs-common
```

Mount the NAS share:

```bash
$ sudo mkdir /media/user/mnt
$ sudo mount -t nfs <server_address>:/volume#/share /media/user/mnt
```