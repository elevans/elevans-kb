# Linux fixes
This document describes various linux fixes I've found through my searches on the internet.

## Security

This section is for security software based fixes (_e.g._ `apt-key` ring, firewalls, vpns).

### `apt-key` deprecation warning

This warning is raised when adding a 3rd party key to the deprecated `apt-key`. In order to resolve this
warning you need to export the old keys from `apt-key` and add it to the keyring.

1. List the apt-key contents


```bash
$ sudo apt-key list
```

2. Find the desired entry and copy the last 8 characters from the ID string.

```bash
pub   rsa2048 2015-10-28 [SC]
      BC52 8686 B50D 79E3 39D3  721C EB3E 94AD BE12 29CF
uid   [ unknown] Example (Release signing) <gpgsecurity@example.com>
```

In this case the last 8 characters are `BE1229CF`.

3. Export the key, specify a `gpg` file name thats relevant to the package the key is for and import it into the keyring.

```bash
$ sudo apt-key export BE1229CF | sudo gpg --dearmour -o /etc/apt/trusted.gpg.d/example.gpg 
```

4. Update the system.

```bash
$ sudo apt update
```