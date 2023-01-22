# Users

## Create new users and add to `sudo` group

1. Create a new user.

```bash
$ sudo adduser newuser
Adding user `newuser' ...
Adding new group `newuser' (1001) ...
Adding new user `newuser' (1001) with group `newuser' ...
Creating home directory `/home/newuser' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for newuser
Enter the new value, or press ENTER for the default
Full Name []: New User
Room Number []:
Work Phone []:
Home Phone []: 
Other []: 
Is the information correct? [Y/n] y
```

2. Add the user to the sudo group.

```bash
$ sudo usermod -aG sudo newuser
```

3. Verify the new user was added to the `sudo` group.

```bash
$ groups newuser
newuser: newuser sudo
```

4. Verify `sudo` access.

```bash
$ su - newuser
$ whoami
newuser
$ sudo ls /root
```