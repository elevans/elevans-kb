# Scans

## ClamAV: Perform full system scan with logging (`clamscan`)

It's not necessary to run `freshclam` to get new definitions as there is a daemon that runs it automatically. However you can run it manually by running the following commands:

```bash
$ sudo systemctl stop clamav-freshclam.service
$ sudo freshclam
```

To run a full system scan with logging, run the following command. Replace the `<log_file>` name with the type of scan and date of the log:

```bash
$ sudo clamscan -r / | grep FOUND >> ~/Documents/logs/<log_file>.txt
```