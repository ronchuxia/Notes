scp (secure copy) uses the same authentication as SSH. It has been largely replaced by `rsync`.

Secure copy from local to remote.  
```shell
scp <source> <username>@<hostname-or-ip>:<destination>
```

Secure copy from remote to local.  
```shell
scp <username>@<hostname-or-ip>:<source> <destination>
```

Options:  
- `-r`: Copy directory.