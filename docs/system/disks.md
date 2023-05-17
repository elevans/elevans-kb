# Disk functions

## Create a Virtual Hard Disk (VHD) image

The following steps will guide you on how to create a VHD image of unspecified size.

```bash
$ sudo dd if=/dev/zero of=VHD.img bs=1M count=1200
```

- `if=/dev/zero`: input file to privde a character stream for inializing data storage
- `of=VHD.img`: image file to be created as storage volume
- `bs=1M`: read and write in 1M chunk size
- `count=1200`: amount of data to copy in megabytes, specifies image size

Next format the image with a file system (_e.g._ ext4).

```bash
$ sudo mkfs -t ext4 /path/to/VHD.img
mke2fs 1.46.5 (30-Dec-2021)
Discarding device blocks: done                            
Creating filesystem with 307200 4k blocks and 76800 inodes
Filesystem UUID: eb2eb3ee-0837-4244-89e3-c3fbd130aa34
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information: done 
```

Finally mount the VHD image file to a mount point.

```bash
$ sudo mount /path/to/VHD.img /path/to/mnt/
```