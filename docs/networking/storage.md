# Storage

## Mount and share a network drive

1. List connected storage devices with the following command. Copy the UUID number and file system type of the target drive.

```bash
$ lsblk -o NAME,FSTYPE,UUID,MOUNTPOINTS
NAME        FSTYPE   UUID                                 MOUNTPOINTS
loop0       squashfs                                      /snap/core20/1590
loop1       squashfs                                      /snap/core20/1782
loop2       squashfs                                      /snap/lxd/22927
loop3       squashfs                                      /snap/lxd/23545
loop4       squashfs                                      /snap/snapd/17885
loop5       squashfs                                      /snap/snapd/17954
sda         ext4     9ccc18c6-a72f-4b97-a16b-e43ff8272928 
mmcblk0                                                   
├─mmcblk0p1 vfat     D7E2-9D99                            /boot/firmware
└─mmcblk0p2 ext4     b09bb4c8-de4d-4ce6-a93f-30c4c9241a58 /
```

2. Create a mount point.

```bash
$ sudo mkdir /media/mount
```

3. To mount the drive manually use the following command:

```bash
$ sudo mount /dev/sd# /path/to/mount
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
UUID=9ccc18c6-a72f-4b97-a16b-e43ff8272928 /media/d0 ext4 defaults 0 2
```

_Note that `0` enables or disables backup of the drive. Normally this is set to `0`. The `2` in the last arg position enables `fsck` checks. The primary boot device should be `1`, all other drives should be `2`. Setting this arg to `0` disables the `fsck` checks._

## Share a drive with Samba

1. Install Samba:

```bash
$ sudo apt update
$ sudo apt install samba
```

2. Allow Samba through the firewall.

```bash
$ sudo ufw allow samba
```

3. Create a `share` user group.

```bash
$ sudo groupadd share
```

4. Create a system user and add them to the `share` group.

```bash
$ sudo adduser shareuser
Adding user `shareuser' ...
Adding new group `shareuser' (1001) ...
Adding new user `shareuser' (1001) with group `shareuser' ...
Creating home directory `/home/shareuser' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for shareuser
Enter the new value, or press ENTER for the default
Full Name []: New User
Room Number []:
Work Phone []:
Home Phone []: 
Other []: 
Is the information correct? [Y/n] y
$ sudo usermod -aG share shareuser
```

5. Add the user to Samba and create their password.

```bash
$ sudo smpasswd -a shareuser
New SMB password:
Retype new SMB password:
```

6. Change the permissions on the target share drive/directory.

```bash
$ sudo chgrp share /path/to/share
$ sudo chmod 770 /path/to/share
```

7. Edit the Samba configuration file at `/etc/samba/smb.conf` with the drive details. For example, add an entry like this:

```
[share_name]
   comment = A comment
   path = /path/to/dir
   valid users = @share
   read only = no
   browsable = yes
   writeable = yes
   public = yes
   create mask = 0660
   directory mask = 0770
   force group = +share
```

8. Restart Samba service.

```bash
$ sudo service smbd restart
```

Some additional notes about the share configuration:
- `valid users`: only users of the group `share` have access rights. The `@` denotes a group name.
- `force group = +share`: files and directories are created with this group, instead of the user group
- `create mask = 0660`: files in the share are created with permissions to allow all group users to read and write fiels created by other users.
- `directory mask = 0770`: same as `create mask` but for directories.
