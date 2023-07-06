# Storage

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

4. Create a system user.

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
```

5. Add them to the `share` group.

``` bash
$ sudo usermod -aG share shareuser
```

6. Add the user to Samba and create their password.

```bash
$ sudo smbpasswd -a shareuser
New SMB password:
Retype new SMB password:
```

7. _Optional_: Change the ownship of the existing files on the share drive and grant read/write permissions to the group.

```bash
$ sudo chown -R :share /path/to/share
$ sudo chmod -R g+rw /path/to/share
```

8. Edit the Samba configuration file at `/etc/samba/smb.conf` with the drive details. For example, add an entry like this:

```
[global]
   workgroup = WORKGROUP
   server string = Samba server
   security = user
   map to guest = bad user
   guest account = nobody
   directory mask = 0775
   create mask = 0664

[share_name]
   comment = A comment
   path = /path/to/dir
   valid users = @share
   force group = share
   read only = no
   writeable = yes
   browseable = yes
   directory mask = 0775
   create mask = 0664
   public = yes
```

9. Restart Samba service.

```bash
$ sudo service smbd restart
```

Some additional notes about the share configuration:
- `valid users`: Defines the users or groups that are allowed access to the share. In this case, it is set to `@share`, which refers to the "share" group.
- `force group = share`: Forces the group ownership of files and directories within the share to be the specified group. Here, it is set to "share" to ensure the "share" group has ownership.
- `create mask = 0664`: Sets the default permissions for newly created files. The value `0664` means read and write permissions for the owner and group, and read permissions for others.
- `directory mask = 0770`: Sets the default permissions for newly created directories. The value `0775` means read, write, and execute permissions for the owner and group, and read and execute permissions for others.
- `read only = no`: Specifies whether the share is read-only or writeable. It is set to "no" to allow write access.
- `writeable = yes`: Same as read only, specifies if the share is writeable.
- `browseable = yes`: Specifies whether the share is visible when browsing the network.