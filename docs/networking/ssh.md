# SSH

## Generating an SSH private/public key pair

To crate an SSH private/public key pair

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

To use your `.pub` key on a target machine/server simply copy your `id_ed25519.pub` file from the host machine to your `~/.ssh/authorized_keys/` folder on the target machine.

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