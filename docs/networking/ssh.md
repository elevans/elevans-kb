# SSH

## Generating an SSH private/public key pair

In your terminal run the following command to generate a new SSH key pair using the `Ed25519` algorithm.

```bash
$ ssh-keygen -t ed25519 -C "key_id"
```

Hit enter to apply the default to the prompts. Once completed your new SSH public SSH key will be located at `~/.ssh/id_ed25519.pub`.

## Send files via SSH

To send files via SSH, install and use `scp`. Note that an active connection to the server or client is not needed, just a running SSH server and client instance. `scp` uses the following syntax:

```bash
$ scp /path/to/local/file <username>@<remotehost>:/path/to/remote/dir
```

To send folders, use the `-r` recursive switch. For example:

```bash
$ scp -r /path/to/local/dir <username>@<remotehost>:/path/to/remote/dir
```

## Using your SSH `.pub` key on target machine

To use your `.pub` key on a target machine/server simply copy the contents of your `id_ed25519.pub` file from the host machine to the `~/.ssh/authorized_keys` file on the target machine.

## Setup SSH config

You can configure SSH to use a config file that holds information like the username, password, IP _etc..._ with an associated alias.

`~/.ssh/config`

```bash
Host <alias_1>
        HostName 192.168.0.1

Host <alias_2>
        HostName 192.168.0.2
```

Example usage:

```bash
$ ssh <alias_1>
```

## Moving SSH keys between comuters

First move the `.ssh` folder to the new computer's `/home/user/` directory. Next change each file's permissions to match
the configuration below:

```bash
-rw-r--r-- 1 edward edward  592 Dec 29 09:10 config
-rw------- 1 edward edward  411 Dec 26 13:53 id_ed25519
-rw-r--r-- 1 edward edward   99 Dec 26 13:53 id_ed25519.pub
-rw------- 1 edward edward 1262 Dec 29 09:10 known_hosts
```

To do this, run the following `chmod` commands:

```bash
$ chmod 700 ~/.ssh
$ chown -R edward:edward ~/.ssh
$ chmod 644 ~/.ssh/config
$ chmod 644 ~/.ssh/id_ed25519.pub
$ chmod 600 ~/.ssh/id_ed25519
$ chmod 600 ~/.ssh/known_hosts
```
