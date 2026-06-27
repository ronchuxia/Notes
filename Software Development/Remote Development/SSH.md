SSH (secure shell) is a protocol for securely logging into and running commands on a remote machine over a network.

Open an SSH session.  
```shell
ssh <username>@<hostname-or-ip>
```

E.g.  
```shell
ssh team9@team9-desktop
```
Hostname is resolved to IP address by a **DNS (Domain Name Service)** server.

# Authentication
Apart from password authentication, you can use public/private key authentication.

Generate a public/private key pair. (Run on your local machine.)
```shell
ssh-keygen -t ed25519 -f ~/.ssh/my_key -C "your_email@example.com"
```
This creates 2 files.
```
~/.ssh/my_key        # private key, keep secret
~/.ssh/my_key.pub    # public key, safe to share
```

Install the **public key** on the server. (Run on the remote machine.)
```
~/.ssh/authorized_keys
```
Each line is one allowed public key.

Open an SSH session with the **private key**. (Run on your local machine.)
```shell
ssh -i ~/.ssh/my_key <username>@<hostname-or-ip>
```

# Local Port Forwarding
Tunnels traffic from a port on your local machine to a port on a remote machine.  
```shell
ssh -L <local-port>:<destination-host>:<destination-port> <username>@<hostname-or-ip>
```
NOTE: `<destination-host>` is relative to the remote SSH server, not the local machine.

E.g.  
```shell
ssh -L 8888:localhost:8888 team9@team9-desktop
```
Connecting to `localhost:8888` on your computer is forwarded through SSH to `localhost:8888` as seen from `team9-desktop`.