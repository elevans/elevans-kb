# File system

## Automount a drive

1. List connected storage devices with the following command. Copy the UUID number and file system type of the target drive.

```bash
$ lsblk -o NAME,FSTYPE,UUID,MOUNTPOINTS
NAME        FSTYPE   UUID                                 MOUNTPOINTS
loop0       squashfs                                      /snap/core20/1826
loop1       squashfs                                      /snap/lxd/24326
loop2       squashfs                                      /snap/snapd/18363
loop3       squashfs                                      /snap/snapd/19459
loop4       squashfs                                      /snap/core20/1977
sda                                                       
└─sda1      ext4     92bf3df2-d4b3-4089-9aa6-ba4ad8753877 
mmcblk0                                                   
├─mmcblk0p1 vfat     B1C2-332F                            /boot/firmware
└─mmcblk0p2 ext4     3b687fda-fd50-40d7-9407-5f6103485cda /
```

2. Create a mount point.

```bash
$ sudo mkdir /media/mount
```

3. To mount the drive manually use the following command:

```bash
$ sudo mount /dev/sda# /path/to/mount
```

Note that this only mounts the drive for the current session. You will need to remount the drive again after a roboot. To automatically mount the drive follow the next steps to edit the `/etc/fstab` file.

4. Add drives to `/etc/fstab` for auto mount on bootup.

At the end of the `/etc/fstab`file. 

```
<UUID> <mount point> <file system type> <options> <dump>
UUID=<UUID> <PATH_TO_MOUNT> <FILE_TYPE> defaults 0 2
```

For example, for drive `dev/sda`:

```
UUID=92bf3df2-d4b3-4089-9aa6-ba4ad8753877 /media/d0 ext4 defaults 0 2
```

_Note that `0` enables or disables backup of the drive. Normally this is set to `0`. The `2` in the last arg position enables `fsck` checks. The primary boot device should be `1`, all other drives should be `2`. Setting this arg to `0` disables the `fsck` checks._