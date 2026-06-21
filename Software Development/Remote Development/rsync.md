rsync is a file synchronization and transfer tool that only copies the differences between source and destination. It is faster than `cp` and `scp`.

Transfer file locally.  
```shell
rsync -ah --info=progress2 <source> <destination>
```

Transfer file from local to remote or from remote to local.  
```shell
rsync -ah <source> <username>@<hostname-or-ip>:<destination>
rsync -ah <username>@<hostname-or-ip>:<source> <destination> 
```
rsync transfers files over SSH by default when a remote host is specified.

Options:  
- `-a`: Archive mode (preserves permissions, timestamps, symlinks, etc.).
- `-h`: Human-readable size.
- `--info=progress2`: Show a progress bar. (`rsync` estimates the file size as it copies, so the progress bar may be unstable.)
- `--remove-source-files`: Remove source files (but preserves folders).