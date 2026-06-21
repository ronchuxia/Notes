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